check=`curl -o /dev/null -s -m 10 --connect-timeout 10 -w %{http_code}  192.168.99.14:9010/server/login.jsp`
if [ "$check" == "200" ]
then
fi