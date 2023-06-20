ipcs 

ipcs -l命令可以查看各个资源的系统限制信息，可以看到系统允许的最大信号量集及信号量个数限制、最大的消息队列中消息个数等信息。

1、从中可以看到以下信号量的限制信息，其中信号量集最大个数为32000、每个信号量集中信号量最大个数为32000、所有信号量最大个数为1024000000、每个信号量可以被同时调用的次数为500，这些参数是linux系统下的默认参数，对于限制参数也可以做一定程度的优化，会有一定程度上性能的提升，具体优化方法可以搜索相关帖子。

![image-20211228182609804](C:\Users\c30021057\AppData\Roaming\Typora\typora-user-images\image-20211228182609804.png)

### grep -v

就是反向过滤文本行的搜索

当控制台输出很多时，有很多是我们不想看到的，就可以用到grep -v命令。

> grep name# 表示只查看包含name这个关键字的行内容
> grep -v name # 表示查看除了含有name之外的行内容
>
> grep -w用于字符串精确匹配



### 查看磁盘空间

- df -hl：查看磁盘剩余空间
- df -h：查看每个根路径的分区大小
- du -sh [目录名]：返回该目录的大小
- du -sm [文件夹]：返回该文件夹总M数
- du -h [目录名]：查看指定文件夹下的所有文件大小

### Linux_shell条件判断if中的-a到-z的意思

```
[ -a FILE ] 如果 FILE 存在则为真。

[ -b FILE ] 如果 FILE 存在且是一个块特殊文件则为真。 
[ -c FILE ] 如果 FILE 存在且是一个字特殊文件则为真。 
[ -d FILE ] 如果 FILE 存在且是一个目录则为真。 
[ -e FILE ] 如果 FILE 存在则为真。 
[ -f FILE ] 如果 FILE 存在且是一个普通文件则为真。 
[ -g FILE ] 如果 FILE 存在且已经设置了SGID则为真。 [ -h FILE ] 如果 FILE 存在且是一个符号连接则为真。 
[ -k FILE ] 如果 FILE 存在且已经设置了粘制位则为真。 
[ -p FILE ] 如果 FILE 存在且是一个名字管道(F如果O)则为真。 
[ -r FILE ] 如果 FILE 存在且是可读的则为真。 
[ -s FILE ] 如果 FILE 存在且大小不为0则为真。 
[ -t FD ] 如果文件描述符 FD 打开且指向一个终端则为真。 
[ -u FILE ] 如果 FILE 存在且设置了SUID (set user ID)则为真。 
[ -w FILE ] 如果 FILE 如果 FILE 存在且是可写的则为真。 
[ -x FILE ] 如果 FILE 存在且是可执行的则为真。 
[ -O FILE ] 如果 FILE 存在且属有效用户ID则为真。 
[ -G FILE ] 如果 FILE 存在且属有效用户组则为真。 
[ -L FILE ] 如果 FILE 存在且是一个符号连接则为真。 
[ -N FILE ] 如果 FILE 存在 and has been mod如果ied since it was last read则为真。 
[ -S FILE ] 如果 FILE 存在且是一个套接字则为真。 
[ FILE1 -nt FILE2 ] 如果 FILE1 has been changed more recently than FILE2, or 如果 FILE1 exists and FILE2 does not则为真。 
[ FILE1 -ot FILE2 ] 如果 FILE1 比 FILE2 要老, 或者 FILE2 存在且 FILE1 不存在则为真。 
[ FILE1 -ef FILE2 ] 如果 FILE1 和 FILE2 指向相同的设备和节点号则为真。 
[ -o OPTIONNAME ] 如果 shell选项 “OPTIONNAME” 开启则为真。 
[ -z STRING ] “STRING” 的长度为零则为真。 
[ -n STRING ] or [ STRING ] “STRING” 的长度为非零 non-zero则为真。 
[ STRING1 == STRING2 ] 如果2个字符串相同。 “=” may be used instead of “==” for strict POSIX compliance则为真。 
[ STRING1 != STRING2 ] 如果字符串不相等则为真。 
[ STRING1 < STRING2 ] 如果 “STRING1” sorts before “STRING2” lexicographically in the current locale则为真。 
[ STRING1 > STRING2 ] 如果 “STRING1” sorts after “STRING2” lexicographically in the current locale则为真。
```



### **Linux中echo $命令的作用**

- echo $$ 返回登录shell的PID
- echo $? 返回上一个命令的状态，0表示没有错误，其它任何值表明有错误
- echo $# 返回传递到脚本的参数个数
- echo $* 以一个单字符串显示所有向脚本传递的参数，与位置变量不同，此选项参数可超过9个
- echo $! 返回后台运行的最后一个进程的进程ID号
- echo $@ 返回传递到脚本的参数个数，但是使用时加引号，并在引号中返回每个参数
- echo $- 显示shell使用的当前选项
- echo $0 是脚本本身的名字
- echo $_ 是保存之前执行的命令的最后一个参数
- echo $1 传入脚本的第一个参数
- echo $2 传入脚本的第二个参数



### 僵尸进程

```
ps -ef | grep defunct | grep -v grep | wc -l

ps -e -o ppid,stat | grep Z | cut –d” ” -f2 | xargs kill -9

kill -HUP 'ps -A -ostat,ppid | grep -e '^[Zz]' | awk "{print $2}"'
```



### ipmitool

```
https://blog.csdn.net/ljlfather/article/details/102919880
查看网络配置
ipmitool lan print 2
（1）为通道配置 静态 类型：
格式： ipmitool lan set 通道ID ipsrc ip获取类型
root@master:~# ipmitool lan set 1 ipsrc static

（2）配置 ip
格式： ipmitool lan set 通道ID  ipaddr  IP地址
root@master:~# ipmitool lan set 1 ipaddr 192.168.10.10

（3）配置掩码
格式： ipmitool lan set 通道ID  netmask  掩码地址
root@master:~# ipmitool lan set 1 netmask 255.255.255.0

（4）配置网关
格式： ipmitool  lan  set  通道ID  defgw  ipaddr  网关地址
root@master:~# ipmitool lan set 1 defgw ipaddr 192.168.10.11

（5）查看网络配置
格式： ipmitool  lan  print 通道ID
root@master:~# ipmitool lan print 1
```



### readlink

```
# 用来找出符号链接所指向的位置*
readlink /usr/bin/awk

如果没有链接 加-f参数，有链接返回link全路径，没有则返回 -f 后面路径*
readlink -f /usr/bin/awk

目前存在，没有链接， 返回 -f 后面绝对路径（相对路径会计算成绝对路径）

```



### SCP

```
1、从自己的电脑上把文件xxx复制到另一台远程机上的命令示例：

scp 本机文件xxx的路径   另一台机器的用户名@IP地址:~/Desktop/xxx
 例如：scp ~/Desktop/Xcode12.4   Cindy@10.10.27.1:~/Desktop/Xcode12.4.xip

2、从另一台远程机上把文件xxx复制到自己电脑上的命令示例：

scp -r 另一台机器的用户名@IP地址:~/Desktop/xxx   要存放Xcode13.1的本机路径

例如：scp -r Cindy@10.10.27.1:~/Downloads/Xcode_13.1.xip ~/Desktop/Xcode_13.1.xip
```





### crantab

```
/var/spool/cron/root
日志 /var/log/cron*

可以将每条crontab中的任务增加自己的日志，便于查找执行失败原因。
eg：6 * * * * /home/stack/test.sh >>/mylog.log 2>&1检查crontab服务状态

服务管理
/etc/init.d/crond status
/etc/init.d/crond restart
/etc/init.d/crond start/stop/restart/reload
```



### pdb调试

```
c (继续)
l (查找当前位于哪里)
s (进入子程序,如果当前有一个函数调用，那么 s 会进入被调用的函数体)
n(ext) 让程序运行下一行，如果当前语句有一个函数调用，用 n 是不会进入被调用的函数体中的
r (运行直到子程序结束)
!<python 命令>
h (帮助)
a(rgs) 打印当前函数的参数
j(ump) 让程序跳转到指定的行数
l(ist) 可以列出当前将要运行的代码块
p(rint) 最有用的命令之一，打印某个变量
q(uit) 退出调试
r(eturn) 继续执行，直到函数体返回
```





### 重建RPM数据库

```
# 删除指定的rpmdb路径
rm -f ${rpm_dbpath}/*

# 初始化rpmdb
rpm --initdb --dbpath="${rpm_dbpath}"
    
# 重建rpmdb
rpm --rebuilddb --dbpath="${rpm_dbpath}"

https://blog.csdn.net/biaotai/article/details/119998274
```





