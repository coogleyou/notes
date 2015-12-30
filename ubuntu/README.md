# Ubuntu工具
##Atom安装
目前只支持 64 位的 Ubuntu 14.04, 13.10 or 12.04
```bash
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```
##Mysql自动启动
```bash
#!/bin/bash

result=`/usr/bin/mysqladmin ping`
expected='mysqld is alive'

if [[ "$result" != "$expected" ]]
then
echo "It's dead - restart mysql"

# email subject
SUBJECT="[MYSQL ERROR] - Attempting to restart service"

# Email To ?
EMAIL="info@endyourif.com"

# Email text/message
EMAILMESSAGE="/tmp/emailmessage.txt"
echo "$result was received"> $EMAILMESSAGE
echo "when we were expected $expected" >>$EMAILMESSAGE
# send an email using /bin/mail
mail -s "$SUBJECT" "$EMAIL" < $EMAILMESSAGE

sudo /etc/init.d/mysql restart
fi
```
##查看常用的10个linux命令
`history | awk '{a[$2]++}END{for(i in a){print a[i] " " i}}' | sort -rn | head`
##修改Ubuntu系统代理
###设置代理
```bash
gsettings set org.gnome.system.proxy.socks host ’192.168.1.1′
gsettings set org.gnome.system.proxy.socks port 8080
gsettings set org.gnome.system.proxy mode ‘manual’
```
###禁用代理
`gsettings set org.gnome.system.proxy mode ‘none’`




