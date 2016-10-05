# 第八章 密码攻击

> 作者：Willie L. Pritchett, David De Smet

> 译者：[飞龙](https://github.com/)

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

这一章中，我们要探索一些攻击密码来获得用户账户的方式。密码破解是所有渗透测试者都需要执行的任务。本质上，任何系统的最不安全的部分就是由用户提交的密码。无论密码策略如何，人们必然讨厌输入强密码，或者时常更新它们。这会使它们易于成为黑客的目标。

## 8.1 在线密码攻击

这个秘籍中我们会使用 Hydra 密码破解器。有时候我们有机会来物理攻击基于 Windows 的计算机，直接获取安全账户管理器（SAM）。但是，我们也有时不能这样做，所以这是在线密码攻击具有优势的情况。

Hydra 支持许多协议，包括（但不仅限于）FTP、HTTP、HTTPS、MySQL、MSSQL、Oracle、Cisco、IMAP、VNC 和更多的协议。需要注意的是，由于这种攻击可能会产生噪声，这会增加你被侦测到的可能。

### 准备

需要内部网络或互联网的链接，也需要一台用作受害者的计算机。

### 操作步骤

让我们开始破解在线密码。

1.  在开始菜单中，选择` Applications | Kali Linux | Password Attacks | Online Attacks | hydra-gtk`。

    ![](img/8-1-1.jpg)
    
2.  既然我们已经把 Hydra 打开了，我们需要设置我们的单词列表。点击`Passwords`（密码）标签页。我们需要使用用户名列表和密码列表。输入你的用户名和密码列表的位置。同时选择` Loop around users `（循环使用用户名）和` Try  empty password`（尝试空密码）。

    +   用户名列表：`/usr/share/wfuzz/wordlist/fuzzdb/wordlistsuser-passwd/names/nameslist.txt`
    +   密码列表：`/usr/share/wfuzz/wordlist/fuzzdb/wordlistsuser-passwd/passwds/john.txt`
    
    > 你可以使用的快捷方式是，点击单词列表框来打开文件系统窗口。
    
    ![](img/8-1-2.jpg)
    
3.  下面，我们要做一些调整。在`Performance Options`（执行选项）下面，我们将任务数量从 16 设置为 2。原因是我们不打算让这么多进程运行，这样会使服务器崩溃。虽然它是可选的，我们也希望选择`Exit after first found pair `（在首次发现匹配之后退出）选项。

    ![](img/8-1-3.jpg)
    
4.  最后，我们要设置我们的目标。点击`Target`（目标）标签页并设置我们的目标和协议。这里，我们使用 Metasploitable 主机（`192.168.10.111`）的 MySQL 端口。

    ![](img/8-1-4.jpg)

5.  最后我们点击`Start`（开始）标签页的`Start`按钮来启动攻击。

    ![](img/8-1-5.jpg)
    
### 工作原理

这个秘籍中，我们使用 Hydra 来对目标执行字典攻击。Hydra 允许我们指定目标，并且使用用户名和密码列表。它会通过使用来自两个列表的不同用户名和密码组合来爆破密码。

## 8.2 破解 HTTP 密码

这个秘籍中，我们将要使用 Hydra 密码破解器来破解 HTTP 密码。网站和 Web 应用的访问通常由用户名和密码组合来控制。就像任何密码类型那样，用户通常会输入弱密码。

### 准备

需要内部网络或互联网的链接，也需要一台用作受害者的计算机。

### 操作步骤

让我们开始破解 HTTP 密码。

1.  在开始菜单中，选择` Applications | Kali Linux | Password Attacks | Online Attacks | hydra-gtk`。

    ![](img/8-2-1.jpg)
    
2.  既然我们已经把 Hydra 打开了，我们需要设置我们的单词列表。点击`Passwords`（密码）标签页。我们需要使用用户名列表和密码列表。输入你的用户名和密码列表的位置。同时选择` Loop around users `（循环使用用户名）和` Try  empty password`（尝试空密码）。

    +   用户名列表：`/usr/share/wfuzz/wordlist/fuzzdb/wordlistsuser-passwd/names/nameslist.txt`
    +   密码列表：`/usr/share/wfuzz/wordlist/fuzzdb/wordlistsuser-passwd/passwds/john.txt`
    
    > 你可以使用的快捷方式是，点击单词列表框来打开文件系统窗口。
    
    ![](img/8-2-2.jpg)
    
3.  下面，我们要做一些调整。在`Performance Options`（执行选项）下面，我们将任务数量从 16 设置为 2。原因是我们不打算让这么多进程运行，这样会使服务器崩溃。虽然它是可选的，我们也希望选择`Exit after first found pair `（在首次发现匹配之后退出）选项。

    ![](img/8-2-3.jpg)
    
4.  最后，我们要设置我们的目标。点击`Target`（目标）标签页并设置我们的目标和协议。这里，我们使用 Metasploitable 主机（`192.168.10.111`）的 HTTP 端口。

    ![](img/8-2-4.jpg)

5.  最后我们点击`Start`（开始）标签页的`Start`按钮来启动攻击。

    ![](img/8-2-5.jpg)

## 8.3 获得路由访问

这个秘籍中，我们会使用 Medusa 来进行爆破攻击。

当今，我们处于网络社会之中。随着联网视频游戏系统的诞生，多数家庭拥有数台计算机，并且小型业务以创纪录的趋势增长。路由器也成为了网络连接的基石。然而，富有经验的网络管理员的数量并没有增长，以保护这些路由器，使得许多这种路由器易于被攻击。

### 准备

需要连接到互联网或内部网络的计算机。也需要可用的路由器。

### 操作步骤

1.  在开始菜单中，访问` Applications | Kali Linux | Password Attacks | Online Attacks | medusa`。当 Medusa 启动后，它会加载`help`（帮助）文件。

    ![](img/8-3-1.jpg)

2.  我们现在已选定的选项来云顶 Medusa。

    ```
    medusa –M http -h 192.168.10.1 -u admin -P /usr/share/wfuzz/ wordlist/fuzzdb/wordlists-user-passwd/passwds/john.txt -e ns -n 80 -F
    ```
    
    +   `-M http`允许我们指定模块。这里，我们选择了 HTTP 模块。
    
    +   `-h 192.168.10.1`允许我们指定主机。这里，我们选择了`192.168.10.1`（路由的 IP 地址）。
    
    +   `-u admin`允许我们指定用户。这里我们选择了`admin`。
    
    +   `-P [location of password list]`允许我们指定密码列表的位置。
    
    +   `-e ns`允许我们指定额外的密码检查。`ns`变量允许我们使用用户名作为密码，并且使用空密码。
    
    +   `-n 80`允许我们指定端口号码。这里我们选择了`80`。
    
    +   `-F`允许我们在成功找到用户名密码组合之后停止爆破。
    
    ![](img/8-3-2.jpg)
    
3.  Medusa 会运行，并尝试所有用户名和密码组合，直到某次成功。

### 工作原理

这个秘籍中，我们使用 Medusa 来爆破目标路由器的密码。能够这样做的好处就是，一旦你能够访问路由器，你就可以更新它的设置，便于你以后再访问它，或者甚至是重定向发送给它的流量来改变你选择的位置。

### 更多

你也可以直接从命令行运行 Medusa，通过键入`medusa`命令。

你也可以传入其它选项给 Medusa，取决于你的情况。细节请参见帮助文档，通过在终端窗口仅仅键入`medusa`来显示。

**模块类型**

下面是我们可以用于 Medusa 的模块列表：

+ AFP
+ CVS
+ FTP
+ HTTP
+ IMAP
+ MS-SQL
+ MySQL
+ NetWare
+ NNTP
+ PCAnywhere
+ Pop3
+ PostgreSQL
+ REXEC
+ RLOGIN
+ RSH
+ SMBNT
+ SMTP-AUTH
+ SMTp-VRFY
+ SNMP
+ SSHv2
+ Subversion
+ Telnet
+ VMware Authentication
+ VNC
+ Generic Wrapper
+ Web form

## 8.5 使用 John the Ripper 破解 Windows 密码

这个密集中，我们会使用 John the Ripper 来破解 Windows 安全访问管理器（SAM）文件。SAM文件储存了目标系统用户的用户名和密码的哈希。出于安全因素，SAM文件使用授权来保护，并且不能在 Windows 系统运行中直接手动打开或复制。

### 准备

你将会需要访问 SAM 文件。

这个秘籍中，我们假设你能够访问某台 Windows 主机。

### 操作步骤

让我们开始使用 John the Ripper 破解 Windows SAM 文件。我们假设你能够访问某台 Windows 主机，通过远程入侵，或者物理接触，并且能够通过 USB 或 DVD 驱动器启动 Kali Linux。

1.  看看你想挂载哪个硬盘：

    ```
    Fdisk -l
    ```
    
2.  挂载该硬盘，并将`target`设为它的挂载点。

    ```
    mount /dev/sda1 /target/ 
    ```
    
3.  将目录改为 Windows SAM 文件的位置：

    ```
    cd /target/windows/system32/config 
    ```
    
4.  列出目录中所有内容。

    ```
    ls –al
    ```
    
5.  使用 SamDump2 来提取哈希，并将文件放到你的 root 用户目录中的一个叫做`hashes`的文件夹中。

    ```
    samdump2 system SAM > /root/hashes/hash.txt
    ```
    
6.  将目录改为 John the Ripper 所在目录。

7.  运行 John the Ripper：

    ```
    ./john /root/hashes/hash.txt 
    ./john /root/hashes/hash.txt–f:nt  (If attacking a file on a NTFS System) 
    ```
    
## 8.6 字典攻击

这个秘籍中，我们会进行字典或单词列表的攻击。字典攻击使用事先准备的密码集合，并尝试使用单词列表爆破与指定用户匹配的密码。所生成的字典通常由三种类型：

    +   只有用户名：列表只含有用户名。
    +   只有密码：列表只含有密码。
    +   用户名和密码：列表含有生成的用户名和密码。
    
出于演示目的，我们使用 Crucnch 来生成我们自己的密码字典。

### 准备

需要在 Kali 上安装 Crunch。

### 操作步骤

Kali 的好处是已经安装了 Crunch，不像 BackTrack。

1.  打开终端窗口，并输入`crunch`命令来查看 Crunch 的帮助文件。

    ```
    crunch
    ```
    
    ![](img/8-6-1.jpg)
    
2.  使用 Crunch 生成密码的基本语法是，`[minimum length] [maximum length] [character set] [options] `。

3.  Crunch 拥有几种备选选项。一些常用的如下：

    +   `-o`：这个选项允许你指定输出列表的文件名称和位置、
    
    +   `-b`：这个选项允许你指定每个文件的最大字节数。大小可以以 KB/MB/GB 来指定，并且必须和`-o START`触发器一起使用。
    
    +   `-t`：这个选项允许你指定所使用的模式。
    
    +   `-l`：在使用`-t`选项时，这个选项允许你将一些字符标识为占位符（`@`，`%`，`^`）。
    
4.  下面我们执行命令来在桌面上创建密码列表，它最少 8 个字母，最大 10 个字符，并且使用字符集`ABCDEFGabcdefg0123456789`。

    ```
    crunch 8 10 ABCDEFGabcdefg0123456789 –o /root/Desktop/ generatedCrunch.txt
    ```
    
    ![](img/8-6-2.jpg)
    
5.  一旦生成了文件，我们使用 Nano 来打开文件：

    ```
    nano /root/Desktop/generatedCrunch.txt
    ```
    
### 工作原理

这个秘籍中我们使用了 Crunch 来生成密码字典列表。

## 8.7 使用彩虹表

这个秘籍中我们会学到如何在 Kali 中使用彩虹表。彩虹表是特殊字典表，它使用哈希值代替了标准的字典密码来完成攻击。出于演示目的，我们使用 RainbowCrack 来生成彩虹表。

### 操作步骤

1.  打开终端窗口并将目录改为`rtgen`的目录：

    ```
    cd /usr/share/rainbowcrack/
    ```
    
    ![](img/8-7-1.jpg)
    
2.  下面我们要启动`rtgen`来生成基于 MD5 的彩虹表。

    ```
    ./rtgen md5 loweralpha-numeric 1 5 0 3800 33554432 0
    ```
    
    ![](img/8-7-2.jpg)
    
3.  一旦彩虹表生成完毕，你的目录会包含`.rt`文件。这取决于用于生成哈希的处理器数量，大约需要 2~7 个小时。

4.  为了开始破解密码，我们使用`rtsort`程序对彩虹表排序，使其更加易于使用。

### 工作原理

这个秘籍中，我们使用了 RainbowCrack  攻击来生成、排序和破解 MD5 密码。RainbowCrack 能够使用彩虹表破解哈希，基于一些预先准备的哈希值。我们以使用小写字母值生成 MD5 彩虹表来开始。在秘籍的末尾，我们成功创建了彩虹表，并使用它来破解哈希文件。


