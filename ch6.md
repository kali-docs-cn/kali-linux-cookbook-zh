# 第六章 漏洞利用

> 作者：Willie L. Pritchett, David De Smet

> 译者：[飞龙](https://github.com/)

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

## 简介

一旦我们完成了漏洞扫描步骤，我们就了解了必要的知识来尝试利用目标系统上的漏洞。这一章中，我们会使用不同的工具来操作，包括系统测试的瑞士军刀 Metasploit。

## 6.1 安装和配置 Metasploitable

这个秘籍中，我们会安装、配置和启动 Metasploitable 2。 Metasploitable 是基于 Linux 的操作系统，拥有多种可被 Metasploit 攻击的漏洞。它由  Rapid7 （Metasploit 框架的所有者）设计。Metasploitable 是个熟悉 Meterpreter 用法的极好方式。

### 准备

为了执行这个秘籍，我们需要下列东西：

+   互联网连接

+   VirtualBox PC 上的可用空间

+   解压缩工具（这里我们使用 Windows 上的 7-Zip）

### 操作步骤

让我们开始下载 Metasploitable 2。最安全的选择是从 SourceForge 获取下载包：

1.  从这个链接下载 Metasploitable 2：<http://sourceforge.net/ projects/metasploitable/files/Metasploitable2/>。

2.  将文件包括到硬盘的某个位置。

3.  解压文件。

4.  将文件夹内容放到你储存虚拟磁盘文件的位置。

5.  打开 VirtualBox 并点击`New`按钮：

    ![](img/6-1-1.jpg)
    
6.  点击`Next`。

    ![](img/6-1-2.jpg)
    
7.  输入 Metasploitable 2 的名称并将`Operating System: `选择为`Linux`，`Version: `选项`Ubuntu`。像下面的截图那样点击`Next`。

    ![](img/6-1-3.jpg)

8.  如果可用的话，选择 `512 MB`，并点击`Next`。

    ![](img/6-1-4.jpg)
    
9.  选项现有磁盘，并从你下载和保存 Metasploitable 2 文件夹的地方选择 VDMK 文件。

    ![](img/6-1-5.jpg)
    
0.  你的虚拟磁盘窗口会像下面的截图那样。在这个示例中，我们完全不需要更新磁盘空间。这是因为使用 Metasploitable 的时候，你会攻击这个系统，而并不是将它用作操作系统。

    ![](img/6-1-6.jpg)
    
1.  点击`Create`。

    ![](img/6-1-7.jpg)
    
2.  通过点击 Metasploitable 2 的名称和`Start`按钮来启动它。

### 工作原理

这个秘籍中，我们在 Virtualbox 中配置了 Metasploitable 2。我们以从`Sourceforge.net`下载 Metasploitable 开始这个秘籍，之后我们配置了 VDMK 来在 VirtualBox 中运行并以启动该系统结束。

## 6.2 掌握 Armitage，Metasploit 的图形管理工具

新版本的 Metasploit 使用叫做 Armitage 的图形化前端工具。理解 Armitage 非常重要，因为它通过提供可视化的信息，使你对 Metasploit 的使用变得简单。它封装了 Metasploit 控制台，并且通过使用它的列表功能，你可以一次看到比 Metasploit 控制台或 Meterpreter 会话更多的内容。

### 准备

需要互联网或内部网络的连接。

### 操作步骤

让我们开始操作 Armitage：

1.  从桌面上访问`Start | Kali Linux | Exploitation Tools | Network Exploitation Tools | Armitage`。

    ![](img/6-2-1.jpg)

2.  在 Armitage的登录界面中，点击`Connect`（连接）按钮。

    ![](img/6-2-2.jpg)
    
3.  Armitage 可能需要一些时间来连接 Metasploit。当它完成时，你可能看见下面的提示窗口。不要惊慌，一旦 Armitage 能够连接时，它会消失的。在` Start Metaspoit?`界面，点击`Yes`：

    ![](img/6-2-3.jpg)

4.  随后你会看到 Armitage 的主窗口。我们现在讨论主窗口的三个区域（标记为`A`、`B`和`C`，在下面的截图中）。

    +   `A`：这个区域展示了预先配置的模块。你可以通过模块列表下面的搜索框来搜索。
    
    +   `B`：这个区域展示了你的活动目标，我们能够利用它的漏洞。
    
    +   `C`：这个区域展示了多个 Metasploit 标签页。它允许多个 Meterpreter 或控制台会话同时运行和展示。

    ![](img/6-2-4.jpg)
    
    > 启动 Armitage 的一个自动化方式就是在终端窗口中键入下列命令。
    
    > ```
    > armitage
    > ```
    
### 另见

为了了解更多 Meterpreter 的信息，请见“掌握 Meterpreter”一节。
