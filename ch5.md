# 第五章 漏洞评估

> 作者：Willie L. Pritchett, David De Smet

> 译者：[飞龙](https://github.com/)

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

## 简介

扫描和识别靶机的漏洞通常被渗透测试者看做无聊的任务之一。但是，它也是最重要的任务之一。这也应该被当做为你的家庭作业。就像在学校那样，家庭作业和小测验的设计目的是让你熟练通过考试。

漏洞识别需要你做一些作业。你会了解到靶机上什么漏洞更易于利用，便于你发送威力更大的攻击。本质上，如果攻击者本身就是考试，那么漏洞识别就是你准备的机会。

Nessus 和 OpenVAS 都可以扫描出靶机上相似的漏洞。这些漏洞包括：

+ Linux 漏洞
+ Windows 漏洞
+ 本地安全检查
+ 网络服务漏洞

## 5.1 安装、配置和启动 Nessus

在这个秘籍中，我们会安装、配置和启动 Nessus。为了在我们所选的靶机上定位漏洞，Nessus 的漏洞检测有两种版本：家庭版和专业版。

+ 家庭版：家庭版用于非商业/个人用途。以任何原因在专业环境下适用 Nessus 都需要使用专业版。
+ 上夜班：专业版用于商业用途。它包括支持和额外特性，例如无线的并发连接数，以及其它。如果你是一个顾问，需要对某个客户执行测试，专业版就是为你准备的。

对于我们的秘籍，我们假定你使用家庭版。

### 准备

需要满足下列需求：

+ 需要网络连接来完成这个秘籍。
+ Nessus 家庭版的有效许可证。

### 操作步骤

让我们开始安装、配置和启动 Nessus， 首先打开终端窗口：

1.  打开 Web 浏览器，访问这个网址：<http://www. tenable.com/products/nessus/select-your-operating-system>。

2.  在屏幕的左侧，`Download Nessus`的下面，选择`Linux`并且选择`Nessus-5.2.1-debian6_amd64.deb`（或新版本）。

    ![](img/5-1-1.jpg)

3.  将文件下载到本地根目录下。

    ![](img/5-1-2.jpg)
    
4.  打开终端窗口

5.  执行下列命令来安装 Nessus：

    ```
    dpkg -i "Nessus-5.2.1-debian6_i386.deb" 
    ```
    
    这个命令的输出展示在下面：
    
    ![](img/5-1-3.jpg)
    
6.  Nessus 会安装到`/opt/nessus`目录下。

7.  一旦安装好了，你就能通过键入下列命令启动 Nessus：

    ```
    /etc/init.d/nessusd start
    ```
    
    > 在你启动 Nessus 之前，你需要先拥有注册码。你可以从“更多”一节中得到更多信息。
    
8.  通过执行下列命令，激活你的 Nessus：

    ```
    /opt/nessus/bin/nessus-fetch --register XXXX-XXXX-XXXX-XXXX- XXXX
    ```
    
    这一步中，我们会从<http://plugins.nessus.org>获取新的插件。
    
    > 取决于你的网络连接，这可能需要一到两分钟。
    
9.  现在在终端中键入下列命令：

    ```
    /opt/nessus/sbin/nessus-adduser
    ```
    
0.  在登录提示框中，输入用户的登录名称。

1.  输入两次密码。

2.  回答 Y（Yes），将用户设置为管理员。

    > 这一步只需要在第一次使用时操作。
    
3.  完成后，你可以通过键入以下命令来启动 Nessus（没有用户账户则不能工作）。

4.  在<https://127.0.0.1:8834>上登录 Nessus。

    > 如果你打算使用 Nessus，要记得从安装在你的主机上 ，或者虚拟机上的kali Linux 版本中访问。原因是，Nessus会基于所使用的机器来激活自己。如果你安装到优盘上了，在每次重启后你都需要重新激活你的版本。
    
### 工作原理

在这个秘籍中，我们以打开终端窗口，并通过仓库来安装 Nessus 开始。之后我们启动了 Nessus，并为了使用它安装了我们的证书。

### 更多

为了注册我们的 Nessus 副本，你必须拥有有效的许可证，它可以从<http://www.tenable.com/products/nessus/nessus-homefeed>获取。而且，Nessus 运行为浏览器中的 Flash，所以首次启动程序时，你必须为 Firefox 安装 Flash 插件。如果你在使用 Flash 时遇到了问题，访问<www.get.adobe.com/flashplayer>来获得信息。
