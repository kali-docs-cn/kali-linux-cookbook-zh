# 第一章 安装和启动Kali

> 作者：Willie L. Pritchett, David De Smet

> 译者：[飞龙](https://github.com/)

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

## 简介

Kali Linux，简称Kali，是用于安全攻击的最新Linux发行版。它是BackTrack Linux的后继者。不像多数Linux发行版那样，Kali Linux用于渗透测试。渗透测试是一种通过模拟攻击评估计算机系统或网络安全性的方法。在整本书中，我们将会探索一些Kali Linux所提供的工具。

这一章涉及到Kali Linux在不同场景下的的安装和启动，从插入Kali Linux DVD到配置网络。

对于本书中所有秘籍，我们都要使用以64位GNOME作为窗口管理器（WM）和架构的Kali Linux（[http://www.Kali.org/downloads/](http://www.Kali.org/downloads/)）。然而，使用KDE作为WM的用法并不在这本书里涉及，你应该能够遵循这些秘籍，并没有多少问题。

## 1.1 安装到硬盘

硬盘的安装是最基本的操作之一。这个任务需要我们不带DVD运行Kali来完成。

> 执行这个秘籍中的步骤会抹掉你的硬盘，并把Kali标记为你电脑上的主操作系统。

### 准备

在解释整个过程之前，需要满足以下要求：

+ 为KaliLinux的安装准备最小8GB的空闲磁盘空间（然而我们推荐至少25GB来存放这本书中额外的程序和生成的词汇表）。
+ 最小512MB的内存。
+ 在[KaliLinux的下载页面](http://www.kali.org/downloads/)下载Kali Linux。

让我们开始安装吧。

### 操作步骤

1.  在光驱中插入Kali Linux Live DVD来开始。你会看到它的启动菜单。选择`Graphical install`（图形化安装）。

    ![](img/1-1-1.jpg)

2.  选择语言。这里我们选择`English`（英语）。

    ![](img/1-1-2.jpg)

3.  选择你的位置。这里我们选择`United States`（美国）。

    ![](img/1-1-3.jpg)

4.  选择你的键盘配置。这里我们选择`American English`（美国英语）。

    ![](img/1-1-4.jpg)

5.  下面要完成网络服务配置。输入主机名称，这里我们输入`Kali`。

    ![](img/1-1-5.jpg)

6.  下面，我们需要输入域名。这里我们输入`kali.secureworks. com`。

    ![](img/1-1-6.jpg)

7.  现在你会看到输入root密码的地方，需要输入两次。

    ![](img/1-1-7.jpg)

8.  选择你的时区，这里我们选择`Eastern`（东方）。

    ![](img/1-1-8.jpg)

9.  我们现在可以选择磁盘分区方式。你会看到四个选项。选择`Guided - use entire disk`，这会便于你分区。

    ![](img/1-1-9.jpg)

0.  在这一步，你需要知道你的磁盘会被抹掉，点击`Continue`（继续）。

    ![](img/1-1-10.jpg)

1.  下面，你有机会选择三个分区方式之一：所有文件放在一个分区、分离`/home`、以及分离`/home/user/var`和`/tmp`。考虑到Kali用于渗透测试，分区不需要也不必要（即使这对于你的桌面主操作系统是个好主意）。这里我们选择` All files in one partition`（所有文件放在一个分区）并点击`Continue`（继续）。

    ![](img/1-1-11.jpg)

2.  一旦你看到了一个界面，让你知道将要对你磁盘执行的改动，选择`Yes`之后点击`Continue`（继续）。要注意这是撤销抹掉你磁盘所有数据的最后机会。

    ![](img/1-1-12.jpg)

3.  下面，你会被询问是否希望链接到网络镜像。网络镜像允许你接收到Kali的更新。这里我们选择`Yes`之后点击`Continue`（继续）。

    ![](img/1-1-13.jpg)

4.  你可以通过点击`Continue`（继续）跳过HTTP代理界面。

    ![](img/1-1-14.jpg)

5.  最后，你会被询问来安装GRUB启动器到主引导记录（MBR）中。选择`Yes`之后点击`Continue`（继续）。

    ![](img/1-1-15.jpg)

6.  祝贺你现在完成了Kali Linux的安装！点击`Continue`，系统会重启并展示登录界面。

    ![](img/1-1-16.jpg)

## 1.2 安装到U盘或持久存储器中

Kali Linux U盘能够持久化储存系统设置，以及在U盘中永久升级和安装新的软件包，并让我们将个人定制的Kali Linux随时带在身上。

多亏了Win32 Disk Imager，我们可以为大多数Linux发行版创建可启动的U盘，包括持久化存储的Kali Linux。

### 准备

需要下列工具和准备工作以继续：

+ FAT32格式的U盘，最小8GB。
+ Kali Linux ISO镜像。
+ [Win32 Disk Imager](http://sourceforge.net/projects/win32diskimager/)。
+ 你可以从[这里](http://www.kali.org/downloads/)下载Kali。

### 操作步骤

让我们开始讲Kali Linux安装到U盘：

1.  插入格式化且可写入的U盘：

    ![](img/1-2-1.jpg)

2.  启动 Win32 Disk Imager。

3.  点击目录图表，选择Kali Linux DVD ISO镜像的位置：

    ![](img/1-2-2.jpg)

4.  确保`Space used to preserve files across reboots`（用于在启动中保存文件的空间）设置为4096。

    ![](img/1-2-3.jpg)

5.  选择我们的U盘，并点击OK按钮来开始创建可启动的U盘：


6.  当它解压并复制DVD的文件到U盘，以及安装bootloader时，这个过程会花一些时间来完成。

7.  安装完成之后，我们就可以重启电脑，从新创建的Kali Linux U盘以持久存储器来启动了。

    ![](img/1-2-4.jpg)

## 1.3 在 VirtualBox 中安装

这个秘籍会引导你使用知名的开源虚拟机软件VirtualBox，将Kali Linux安装在一个完全分离的访客操作系统中，它在你的宿主操作系统中。

### 准备

需要满足下列要求：

+ [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 的最新版本（本书编写时为4.2.16）。
+ Kali Linux ISO 镜像的副本。你可以在[这里](http://www. Kali.org/downloads/)下载。

### 操作步骤

让我们在VirtualBox中安装Kali Linux：

1.  运行VirtualBox，点击`New`（新建）来启动虚拟机向导：

    ![](img/1-3-1.jpg)

2.  点击`Next`（下一步）按钮，键入虚拟机的名称，并选择OS类型和版本。这里我们选择Linux类型和Ubuntu（64位）作为版本。点击`Next`按钮来继续：

    ![](img/1-3-2.jpg)

3.  选择分配给虚拟机的基本内存（RAM）的总数。我们打算使用默认值，点击`Next`。

4.  为新的虚拟机创建新的虚拟硬盘，点击`Next`按钮。

    ![](img/1-3-3.jpg)

5.  一个新的向导窗口将会打开，保留默认的VDI文件类型，因为我们并不需要使用其它的虚拟机软件。

6.  我们会保留默认选项作为虚拟机磁盘存储的详情。点击`Next`来继续：

7.  设置虚拟机磁盘文件类型和大小：

    ![](img/1-3-4.jpg)

8.  检查设置是否正确，之后点击`Create`（创建）按钮来开始虚拟磁盘文件的创建。

9.  我们将会返回前面的向导，带有虚拟机参数的概览。点击`Create`以结束：

    ![](img/1-3-5.jpg)

0.  新的虚拟机创建之后，我们将要安装Kali Linux。

1.  在VirtualBox的主窗口，高亮Kali Linux，之后点击`Settings`（设置）按钮：

    ![](img/1-3-6.jpg)

2.  现在基本的安装步骤就完成了，我们需要让你将下载的ISO文件用于虚拟光盘。这会为你节省烧录物理DVD的时间来完成这个安装。在`Settings`界面中，点击`Storage`（存储器）菜单选项：

    ![](img/1-3-7.jpg)

3.  下一步，在`Storage Tree`（存储器树形图）下面，高亮`Empty`（空）磁盘图标，它在`IDE Controller`（IDE控制器）的下面。这户选择我们的虚拟CD/DVD ROM驱动器。在屏幕的最右边，在
`Attributes`底下，点击光盘图表。在上面弹出的菜单上选择你的`Choose a virtual CD/DVD disc file...`（Kali Linux ISO CD/DVD光盘文件）选项，并找到你的ISO。一旦你完成了这些步骤，点击OK按钮。

    ![](img/1-3-8.jpg)

4.  点击Start（开始）按钮，之后点击里面的新窗口来进行安装。安装步骤在1.1节中已经包括了。

    > 安装VirtualBox 扩展包也允许我们通过添加USB2.0（EHCI）、VirtualBox RDP和 Intel PXE boot ROM的支持，来扩展虚拟机的功能。

## 1.4 安装  VMware Tools

这个秘籍中，我们会展示如何使用 VMware Tools将Kali Linux安装在虚拟机中。

### 准备

需要满足下列要求：

+ 已经安装好的Kali Linux VMware 虚拟机。
+ 网络连接。

### 操作步骤

让我们开始将Kali Linux 安装到 VMware上：

1.  打开你的虚拟机的访客操作系统并连接到互联网，之后打开`Terminal`（终端）窗口，并键入下列命令来准备核心资源：

    ```
    prepare-kernel-sources
    ```

    > 这些命令假设你使用Linux或者Mac OS。你不需要在Windows下执行它们。

2.  在VMware Workstaion的菜单栏上，访问`VM | Install VMware Tools…`：

    ![](img/1-4-1.jpg)

3.  将VMware Tools安装工具复制到临时目录下，之后将当前位置改为目标目录：

    ```
    cp /media/VMware\ Tools/VMwareTools-8.8.2-590212.tar.gz /tmp/; cd /tmp
    ```

    > 根据你的VMware Tools来替换文件名：`VMwareTools-<version>-<build>.tar.gz`。

4.  使用以下命令解压并安装：

    ```
    tar zxpf VMwareTools-8.8.2-590212.tar.gz
    ```

5.  进入VMware Tools的目录中，之后运行安装工具：

    ```
    cd vmware-tools-distrib/
    ./vmware-install.pl
    ```

6.  按下回车键来接受每个配置询问的默认值；`vmware-config-tools.pl`脚本同上。

7.  最后重启系统，工作就完成了。

### 工作原理

在第一步中，我们准备好了核心资源。之后，我们向访客操作系统插入了虚拟的 VMware Tools CD 。接着，我们创建了挂载点，并挂载虚拟CD。我们在临时目录中复制并解压了安装工具。最后我们保留默认配置来运行安装工具。

## 1.5 修复启动画面

我们首次启动新安装的Kali Linux系统时，会注意到启动画面消失了。为了手动修复它，我们需要解压`Initrd`，修改它，之后将它再次压缩。幸运的是，有一个由 Mati Aharoni（也称为“muts”，Kali Linux的创造者）编写的自动化bash脚本使这件事变得容易。

### 操作步骤

键入下列命令并且按下回车键来修复消失的启动画面：

```
fix-splash
```

## 1.6 启动网络服务

Kali Linux 自带了多种网络服务，它们在多种情况下可能很实用，并且默认是禁用的。这个秘籍中，我们会涉及到通过多种方法设置和启动每个服务的步骤。

### 准备

需要满足下列要求以继续：

+ 带有有效IP地址的网络连接。

### 操作步骤

让我们开始启动默认服务：

1.  启动Apache服务器：

    ```
    service apache2 start
    ```

    我们可以通过浏览本地地址来验证服务器是否打开。

2.  为了启动SSH服务，首次需要生成SSH密钥：

    ```
    sshd-generate
    ```

3.  启动SSH服务器：

    ```
    service ssh start
    ```

4.  使用`netstat`命令来验证服务器是否开启并正在监听：

    ```
    netstat -tpan | grep 22
    ```

5.  启动FTP服务器：

    ```
    service pure-ftpd start
    ```

6.  使用下列命令来验证FTP服务器：

    ```
    netstat -ant | grep 21
    ```

    > 你也可以使用` ps-ef | grep 21 `命令。

7.  使用下列命令来停止服务：

    ```
    service <servicename> stop
    ```

    其中`<servicename>`代表我们希望停止的网络服务，例如：

    ```
    service apache2 stop
    ```

8.  使用下列命令来在开机时启用服务：

    ```
    update-rc.d –f <servicename> defaults
    ```

    其中`<servicename>`代表打算启动的网络服务，例如：

    ```
    update-rc.d –f ssh defaults
    ```

    > 你也可以在Kali Linux中通过`Services`（服务）菜单来完成它。从`Start`（开始）菜单开始，访问`Kali Linux | Services`。

## 1.7 设置无线网络

最后，我们来到了这一章的最后一个秘籍。这个秘籍中，我们会了解在安全状态下的无线网络连接步骤，通过Wicd Network Manager和提供加密的细节。无线网络的设置允许我们以无线方式使用Kali Linux。在真实的、合乎道德的渗透测试中，我们可以不依赖于网线而自由地使用所有常规桌面。

### 操作步骤

让我们开始设置无线网络：

1.  从桌面启动网络管理器，通过点击`Applications`（应用）菜单并且访问`Internet | Wicd Network Manager`，或者在终端窗口中键入下列命令：

    ```
    wicd-gtk --no-tray
    ```

2.  Wicd Network Manager会打开，并带有可用网络的列表：

    ![](img/1-7-1.jpg)

3.  点击`Properties`（属性）按钮来设定网络细节。完成之后点击OK。

    ![](img/1-7-2.jpg)

4.  最后，点击`Connect`（连接）按钮，就完成了。

### 工作原理

这个秘籍中，我们总结了无线网络的设置方式。这个秘籍以启动网络管理器，和连接到我们的路由器作为开始。
