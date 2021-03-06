# Mysql

记录Mysql经验

## 修改最大连接数
方法一：

进入MySQL安装目录 打开MySQL配置文件 `my.ini` 或 `my.cnf`查找 `max_connections=100` 修改为 `max_connections=1000` 服务里重起MySQL即可

方法二：

MySQL最大连接数默认是100客户端登录：

    MySQL -uusername -ppassword

设置新的MySQL最大连接数为200：

    MySQL> set GLOBAL max_connections=200

显示当前运行的Query：

    MySQL> show processlist

显示当前状态：

    MySQL> show status

退出客户端：MySQL> exit

查看当前MySQL最大连接数：MySQLadmin -uusername -ppassword variables

方法三：

以centos 4.4 下面的MySQL 5.0.33 手工编译版本为例说明：

    vi /usr/local/MySQL/bin/MySQLd_safe

找到safe_MySQLd编辑它，找到MySQLd启动的那两行，在后面加上参数 ：

    -O max_connections=1500

具体一点就是下面的位置：

用红字特别说明：

    then $NOHUP_NICENESS $ledir/$MySQLD
    $defaults --basedir=$MY_BASEDIR_VERSION
    --datadir=$DATADIR $USER_OPTION
    --pid-file=$pid_file
    --skip-external-locking
    -O max_connections=1500
    >> $err_log 2>&1 else
    eval "$NOHUP_NICENESS $ledir/$MySQLD
    $defaults --basedir=$MY_BASEDIR_VERSION
    --datadir=$DATADIR $USER_OPTION
    --pid-file=$pid_file
    --skip-external-locking $args
    -O max_connections=1500 >>
    $err_log 2>&1"

保存。

    # service MySQLd restart
    # /usr/local/MySQL/bin/MySQLadmin -uroot -p variables

输入root数据库账号的密码后可看到

max_connections 1500 即新改动已经生效。

还有一种方法，

修改原代码:

解开MySQL的原代码，进入里面的sql目录修改MySQLd.cc找到下面一行：

    {"max_connections", OPT_MAX_CONNECTIONS,
    "The number of simultaneous clients allowed.", (gptr*) &max_connections,
    (gptr*) &max_connections, 0, GET_ULONG, REQUIRED_ARG, 100, 1, 16384, 0, 1,
    0},

把它改为：

    {"max_connections", OPT_MAX_CONNECTIONS,
    "The number of simultaneous clients allowed.", (gptr*) &max_connections,
    (gptr*) &max_connections, 0, GET_ULONG, REQUIRED_ARG, 1500, 1, 16384, 0, 1,
    0},

存盘退出，然后./configure ;make;make install可以获得同样的效果。以上的相关内容就是对修改MySQL最大连接数的3种方法的介绍，望你能有所收获。


