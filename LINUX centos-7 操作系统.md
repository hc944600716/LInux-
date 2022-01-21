## LINUX centos-7 操作系统

## 1.Linux 优点

## 1.完全免费

Linux是一款完全免费的操作系统，任何人都可以从网络上下载到它的源代码，并可以根据自己的需求进行定制化的开发，而且没有版权限制。

## 2.安全稳定

Linux采取了很多安全技术措施，包括读写权限控制、带保护的子系统、审计跟踪、核心授权等，这为网络环境中的用户提供了安全保障。实际上有很多运行Linux的服务器可以持续运行长达数年而无须重启，依然可以性能良好地提供服务，其安全稳定性已经在各个领域得到了广泛的证实。

## 3.多用户，多任务

多用户是指系统资源可以同时被不同的用户使用，每个用户对自己的资源有特定的权限，互不影响。多任务是现代化计算机的主要特点，指的是计算机能同时运行多个程序，且程序之间彼此独立，Linux内核负责调度每个进程，使之平等地访问处理器。由于CPU处理速度极快，从用户的角度来看所有的进程好像在并行运行。

## 4.独立性

## 5.可移植性

Linux中95%以上的代码都是用C语言编写的，由于C语言是一种机器无关的高级语言，是可移植的，因此Linux系统也是可移植的。

# 2.Linux 命令

## 2-1.修改网络配置

vmware 选择nat ，创建一个局域网时主机与本机连接交互

ip addr 查看网络配置

cd /etc/sysconfig/network-scripts/

vi ifcfg-en33 

按i插入模式

esc退出编辑

:wq 保存 退出

修改前：

<img src="C:\Users\94460\AppData\Roaming\Typora\typora-user-images\image-20211107194459578.png" alt="image-20211107194459578" style="zoom:80%;" />

修改后：

BOOTPROTO=static

ONBOOT=yes

IPADRR=192.168.2.190

NETMASK=255.255.255.0

GATEWAY=192.168.2.1

![image-20211107195107468](C:\Users\94460\AppData\Roaming\Typora\typora-user-images\image-20211107195107468.png)

刷新网卡配置 重启

systemctl restart network

**注意 ：linux ip地址网络号 与 vmware 8的IP地址网络号 保持一致

## 2-2.目录结构

- / 

- /root 

- /bin， 存放常用命令的目录，如vi,su

- /sbin, 具有一定权限权限才能使用的命令

- /mnt,  默认挂载光驱和软驱的目录

- /etc,  存放配置的想改文件

- /var， 存放经常变化的文件，如网络连接的sock文件，log

- /boot， 存放引导系统文件启动的相关文件

- /usr, 安装一个软件的默认安装目录，相当于widows下的program FIles

- /proc，此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有/proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/*等

- /tmp： 一般用户或正在执行的程序临时存放文件的目录,任何人都可以访问,重要数据不可放置在此目录下

- /opt：给主机额外安装软件所摆放的目录。如：FC4使用的Fedora 社群开发软件，如果想要自行安装新的KDE 桌面软件，可以将该软件安装在该目录下。以前的 Linux 系统中，习惯放置在 /usr/local 目录下

- /lost+fount： 系统异常产生错误时，会将一些遗失的片段放置于此目录下，通常这个目录会自动出现在装置目录下。如加载硬盘于/disk 中，此目录下就会自动产生目录/disk/lost+found

- /srv： 服务启动之后需要访问的数据目录，如www服务需要访问的网页数据存放在/srv/www内

- /del ,类似windows资源管理器

  

## 2-3.目录命令
  ### 2-3-1 pwd

  查看当前工作目录

  ```
  [root@localhost ~]# pwd
  /root
  ```

  ### 2-3-1  ls

  查看当前目录下的文件、

  ls -al 长格式显示所有文件

  ls - i 查看文件的i节点号

  ```
  [root@localhost ~]# ls -al
  总用量 36
  dr-xr-x---.  4 root root  225 10月 21 21:41 .
  dr-xr-xr-x. 18 root root  245 10月 21 21:30 ..
  -rw-------.  1 root root 2786 10月 13 03:34 anaconda-ks.cfg
  -rw-------.  1 root root 2786 11月  7 04:01 .bash_history
  -rw-r--r--.  1 root root   18 12月 28 2013 .bash_logout
  -rw-r--r--.  1 root root  176 12月 28 2013 .bash_profile
  -rw-r--r--.  1 root root  176 12月 28 2013 .bashrc
  drwx------.  3 root root   18 10月 18 18:19 .cache
  drwxr-xr-x.  3 root root   18 10月 18 18:19 .config
  -rw-r--r--.  1 root root  100 12月 28 2013 .cshrc
  -rw-------.  1 root root 2025 10月 13 03:34 original-ks.cfg
  -rw-r--r--.  1 root root    0 10月 21 21:41 PingUp.txt
  -rw-r--r--.  1 root root  129 12月 28 2013 .tcshrc
  -rw-------.  1 root root  132 10月 21 08:31 .xauthifXSRD
  
  ```

###   2-3-2  cd 

功能 ：切换到指定目录

cd 绝对目录

cd 或cd-  cd /home  cd .. 返回家目录

cd - 返回上一级目录

cd .. 返回当前目录的上一级

../  上一级目录 

./ 当前目录

—  用户的家目录

### 2-3-3 mkdir

mkdir 路径 /文件名（-p 递归创建文件） 创建空文件夹

### 2-3-4 rm

rm 删除文件夹或文件 （-f  强制删除 -i 在删除前提示  -r 递归删除）

删除目录 rm -rf  ./目录

rmdir 只能用于删除空文件夹

### 2-3-5  cp

cp 路径/文件 （需要复制的文件）路径/文件（复制的文件） 可用于文件重命名

```
[root@localhost ~]# cp PingUp.txt  2.txt
```

### 2-3-6 mv

mv 文件路径/文件名 （移动到） 文件路径/文件名

重命名  mv 文件名 新文件名



## 2-4 文件相关命令

### 2-4-1 touch 

新建一个空文件

```
[root@localhost ~]# ls
1  anaconda-ks.cfg  original-ks.cfg  PingUp.txt
[root@localhost ~]# touch 123
[root@localhost ~]# ls
1  123  anaconda-ks.cfg  original-ks.cfg  PingUp.txt
```

###   2-4-2 echo  

​	 echo 输出信息

```
[root@localhost ~]# echo nihao
nihao
```

###   2-4-3 cat

​	cat  查看文件

```
[root@localhost ~]# cat 1.txt 
hollow 
```

###   2-4-4 more

 	 more 查看一页文件

```
[root@localhost ~]# more 1.txt 
import requests as re import lxml from bs4 import BeautifulSoup from PIL import Image def img_code():     url="https://
so.gushiwen.cn/user/login.aspx?from=http://so.gushiwen.cn/user/collect.aspx"     header={"User-Agent":"Mozilla/5.0 (Win
dows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36"}     responce=re.get(url
,headers=header) # print(responce.text)     soup=BeautifulSoup(responce.text,'lxml')     soup.select("img")[1]["src"]  
       soup=BeautifulSoup(responce.text,'lxml')     url_1=soup.select("img")[1]["src"]     url_2="https://so.gushiwen.c
n"     url_img=url_2+url_1 # print(url_img)     img_code=re.get(url_img,headers=header) # print(img_code.content)     w
ith open(r"./code.jpg","wb") as f:         f.write(img_code.content)         f.close     img=Image.open(r"./code.jpg") 
    img.show()   if __name__=='__main__':     img_code() code=input("请输入验证码：") url_login="https://so.gushiwen.cn
/user/login.aspx?from=http://so.gushiwen.cn/user/collect.aspx" data={    " from":"http://so.gushiwen.cn/user/collect.as
px",     "email":"15696791165",     "pwd":"hechuan520",     "code":code,     "denglu":"登录" }   responce = re.get(url_
login,data=data) print(response)

```

空格键 ：向下翻一页

enter ： 向下翻一行

q：退出more，不在显示内容

ctrl + f ：向下翻一页

ctrl + b ：返回上一页

=：输出当前行的行号

：f ：输出文件名和当前行好



### 2-4-5 head

head  -n 查看文件内容只看头n行 默认10行

### 2-4-6 tail

tail -n 10  文件  查看文件末尾n行 默认十行

tail -f follow输出文件修改的内容，用于追踪文件修改

### 2-4-7 wc          

word count

wc 统计指定文本的行数 ，字数，字节数

-l：line 显示行数

-w :显示单词数

-c ： 显示字节数

### 2-4-8 stat

查看文件具体存储信息和时间等信息

```
[root@localhost ~]# stat 1.txt 
  文件："1.txt"
  大小：1234            块：8          IO 块：4096   普通文件
设备：803h/2051d        Inode：67415798    硬链接：1
权限：(0644/-rw-r--r--)  Uid：(    0/    root)   Gid：(    0/    root)
环境：unconfined_u:object_r:admin_home_t:s0
最近访问：2021-11-07 06:52:28.397461798 -0800
最近更改：2021-11-07 06:52:23.355412945 -0800
最近改动：2021-11-07 06:52:23.355412945 -0800
创建时间：-
```



### 2-4-9 file 

查看文件类型

```
[root@localhost ~]# file 1.txt 
1.txt: UTF-8 Unicode text, with very long lines
```

### 2-4-10 wegt

​	下载网络文件

-b：background 后台下载

-p： dictionary-profix 下载到指定目录

-t ：tries 尝试最大数

-c：continue 断点传输

-p：page-requisite 下载页面所有内容 包括图片，视频

安装 wegt ：yum install wegt

```
[root@localhost ~]# wget https://i0.hdslb.com/bfs/face/4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp
--2021-11-08 23:36:49--  https://i0.hdslb.com/bfs/face/4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp
正在解析主机 i0.hdslb.com (i0.hdslb.com)... 42.248.92.1, 240e:f7:a060:206:1::6
正在连接 i0.hdslb.com (i0.hdslb.com)|42.248.92.1|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：1328 (1.3K) [image/webp]
正在保存至: “4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp”

100%[=============================================================================>] 1,328       --.-K/s 用时 0s      

2021-11-08 23:36:50 (438 MB/s) - 已保存 “4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp” [1328/1328])
```

### 2-4-11 find

find [范围]  [匹配条件]

-name : 按名称查找

-user : 按照所有者

 -size ：按照大小查找 （+n 大于 -n小于，n 等于）

查找 /root 下的名为 1. txt的文件

```
[root@localhost ~]# find /root 1.txt
/root
/root/.bash_logout
/root/.bash_profile
/root/.bashrc
/root/.cshrc
/root/.tcshrc
/root/original-ks.cfg
/root/anaconda-ks.cfg
/root/.cache
/root/.cache/abrt
/root/.cache/abrt/lastnotification
/root/.config
/root/.config/abrt
/root/.bash_history
/root/.xauthifXSRD
/root/PingUp.txt
/root/1
/root/123
/root/1.txt
/root/.xauth0U4QKP
/root/4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp
1.txt
```

find /root  -user root  查找 /root 下所有者为root 的文件

```
[root@localhost ~]# find /root  -user root
/root
/root/.bash_logout
/root/.bash_profile
/root/.bashrc
/root/.cshrc
/root/.tcshrc
/root/original-ks.cfg
/root/anaconda-ks.cfg
/root/.cache
/root/.cache/abrt
/root/.cache/abrt/lastnotification
/root/.config
/root/.config/abrt
/root/.bash_history
/root/.xauthifXSRD
/root/PingUp.txt
/root/1
/root/123
/root/1.txt
/root/.xauth0U4QKP
/root/4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp
```

find  /root  -size  -102400  在/root 下查找小于100m的文件

```
[root@localhost ~]# find  /root  -size  -102400
/root
/root/.bash_logout
/root/.bash_profile
/root/.bashrc
/root/.cshrc
/root/.tcshrc
/root/original-ks.cfg
/root/anaconda-ks.cfg
/root/.cache
/root/.cache/abrt
/root/.cache/abrt/lastnotification
/root/.config
/root/.config/abrt
/root/.bash_history
/root/.xauthifXSRD
/root/PingUp.txt
/root/1
/root/123
/root/1.txt
/root/.xauth0U4QKP
/root/4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp
```

###   2-4-12  grep

​	grep [参数] 查找内容 源文件

 	grep -n import 1.txt  查找1.txt 文件中的 import 个数 并红色显示 

![image-20211109155703476](C:\Users\94460\AppData\Roaming\Typora\typora-user-images\image-20211109155703476.png)

​		grep  -c  import 1. txt  返回1.txt中查找到的 import 的个数

```
[root@localhost ~]# grep  -c  import  1.txt 
4
```

### 	2-4-13 which

 	which [选项] 命令

查找cd 命令所在目录

```
[root@localhost ~]# which cd
/usr/bin/cd
```

##  2-5 日期命令

2-5-1 data

date [选项] [格式]

显示时间

-s set 以字符串格式设置时间

格式

+%Y ：显示当前年份

+%m：显示当前月份

+%d：显示当前是哪一天

+%H ：显示当前小时

+%M：显示当前分

+%S : 显示当前秒

+%Y-%m-%d：显示当前年月日

```
[root@localhost ~]# date +%Y-%m-%d
2021-11-09
```

 date +%Y-%m-%d  >> 21.txt  将时间输入到21.txt      >覆盖  >> 追加

```
[root@localhost ~]#  date +%Y-%m-%d  >>21.txt
[root@localhost ~]# ls
1    1.txt   4dc2d0a465c1d32e7e4b6a4b8aec6b20a95eb793.jpg@240w_240h_1c_1s.webp  original-ks.cfg
123  21.txt  anaconda-ks.cfg                                                    PingUp.txt
[root@localhost ~]# cat 21.txt 
2021-11-09
```

“+%Y-%m-%d  %H%M%S”： 显示当前年月日 时分秒

```
[root@localhost ~]# date
2021年 11月 09日 星期二 00:16:11 PST

```



## 2-6 进程相关命令

### 2-6-1  ps

ps [ 选项]

查看形同中的全部进程

-a  all 显示现行机所有程序，包括其他用户

-u ：userlist 以用户为主的格式显示进程状况

-x： 显示所有程序 ，不以终端机区分

ps -xua |grep sftp 查找进程中的 sftp 的进程id

```
[root@localhost ~]# ps -xua |grep sftp
root       3528  0.0  0.1  72252  2820 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root       3536  0.0  0.1  72252  2672 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root       3544  0.0  0.1  72252  2676 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root       3552  0.0  0.1  72252  2676 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root       3560  0.0  0.1  72252  2680 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root       3568  0.0  0.1  72252  2676 ?        Ss   11月08   0:00 /usr/libexec/openssh/sftp-server
root     109777  0.0  0.0 112828   976 pts/1    S+   00:34   0:00 grep --color=auto sftp
```

每一项内容解释

| 项      | 含义                                                         |
| ------- | ------------------------------------------------------------ |
| USER    | 进程由那个用户产生                                           |
| PID     | 进程id                                                       |
| %CPU    | 该进程占用CPU的百分比                                        |
| %MEM    | 该进程占用内存的百分比                                       |
| VSZ     | 占用虚拟内存大小，单位kb                                     |
| RSS     | 占用世界物理内存大小，单位kb                                 |
| TTY     | 表示该进程在那个终端中运行                                   |
| STAT    | 进程状态 R(运行)，S(休眠)，T(停止)，s(包含的子进程)，+(后台进程) |
| COMMOND | 产生该进程的命令                                             |





















## SH命令



```sh
[root@localhost tmp]# sh example.sh 
our first example

we are currently in the flowing directory
/tmp

This directory contaions the following files
example.sh                                                                    systemd-private-38edda7e5094409582e9d93a5433ae03-chronyd.service-5YmxH7
ssh-gBxx85p0d1ov                                                              systemd-private-38edda7e5094409582e9d93a5433ae03-colord.service-Wd4DFS
ssh-nvMuaIkuTbMk                                                              systemd-private-38edda7e5094409582e9d93a5433ae03-cups.service-ydOqs4
ssh-x2AV7kTi2UYC                                                              systemd-private-38edda7e5094409582e9d93a5433ae03-fwupd.service-rApk64
systemd-private-09b620cd30624228852726091e5457bc-bolt.service-KLyS6j          systemd-private-38edda7e5094409582e9d93a5433ae03-rtkit-daemon.service-TbBUwo
systemd-private-09b620cd30624228852726091e5457bc-chronyd.service-YbEROr       systemd-private-b68fba5dd6e742b28279eb117534fe96-bolt.service-y3Cly5
systemd-private-09b620cd30624228852726091e5457bc-colord.service-0sDVDn        systemd-private-b68fba5dd6e742b28279eb117534fe96-chronyd.service-qx2I0M
systemd-private-09b620cd30624228852726091e5457bc-cups.service-4o0omg          systemd-private-b68fba5dd6e742b28279eb117534fe96-colord.service-8caOST
systemd-private-09b620cd30624228852726091e5457bc-rtkit-daemon.service-q9s7DS  systemd-private-b68fba5dd6e742b28279eb117534fe96-cups.service-GNwlAX
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-bolt.service-A3CcR5          systemd-private-b68fba5dd6e742b28279eb117534fe96-fwupd.service-Cu8Z1v
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-chronyd.service-WDuN9K       systemd-private-b68fba5dd6e742b28279eb117534fe96-rtkit-daemon.service-Uh2CFO
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-colord.service-e73y5U        tracker-extract-files.1000
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-cups.service-o971JZ          vmware-root_570-2998936411
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-fwupd.service-dns8Dm         vmware-root_592-2689275023
systemd-private-0e40f6f9d44346be9ee6047b935a63a0-rtkit-daemon.service-wWKUJJ  vmware-root_600-2722697857
systemd-private-2205989df7d94a7ba73a2c534cfebe5e-bolt.service-Plrpk3          vmware-root_617-4022243191
systemd-private-2205989df7d94a7ba73a2c534cfebe5e-chronyd.service-c59Wl8       vmware-root_625-4021587817
systemd-private-2205989df7d94a7ba73a2c534cfebe5e-colord.service-Gr3FWY        vmware-root_643-3979708515
systemd-private-2205989df7d94a7ba73a2c534cfebe5e-cups.service-MNCVj4          vmware-root_651-4013395565
systemd-private-2205989df7d94a7ba73a2c534cfebe5e-rtkit-daemon.service-GR736o  vmware-root_656-2689274927
systemd-private-38edda7e5094409582e9d93a5433ae03-bolt.service-13ZMIX          yum_save_tx.2021-11-08.22-57.W187ai.yumtx
[root@localhost tmp]# cat example.sh 
#!/bin/sh
echo "our first example"
echo #this inserts an empty line in output
echo 'we are currently in the flowing directory'
/bin/pwd
echo 
echo "This directory contaions the following files"
/bin/ls

```

### 1.变量

赋值 

```sh
name=“何川” 中间有空格需要加引号
number=10
echo $name
echo $number
结果
[root@localhost tmp]# name=“hehcuan”
[root@localhost tmp]# number=10
[root@localhost tmp]# echo $name
“hehcuan”
[root@localhost tmp]# echo $number
10

```

#### 变量叠加

```sh
name="林志玲"
aa=123
aa="${aa}"456
aa=${aa}789
echo $name
set  #变量删除
unset name
```

结果

```shell
[root@localhost tmp]# name="林志玲"
[root@localhost tmp]# aa=123
[root@localhost tmp]# aa="${aa}"456
[root@localhost tmp]# aa=${aa}789
[root@localhost tmp]# echo $name
林志玲
[root@localhost tmp]# echo $aa
123456789
[root@localhost tmp]# unset name
[root@localhost tmp]# echo $name
                              #空一行

```

```sh
#!/bin/sh
num1=$1
num2=$2
sum=$((num1+num2))
echo $sum
```

结果

```shell
[root@localhost tmp]# sh example.sh  1  2
3
```

$@ 代表全部参数 单独划分

$# 代表全部参数 统一整体

$n $0代表
