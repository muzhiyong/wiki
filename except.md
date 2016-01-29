		expect交互{

			exp_continue         # 多个spawn命令时并行
			interact             # 执行完成后保持交互状态，把控制权交给控制台
			expect "password:"   # 判断关键字符
			send "passwd\r"      # 执行交互动作，与手工输入密码的动作等效。字符串结尾加"\r"

			ssh后sudo{

				#!/bin/bash
				#sudo注释下行允许后台运行
				#Defaults requiretty
				#sudo去掉!允许远程
				#Defaults !visiblepw

				/usr/bin/expect -c '
				set timeout 5
				spawn ssh -o StrictHostKeyChecking=no xuesong1@192.168.42.128 "sudo grep xuesong1 /etc/passwd"
				expect {
					"passphrase" {
						send_user "sshkey\n"
						send "xuesong\r";
						expect {
							"sudo" {
							send_user "sudo\n"
							send "xuesong\r"
							interact
							}
							eof {
							send_user "sudo eof\n"
							}
						}
					}
					"password:" {
						send_user "ssh\n"
						send "xuesong\r";
						expect {
							"sudo" {
							send_user "sudo\n"
							send "xuesong\r"
							interact
							}
							eof {
							send_user "sudo eof\n"
							}
						}
					}
					"sudo" {
							send_user "sudo\n"
							send "xuesong\r"
							interact
							}
					eof {
						send_user "ssh eof\n"
					}
				}
				'

			}

			ssh执行命令操作{
			
				/usr/bin/expect -c "
				proc jiaohu {} {
					send_user expect_start
					expect {
						password {
							send ${RemotePasswd}\r;
							send_user expect_eof
							expect {
								\"does not exist\" {
									send_user expect_failure
									exit 10
								}
								password {
									send_user expect_failure
									exit 5
								}
								Password {
									send ${RemoteRootPasswd}\r;
									send_user expect_eof
									expect {
										incorrect {
											send_user expect_failure
											exit 6
										}
										eof 
									}
								}
								eof
							}
						}
						passphrase {
							send ${KeyPasswd}\r;
							send_user expect_eof
							expect {
								\"does not exist\" {
									send_user expect_failure
									exit 10
								}
								passphrase{
									send_user expect_failure
									exit 7
								}
								Password {
									send ${RemoteRootPasswd}\r;
									send_user expect_eof
									expect {
										incorrect {
											send_user expect_failure
											exit 6
										}
										eof
									}
								}
								eof
							}
						}
						Password {
							send ${RemoteRootPasswd}\r;
							send_user expect_eof
							expect {
								incorrect {
									send_user expect_failure
									exit 6
								}
								eof
							}
						}
						\"No route to host\" {
							send_user expect_failure
							exit 4
						}
						\"Invalid argument\" {
							send_user expect_failure
							exit 8
						}
						\"Connection refused\" {
							send_user expect_failure
							exit 9
						}
						\"does not exist\" {
							send_user expect_failure
							exit 10
						}
						
						\"Connection timed out\" {
							send_user expect_failure
							exit 11
						}
						timeout {
							send_user expect_failure
							exit 3
						}
						eof
					}
				}
				set timeout $TimeOut
				switch $1 {
					Ssh_Cmd {
						spawn ssh -t -p $Port -o StrictHostKeyChecking=no $RemoteUser@$Ip /bin/su - root -c \\\"$Cmd\\\"
						jiaohu
					}
					Ssh_Script {
						spawn scp -P $Port -o StrictHostKeyChecking=no $ScriptPath $RemoteUser@$Ip:/tmp/${ScriptPath##*/};
						jiaohu
						spawn ssh -t -p $Port -o StrictHostKeyChecking=no $RemoteUser@$Ip /bin/su - root -c  \\\"/bin/sh /tmp/${ScriptPath##*/}\\\" ;
						jiaohu
					}
					Scp_File {
						spawn scp -P $Port -o StrictHostKeyChecking=no -r $ScpPath $RemoteUser@$Ip:${ScpRemotePath};
						jiaohu
					}
				}
				"
				state=`echo $?`

			}

			交互双引号引用较长变量{
			
				#!/bin/bash
				RemoteUser=xuesong12
				Ip=192.168.1.2
				RemotePasswd=xuesong
				Cmd="/bin/echo "$PubKey" > "$RemoteKey"/authorized_keys"

				/usr/bin/expect -c "
				set timeout 10
				spawn ssh -o StrictHostKeyChecking=no $RemoteUser@$Ip {$Cmd};
				expect {
					password: {
						send_user RemotePasswd\n
						send ${RemotePasswd}\r;
						interact;
					}
					eof {
						send_user eof\n
					}
				}
				"

			}

			telnet交互{
			
				#!/bin/bash
				Ip="10.0.1.53"
				a="\{\'method\'\:\'doLogin\'\,\'params\'\:\{\'uName\'\:\'bobbietest\'\}"
				/usr/bin/expect -c"
						set timeout 15
						spawn telnet ${Ip} 8000
						expect "Escape"
						send "${a}\\r"
						expect {
								-re "\"err.*none\"" {
										exit 0
								}
								timeout {                       
										exit 1
								}
								eof {
										exit 2
								}
						}
				"
				echo $?

			}

			模拟ssh登录{
				#好处:可加载环境变量

				#!/bin/bash
				Ip='192.168.1.6'            # 循环就行
				RemoteUser='user'           # 普通用户
				RemotePasswd='userpasswd'   # 普通用户的密码
				RemoteRootPasswd='rootpasswd'
				/usr/bin/expect -c "
				set timeout -1
				spawn ssh -t -p $Port -o StrictHostKeyChecking=no $RemoteUser@$Ip
				expect {
					password {
						send_user RemotePasswd
						send ${RemotePasswd}\r;
						expect {
							\"does not exist\" {
								send_user \"root user does not exist\n\"
								exit 10
							}
							password {
								send_user \"user passwd error\n\"
								exit 5
							}
							Last {
								send \"su - batch\n\"
								expect {
									Password {
										send_user RemoteRootPasswd
										send ${RemoteRootPasswd}\r;
										expect {
											\"]#\" {
												send \"sh /tmp/update.sh update\n \"
												expect {
													\"]#\" {
														send_user ${Ip}_Update_Done\n
													}
													eof
												}
											}
										}
									}
								}
							}
						}
					}
					\"No route to host\" {
						send_user \"host not found\n\"
						exit 4
					}
					\"Invalid argument\" {
						send_user \"incorrect parameter\n\"
						exit 8
					}
					\"Connection refused\" {
						send_user \"invalid port parameters\n\"
						exit 9
					}
					\"does not exist\" {
						send_user \"root user does not exist\"
						exit 10
					}
					timeout {
						send_user \"connection timeout \n\"
						exit 3
					}
					eof
				}
				"
				state=`echo $?`

			}

		}