## 命令行

> 参考：[Linux命令大全](https://man.linuxde.net/)

> 推荐阅读《命令行艺术》[jlevy/the-art-of-command-line](https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md)

### 命令行使用

#### 快捷键

- ctrl-u 删除光标前所有内容
- ctrl-k 删除光标后所有内容
- ctrl-w 删除你键入的最后一个单词
- alt-b , alt-f 可以以单词为单位移动光标（mac 不适用）
- ctrl-a 将光标移至行首
- ctrl-e 可以将光标移至行尾
- ctrl-l 可以清屏
- ctrl-r 搜索命令行历史记录，重复按查找下一个
- ctrl-x ctrl-e 打开一个编辑器来编辑当前输入的命令（按顺序按两快捷键）

#### 参数格式

```bash
命令 <必选参数1|必选参数2> [--git option {必选参数1|必选参数2|必选参数3}] [可选参数...] {(默认参数)|参数|参数}

尖括号< >：必选参数，实际使用时应将其替换为所需要的参数
大括号{ }：必选参数，内部使用，包含此处允许使用的参数
方括号[ ]：可选参数，在命令中根据需要加以取舍
小括号( )：指明参数的默认值，只用于{ }中
竖线|：用于分隔多个互斥参数，含义为“或”，使用时只能选择一个。
省略号...：任意多个参数。
```

### 基本使用

```bash
ls -al > myfile     # 默认输出内容到屏幕，通过 > 符号可以输出到文件中

ls -al; pwd;        # 执行多条命令（互相不依赖执行结果）
mkdir images && cd images # 执行多条命令（后面命令依赖前面命令到成功）,也可以使用 || 组合

echo 'some' | tail # 管道：命令之间用竖线分割，上一个命令的结果会作为下一个命令的输入
cd -               # 回到之前的路径
alias ll='ls -latr'# 创建了一个新的命令别名 ll
```

### cp

文件操作

```bash
cp file newfile     # 复制文件
cp –r test/ newtest # 复制目录
```

### 进程相关

[更多参考](https://www.runoob.com/w3cnote/linux-check-port-usage.html)

```bash
lsof -i          # 查看所有网络连接信息
lsof -i 8080     # 查看占用 8080 端口进程
kill {pid}       # 杀死进程 
netstat -ntlp    # 查看所有tcp端口占用
lsof -i tcp:8080 # mac 查看端口占用
netstat -tunlp | grep [端口号]
```

### grep

[文本搜索工具](https://www.runoob.com/linux/linux-comm-grep.html)

```bash
grep text access.log | jsonlog # 以json的格式输出匹配的文本，需要装json工具

# 从根目录开始查找所有扩展名为 .log 的文本文件，并找出包含 "ERROR" 的行：
find / -type f -name "*.log" | xargs grep "ERROR"

grep –e "正则表达式" 文件名 # 从文件内容查找与正则表达式匹配的行：
grep -E '123|abc' filename # 多个关键字-或
grep pattern1 files | grep pattern2 # 多个关键字-与
grep –i "被查找的字符串" 文件名  # 查找时不区分大小写：
grep -w pattern files # 单词匹配
grep -C number pattern files # 匹配的上下文分别显示[number]行，
grep -rn --exclude-dir="node_modules"  "xxx"  ./ # 在指定目录搜索并排除目录
```

### scp

服务器间传输文件

```bash
# 从服务器下载文件
scp username@remotehost.com:/path/to/foobar.txt /some/local/directory
# 本地文件上传到服务器
scp /some/local/directory/foobar.txt username@remotehost.com:/destination/path/
```

### curl

发送 http 请求 [更多参考](https://www.ruanyifeng.com/blog/2019/09/curl-reference.html)

```bash
# post 请求 (需要设置 header)
curl -H 'Content-Type: application/json' -d '{"type": "BUSINESS"}' -X POST http://localhost:8000/config/configs

# 下载文件到指定位置并显示进度
curl http://man.linuxde.net/test.iso -o filename.iso --progress

# 设置 cookie
curl http://localhost:8000 --cookie "user=root;pass=123456"

# 只打印响应到头部信息
curl -I http://localhost:8000
```

### less

分页查看文本，适合查看大文件或内容

```bash
less access.log  # 分页查看文件
ps -ef | less    # 分页查看进程

# 指令：
# /字符串：向下搜索“字符串”的功能
# ?字符串：向上搜索“字符串”的功能
# n：重复前一个搜索（与 / 或 ? 有关）
# N：反向重复前一个搜索（与 / 或 ? 有关）
# b  向后翻一页
# d  向后翻半页
# h  显示帮助界面
# Q  退出less 命令
# u  向前滚动半页
# y  向前滚动一行
# 空格键 滚动一页
# 回车键 滚动一行
```

### find

在指定目录下根据条件查找文件

```bash
find . -name test.txt 
find . -name *.log
find / -size +500M      # 查找大于 500M 的文件
```

### df

查看磁盘占用情况

```bash
df [-ahikHTm] [目录或文件名]
df -h # 以易读的方式展示磁盘情况
```

### du

查看文件和目录的使用的磁盘空间

```bash
du [-abcDhHklmsSx][-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>]
[--max-depth=<目录层数>][--help][--version][目录或文件]

du         # 列出当前目录下所有目录的大小
du -a      # 文件的大小也列出来
du -sh ./* # 列出当前目录下一级子目录的大小
du -lh --max-depth=1 # 查看当前目录下一级子文件和子目录占用的磁盘容量
```

### tar

打包压缩工具

```bash
tar -czvf demo.tar.gz demo # 打包并压缩 demo 目录或者 demo 文件为 demo.tar.gz 文件
tar -czvf --exclude '.DS_Store' demo.tar.gz  demo # 排除 .DS_Store 文件
tar -tzvf demo.tar.gz      # 列出压缩文件内容
tar -xzvf demo.tar.gz      # 解压 demo.tar.gz 文件
tar -xzvf demo.tar.gz -C /home  # 解压 demo.tar.gz 文件到 /home 目录下
```

### chmod

文件权限

```bash
# 8 进制模式，依次代表：属主、组、其他用户
chmod 666 index.js

# 符号模式
# u:代表用户 g:代表组 o:代表其他 a:代表上述所有
# + 增加，- 移除，= 设置为
[ugoa…][[+-=][rwxXstugo…]
chmod g+r index.js        # 给文件所属属组用户赋予读取权限

# 改变属主
chown guest index.js      # 属主变成guest
```

### scp

（secure copy）linux 之间复制文件

```bash
# 本地复制到远程
scp local_file remote_username@remote_ip:remote_folder # 复制文件到指定目录
scp local_file remote_username@remote_ip:remote_file   # 复制文件为指定文件
scp -r local_folder remote_username@remote_ip:remote_folder # 复制目录到指定目录

# 远程复制到本地（更换参数位置即可）
scp remote_username@remote_ip:remote_file local_folder
scp remote_username@remote_ip:remote_folder local_folder
```

### which

常用于查找可直接执行的命令，只在$PATH路径中搜索，查找范围最小。

```bash
which nginx    # 查找第一个 nginx 命令的文件位置
which -a nginx # -a 查找所有的
```

### wc

统计文件的字节数、字数、行数

```bash
 find src | xargs wc -l       # 统计 src 目录下所有文件行数
 git ls-files | xargs wc -l   # 统计 git 仓库中所有文件行数
```

## 基本概念

> [https://www.w3cschool.cn/linux/linux-tutorial.html](https://www.w3cschool.cn/linux/linux-tutorial.html)

### 版本

Linux 是类 Unix 的操作系统内核，在 Linux 内核的基础上二次开发了多种**发行版本**，例如较流行的 Ubuntu 和 CentOS。

### 文件系统

#### 文件

在 Linux 中，一切皆文件，包括硬件设备，系统以读写文件的方式对文件进行访问。

伪文件不占用磁盘空间

Linux 中的文件拓展名跟文件类型没有关系，只有命名上的作用，习惯上用来区分文件类型。

![picture 9](http://qiniu.houserqu.com/80c17be9f105a7bf2a9b25dd58c406ae1e8da5ce662e0946c9047584554da77c.png)  

#### 目录结构

![picture 4](http://qiniu.houserqu.com/00a4f81902797aa2a6eef345353d7d449c205ae261ca9b36e1a336aaace22ee0.png)  


- **/bin**：bin是Binary的缩写, 这个目录存放着最经常使用的命令。

- **/boot：**这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。

- **/dev ：**dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。

- **/etc：**这个目录用来存放所有的系统管理所需要的配置文件和子目录。

- **/home**：用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

- **/lib**：这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。

- **/lost+found**：这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

- **/media** linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。

- **/mnt**：系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

- **/opt**： 这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

- **/proc**：这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

- **/root**：该目录为系统管理员，也称作超级权限者的用户主目录。

- **/sbin**：s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。

- **/selinux**： 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

- **/srv**： 该目录存放一些服务启动之后需要提取的数据。

- **/sys**： 这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统。

  该文件系统是内核设备树的一个直观反映。

  当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

- **/tmp**：这个目录是用来存放一些临时文件的。

- **/usr**： 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似与windows下的program files目录。

- **/usr/bin：**系统用户使用的应用程序。

- **/usr/sbin：**超级用户使用的比较高级的管理程序和系统守护程序。

- **/usr/src：**内核源代码默认的放置目录。

- **/var**：这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

#### 文件权限

`ls -l` 命令可以查看目录下文件和子目录的权限。

![picture 5](http://qiniu.houserqu.com/b5233d6249e5cc905779fe3c09daad977811e48621bd084f4af0ce60941cb243.png)  

![picture 6](http://qiniu.houserqu.com/4f70331bdc109cfc6221ffef263a7acf4cd38a4741a181cd536b8659bcf34410.png)  

第一个字符代表文件类型（见上文）

- `r`代表对象是可读的
- `w` 代表对象是可写的
- `x` 代表对象是可执行的

权限进制对照表

![picture 8](http://qiniu.houserqu.com/800de84ab5bdb12209b4efc1e1c205df6c22b2de22947ffde02de4e6ec7815db.png)  


使用 [chmod](https://www.notion.so/houserqu/b8cca8084d2b4c67a6ca81191dc00bf1) 进行文件权限的管理

## 常见问题

### 命令行乱码

跟系统使用的字符集有关，可以通过 `echo $LANG` 查看当前的字符集，如果输出的是 LANG=C 说明使用的默认字符集，显示中文会乱码，可以通过 `export LANG="zh_CN.UTF-8"` 来临时设置中文字符集，如果需要永久生效，可以写到 /etc/profile 文件。

### 内存释放

- `free -h` 查看内存占用率
- `top` 动态查看进程 cpu、内存使用情况
- 释放缓存：`sync && echo 3 > /proc/sys/vm/drop_caches`