# Linux 学习笔记（二）基本 Linux 命令

* 本笔记基于 刘遄 的《Linux 就该这么学》一书。
* 本章将首先介绍 Shell 语言，然后介绍各种 Linux 操作命令，如帮助命令、常用系统工作命令、系统状态检测命令、工作目录切换命令、文本文件编辑命令、文件目录管理命令、打包压缩与搜索命令等。
* 在本章学习完毕后，建议浏览下面的网页继续学习 Linux 命令：
  * [https://www.linuxcool.com](https://www.linuxcool.com/)



## Shell 简介

### 为什么要使用 Shell？

#### 系统内核

* 众所周知，计算机硬件是由运算器、控制器、存储器、输入/输出设备等共同组成的，而让各种硬件设备**各司其职**又**协同运行**的东西就是系统内核。
* Linux 系统内核负责完成硬件资源的分配和调度等管理任务。
* 由此可见，系统内核对于计算机的正常运行时十分重要的，因此不建议去**直接编辑**内核参数，而是让用户通过基于**系统调用接口**开发出的**程序和服务**来管理计算机，以满足日常工作的需要。

![1](Linux_2_pic/1.png)

#### 图形化工具的不足

* Linux 中的很多**图形化工具**（比如逻辑卷管理器[ Logical Volumn Manager，LVM ]）确实非常好用，极大地降低了运维人员操作出错的概率，值得称赞。
* 但是，很多图形化工具其实是调用了**脚本**来完成相应的工作，往往只是为了完成某种工作而设计的，缺乏Linux命令原有的**灵活性**及**可控性**。而且图形化工具相较于 Linux 命令行界面更加**消耗系统资源**，因此经验丰富的运维人员甚至都不会给 Linux 系统**安装图形界面**，需要开始运维工作时直接通过**命令行模式远程连接**过去，不得不说这样做确实挺高效的。



### Shell 终端与 Bash 解释器

* Shell，也称为**终端**或**壳**，就是一种命令行工具，充当的是人与内核之间的翻译官，用户把一些命令"告诉"终端，它再调用一些程序和服务来完成某些工作。
* Bourne-Again SHell，Bash，是一种解释器（终端），也是现在包括红帽系统在内的许多主流 Linux 系统默认使用该终端。
* 选择 Bash 解释器作为命令行终端主要由如下 4 项优势：
  * 上下方向键来调取**历史执行**的 Linux 命令；
  * 命令或参数仅需输入前几位就可以用 **Tab 键**补全；
  * 具有强大的**批处理脚本**；
  * 具有实用的**环境变量**功能。
* 具备一定工作经验以后，才能领悟 Linux 命令的奥秘。



### 打开命令行

* 开启虚拟机，如果进入蓝色锁屏界面，上拉即可进入登录界面。我们不能直接登录普通用户 linuxprobe，而是用管理员登录。
* 点击 Not listed? 按键，弹出对话框，输入用户名（root），以及安装时的管理员登录密码。即可以管理员身份运行。

![2](Linux_2_pic/2.png)

* 进入主界面，在桌面上右键，选择 Open in Terminal。这样就打开了一个 Shell 窗口：

![3](Linux_2_pic/3.png)

* 接着就可以开始输入命令了，下面是输入了 man man 命令：

![4](Linux_2_pic/4.png)



## 查看帮助命令

* 如何和 Bash 好好沟通是最重要的问题。
* 要想准确、高效地完成任务，除了依赖于命令本身，还应该根据实际情况**灵活调整各种命令的参数**。

### Linux 命令格式

* 常见执行 Linux 命令的格式是这样的：

  * 命令名称 【命令参数】 【命令对象】
  * 注意，命令名称、命令参数、命令对象之前请用空格键分隔。
* 命令对象：要处理的文件、目录、用户等资源；
* 命令参数：可以用**长格式**，也可以用**短格式**：

  * 若用长格式（完整的选项名称），用 -- 作为前缀；
  * 若用短格式（单个字母的缩写），用 - 作为前缀。
* Linux 新手不会执行命令是因为参数比较复杂，参数值需要随不同的命令和需求情况而发生改变。灵活搭配参数需要长时间的积累。

```shell
man --help # 长格式
man -h # 短格式
```

 

### man 命令

* 以 man 命令为第一个例子来介绍。man 命令是用来查看帮助文本的命令。
* 举一个 man 命令的小例子，输入 "man man"，即可得到 man 命令本身的帮助文本：

![5](Linux_2_pic/5.png)



### 帮助信息常用操作按键

* 列举了一些按键的用途：

|   按键    |                用途                 |
| :-------: | :---------------------------------: |
|   space   |             向下翻一页              |
| Page down |             向下翻一页              |
|  Page up  |             向上翻一页              |
|   home    |            直接前往首页             |
|    end    |            直接前往尾页             |
|     /     | 从上至下搜索某个关键词，如 "/linux" |
|     ?     | 从下至上搜索某个关键词，如 "?linux" |
|     n     |     定位到下一个搜索到的关键词      |
|     N     |     定位到上一个搜索到的关键词      |
|     q     |            退出帮助文档             |



### 帮助信息结构与意义

* 一般帮助信息会很长很多，如果不了解目录结构，会难以及时找到需要的信息。

|  结构名称   |        代表的意义        |
| :---------: | :----------------------: |
|    NAME     |           名称           |
|  SYNOPSIS   |    参数的大致使用方法    |
| DESCRIPTION |         介绍说明         |
|  EXAMPLES   | 例子演示（附带简单说明） |
|  OVERVIEW   |           概述           |
|  DEFAULTS   |        默认的功能        |
|   OPTIONS   | 具体的可用选项（带介绍） |
| ENVIRONMENT |         环境变量         |
|    FILES    |        用到的文件        |
|  SEE ALSO   |         相关资料         |
|   HISTORY   |    维护历史与联系方式    |



## 常用系统工作命令

* 下面介绍几个常用的系统工作命令。其他命令将随着后面的章节学习进行介绍。

### echo 命令

* echo 命令用于在终端输出**字符串**或**变量**提取后的值。

#### 格式

* echo [字符串 | $变量]

#### 例子

* 把**字符串** "Linuxprobe.com" 输出到终端屏幕的命令：

```shell
echo linuxprobe.com
# linuxprobe.com
```

* 使用 $ 方式提取**变量** SHELL 的值，并将其输出到屏幕上：

```shell
echo $SHELL
# /bin/bash
```



### date 命令

* date 命令用于**显示**和**设置**系统的**时间或日期**。

#### 格式

* date [选项] [+指定的格式]

#### 用法

* 在 date 命令中输入以 "+" 开头的参数，可按照指定的格式来输出系统的时间或日期。
* 在日常工作时可以把**备份数据的命令**与**指定格式输出的时间信息**结合，
  * 例如，可按照将文件 "年-月-日" 打包成 "backup-2017-9-1.tar.gz"，用户只要看一眼文件名称就能大概了解到文件的备份时间。

#### 参数

* date 命令中常见的参数格式及作用如表所示：

| 参数 |      作用      |
| :--: | :------------: |
|  %t  |  跳格[Tab 键]  |
|  %H  | 小时（00~23）  |
|  %I  | 小时（00~12）  |
|  %M  | 分钟（00~59）  |
|  %S  |  秒（00~59）   |
|  %j  | 今年中的第几天 |

#### 例子

* 用**默认格式**查看当前系统时间：

```shell
date
# Thu Jul 16 17:09:36 CST 2020
```

* 按照 "年-月-日  小时:分钟:秒" 格式查看当前系统时间：

```shell
date "+%Y-%m-%d %H:%M:%S"
# 2020-07-16 17:10:15
```

* 将系统的当前时间设置为 2017 年 9 月 1 日 8 点 30 分：

```shell
date -s "20170901 8:30:00"
# Fri Sep  1 08:30:00 CST 2017
```

* 重新查看当前系统时间：

```shell
date
# Fri Sep  1 08:30:06 CST 2017
```

* 查看今天是当年的第几天（这个参数能很好地区分备份时间的新旧，数字越大越靠近当前时间）：

```shell
date "+%j"
# 244
```



### reboot 命令

* reboot 命令用于重启系统，其格式直接输入 reboot 即可。
* 重启计算器这种操作会涉及硬件资源的管理权限，因此默认**只有 root 管理员**来重启。



### poweroff 命令

* poweroff 命令用于关闭系统，其格式直接输入 poweroff 即可。
* 关闭电脑这种操作会涉及硬件资源的管理权限，因此默认**只有 root 管理员**来重启。



### wget 命令

* wget 命令用于在终端中下载网络文件。

#### 注意

* 该函数在目前未完成网络配置的时候无法进行该实验操作。等后面学完网卡的配置章节后再来进行实验。

#### 格式

* wget [参数] 下载地址

#### 参数

* wget 命令的参数如下：

| 参数 |                 作用                 |
| :--: | :----------------------------------: |
|  -b  |             后台下载模式             |
|  -P  |            下载到指定目录            |
|  -t  |             最大尝试次数             |
|  -c  |               断点续传               |
|  -p  | 下载页面内所有资源，包括图片、视频等 |
|  -r  |               递归下载               |

#### 例子

* 本节中的例子没有实验结果，因为尚未配置网卡。
* 下载《linux 就该这么学》的电子文档：

```shell
wget http://www.linuxprobe.com/docs/LinuxProbe.pdf
```

* 递归下载 www.linuxprobe.com 网站内的所有页面数据以及文件：

```shell
wget -r -p http://www.linuxprobe.com
```



### ps 命令

* ps 命令用于查看系统中的进程状态。

#### 格式

* ps [参数]

#### 用法

* ps 命令会产生很多的输出值；
* 通常会将 ps 命令与第 3 章的管道符技术搭配使用，用来抓取与某个指定服务进程相对应的 PID 号码。

#### 参数

* ps 命令的常见参数以及作用如下：

| 参数 |                作用                |
| :--: | :--------------------------------: |
|  -a  | 显示所有进程（包括其他用户的进程） |
|  -u  |        用户以及其他详细信息        |
|  -x  |       显示没有控制终端的进程       |

#### 进程状态

* Linux 系统中时刻运行着许多进程，如果能够合理管理它们，就可以优化系统性能。
* 在 Linux 系统中，有 5 种常见的状态：
  * R（运行）：进程**正在运行**或**在队列中等待**。
  * S（中断）：进程处于**休眠**中，当某**条件形成**后或者**接收到信号**时，则脱离该状态。
  * D（不可中断）：进程**不响应**系统**异步信号**，即便用 kill 命令也**不能将其中断**。
  * Z（僵死）：进程**已经终止**，但进程**描述符**依然存在，直到**父进程调用 wait4() 系统函数**后将进程释放。
  * T（停止）：进程收到**停止信号**后**停止运行**。

#### 重要实例

* **ps aux** 可以查看所有进程状态信息：
  * 需要注意，在 Linux 系统中短格式是可以合并的，合并后保留一个 "-" 号即可。
  * 另外，ps 命令可允许参数不加 "-" 号，因此可直接写成 ps aux 的样子。

```shell
ps aux
# 下面是输出：
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root          1  1.3  0.4  53672  7604 ?        Ss   22:08   0:02 /usr/lib/syste
root          2  0.0  0.0      0     0 ?        S    22:08   0:00 [kthreadd]
root          3  0.1  0.0      0     0 ?        S    22:08   0:00 [ksoftirqd/0]
root          4  0.0  0.0      0     0 ?        S    22:08   0:00 [kworker/0:0]
root          5  0.0  0.0      0     0 ?        S<   22:08   0:00 [kworker/0:0H]
root          6  0.0  0.0      0     0 ?        S    22:08   0:00 [kworker/u256:
root          7  0.1  0.0      0     0 ?        S    22:08   0:00 [migration/0]
root          8  0.0  0.0      0     0 ?        S    22:08   0:00 [rcu_bh]
...后面的省略不表
```

#### 各列输出值的含义

* 有必要了解一下各个列输出值的含义：

|  列名   |            含义            |
| :-----: | :------------------------: |
|  USER   |        进程的所有者        |
|   PID   |         进程 ID 号         |
|  %CPU   |        运算器占用率        |
|  %MEM   |         内存占用率         |
|   VSZ   |  虚拟内存使用量（单位KB）  |
|   RSS   | 占用的固定内存量（单位KB） |
|   TTY   |          所在终端          |
|  STAT   |          进程状态          |
|  START  |        被启动的时间        |
|  TIME   |    实际使用 CPU 的时间     |
| COMMAND |       命令名称与参数       |



### top 命令

* top 命令用于动态地监视进程活动与系统负载等信息，其格式直接输入 top 即可。
* top 命令可以看做是 Linux 中强化版的**任务管理器**。

#### 运行界面信息

* top 命令的执行界面如下图所示：

![6](Linux_2_pic/6.png)

* top 命令的前 5 行为系统整体统计信息，其含义为：
  * 第 1 行：系统时间、运行时间、登录终端数、系统负载。
    * 提供负载的三个数值分别为 1 分钟、5 分钟、15 分钟内的平均值，数值越小负载越低。
  * 第 2 行：进程总数、运行中的进程数、睡眠中的进程数、停止的进程数、僵死的进程数。
  * 第 3 行：用户占用资源百分比、系统内核占用资源百分比、改变过优先级的进程资源百分比、空闲的资源百分比等。
    * 该行数据均为 CPU 数据并以百分比格式显示，例如 98.9 id 意思是有 98.9% 的 CPU 处理器资源处于空闲。
  * 第 4 行：物理内存总量、内存使用量、内存空闲量、作为内核缓存的内存量。
  * 第 5 行：虚拟内存总量、虚拟内存使用量、虚拟内存空限量、已被提前加载的内存量。
* 后续的是所有进程的情况。



### pidof 命令

* pidof 命令用于查询某个指定服务进程的 PID 值。

#### 格式

* pidof [参数] [服务名称]

#### 用法

* 每个进程的进程号码值（PID）是唯一的，可以通过 PID 区分不同的进程。

#### 例子

* 可使用如下命令查询本机上 sshd 服务程序的 PID：

```shell
pidof sshd
# 2158
```



### kill 命令

* kill 命令用于**终止**某个**指定 PID** 的服务进程。

#### 格式

* kill [参数] [进程 PID]

#### 例子

* 下面的例子使用 kill 命令把上面用 pidof 命令查询到的进程终止掉。相当于强制停止 sshd 服务。

```shell
kill 2156
```



#### killall 命令

* killall 命令用于终止某个指定名称的服务**所对应的全部进程**。

#### 格式

* killall [参数] [进程名称]

#### 用法

* 通常来说，复杂软件的服务程序会有**多个进程协同**为用户提供服务，如果逐个去结束进程比较麻烦；
* 使用 killall 命令来**批量结束**某个服务程序带有的全部进程。

#### 例子

* 下面以 httpd 服务程序为例，来结束其全部进程。由于 RHEL7 系统默认没有安装 httpd 服务程序，所以本实验暂时无法执行。

```shell
pidof httpd
# 13581 13580 13579 13578 13577 13576
killall httpd
pidof httpd
```



### 注意点

* 如果在终端中执行一个命令后想立即停止，可以使用 `Ctrl` + `C` 组合键。
* 如果命令执行时不断在屏幕上输出信息，影响到后续命令的输入，可以在执行末尾添加一个 & 符号，命令将进入后台来执行。



## 系统状态检测命令

* 为了更快、更好的了解 Linux 服务器，必须具备快速查看 Linux 系统运行状态的能力，在此方面有很多非常相关的命令。

### ifconfig 命令

* ifconfig 命令用于**获取网卡配置**与**网络状态**等信息。

#### 格式

* ifconfig [网络设备] [参数]

#### 返回信息

* 下面给出一个 ifconfig 命令的返回信息：

```shell
ifconfig
```

![7](Linux_2_pic/7.png)

* ifconfig 命令主要查看的就是网卡名称、**inet** 参数后面的 **ip 地址**，**ether** 参数后面的**网卡物理地址**（又称为 MAC 地址），
  * 以及 **RX、TX** 的**接收数据包**与**发送数据包**的**个数及累计流量**。



### uname 命令

* uname 命令用于查看**系统内核与系统版本等信息**。

#### 格式

* uname [-a]

#### 返回信息

* 在使用 uname 命令时，一般会固定搭配上 -a 参数来完整地查看系统信息。
* 下面给出一个命令执行的例子：

```shell
uname -a
# Linux linuxprobe.com 3.10.0-123.el7.x86_64 #1 SMP Mon May 5 11:16:57 EDT 2014 x86_64 x86_64 x86_64 GNU/Linux
```

* 上述命令返回的是：当前系统内核名称、主机名、内核发行版本、节点名、系统时间、硬件名称、硬件平台、处理器类型以及操作系统名称等信息。



### uptime 命令

* uptime 命令用于查看**系统的负载信息**。其格式直接输入 uptime 即可。

#### 返回信息

* 下面给出一个命令执行的例子：

```shell
uptime
#  14:02:15 up  5:44,  2 users,  load average: 0.07, 0.03, 0.05
```

* 该命令输出了当前系统时间、系统已运行时间、启用终端数量以及**平均负载值**等信息。
* 平均负载值指的是系统在最近 1 分钟、5 分钟、15 分钟内的压力情况。
  * 负载值越低越好，尽量不要长期超过 1，在生产环境中不要超过 5。



### free 命令

* free 命令用于显示当前系统中**内存的使用量**信息。

#### 格式

* free [-h]

#### 返回信息

* 为了保证 Linux 系统不会因资源耗尽而突然宕机，需要时刻关注**内存使用量**。
* 使用 free 命令可以结合 -h 参数以更人性化的方式输出当前内存的实时使用信息：

```shell
free -h
```

![8](Linux_2_pic/8.png)

* 每列的信息：

|  total   |  used  |  free  |      shared      |     buffers      |    cached    |
| :------: | :----: | :----: | :--------------: | :--------------: | :----------: |
| 内存总量 | 已用量 | 可用量 | 进程共享的内存量 | 磁盘缓存的内存量 | 缓存的内存量 |



### who 命令

* who 命令用于查看当前**登入主机的用户终端**信息。

#### 格式

* who [参数]

#### 返回信息

* 下面给出一个执行 who 命令的例子：

```shell
who
```

![9](Linux_2_pic/9.png)

* 该命令显示了正在登录本机的用户的名称以及他们正在开启的终端信息：
  * 输出的三列内容分别是：登录的用户名、终端设备、登录到系统的时间。



### last 命令

* last 命令用于查看**所有系统的登录记录**。

#### 格式

* last [参数]

#### 返回信息

* 下面给出一个 last 命令执行的例子：

```shell
last
```

![10](Linux_2_pic/10.png)

* last 命令用于查看本机的登录记录。
  * 但由于这些信息都是以日志文件的形式保存在系统中，因此黑客可以很容易地对内容进行篡改。
  * 千万不要单纯以该命令的**输出信息而判断**系统有无被恶意入侵！



### history 命令

* history 命令用于显示**历史执行过的命令**。

#### 格式

* history [-c]

#### 基本用法

* 执行 history 能显示出当前用户在本地计算机中执行过的最近 1000 条命令记录。
  * 如果觉得 1000 不够用还可以自定义 /etc/profile 文件中的 HISTSIZE 变量值。
* 下面是执行 history 的例子（图片仅截取了一部分）：

```shell
history
```

![11](Linux_2_pic/11.png)

#### 选择历史再次执行

* 使用 "! 编码数字" 的方式可**重新执行**某个历史命令。

```shell
!7 # date 语句被执行
```

![12](Linux_2_pic/12.png)

#### 历史记录保存

* 历史命令会被保存到用户家目录中的 .bash_history 文件中。
  * Linux系统中以点（.）开头的文件均代表**隐藏文件**，这些文件大多数为**系统服务**文件，可以用 cat 命令查看其文件内容。

```shell
cat ~/.bash_history
```

![13](Linux_2_pic/13.png)

#### 清空命令记录

* 使用 -c 参数会**清空**所有的命令历史记录：

```shell
history -c
```



### sosreport 命令

* sosreport 命令用于收集系统配置及架构信息并**输出诊断文档**，其格式直接输入 sosreport 即可。

#### 用法

* 当 Linux 系统出现故障需要联系技术支持人员时，大多数时候需要先使用这个命令来简单收集系统运行状态和服务配置信息。
  * 以便让技术支持人员能够远程解决一些小问题，或让他们能提前了解某些复杂问题。

#### 例子

* 下面是一个诊断信息的例子，并且返回值上用红字标注了一些输出信息的含义。

```shell
sosreport
```

![14](Linux_2_pic/14.png)



## 工作目录切换命令

* 工作目录指的是用户当前在系统中所处的位置。由于工作目录牵涉到系统存储结构相关知识，所以在这里我们仅做了解，一些内容无法实验进行。

### pwd 命令

* pwd 命令用于显示用户**当前所处的工作目录**。

#### 格式

* pwd [选项]

#### 例子

* 下面给出一个实例：

```shell
pwd
# /root/Desktop
```



### cd 命令

* cd 命令用于**切换工作路径**。该命令可以说是最常用的 Linux 命令了。

#### 格式

* cd [目录名称]

#### cd 目录

* cd 命令后直接跟目录就是在原目录的基础上继续进入输入的文件夹。

```shell
cd Desktop/linux/
```

#### cd 路径

* cd 命令后接路径就是跳出该目录，而进入路径所在的文件目录。

```shell
cd /etc # 切换etc文件夹
cd /bin # 切换bin文件夹
```

#### cd -

* cd - 命令可以返回到上一次所处的目录：

```python
cd -
```

#### cd ~

* cd ~ 命令可以返回到当前用户的家目录。

```shell
cd ~
```

#### cd ~username

* cd ~username 命令可以返回到某个用户的家目录。

```shell
cd ~linuxprobe
```



### ls 命令

* ls 命令用于显示目录中的文件信息。

#### 格式

* ls [选项] [文件]

#### 用法

* 所处的工作目录不同，当前工作目录下的文件肯定不同。使用参数来达到目录的不同显示结果：
  * -a 参数：看到全部文件（包括隐藏文件）；
  * -l 参数：查看文件的属性、大小等详细信息；
  * -d 参数：查看该目录的属性信息。
  * 可以将两个参数整合来查看所有文件及其详细信息：

```shell
ls -al
```

![15](Linux_2_pic/15.png)

```shell
ls -ld \etc # 显示目录etc的详细属性信息
```



## 文本文件编辑命令

### cat 命令

* cat 命令用于查看**纯文本文件**（**内容较少的**）。

#### 格式

* cat [选项] [文件]

#### 例子

* 注意，Linux 系统中有多个用于查看文本内容的命令，而 cat 用于查看**内容较少**的文本文件。
* 添加 -n 参数可以**显示行号**。
* 下面给出一个文件查看的例子：

```shell
cat -n initial-setup-ks.cfg
```

![16](Linux_2_pic/16.png)



### more 命令

* more 命令用于查看纯文本文件（内容较多的）。

#### 格式 

* more [选项] 文件

#### 用法

* 如果对长篇的文本内容使用 cat 命令，信息就会在屏幕上快速翻滚，导致自己还没看到，内容就翻篇了。
* 因此对于长篇文本内容推荐使用 more 命令来查看。more 命令会在最下面用**百分比**的形式来提示您已经阅读了多少内容。

```shell
more initial-setup-ks.cfg
```

![17](Linux_2_pic/17.png)

* 使用**空格键**或**回车键**向下翻页，下面是上例翻页后的输出：

![18](Linux_2_pic/18.png)



### head 命令

* head 命令用于查看纯文本文档的前 n 行。

#### 格式

* head [选项] [文件]

#### 例子

* 使用 -n 参数加一个数字来得到显示的行数：

```shell
head -n 20 initial-setup-ks.cfg
```

![19](Linux_2_pic/19.png)



### tail 命令

* tail 命令用于查看纯文本文档的**后 n 行**或**持续刷新内容**。

#### 格式

* tail [选项] [文件]

#### 用法

* tail 的第一种用法时查看文档的后 n 行，方法和 head 完全一致，如 tail -n 20 文件名 即可。
* tail 命令的另一个功能是可以**持续刷新**一个文件的内容，当想要**实时查看最新日志文件**时，这特别有用。
  * 此时的命令格式为：tail -f 文件名。

```shell
tail -f /var/log/messages
```

![20](Linux_2_pic/20.png)



### tr 命令

* tr 命令用于替换文本文件中的字符。

#### 格式

* tr [原始字符] [目标字符]

#### 用法

* 有时需要快速替换文本中的一些词汇，或者把整个文本内容中的词汇都进行替换，如果进行手工替换工作量太大。
* 这时，可以使用 cat 先读取待处理的文本，然后通过管道符（第三部分介绍）把这些文本内容传递给 tr 命令进行替换即可。
* 这里只需了解一下例子即可，下面的例子把文本文件中的内容都替换成了大写：

```shell
cat anaconda-ks.cfg | tr [a-z] [A-Z]
```

![21](Linux_2_pic/21.png)



### wc 命令

* wc 命令用于统计指定文本的行数、字数、字节数。

#### 格式

* wc [参数] 文本

#### 参数

* 下面说明一下该命令参数的意义：

| 参数 | 作用         |
| ---- | ------------ |
| -l   | 只显示行数   |
| -w   | 只显示单词数 |
| -c   | 只显示字节数 |

#### 例子

* 第一个例子是检查某个文本文件的行数、单词数、字节数：

```shell
wc -lwc anaconda-ks.cfg
#   46   99 1043 anaconda-ks.cfg
```

* Linux 系统中，passwd 是用于保存系统账户信息的文件，可以通过统计行数来统计当前系统中有多少个用户：

```shell
wc -l /etc/passwd
# 38 /etc/passwd
```



### stat 命令

* stat 命令用于查看文件的**具体存储信息**和**时间**等信息。

#### 格式

* stat 文件名称

#### 用法

* 查看的信息主要是文件的三种时间状态：Access、Modify、Change。这三个参数的意义将在 touch 命令中详细讲解：

```shell
stat anaconda-ks.cfg
```

![22](Linux_2_pic/22.png)



### cut 命令

* cut 命令用于按 "列" 提取文本字符。

#### 格式

* cut [参数] 文本

#### 用法

* 一般来说，按"行"提取是比较简单的，只需要设置好搜索关键词即可。
* 如果按列搜索，不仅要使用 -f 参数来设置需要看的列数；
* 需要使用 -d 参数来设置间隔符号。

#### 例子

* passwd 在保存用户数据信息时，由于用户信息的每一项值之间是采用冒号来间隔的，接下来尝试提取 passwd 文件中的用户名信息，即以 ":" 为间隔符号的第一列内容：

```shell
head -n 2 /etc/passwd
...
cut -d: -f1 /etc/passwd
```

![23](Linux_2_pic/23.png)



### diff 命令

* diff 命令用于比较多个文本文件的差异。

#### 格式

* diff [参数] 文件

#### 用法

* 使用 diff 命令时，可以使用 --brief 参数来确认两个文件是否不同；
* 也可以使用 -c 参数来比较内容的具体不同之处。

#### 例子

* 由于没有建立该文本文档，只提供代码，具体例子见参考书。

```shell
diff --brief diff_A.txt diff_B.txt
diff -c diff_A.txt diff_B.txt
```



## 文件目录管理命令

* 本节介绍文件的创建、修改、复制、剪切、更名与删除等操作。

### touch 命令

* touch 命令用于**创建空白文件**或**设置文件的时间**。

#### 格式

* touch [选项] [文件]

#### 用法

* 用 touch + 文件名的方法可以直接创建空白文本文件。

```shell
touch linuxprobe
ls
```

![25](Linux_2_pic/25.png)

* 用其他参数可以设置文件内容的时间。包括修改时间（mtime，Modify），文件权限或属性的更改时间（ctime，Change），文件的读取时间（atime，Access）。

| 参数 | 作用                      |
| ---- | ------------------------- |
| -a   | 仅修改"读取时间"（atime） |
| -m   | 仅修改"修改时间"（mtime） |
| -d   | 同时修改 atime 与 mtime   |

#### 例子

* 先用 ls 命令查看一个文件的修改时间，然后修改这个文件，最后通过 touch 命令把修改后的文件时间设置成修改之前的时间。

```shell
ls -l anaconda-ks.cfg
# -rw-------. 1 root root 1043 Jul 16 01:21 anaconda-ks.cfg
echo "Visit the LinuxProbe.com to learn linux skills" >> anaconda-ks.cfg
ls -l anaconda-ks.cfg
# -rw-------. 1 root root 1090 Jul 19 16:07 anaconda-ks.cfg
touch -d "2017-05-04 15:44" anaconda-ks.cfg
ls -l anaconda-ks.cfg
# -rw-------. 1 root root 1090 May  4  2017 anaconda-ks.cfg
```

![24](Linux_2_pic/24.png)



### mkdir 命令

* mkdir 命令用于创建空白的目录。

#### 格式

* mkdir [选项] 目录

#### 用法

* 文件夹是最常见的文件类型之一，下例能创建一个单个空白目录：

```shell
mkdir linuxprobe
cd linuxprobe
```

![26](Linux_2_pic/26.png)

* 该命令还可以结合 -p 参数来递归创建出具有嵌套叠层关系的文件目录：

```shell
mkdir -p a/b/c/d/e
cd a
cd b
```

![27](Linux_2_pic/27.png)



### cp 命令

* cp 命令用于**复制文件或目录**。

#### 格式

* cp [选项] 源文件 目标文件

#### 三种情况

* 如果目标文件是目录，则会把源文件复制到该目录中；
* 如果目标文件是普通文件，则会询问是否要覆盖它；
* 如果目标文件不存在，则执行正常的复制操作。

#### 参数

* 以下是 cp 命令的参数及作用：

| 参数 |                     作用                     |
| :--: | :------------------------------------------: |
|  -p  |              保留原始文件的属性              |
|  -d  | 若对象为"链接文件"，则保留该"链接文件"的属性 |
|  -r  |           递归持续复制（用于目录）           |
|  -i  |         若目标文件存在则询问是否覆盖         |
|  -a  |      相当于 -pdr（p、d、r 为上述参数）       |

#### 例子

* 使用 touch 创建一个名为 install.log 的普通空白文件，然后将其复制为一份名为 x.log 的备份文件，然后再使用 ls 命令查看：

```shell
touch install.log
cp install.log x.log
ls
```

![28](Linux_2_pic/28.png)



### mv 命令

* mv 命令用于剪切文件或将文件重命名。

#### 格式

* mv [选项] 源文件 [目标路径 | 目标文件名]

#### 用法

* 剪切操作默认会把源文件删除掉，只保留剪切后的文件。
* 如果在同一个目录中对一个文件进行剪切操作，其实就是对它进行重命名：

```shell
mv x.log linux.log
ls
```

![29](Linux_2_pic/29.png)



### rm 命令

* rm 命令用于删除文件或目录。

#### 格式

* rm [选项] 文件

#### 用法

* 在 Linux 系统中删除文件时，系统会默认询问是否要执行删除操作。
* 如果不想总是看到这种**反复的确认信息**，在 rm 命令后加 -f 参数来强制删除。
* 如果想要删除一个目录，需要在 rm 命令后面一个加 -r 参数才可以，否则删除不掉。

#### 例子

* 尝试删除用前面创建的 install.log 和 linux.log 文件：

```shell
rm install.log
rm -f linux.log
ls
```

![30](Linux_2_pic/30.png)



### dd 命令

* dd 命令用于按照指定大小和个数的数据块来复制文件或转换文件。

#### 格式

* dd [参数]

#### 参数

* dd 命令的参数以及作用如下：

| 参数  |          作用          |
| :---: | :--------------------: |
|  if   |     输入的文件名称     |
|  of   |     输出的文件名称     |
|  bs   |   设置每个"块"的大小   |
| count | 设置要复制的"块"的个数 |

#### 数据块复制

* 在按照指定大小和个数的数据块来复制文件的内容，还可以在复制过程中转换其中的数据。
* 这里我们介绍一个设备文件 **/dev/zero**，该文件不会占用系统的存储空间，但却可以提供无穷无尽的数据。
  * 因此可以用它作为 dd 命令的输入文件，来生成一个指定大小的文件。
* 这里我们给出一个例子，用 zero 设备文件生成一个 30M 的文件：

```shell
dd if=/dev/zero of=30_file count=1 bs=30M
```

![31](Linux_2_pic/31.png)



#### 镜像文件

* dd 命令的另一功能是把光盘制作成 iso 格式的镜像文件，在 Windows 系统中需要借助第三方软件才能做到，在 Linux 系统中可以直接用 dd 命令压制光盘镜像文件：

```shell
dd if=/dev/cdrom of=RHEL-server-7.0-x86_64-LinuxProbe.Com.iso
```

* 由于没有 cdrom，该语句暂时不提供执行结果。请参看书籍中的结果。

#### bs 与 count 的关系

* bs 块的大小和 count 个数是相辅相成的。bs 块大小和 count 个数共同决定了复制数据块的大小。只要能满足需求，可随意组合搭配方式。



### file 命令

* file 命令用于查看文件的类型。

#### 格式

* file 文件名

#### 用法

* Linux 系统中，由于文本、目录、设备等所有这些一切都统称为文件，而不能单凭后缀就知道具体的文件类型。
* 借助 file 命令就可以查看文件类型：

```shell
file anaconda-ks.cfg
file /dev/sda
```

![32](Linux_2_pic/32.png)



## 打包压缩与搜索命令

* 在网络上人们倾向于传输压缩格式的文件，由于压缩文件体积小，在网速相同的情况下，传输时间短。本节的指令虽然很少但是参数很复杂，因此放在最后讲解。

### tar 命令

* tar 命令用于对文件进行打包压缩或解压。

#### 格式

* tar [选项] [文件]

#### 注意点

* Linux 系统中，常见的文件格式比较多，其中主要使用的是 .tar 或 .tar.gz 或 .tar.bz2 格式。
  * 不用担心格式太多而记不住，其实这些格式都是由 tar 命令来生成的。

#### 参数

* 下面是该命令的一些常见参数：

| 参数 |          作用          |
| :--: | :--------------------: |
|  -c  |      创建压缩文件      |
|  -x  |      解开压缩文件      |
|  -t  | 查看压缩包内有哪些文件 |
|  -z  |   用 Gzip 压缩或解压   |
|  -j  |  用 bzip2 压缩或解压   |
|  -v  |  显示压缩或解压的过程  |
|  -f  |       目标文件名       |
|  -p  |  保留原始的权限与属性  |
|  -P  |   使用绝对路径来压缩   |
|  -C  |    指定解压到的目录    |

#### 参数的注意点

* **-c** 参数用于创建压缩文件，**-x** 参数用于解压文件，两个参数**不能同时使用**。

* -z 参数指定使用 Gzip 格式来压缩和解压文件，-j 参数指定使用 bzip2 格式来压缩或解压文件。
  * 用户使用时应根据**文件的后缀**来决定应使用何种格式参数进行解压。
* -v 参数可以不断向用户**显示压缩或解压的过程**。**特别推荐使用 **。
  * 因为有时解压操作要耗费数个小时，如果屏幕一直没有输出，不好判断电脑打包的进度情况，也会怀疑电脑死机。
* -C 参数用于指定要解压到哪个指定的目录。
* -f 参数特别重要，且必须放到参数的最后一位，代表要压缩或解压的软件包名称。

#### 常见用法

* tar -czvf 压缩包名称.tar.gz 要打包的目录
  * 该命令可实现把指定的文件进行打包压缩；
* tar -xzvf 压缩包名称.tar.gz 解压到的目录
  * 该命令是响应的解压命令。
* 上述两个命令中的 -czvf 可替换为 czvf，-xzvf 可替换为 xzvf。

#### 例子

* 下面使用 tar 命令把 /etc 目录通过 gzip 格式进行打包压缩，并将文件命名为 etc.tar.gz：

```shell
tar -czvf etc.tar.gz /etc
```

![33](Linux_2_pic/33.png)

（后续输出省略）

* 接下来将打包后的压缩包文件指定解压到 /root/etc 目录中（先使用 mkdir 命令来创建 /root/etc 目录）：

```shell
mkdir /root/etc
tar xzvf etc.tar.gz -C /root/etc
```

![34](Linux_2_pic/34.png)

（后续输出省略）



### grep 命令

* grep 命令用于在文本中执行**关键词搜索**。

#### 格式

* grep [选项] [文件]

#### 参数

* grep 命令的参数以及作用如下：

| 参数 |                       作用                       |
| :--: | :----------------------------------------------: |
|  -b  | 将可执行文件（binary）当做文本文件（text）来搜索 |
|  -c  |                 仅显示找到的行数                 |
|  -i  |                    忽略大小写                    |
|  -n  |                     显示行号                     |
|  -v  |                     反向选择                     |

#### 用法

* grep 命令时使用最广泛的文本搜索匹配工具，虽然有很多参数，但大多数基本上用不到。
* 其中最常用的参数：
  * -n 参数用来显示搜索到信息的行号；
  * -v 参数用于反选信息（即没有包含关键词的所有信息行）。
* 其他参数等到用到时再 man grep 查询也来得及。

#### 例子

* Linux 系统中，/etc/passwd 文件保存着所有的用户信息，而一旦用户的登录终端被设置成 /sbin/nologin，则不再允许登录系统。
  * 使用 grep 命令来查找出当前系统中不允许登录系统的所有用户信息：

```shell
grep /sbin/nologin /etc/passwd
```

![35](Linux_2_pic/35.png)



### find 命令

* find 命令用于按照**指定条件**来**查找**条件。

#### 格式

* find [查找路径] 寻找条件 操作

#### 用法

* Linux 系统中的一切都是文件，搜索文件的工作一般是通过 find 命令来完成的。
  * 它可以使用不同的文件特性作为寻找条件（如文件名、大小、修改时间、权限等信息）。
* 一旦匹配成功则默认将信息显示到屏幕上。

#### 参数

* find 命令的参数及作用：

|        参数        |                             作用                             |
| :----------------: | :----------------------------------------------------------: |
|       -name        |                           匹配名称                           |
|       -perm        |        匹配权限（mode 为完全匹配，-mode 为包含即可）         |
|       -user        |                          匹配所有者                          |
|       -group       |                          匹配所有组                          |
|    -mtime -n +n    |     匹配修改内容的时间（-n 指 n 天以内，+n 指 n 天以前）     |
|    -atime -n +n    |     匹配访问文件的时间（-n 指 n 天以内，+n 指 n 天以前）     |
|    -ctime -n +n    |   匹配修改文件权限的时间（-n 指 n 天以内，+n 指 n 天以前）   |
|      -nouser       |                      匹配无所有者的文件                      |
|      -nogroup      |                      匹配无所有组的文件                      |
|   -newer f1 !f2    |               匹配比文件 f1 新但比 f2 旧的文件               |
| --type b/d/c/p/l/f |           匹配文件类型（后面的字母参数在下面说明）           |
|       -size        | 匹配文件的大小（+50KB 为查找超过 50KB 的文件，而 -50KB 为查找小于 50KB 的文件） |
|       -prune       |                         忽略某个目录                         |
| -exec ...... {} \; |             后面可跟用于进一步处理搜索结果的命令             |

#### 参数说明

* --type b/d/c/p/l/f 后面的字母参数依次表示块设备、目录、字符设备、管道、链接文件、文本文件。
* -exec 参数用于把 find 命令搜索到的结果交由紧随其后的命令作进一步处理，它十分类似于管道符技术（**笔记三**），并且由于 find 命令对参数的特殊要求，因此虽然 exec 是长格式形式，但依然只需要一个减号（-）。

#### 例子

* 根据文件系统层次标准（Filesystem Hierarchy Standard）协议，Linux 系统中的配置文件会保存到 /etc 目录中（**笔记六**）。如果要想获取到该目录中所有以 host 开头的文件列表，可以执行如下命令：

```shell
find /etc -name "host*" -print
```

![36](Linux_2_pic/36.png)

* 如果要在整个系统中搜索权限包括 SUID 权限的所有文件（**笔记五**），只需使用 -4000 即可：

```shell
find / -perm -4000 -print
```

![37](Linux_2_pic/37.png)

* 在整个文件系统中找出所有归属于 linuxprobe 用户的文件并复制到 /root/findresults 目录：

```shell
find / -user linuxprobe -exec cp -a {} /root/findresults/ \;
```

* 上例中使用到了 -exec 参数，其中 {} 表示 find 命令搜索出的每一个文件，而且命令的结尾必须是 "\;"。

![38](Linux_2_pic/38.png)



## 总结与说明

* 本章详细介绍了常用的 Linux 命令，其中的很多命令需要在后面的学习中才能进一步掌握其用途。接下来我们进入管道符、重定向和环境变量的学习。



* Written by：Sirius. Lu
* Reference：刘遄 《Linux 就该这么学》
* 2020.7.19