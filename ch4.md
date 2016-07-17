# 第四章 信息收集

## 简介

攻击的重要阶段之一就是信息收集。为了能够实施攻击，我们需要收集关于目标的基本信息。我们获得的信息越多，攻击成功的概率就越高。

我也强调这一阶段的一个重要方面，它就是记录。在编写这本书的时候，最新的Kali发行版包含了一组工具用于帮助我们核对和组织来自目标的数据，允许我们更好地侦查目标。类似Maltego CaseFile和 KeepNote的工具就是一个例子。

## 4.1 服务枚举

在这个秘籍中，我们将会展示一些服务枚举的小技巧。枚举是允许我们从网络收集信息的过程。我们将要研究DNS枚举和SNMP枚举技术。DNS枚举是定位某个组织的所有DNS服务器和DNS条目的过程。DN枚举允许我们收集有关该组织的重要信息，例如用户名、计算机名称、IP地址以及其它。为了完成这些任务我们会使用DNSenum。对于SNMP枚举，我们会使用叫做SnmpEnum的工具，它是一个强大的SNMP枚举工具，允许我们分析网络上的SNMP流量。

### 操作步骤

让我们以DNS枚举作为开始：

1.  我们使用DNSenum进行DNS枚举。为了开始DNS枚举，打开Gnome终端，并且输入一下命令：

    ```
    cd /usr/bin
    ./dnsenum --enum adomainnameontheinternet.com
    ```

    > 请不要在不属于你的公共网站或者不是你自己的服务器上运行这个工具。这里我们将`adomainnameontheinternet.com`作为一个例子，你应该替换掉这个目标。要当心！

2.  我们需要获取信息输出，例如主机、名称服务器、邮件服务器，如果幸运的话还可以得到区域转换：

    ![](img/4-1-1.jpg)

3.  我们可以使用一些额外的选项来运行DNSenum，它们包括这些东西：

    + `-- threads [number]`允许你设置一次所运行的线程数量。
    + `-r`允许你开启递归查找。
    + `-d`允许你设置在WHOIS请求之间的时间延迟，单位为秒。
    + `-o`允许我们制定输出位置。
    + `-w`允许我们开启WHOIS查询。

    > 更多WHOIS上的例子，请见[WHOIS的维基百科](http://en.wikipedia.org/wiki/Whois)。

4.  我们可以使用另一个命令`snmpwalk`来检测Windows主机。Snmpwalk是一个使用SNMP GETNEXT请求在网络实体中查询信息树的SNMP应用。在命令行中键入下列命令：

    ```
    snmpwalk -c public 192.168.10.200 -v 2c
    ```

5.  我们也可以枚举安装的软件：

    ```
    snmpwalk -c public 192.168.10.200 -v 1 | grep  hrSWInstalledName

    HOST-RESOURCES-MIB::hrSWInstalledName.1 = STRING: "VMware  Tools" HOST-RESOURCES-MIB::hrSWInstalledName.2 = STRING: "WebFldrs"
    ```

6.  以及使用相同工具枚举开放的TCP端口：

    ```
    snmpwalk -c public 192.168.10.200 -v 1 | grep tcpConnState |  cut -d"." -f6 | sort –nu

    21
    25
    80
    443
    ```

7.  另一个通过SNMP收集信息的工具叫做`snmpcheck`：

    ```
    cd /usr/bin
    snmpcheck -t 192.168.10.200
    ```

8.  为了使用fierce（一个尝试多种技术来寻找所有目标所用的IP地址和域名的工具）进行域名扫描，我们可以键入以下命令：

    ```
    cd /usr/bin
    fierce -dns adomainnameontheinternet.com
    ```

    > 请不要在不属于你的公共网站或者不是你自己的服务器上运行这个工具。这里我们将`adomainnameontheinternet.com`作为一个例子，你应该替换掉这个目标。要当心！

9.  为了以指定的词语列表进行相同的操作，键入以下命令：

    ```
    fierce -dns adomainnameontheinternet.com -wordlist  hosts.txt -file /tmp/output.txt
    ```

0.  为了在SMTP服务器上启动用户的SMTP枚举，键入以下命令：

    ```
    smtp-user-enum -M VRFY -U /tmp/users.txt -t 192.168.10.200
    ```

1.  我们现在可以记录所获得的结果了。
