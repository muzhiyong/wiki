	svn更新代码{

		--force # 强制覆盖
		/usr/bin/svn --username user --password passwd co  $Code  ${SvnPath}src/                 # 检出整个项目
		/usr/bin/svn --username user --password passwd export  $Code$File ${SvnPath}src/$File    # 导出个别文件

	}