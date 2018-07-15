---
layout: post
title:  "Kibana guide"
categories: Kibana guide
tags: Kibana guide
author: 若水三千
---

* content
{:toc}

# 说明 #

文档菜单截图和操作测试部分基于 Kibana 6.3.0 ，数据环境使用 Elasticsearch 6.3.1以及实例数据库进行使用测试。


# 搭建 #

- 下载
- 安装
- 启动
- 配置
- 升级


1. 支持的平台      
官方提供 Linux、Darwin 和 Windows 系统下的安装包。*<font color="darkorange">Kibana 基于 Node.js 运行，由于在这些平台上，一些核心的 Node.js 文件以二进制文件形式提供，因此无法在自维护的 Node.js 环境中运行。</font>*

2. Elasticsearch 版本      
Kibana 的主版本号需和 Elasticsearch 的主版本号保持一致，不同主版本号的 Kibana 和 Elasticsearch 是不兼容的（如 Kibana 5.x 和 Elasticsearch 2.x），若主版本号相同，运行 Kibana 子版本号比 Elasticsearch 子版本号新的版本也是不支持的（例如 Kibana 5.1 和 Elasticsearch 5.0）。
Elasticsearch 子版本号大于 Kibana 的版本基本不存在问题，这样做的目的是便于 Elasticsearch 版本的升级（例如 Kibana 5.0 和 Elasticsearch 5.1）。不过此时，Kibana 启动日志会输出一个警告，所以通常推荐使用 Kibana 和 Elasticsearch 相同版本来进行部署。
不同子版本的 Kibana 和 Elasticsearch 补丁是支持的（例如：Kibana 5.0.0 和 Elasticsearch 5.0.1），但是我们鼓励您去应用最新的补丁来更新版本。

## 一、安装 ##
>    从6.0.0开始，Kibana 只支持64位操作系统。


Kibana 提供以下格式的安装包：
<table>
    <tr>
        <td>
            <font color="rosybrown"><b>tar.gz/zip</b></font></td>
        <td> 
             <b>tar.gz</b> Linux、 Darwin 系统安装包。<br/>
             <b>zip</b> 唯一支持 Windows 系统的安装包。
        </td>
    </tr>
    <tr>
        <td>
            <font color="rosybrown"><b>deb</b></font>
        </td>
        <td>
            Debian、Ubuntu 和其他支持 Debian 的系统下的安装包, 可以从Elastic 官网或 Debian 仓库中下载。<br/>
            <a href="https://www.elastic.co/guide/cn/kibana/current/deb.html">Debian安装包下载地址</a> 
        </td>
    </tr>
    <tr>
        <td>
            <font color="rosybrown"><b>rpm</b></font>
        </td>
        <td>
        Red Hat、Centos、SLES、OpenSuSe 和其他支持 RPM 的系统下的安装包。可以从 Elastic 官网或者 RPM 仓库下载。<br/>
            <a href="https://www.elastic.co/guide/cn/kibana/current/rpm.html">RPM包下载地址</a>
        </td>
    </tr>
    <tr>
        <td>
            <font color="rosybrown"><b>docker</b></font>
        </td>
        <td>
            Elastic Docker 仓库中有包含 Kibana 的 Docker 镜像，并预装了 X-Pack 。
            Docker 容器中运行 Kibana
        </td>
    </tr>
</table>

>    如果您安装的 Elasticsearch 是受 X-Pack 安全插件保护的，请查看X-Pack 安全插件获取更多的配置信息。

#### 1.1 使用`.tar.gz` ####

Kibana 的最新稳定版本可以在[Kinana 下载页](https://www.elastic.co/downloads/kibana)找到。其它版本可以在[已发布版本](https://www.elastic.co/downloads/past-releases)中查看

###### **1.下载安装 Linux 64 位包** ######

``` shell
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-linux-x86_64.tar.gz
sha1sum kibana-6.3.0-linux-x86_64.tar.gz    ①
tar -xzf kibana-6.3.0-linux-x86_64.tar.gz 
cd kibana/                                  ② 
```

① 比较 `sha1sum` 或 `shasum` 计算的 SHA 跟 [官方的 SHA](https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-linux-x86_64.tar.gz.sha1) 是否一致。  
② 该目录是 `$KIBANA_HOME` 。

###### **2.下载安装 Darwin 包** ######

``` shell
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-darwin-x86_64.tar.gz
shasum kibana-6.3.0-darwin-x86_64.tar.gz 
tar -xzf kibana-6.3.0-darwin-x86_64.tar.gz
cd kibana/ 
```

###### **3. 启动 Kibana** ######

``` shell
./bin/kibana
```
 Kibana 默认在前台启动，打印日志到标准输出 (`stdout`)，可以通过 `Ctrl-C` 命令终止运行，`bg` 可切换到后台。

###### **4. 配置 Kibana** ######
默认配置文件 `$KIBANA_HOME/config/kibana.yml`。该配置文件的格式在 <a href="#setting">配置 Kibana </a>中做了说明。

###### **5. `.tar.gz` 文件目录** ######
`.tar.gz` 整个包是独立的。默认情况下，所有的文件和目录都在 $KIBANA_HOME — 解压包时创建的目录下。您不需要创建任何目录来使用 Kibana，卸载 Kibana 简单地删除 `$KIBANA_HOME` 目录。建议修改配置文件和数据目录位置，以防误删除重要数据。

<table>
    <tr>
        <td>
            <b>类型</b>
        </td>
        <td>
            <b>描述</b>
        </td>
        <td>
            <b>默认位置</b>
        </td>
    </tr>
    <tr>
        <td>
            <b>home</b>
        </td>
        <td>
            Kibana home 目录或 $KIBANA_HOME 。
        </td>
        <td>
            解压包时创建的目录
        </td>
    </tr>
    <tr>
        <td>
            <b>bin</b>
        </td>
        <td>
            二进制脚本，包括 kibana 启动 Kibana 服务和 kibana-plugin 安装插件。
        </td>
        <td>
            $KIBANA_HOME\bin
        </td>
    </tr>
    <tr>
        <td>
            <b>config</b>
        </td>
        <td>
            配置文件，包括 kibana.yml 。
        </td>
        <td>
            $KIBANA_HOME\config
        </td>
    </tr>
    <tr>
        <td>
            <b>data</b>
        </td>
        <td>
            Kibana 和其插件写入磁盘的数据文件位置。
        </td>
        <td>
            $KIBANA_HOME\data
        </td>
    </tr>
    <tr>
        <td>
            <b>optimize</b>
        </td>
        <td>
            编译过的源码。某些管理操作(如，插件安装)导致运行时重新编译源码。
        </td>
        <td>
            $KIBANA_HOME\optimize
        </td>
    </tr>
    <tr>
        <td>
            <b>plugins</b>
        </td>
        <td>
            插件文件位置。每一个插件都有一个单独的二级目录。
        </td>
        <td>
            $KIBANA_HOME\plugins
        </td>
    </tr>
</table>

#### 1.2 使用`Debian` ####
###### **1.导入 Elastic PGP 密钥** ######
所有部署包的签名使用的是 Elastic Signing Key (PGP key D88E42B4, 从 https://pgp.mit.edu 可以获得)，指纹为：
> 4609 5ACC 8548 582C 1A26 99A9 D27D 666C D88E 42B4

下载并安装签名公钥：  
``` shell
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

###### **2.从 APT 仓库安装** ######
在开始前，您需要在 Debian 系统上安装 `apt-transport-https` 包：

``` shell
sudo apt-get install apt-transport-https
```
保存仓库的定义到 `/etc/apt/sources.list.d/elastic-6.x.list`

``` shell
echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
```

>    ![](../../../../images/warning.png)  
>    <font color="#CC3333">请不要用 `add-apt-repository` 因为它需要添加 deb-src，但是我们没有提供包源。如果您已经添加了 deb-src，您将会遇到如下错误：</font>
>>    <font color="#9933FF">Unable to find expected entry 'main/source/Sources' in Release file (Wrong sources.list entry or malformed file)</font> 
> 
>    <font color="#CC3333">从 /etc/apt/sources.list 文件中删除 deb-src，便可以正常安装。</font>

使用以下命令安装 Kibana Debian 包：
``` shell
sudo apt-get update && sudo apt-get install kibana
```

>    ![](../../../../images/warning.png) 
>    <font color="#CC3333">如果在仓库中有两条相同的 Kibana 入口，执行 apt-get update 命令时您将会遇到如下错误：</font>
>>    <font color="#CC3333">Duplicate sources.list entry https://artifacts.elastic.co/packages/6.x/apt/ ...</font>`
>    <font color="#CC3333">检查这些文件中是否有重复记录： /etc/apt/sources.list.d/kibana-6.x.list、 /etc/apt/sources.list.d/ 和 /etc/apt/sources.list 。</font>

###### **3.手动下载安装 Debian 包** ######
Kibana v6.3.0 的 Debian 包从网站下载安装：
``` shell
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-amd64.deb
sha1sum kibana-6.3.0-amd64.deb 
sudo dpkg -i kibana-6.3.0-amd64.deb
```
###### **4.SysV init 和 systemd 对比** ######
Kibana 安装后不会自动启动。如何启动和停止 Kibana，依赖于操作系统。使用 SysV init 还是 systemd （新的发行版使用），可以通过以下命令来显示使用的是哪种：
``` shell
ps -p 1
```

###### **5.使用SysV init 运行Kibana** ######
使用 `update-rc.d` 命令配置 Kibana 开机自启动：
``` shell
sudo update-rc.d kibana defaults 95 10
```
使用 `service` 命令来启动和停止：
``` shell
sudo -i service kibana start
sudo -i service kibana stop
```
无论什么原因，如果 Kibana 启动失败，它会输出失败原因到 STDOUT。日志文件位于 `/var/log/kibana/` 目录中。

###### **6.使用 systemd 运行 Kibana** ######
配置 Kibana 开机自启，执行以下命令：
``` shell
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable kibana.service
```
Kibana 启动和停止命令如下：
``` shell
sudo systemctl start kibana.service
sudo systemctl stop kibana.service
```
这些命令不提供任何关于 Kibana 是否成功启动的反馈信息。而是将这些信息写入日志文件中，日志文件的位置在 `/var/log/kibana/` 。

###### **7.通过配置文件配置 Kibana** ######
Kibana 默认情况下从 `$KIBANA_HOME/config/kibana.yml` 加载配置文件。该配置文件的格式在[配置 Kibana](https://www.elastic.co/guide/cn/kibana/current/settings.html)  中有相关说明。

###### **8.Debian 包目录** ######
<table>
    <tr>
        <td>
            <b>类型</b>
        </td>
        <td>
            <b>描述</b>
        </td>
        <td>
            <b>默认位置</b>
        </td>
    </tr>
    <tr>
        <td>
            <b>home</b>
        </td>
        <td>
            Kibana home 目录或 $KIBANA_HOME 。
        </td>
        <td>
            /usr/share/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>bin</b>
        </td>
        <td>
            二进制脚本，包括 kibana 启动 Kibana server和 kibana-plugin 安装插件。
        </td>
        <td>
             /usr/share/kibana/bin
        </td>
    </tr>
    <tr>
        <td>
            <b>config</b>
        </td>
        <td>
            配置文件，包括 kibana.yml 。
        </td>
        <td>
            /etc/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>data</b>
        </td>
        <td>
            Kibana 和其插件写入磁盘的数据文件位置。
        </td>
        <td>
            /var/lib/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>optimize</b>
        </td>
        <td>
            编译过的源码。某些管理操作(如，插件安装)导致运行时重新编译源码。
        </td>
        <td>
            /usr/share/kibana/optimize
        </td>
    </tr>
    <tr>
        <td>
            <b>plugins</b>
        </td>
        <td>
            插件文件位置。每一个插件都有一个单独的二级目录。
        </td>
        <td>
            /usr/share/kibana/plugins
        </td>
    </tr>
</table>

#### 1.3 使用`RPM` ####
###### **1.导入 Elastic PGP 密钥** ######
所有部署包的签名使用的是 Elastic Signing Key (PGP key D88E42B4, 从 https://pgp.mit.edu 可以获得)，指纹为：
> 4609 5ACC 8548 582C 1A26 99A9 D27D 666C D88E 42B4

下载并安装签名公钥：  
``` shell
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

###### **2.从 RPM 仓库安装** ######
对于 RedHat 的发行版，在 `/etc/yum.repos.d/` 目录下新建一个 `kibana.repo` 文件，对于 OpenSuSE 的发行版，在 `/etc/zypp/repos.d/` 目录下新建一个 `kibana.repo 文件`，包含如下内容:

``` 
[kibana-6.x]
name=Kibana repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
您的仓库已经准备好了。现在您可以用下面的命令来安装 Kibana：

``` shell
sudo yum install kibana      ①
sudo dnf install kibana      ②
sudo zypper install kibana   ③
```
① 在 CentOS 和较低版本的 Red Hat 发行版上使用 yum 。  
② 在 Fedora 和较高版本的 Red Hat 发行版上使用 dnf 。  
③ 在 OpenSUSE 的发行版上使用 zypper 。  

###### **3.手动下载安装 RPM 包** ######
Kibana v6.3.0 的 RPM 包从网站下载安装：
``` shell
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-x86_64.rpm
sha1sum kibana-6.3.0-x86_64.rpm 
sudo rpm --install kibana-6.3.0-x86_64.rpm
```
###### **4.SysV init 和 systemd 对比** ######
Kibana 安装后不会自启动。如何启动和停止 Kibana，依赖于操作系统。使用 SysV init 还是 systemd （新的发行版使用），可以通过以下命令来显示使用的是哪种：
``` shell
ps -p 1
```

###### **5.使用SysV init 运行Kibana** ######
使用 `chkconfig` 命令配置 Kibana 开机自启动：
``` shell
sudo chkconfig --add kibana
```
使用 `service` 命令来启动和停止：
``` shell
sudo -i service kibana start
sudo -i service kibana stop
```
无论什么原因，如果 Kibana 启动失败，它会输出失败原因到 STDOUT。日志文件位于 `/var/log/kibana/` 目录中。

###### **6.使用 systemd 运行 Kibana** ######
配置 Kibana 开机自启，执行以下命令：
``` shell
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable kibana.service
```
Kibana 启动和停止命令如下：
``` shell
sudo systemctl start kibana.service
sudo systemctl stop kibana.service
```
这些命令不提供任何关于 Kibana 是否成功启动的反馈信息。而是将这些信息写入日志文件中，日志文件的位置在 `/var/log/kibana/` 。

###### **7.通过配置文件配置 Kibana** ######
Kibana 默认情况下从 `$KIBANA_HOME/config/kibana.yml` 加载配置文件。该配置文件的格式在[配置 Kibana](https://www.elastic.co/guide/cn/kibana/current/settings.html)  中有相关说明。

###### **8.RPM 包目录** ######
<table>
    <tr>
        <td>
            <b>类型</b>
        </td>
        <td>
            <b>描述</b>
        </td>
        <td>
            <b>默认位置</b>
        </td>
    </tr>
    <tr>
        <td>
            <b>home</b>
        </td>
        <td>
            Kibana home 目录或 $KIBANA_HOME 。
        </td>
        <td>
            /usr/share/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>bin</b>
        </td>
        <td>
            二进制脚本，包括 kibana 启动 Kibana server和 kibana-plugin 安装插件。
        </td>
        <td>
             /usr/share/kibana/bin
        </td>
    </tr>
    <tr>
        <td>
            <b>config</b>
        </td>
        <td>
            配置文件，包括 kibana.yml 。
        </td>
        <td>
            /etc/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>data</b>
        </td>
        <td>
            Kibana 和其插件写入磁盘的数据文件位置。
        </td>
        <td>
            /var/lib/kibana
        </td>
    </tr>
    <tr>
        <td>
            <b>optimize</b>
        </td>
        <td>
            编译过的源码。某些管理操作(如，插件安装)导致运行时重新编译源码。
        </td>
        <td>
            /usr/share/kibana/optimize
        </td>
    </tr>
    <tr>
        <td>
            <b>plugins</b>
        </td>
        <td>
            插件文件位置。每一个插件都有一个单独的二级目录。
        </td>
        <td>
            /usr/share/kibana/plugins
        </td>
    </tr>
</table>

#### 1.4 Windows ####

###### **1.下载 .zip 文件** ######
下载 Kibana v6.3.0 的 .zip windows 文件： https://artifacts.elastic.co/downloads/kibana/kibana-6.3.0-windows-x86_64.zip

解压 zip 文件。默认创建一个 kibana-6.3.0-windows-x86_64 文件夹，也就是我们指的 $KIBANA_HOME 。在一个终端窗口中， CD 到 $KIBANA_HOME 目录，例如：
```
CD c:\kibana-6.3.0-windows-x86_64
```
###### **2.启动 Kibana** ######
Kibana 可以从命令行启动，如下：
```
.\bin\kibana
```
Kibana 默认在前台启动，输出 log 到 STDOUT ，可以通过 Ctrl-C 停止 Kibana。

###### **3.配置 Kibana** ######
默认从 `$KIBANA_HOME/config/kibana.yml` 加载配置文件。该配置文件的格式在 配置 Kibana 中做了说明。

###### **4..zip 目录** ######
默认解压所有的文件和目录都在 $KIBANA_HOME — 解压时创建的目录下。卸载 Kibana 只需要简单的删除 $KIBANA_HOME 目录。建议修改一下配置文件和数据目录，这样就不会误删重要数据。
<table>
    <tr>
        <td>
            <b>类型</b>
        </td>
        <td>
            <b>描述</b>
        </td>
        <td>
            <b>默认位置</b>
        </td>
    </tr>
    <tr>
        <td>
            <b>home</b>
        </td>
        <td>
            Kibana home 目录或 $KIBANA_HOME 。
        </td>
        <td>
            解压包时创建的目录
        </td>
    </tr>
    <tr>
        <td>
            <b>bin</b>
        </td>
        <td>
            二进制脚本，包括 kibana 启动 Kibana 服务和 kibana-plugin 安装插件。
        </td>
        <td>
            $KIBANA_HOME\bin
        </td>
    </tr>
    <tr>
        <td>
            <b>config</b>
        </td>
        <td>
            配置文件，包括 kibana.yml 。
        </td>
        <td>
            $KIBANA_HOME\config
        </td>
    </tr>
    <tr>
        <td>
            <b>data</b>
        </td>
        <td>
            Kibana 和其插件写入磁盘的数据文件位置。
        </td>
        <td>
            $KIBANA_HOME\data
        </td>
    </tr>
    <tr>
        <td>
            <b>optimize</b>
        </td>
        <td>
            编译过的源码。某些管理操作(如，插件安装)导致运行时重新编译源码。
        </td>
        <td>
            $KIBANA_HOME\optimize
        </td>
    </tr>
    <tr>
        <td>
            <b>plugins</b>
        </td>
        <td>
            插件文件位置。每一个插件都有一个单独的二级目录。
        </td>
        <td>
            $KIBANA_HOME\plugins
        </td>
    </tr>
</table>

## 二、配置参数 ##
Kibana server 启动时从 `kibana.yml` 文件中读取配置参数。Kibana 默认配置 localhost:5601 。连接其他机器上的 Elasticsearch，需要更新 kibana.yml 文件。或者启用 SSL 和设置其他选项。


**Kibana 配置项**

<table class="flex">
    <tr>
        <td><b>参数</b></td>
        <td><b>说明</b></td>
        <td><b>缺省值</b></td>
    </tr>
    <tr>
        <td><b>server.port</b></td>
        <td>端口号。</td>
        <td>5601</td>
    </tr>
    <tr>
        <td><b>server.host</b></td>
        <td>主机地址。</td>
        <td>localhost</td> 
    </tr>
    <tr>
        <td><b>server.basePath</b></td>
        <td>如果启用代理，指定 Kibana 的路径，仅影响 Kibana 生成的 URLs，转发请求到 Kibana 时代理会重写基础路径值，参数值项不能以斜杠 (/)结尾。</td>
        <td></td> 
    </tr>
    <tr>
        <td><b>server.maxPayloadBytes</b></td>
        <td>服务器请求的最大负载，单位字节。</td>
        <td>1048576</td>     
    </tr>     
    <tr>
        <td><b>server.name</b></td>
        <td>Kibana 实例的名称（对外显示）。</td>
        <td>您的主机名</td>
    </tr>
    <tr> 
        <td><b>server.defaultRoute</b></td>
        <td>配置 Kibana 登录页面的默认路径。</td>
        <td>/app/kibana</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.url</b></td>
        <td>用来处理所有查询的 Elasticsearch 实例的 URL 。</td>
        <td>http://localhost:9200</td> 
    </tr>
    <tr> 
        <td><b>elasticsearch.preserveHost</b></td>
        <td>值为 true 时，Kibana 使用 server.host 设定的主机名，值为 false 时，Kibana 使用主机的主机名来连接 Kibana 实例。</td>
        <td>true</td>
    </tr>
    <tr> 
        <td><b>kibana.index</b></td>
        <td>Kibana 使用 Elasticsearch 的索引来存储检索，可视化控件以及仪表板。如果没有索引，Kibana 会创建一个新的索引。</td>
        <td>.kibana</td>
    </tr>
    <tr> 
        <td><b>kibana.defaultAppId</b></td>
        <td>默认加载的应用。</td>
        <td>discover</td>
    </tr>
    <tr> 
        <td><b>tilemap.url</b></td>
        <td>
Kibana 用来在 tile 地图可视化组件中展示地图服务的 URL。默认时，Kibana 从外部的元数据服务读取 url，用户也可以覆盖该参数，使用自己的 tile 地图服务。例如："https://tiles.elastic.co/v2/default/{z}/{x}/{y}.png?elastic_tile_service_tos=agree&my_app_name=kibana"
        </td>
        <td></td>
    </tr>
    <tr> 
        <td><b>tilemap.options.minZoom</b></td>
        <td>最小缩放级别。</td>
        <td>1</td>
    </tr>
    <tr> 
        <td><b>tilemap.options.maxZoom</b></td>
        <td>最大缩放级别。</td>
        <td>10</td>
    </tr>
    <tr> 
        <td><b>tilemap.options.attribution</b></td>
        <td><a href="https://www.elastic.co/elastic-tile-service"> Elastic Tile Service</a> 地图属性字符串。</td>
        <td>©</td> 
    </tr>
    <tr> 
        <td><b>tilemap.options.subdomains</b></td>
        <td>服务使用的二级域名列表，用 {s} 指定二级域名的 URL 地址。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.username 和 elasticsearch.password</b></td>
        <td>Elasticsearch 基本的权限认证设置，配置基于用户名和密码的认证，用于 Kibana 启动时维护索引。Kibana 用户仍需要 Elasticsearch 由 Kibana 服务端代理的提供认证。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>server.ssl.enabled</b></td>
        <td>为浏览器端请求提供启用 SSL加密，设为 true 时， server.ssl.certificate 和 server.ssl.key 也要设置。</td>
        <td>false</td>
    </tr>
    <tr> 
        <td><b>server.ssl.certificate 和 server.ssl.key</b></td>
        <td>PEM 格式 SSL 证书和 SSL 密钥文件的路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>server.ssl.keyPassphrase</b></td>
        <td>解密私钥的口令，可选项，密钥可能没有进行加密。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>server.ssl.certificateAuthorities</b></td>
        <td>可信任 PEM 编码的证书文件路径列表。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>server.ssl.supportedProtocols</b></td>
        <td>版本支持的协议，有效的协议类型: TLSv1 、 TLSv1.1 、 TLSv1.2 。</td>
        <td>TLSv1、TLSv1.1、TLSv1.2</td> 
    </tr>
    <tr> 
        <td><b>server.ssl.cipherSuites</b></td>
        <td>具体格式和有效参数可参考<a href="https://www.openssl.org/docs/man1.0.2/apps/ciphers.html#CIPHER-LIST-FORMAT">OpenSSL cipher list format documentation</a>。</td>
        <td>ECDHE-RSA-AES128-GCM-SHA256, ECDHE-ECDSA-AES128-GCM-SHA256, ECDHE-RSA-AES256-GCM-SHA384, ECDHE-ECDSA-AES256-GCM-SHA384, DHE-RSA-AES128-GCM-SHA256, ECDHE-RSA-AES128-SHA256, DHE-RSA-AES128-SHA256, ECDHE-RSA-AES256-SHA384, DHE-RSA-AES256-SHA384, ECDHE-RSA-AES256-SHA256, DHE-RSA-AES256-SHA256, HIGH,!aNULL, !eNULL, !EXPORT, !DES, !RC4, !MD5, !PSK, !SRP, !CAMELLIA.</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.ssl.certificate 和 elasticsearch.ssl.key</b></td>
        <td>可选配置项，提供 PEM 格式的 SSL 证书和密钥文件的路径。确保 Elasticsearch 后端使用同样的密钥文件。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.ssl.keyPassphrase</b></td>
        <td>解密私钥的口令，可选，因为密钥可能没有加密。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.ssl.certificateAuthorities</b></td>
        <td>指定用于 Elasticsearch 实例的 PEM 证书文件路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.ssl.verificationMode</b></td>
        <td>控制证书的认证，可用的值有none、certificate、full。 full 执行主机名验证，certificate 不执行主机名验证。</td>
        <td>full</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.pingTimeout</b></td>
        <td>等待 Elasticsearch 的响应时间。</td>
        <td>同 elasticsearch.requestTimeout setting 的值</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.requestTimeout</b></td>
        <td>等待后端或 Elasticsearch 的响应时间，单位微秒，值必须为正整数。</td>
        <td>30000</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.requestHeadersWhitelist</b></td>
        <td>Kibana 客户端发送到 Elasticsearch 头体，发送 no 头体，设置该值为[]。</td>
        <td>[ 'authorization' ]</td>
    </tr>
    <tr> 
       <td> <b>elasticsearch.customHeaders</b></td>
       <td>Elasticsearch的头体和值，不管 elasticsearch.requestHeadersWhitelist 如何配置，任何自定义的头体不会被客户端头体覆盖。</td>
       <td>{}</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.shardTimeout</b></td>
        <td>Elasticsearch 等待分片响应时间，单位微秒，0表示禁用。</td>
        <td>0</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.startupTimeout</b></td>
        <td>Kibana 启动时等待 Elasticsearch 的时间，单位微秒。</td>
        <td>5000</td>
    </tr>
    <tr> 
        <td><b>pid.file</b></td>
        <td>指定 Kibana 的进程 ID 文件的路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>logging.dest</b></td>
        <td>Kibana 日志输出的文件。</td>
        <td>stdout</td>    
    </tr>
    <tr> 
        <td><b>logging.silent</b></td>
        <td>该值设为 true 时，禁止所有日志输出。</td>
        <td>false</td>
    </tr>
    <tr> 
        <td><b>logging.quiet</b></td>
        <td>该值设为 true 时，禁止除错误信息除外的所有日志输出。</td>
        <td>false</td>
    </tr>
    <tr> 
        <td><b>logging.verbose</b></td>
        <td>该值设为 true 时，记下所有事件包括系统使用信息和所有请求的日志。</td>
        <td>false</td>
    </tr>
    <tr> 
        <td><b>ops.interval</b></td>
        <td>设置系统和进程取样间隔，单位微妙，最小值100。</td>
        <td>5000</td>
    </tr>
    <tr> 
        <td><b>status.allowAnonymous</b></td>
        <td>如果启用了权限，该项设置为 true 即允许所有非授权用户访问 Kibana 服务端 API 和状态页面。</td>
        <td>false</td>
    </tr>
    <tr> 
        <td><b>cpu.cgroup.path.override</b></td>
        <td>如果挂载点跟 /proc/self/cgroup 不一致，覆盖 cgroup cpu 路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>cpuacct.cgroup.path.override</b></td>
        <td>如果挂载点跟 /proc/self/cgroup 不一致，覆盖 cgroup cpuacct 路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>console.enabled</b></td>
        <td>设为 false 表示禁用控制台，切换该值后服务端下次启动时会重新生成资源文件，导致页面服务响应延迟。</td>
        <td>true</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.url</b></td>
        <td>Elasticsearch tribe 实例的 URL，用于所有查询。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.username 和 elasticsearch.tribe.password</b></td>
        <td>Elasticsearch 设置了基本的权限认证，该配置项提供了用户名和密码，用于 Kibana 启动时维护索引。Kibana 用户仍需要 Elasticsearch 由 Kibana 服务端代理的认证。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.ssl.certificate 和 elasticsearch.tribe.ssl.key</b></td>
        <td>可选配置，提供 PEM 格式 SSL 证书和密钥文件的路径。确保 Elasticsearch 后端使用同样的密钥文件。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.ssl.keyPassphrase</b></td>
        <td>解密私钥的口令，可选，密钥可能没有加密。</td>
        <td></td>
    </tr>
    <tr>
        <td><b>elasticsearch.tribe.ssl.certificateAuthorities</b></td>
        <td>指定用于 Elasticsearch tribe 实例的 PEM 证书文件路径。</td>
        <td></td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.ssl.verificationMode</b></td>
        <td>控制证书的认证，可用的值有 none、certificate、full。full 执行主机名验证，certificate 不执行主机名验证。</td>
        <td>full</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.pingTimeout</b></td>
        <td>等待 Elasticsearch 的响应时间。</td>
        <td>elasticsearch.tribe.requestTimeout setting 的值</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.requestTimeout</b></td>
        <td>等待后端或 Elasticsearch 的响应时间，单位微秒，该值必须为正整数。</td>
        <td>30000</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.requestHeadersWhitelist</b></td>
        <td>Kibana 发往 Elasticsearch 的客户端头体，发送 no 头体，设置该值为[]。</td>
        <td>[ 'authorization' ]</td>
    </tr>
    <tr> 
        <td><b>elasticsearch.tribe.customHeaders</b></td>
        <td>发往 Elasticsearch的头体和值，不管 elasticsearch.tribe.requestHeadersWhitelist 如何配置，任何自定义的头体不会被客户端头体覆盖。</td>
        <td>{}</td>
   </tr>
</table>


## 三、Docker容器运行 ##

Kibana 的 Docker 镜像可以从 Elastic 官网上的 Docker 镜像仓库获取。该镜像是随 X-Pack 一起打包的。

>    注意
>    X-Pack 在这个 image 中是预装好的。安装了 X-Pack，Kibana 会去连接同样带有 X-Pack 的 Elasticsearch 集群。

###### **1.获取镜像** ######

向 Elastic Docker 仓库发送 docker pull 命令就获取 Kibana Docker 镜像。

``` shell
docker pull docker.elastic.co/kibana/kibana:6.3.0
```

###### **2.Docker中 Kibana 配置** ######

Docker 镜像支持了多种方法来配置 Kibana。普遍的实践是修改 Kibana 中的配置文件 kibana.yml （参见配置小节），也可以使用环境变量来进配置。

1.**绑定配置**

一种配置 Docker 中 Kibana 的方法是通过绑定配置文件 kibana.yml 。使用 `docker-compose` 工具，如下绑定：

```
services:
  kibana:
    image: docker.elastic.co/kibana/kibana:6.3.0
    volumes:
      - ./kibana.yml:/usr/share/kibana/config/kibana.yml
```

2.**环境变量**

通过环境变量的进行设置。环境变量表如下：

<table class="flex">
    <tr>
        <td>环境变量（Environment Variable）</td>
        <td>Kibana设置（Kibana Setting）</td>
    </tr>
    <tr> 
        <td>ELASTICSEARCH_CUSTOMHEADERS</td>
        <td>elasticsearch.customHeaders</td>
    </tr>
    <tr> 
        <td>ELASTICSEARCH_PASSWORD</td>
        <td>elasticsearch.password</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_PINGTIMEOUT</td>
        <td>elasticsearch.pingTimeout</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_PRESERVEHOST</td>
        <td>elasticsearch.preserveHost</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_REQUESTHEADERSWHITELIST</td>
        <td>elasticsearch.requestHeadersWhitelist</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_REQUESTTIMEOUT</td>
        <td>elasticsearch.requestTimeout</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_SHARDTIMEOUT</td>
        <td>elasticsearch.shardTimeout</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_SSL_CA</td>
        <td>elasticsearch.ssl.ca</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_SSL_CERT</td>
        <td>elasticsearch.ssl.cert</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_SSL_KEY</td>
        <td>elasticsearch.ssl.key</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_SSL_VERIFY</td>
        <td>elasticsearch.ssl.verify</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_STARTUPTIMEOUT</td>
        <td>elasticsearch.startupTimeout</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_URL</td>
        <td>elasticsearch.url</td>
    </tr>
    <tr>
        <td>ELASTICSEARCH_USERNAME</td>
        <td>elasticsearch.username</td>
    </tr>
    <tr>
        <td>KIBANA_DEFAULTAPPID</td>
        <td>kibana.defaultAppId</td>
    </tr>
    <tr>
        <td>KIBANA_INDEX</td>
        <td>kibana.index</td>
    </tr>
    <tr>
        <td>LOGGING_DEST</td>
        <td>logging.dest</td>
    </tr>
    <tr>
        <td>LOGGING_QUIET</td>
        <td>logging.quiet</td>
    </tr>
    <tr>
        <td>LOGGING_SILENT</td>
        <td>logging.silent</td>
    </tr>
    <tr>
        <td>LOGGING_VERBOSE</td>
        <td>logging.verbose</td>
    </tr>
    <tr>
        <td>OPS_INTERVAL</td>
        <td>ops.interval</td>
    </tr>
    <tr>
        <td>PID_FILE</td>
        <td>pid.file</td>
    </tr>
    <tr>
        <td>SERVER_BASEPATH</td>
        <td>server.basePath</td>
    </tr>
    <tr>
        <td>SERVER_HOST</td>
        <td>server.host</td>
    </tr>
    <tr>
        <td>SERVER_MAXPAYLOADBYTES</td>
        <td>server.maxPayloadBytes</td>
    </tr>
    <tr>
        <td>SERVER_NAME</td>
        <td>server.name</td>
    </tr>
    <tr>
        <td>SERVER_PORT</td>
        <td>server.port</td>
    </tr>
    <tr>
        <td>SERVER_SSL_CERT</td>
        <td>server.ssl.cert</td>
    </tr>
    <tr>
        <td>SERVER_SSL_KEY</td>
        <td>server.ssl.key</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_ELASTICSEARCH_URL</td>
        <td>xpack.monitoring.elasticsearch.url</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_ELASTICSEARCH_USERNAME</td>
        <td>xpack.monitoring.elasticsearch.username</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_ELASTICSEARCH_PASSWORD</td>
        <td>xpack.monitoring.elasticsearch.password</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_ENABLED</td>
        <td>xpack.monitoring.enabled</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_MAX_BUCKET_SIZE</td>
        <td>xpack.monitoring.max_bucket_size</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_MIN_INTERVAL_SECONDS</td>
        <td>xpack.monitoring.min_interval_seconds</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_NODE_RESOLVER</td>
        <td>xpack.monitoring.node_resolver</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_REPORT_STATS</td>
        <td>xpack.monitoring.report_stats</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_KIBANA_COLLECTION_ENABLED</td>
        <td>xpack.monitoring.kibana.collection.enabled</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_KIBANA_COLLECTION_INTERVAL</td>
        <td>xpack.monitoring.kibana.collection.interval</td>
    </tr>
    <tr>
        <td>XPACK_MONITORING_UI_CONTAINER_ELASTICSEARCH_ENABLED</td>
        <td>xpack.monitoring.ui.container.elasticsearch.enabled</td>
    </tr>
    <tr>
        <td>XPACK_SECURITY_ENABLED</td>
        <td>xpack.security.enabled</td>
    </tr>
    <tr>
        <td>XPACK_SECURITY_COOKIENAME</td>
        <td>xpack.security.cookieName</td>
    </tr>
    <tr>
        <td>XPACK_SECURITY_ENCRYPTIONKEY</td>
        <td>xpack.security.encryptionKey</td>
    </tr>
    <tr>
        <td>XPACK_SECURITY_SECURECOOKIES</td>
        <td>xpack.security.secureCookies</td>
    </tr>
    <tr>
        <td>XPACK_SECURITY_SESSIONTIMEOUT</td>
        <td>xpack.security.sessionTimeout</td>
    </tr>
</table>



变量使用方式如下，用 `docker-compose` 设置：
```
services:
  kibana:
    image: docker.elastic.co/kibana/kibana:6.0.0
    environment:
      SERVER_NAME: kibana.example.org
      ELASTICSEARCH_URL: http://elasticsearch.example.org
```


环境变量优先级高于配置文件优先级。

3.**Docker 默认值**

<table>
    <tr>
        <td>server.host</td>
        <td>"0"</td>
    </tr>
    <tr>
        <td>elasticsearch.url</td>
        <td>http://elasticsearch:9200</td>
    </tr>
    <tr>
        <td>elasticsearch.username</td>
        <td>elastic</td>
    </tr>
    <tr>
        <td>elasticsearch.password</td>
        <td>changeme</td>
    </tr>
    <tr>
        <td>xpack.monitoring.ui.container.elasticsearch.enabled</td>
        <td>true</td>
    </tr>
</table>

这些配置项的默认值在 kibana.yml 中设置。可以通过 自定义 kibana.yml 或者 环境变量覆盖这些默认值。

## 四、访问 Kibana ##

Kibana web 应用，默认通过5601端口访问。只需要在浏览器中使用 localhost:5601 或者 http://YOURDOMAIN.com:5601 。
当访问 Kibana 时，Discover 页默认加载缺省的索引模式。时间过滤器设置的时间为过去15分钟，查询结果为匹配所有 (\*) 。

如果看不到任何文档，增加时间过滤器的时间范围。如果还是没有任何结果，很可能是根本就没有任何文档。

检查 Kibana 状态编辑
通过 localhost:5601/status 来查看 Kibana 的服务器状态，状态页展示了服务器资源使用情况和已安装插件列表。
![](../../../../images/kibana/status.png)

## 五、连接 Kibana 和 Elasticsearch ##

首次使用 Kibana 前，需要设置想要使用 Elasticsearch 索引。如果是第一次访问 Kibana ，会提示您定义一个 index pattern(索引模式) ，用以匹配一个或多个索引。这是初次使用 Kibana 需要配置的。不过，你可以根据需要在任何时候在 Management 页面增加索引模式。

>    提示
>    Kibana 默认尝试连接运行在 `localhost` 上的 Elasticsearch 实例。如果需要连接其他服务器上的 Elasticsearch 实例，可以修改 `kibana.yml` 配置文件中的 `Elasticsearch URL` 参数并重启 Kibana。生产环境上使用 Kibana，请参考 *生产环境中使用 Kibana*小节 。

设置您想通过 Kibana 查询的 Elasticsearch 索引：

1.浏览器访问 Kibana UI 页面。例如， localhost:5601 或者 http://YOURDOMAIN.com:5601 。
![](../../../../images/kibana/index_pattern.png)

2.设置一个索引模式来匹配一个或多个 Elasticsearch 索引名称。缺省 Kibana 会认为数据是由 Logstash 解析送进 Elasticsearch 的。这时可以使用默认的 `logstash-*` 作为索引模式。星号 (*) 匹配0或多个索引名称中的字符。如果 Elasticsearch 索引遵循其他命名约定，请输入一个恰当的模式。该模式也可以直接用单个索引的名称。

3.如果您想做一些基于时间序列的数据比较，可以选择索引中包含时间戳的字段。Kibana 会读取索引映射，列出包含时间戳的所有字段。如果索引中没有基于时间序列的数据，则禁用 Index contains time-based events 选项。

>    警告
>    使用事件时间来创建索引名称在这个版本的 Kibana 中会被标记成 deprecated 。这个功能可能会在下一个 Kibana 的主版本中被彻移除。 Elasticsearch 2.1 拥有强大的日期解析 API 用于分割日期信息，没必要在索引模式名称中指定日期。

4.点击 Create 增加索引模式。第一个模式被自动设置为默认的。当索引模式不止一个时，可以通过点击 **Management > Index Patterns** 索引模式题目上的星星图标来设置缺省的索引模式。

Kibana 访问 Elasticsearch 数据，并展示一个匹配到的索引的字段只读列表。

>    注意
> Kibana 可视化控件中的字段以及 `.kibana` 索引管理依赖动态映射（dynamic mapping）功能，如果动态映射被关闭，您需要手动提供字段的映射以便 Kibana 能正确的创建可视化控件。更多信息，请参考 *Kibana 和 Elasticsearch 动态映射* 小节 。

1. *开始探索您的数据！**  

- 在 `Discover` 页搜索和浏览数据。
- 在 `Visualize` 页做数据图表映射。
- 在 `Dashboard` 页创建并查看自定义仪表板。
- 您可以通过查看 *基础入门来获取* Kibana 获得快速指南。

2. **Kibana 和 Elasticsearch 动态映射**  

Elasticsearch 启用了字段的 [动态映射](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/dynamic-mapping.html "动态映射")。Kibana 需要使用动态映射在可视化控件中正确引用字段，同时管理 `.kibana` 索引，这些索引存储了已保存的搜索、可视化图表和仪表板。

如果 Elasticsearch 使用场景需要禁止动态映射，这就需要手动提供创建可视化控件所需要字段的映射，并手动启用 `.kibana` 索引的动态映射。

下面的步骤假定 Elasticsearch 中不存在索引 `.kibana` ，且 `elasticsearch.yml` 中 `index.mapper.dynamic` 配置为 false ：

1.启动 Elasticsearch。
2.创建 `.kibana` 索引并只针对该索引打开动态映射：

```
PUT .kibana
{
  "index.mapper.dynamic": true
}
```
3.启动 Kibana ，查看 web 页面，确认动态映射不存在错误。

## 六、使用 Kibana Tribe 节点 ##

Kibana 可以配置 Tribe 节点用于数据检索。因为 tribe 节点不能创建索引，Kibana 需要一个独立的连接来维护节点状态。当配置好后，搜索和可视化控件会使用 tribe 节点检索数据，管理操作（如保存仪表板）会发送给非 tribe 节点。

**配置 Kibana Tribe 节点**  
当 `kibana.yml` 中配置了 elasticsearch 时，Tribe 节点使用相同的配置。Tribe 配置的前缀是 `elasticsearch.tribe` ，至少需要配置一个 url：

>    elasticsearch.url: &quot;&lt; your_administration_node &gt;&quot;   
>    elasticsearch.tribe.url: &quot;&lt; your_tribe_node &gt;&quot;   

当配置了 tribe 节点时，更改 Kibana 状态的操作会发给 `elasticsearch.url` 配置的地址。搜索和可视化控件会从 `elasticsearch.tribe.url` 节点检索数据。 `elasticsearch.url` 配置的节点可以是 tribe 节点所连接集群中的其中一个。

整个配置列表请见 *配置 Kibana* 。

**局限性**  

由于使用哪个集群会存在歧义，Kibana 一些特性不可用：

- 控制台
- x-pack 插件的用户和角色管理


## 七、Kibana 生产环境中应用 ##

- Kibana 中使用 X-Pack
- 打开 SSL
- Elasticsearch 多节点负载均衡

Kibana 的配置依赖于您的应用场景。如果只有自己使用，可以在自己的机器上运行 Kibana，配置它指向任何您想要交互的 Elasticsearch 实例。相反，如果有大量的 Kibana 使用者，需要多个 Kibana 实例连接至同一个 Elasticsearch 节点，来保证负载均衡。

尽管 Kibana 不是非常耗费资源，我们仍然建议运行 Kibana 的节点和 Elasticsearch 数据或主节点分开。在 Elasticsearch 集群中分配 Kibana，可以在 Elasticsearch 客户端节点上运行 Kibana。详细信息请参考 *Elasticsearch 多节点负载均衡*。

###### **1.在 Kibana 中使用 X-Pack** ######

启用 X-Pack 安全模块控制用户通过 Kibana 可以访问哪些 Elasticsearch 数据。
当安装 X-Pack 时，Kibana 用户必须登陆。这些用户需要用 `kibana_user` 角色来访问通过 Kibana 管理的索引库。

如果一个用户要通过 Kibana 仪表板访问某个索引库中的数据，但没有查看权限，会收到一个错误提示：索引不存在。X-Pack 的安全机制目前还不能提供某种策略来控制不同的用户加载不同的仪表板。

关于设置 Kibana 用户和 X-Pack 信息，请参见 *X-Pack 安全插件*。

###### **2.启用 SSL** ######

不管是来自客户端的请求，还是 Kibana 服务端发给 Elasticsearch 的请求，Kibana 都支持 SSL 加密。
要加密浏览器和 Kibana 服务端之间的会话，请配置 kibana.yml 文件中的 `server.ssl.enabled`、`server.ssl.certificate` 和 `server.ssl.key` 属性：

>    # SSL for outgoing requests from the Kibana Server (PEM formatted)      
>    server.ssl.enabled: true    
>    server.ssl.key: /path/to/your/server.key        
>    server.ssl.certificate: /path/to/your/server.crt      

如果 Elasticsearch 使用 X-Pack 安全协议或者设置了 HTTPS 代理。您可以设置 Kibana 通过 HTTPS 访问 Elasticsearch，这样 Kibana 服务端和 Elasticsearch 的会话就会被加密。

可以通过在配置文件 kibana.yml 中设置 `Elasticsearch URL` 开启 HTTPS 协议：

>    elasticsearch.url: https://your_elasticsearch_host.com:9200

如果 Elasticsearch 使用了自签名证书，设置 kibana.yml 文件中的 `certificateAuthorities` 属性指向 PEM 文件的位置，设置 `certificateAuthorities` 属性，可以使用默认的 verificationMode 选项 full 。

>    # If you need to provide a CA certificate for your Elasticsearch instance, put    
>    # the path of the pem file here.      
>    elasticsearch.ssl.certificateAuthorities: [ &quot;/path/to/your/ca/cacert.pem&quot; ]

###### **3.多个 Elasticsearch 节点间的负载均衡** ######

在 Elasticsearch 集群的多个节点之间分发 Kibana 节点请求的最简单的方法就是在 Kibana 机器上运行一个 Elasticsearch *协调（Coordinating only node）* 的节点。Elasticsearch 协调节点本质上是智能负载均衡器，也是集群的一部分，如果有需要，这些节点会处理传入的 HTTP 请求，重定向请求给集群中的其它节点，收集并返回结果。更多详细信息，请参考 *节点* 部分。

使用本地客户端节点负载均衡 Kibana 请求：

1.在安装 Kibana 的机器上安装 Elasticsearch。
2.配置节点为协调节点。在配置文件 elasticsearch.yml 中，设置 `node.data`、 `node.master` 和 `node.ingest` 为 false。

>    #    You want this node to be neither master nor data node nor ingest node, but  
>    #    to act as a "search load balancer" (fetching data from nodes,   
>    #    aggregating results, etc.)    
>    #   
>    node.master: false   
>    node.data: false   
>    node.ingest: false

3.客户端节点接入 Elasticsearch 集群。在配置文件 elasticsearch.yml 中，通过 `cluster.name` 选项设置集群名字。

>    cluster.name: my_cluster

4.检查 elasticsearch.yml 中的 transport 和 HTTP 主机配置：`network.host` 和 `transport.host` 。transport.host 需要为集群中其它成员网络可达， network.host 是访问 Kibana 的 HTTP 网络连接(默认为 localhost:9200 )。

>    network.host: localhost   
>    http.port: 9200   
>    
>    # by default transport.host refers to network.host   
>    transport.host: [external ip]     
>    transport.tcp.port: 9300 - 9400

5.请确认 Kibana 设置为指向本地客户端节点。在配置文件 kibana.yml 中，`elasticsearch.url` 应设为 localhost:9200 。

>    # The Elasticsearch instance to use for all your queries.    
>    elasticsearch.url: http://localhost:9200

## 八、升级 ##
#### 8.1 标准升级 ####

#### 8.2 重建索引 ####

#### 8.3 全新安装 ####

 
# 重要变更 #

**6.0 版本中的重要更新**  
本节讨论当您的应用需要迁移到 kibana 6.0 时需要注意的一些改变。

- **不能再继续使用不支持的脚本语言**    
**说明**： Kibana 5.x 允许用户使用 Elasticsearch 支持的任何脚本语言创建脚本化的字段。而 Kibana 6.0 将只支持基于 Painless 和 Lucene 表达式的脚本。      
**影响**： 您需要迁移用 groovy、python、javascript 等脚本创建的字段，将其修改为 Painless 或者 Lucene 的表达式。

- **修改了状态（status） API 的响应格式**  
**说明**： 为了使风格具有一致性，并提供易于理解的响应，状态 API 做了如下修改：        
①属性的名称现在已经使用了 snake case 命名法（名称如果是复合词或者包含短语，各个单词之间用下划线分割，不能有空格），部分属性名称已经做了修改。   
②指标现在提供最新的可用数据，而不是随着时间变化的采样。      
**影响**： 您需要更新使用了状态 API 的地方。  

- **Timelion 中需要使用逗号来分割多个查询**   
**说明**： Kibana 5.x 的 timelion 中，用户可以使用空格作为查询的分隔符，例如： .es(400) .es(500) ， 现在只有逗号才能作为有效的查询分隔符。例如： .es(400), .es(500) 。    
**影响**： 您需要使用新的语法重写 timelion 中存储的查询。  

- **需要64位操作系统**   
**说明**： Kibana 6.0.0 及以后版本只支持64位的操作系统。          
**影响**： 您需要在64位的操作系统上安装 Kibana 6.x 。 不过，当从32位操作系统向64位操作系统迁移时，不需要额外的数据迁移步骤。

- **NODE_ENV 环境变量不再影响 Kibana**  
**说明**： 设置 NODE_ENV 环境变量有可能会以意想不到的方式中断 Kibana 进程，不幸的是，它往往是系统中的常见设置，您不会希望它导致 Kibana 出现任何异常。所以，现在 kibana 将会完全忽略 NODE_ENV 环境变量的设置。      
**影响**： 如果您正在开发一个依赖于 NODE_ENV 环境变量的定制化插件，您需要将其更新为依赖另外一个不同名称的的环境变量。

- **使用 _ 而不是 . 作为分隔符的 Kibana 4.x 式的配置命名规则已经不再被支持**   
**说明**： 在 Kibana 4.2 中，我们使用 . 字符作为分隔符替换 _ 字符，重命名了配置文件 kibana.yml 中的所有配置名称，传统方式的配置依然是可以正常工作的。在 5.0 版本中，当遇到传统配置时我们开始记录过期申明。 在 6.0 及其以后版本中，这些使用下划线而不是 . 字符的旧配置名称将不再起作用。    
**影响**： kibana.yml 配置中任何使用下划线字符分割配置名称的地方，都需要更新为当前版本支持的用法。具体用法请参考 *配置 Kibana* 章节

# 基础入门 #

本节内容概述
- 加载示例数据到 Elasticsearch。
- 定义一个索引规范。
- 利用探索页面查询示例数据。
- 为示例数据设定 可视化控件 。
- 在仪表板中组装可视化控件。

视频教程：

- [Kibana 概要简介之饼图](https://www.elastic.co/blog/kibana-4-video-tutorials-part-1)
- [数据发现、条形图、线形图](https://www.elastic.co/blog/kibana-4-video-tutorials-part-2)
- [Tile 地图](https://www.elastic.co/blog/kibana-4-video-tutorials-part-3)
- [嵌入式 Kibana 可视化控件](https://www.elastic.co/blog/kibana-4-video-tutorials-part-4)

## 一、加载示例数据 ##

示例所需数据：

- 威廉·莎士比亚全集，解析成合适的字段。点击下载： [shakespeare.json](https://download.elastic.co/demos/kibana/gettingstarted/shakespeare_6.0.json)
- 一组虚构的账户与随机生成的数据。点击下载： [accounts.zip](https://download.elastic.co/demos/kibana/gettingstarted/accounts.zip).
- 一组随机生成的日志文件。点击下载： [logs.jsonl.gz](https://download.elastic.co/demos/kibana/gettingstarted/logs.jsonl.gz)

压缩文件，使用以下命令解压缩文件：

```
unzip accounts.zip
gunzip logs.jsonl.gz
```
莎士比亚数据集的组织方式如下：

```
{
    "line_id": INT,
    "play_name": "String",
    "speech_number": INT,
    "line_number": "String",
    "speaker": "String",
    "text_entry": "String",
}
```
帐户数据集的组织方式如下：
```
{
    "account_number": INT,
    "balance": INT,
    "firstname": "String",
    "lastname": "String",
    "age": INT,
    "gender": "M or F",
    "address": "String",
    "employer": "String",
    "email": "String",
    "city": "String",
    "state": "String"
}
```
日志数据集的结构有许多不同的字段，以下是其中比较重要的字段：
```
{
    "memory": INT,
    "geo.coordinates": "geo_point"
    "@timestamp": "date"
}
```
在莎士比亚和日志数据集加载之前，我们需要为字段设置映射。映射把索引中的文档按逻辑分组并指定了字段的属性，比如字段的可搜索性或者该字段是否是 *tokenized* ，或分解成单独的单词。

使用以下命令在终端（如 bash ）建立一个莎士比亚数据集的映射：
```
PUT /shakespeare
{
 "mappings": {
  "doc": {
   "properties": {
    "speaker": {"type": "keyword"},
    "play_name": {"type": "keyword"},
    "line_id": {"type": "integer"},
    "speech_number": {"type": "integer"}
   }
  }
 }
}
```
这个映射指定了数据集的以下特点：

- 因为 *speaker* 和 *play_name* 字段是关键字字段，它们不需要分析。字符串即使包含多个词也仍被视为一个整体。
- *line_id* 和 *speech_number* 字段是整数。
日志数据集映射需要利用 geo_point 类型来标记经度/纬度地理位置字段。

使用下面的命令来为日志建立 geo_point 映射：

```
PUT /logstash-2015.05.18
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
```
```
PUT /logstash-2015.05.19
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
```
```
PUT /logstash-2015.05.20
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
``` 
账户数据集不需要任何映射，基于这一点我们准备用 Elasticsearch bulk API 来加载数据集，命令如下：
```
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/bank/account/_bulk?pretty' --data-binary @accounts.json
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/shakespeare/doc/_bulk?pretty' --data-binary @shakespeare_6.0.json
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/_bulk?pretty' --data-binary @logs.jsonl
```

CONSOLE中验证数据加载是否成功：
```
GET /_cat/indices?v
```
![数据加载结果](../../../../images/kibana/sample_data.png)

## 二、定义自己的索引模式 ##

加载到 Elasticsearch 的每组数据都有一个索引模式（Index Pattern）。 在上一节中，为莎士比亚数据集创建了名为 shakespeare 的索引，为 accounts 数据集创建了名为 bank 的索引。一个索引模式是可以匹配多个索引的带可选通配符的字符串。例如一般在通用日志记录中，一个典型的索引名称一般包含类似 YYYY.MM.DD 格式的日期信息。例如一个包含五月数据的索引模式： logstash-2015.05* 。

在本手册中，我们加载的索引只要名称匹配都可以正常工作。打开浏览器，访问 localhost:5601 。单击 **Management** 选项，然后单击 **Index Patterns** 选项。点击 **Add New** 定义一个新的索引模式。共有两个样本数据集，莎士比亚戏剧和金融账户，不包含时间序列数据。当您为这些数据集创建索引模式时，请确保 **Index contains time-based events** 没有被选中。指定 `shakes*` 作为 Shakespeare 数据集的索引模式，然后点击 **Create** 创建索引模式，然后同样的方法再创建一个名为 `ba*` 的索引模式。

Logstash 数据集会包含时间序列数据，所以点击 **Add New **来定义这个数据集的索引，确保 **Index contains time-based events** 被选中，并从 **Time-field name** 下拉列表中选择 `@timestamp` 字段。（根据测试，只有索引名称字段可以检索到日期字段是，创建索引时才会出现 `Index contains time-based events` 选项。）

>    注意
>    定义索引模式时，匹配该模式的索引必须在 Elasticsearch 中存在。并且那些索引必须包含数据。

## 三、探索您的数据 ##

点击导航中的 `Discover` 进入 Kibana 的数据探索发现。
![](../../../../images/kibana/discover_index.png)

在查询框里输入 Elasticsearch 查询语句来检索数据。在 Discover 页面下查看搜索结果并在 Visualize 下生成并保存搜索的可视化效果。

索引模式位于查询栏下方左侧。索引模式决定了提交查询时检索哪些索引。可以从下拉菜单中选择不同的模式对不同索引进行查询。新增索引模式，可以转到 `Management/Kibana/Index Patterns` 界面下点击 `Add New` 。

您可以把您感兴趣的字段名称和值当做搜索的条件，对于数字字端支持比较运算符，如大于（>）、小于（<）或等于（=）。可以使用逻辑运算符 AND，OR 和 NOT 连接搜索条件，这些运算符需要全部大写。

选择 ba* 索引模式并在查询栏中输入以下字符串：

>    account_number:<100 AND balance:>47500   
查询结果返回0到99之间所有余额超过47,500的账户号码。搜索银行样本数据时，它返回5个结果：帐户号码8，32，78，85和97。
![](../../../../images/kibana/discover_query_result.png)

每个匹配的文档默认显示所有字段。可以将鼠标悬停在可用字段上并点击您想要展示字段旁边的 add 按钮来添加需要展示的字段。例如，如果您仅仅添加 account_number ，就只会显示5个简单的账户号码的列表。
![](../../../../images/kibana/discover_query_filter.png)

## 四、可视化数据 ##

点击导航中的 `Visualize` 进入 Kibana 的数据可视化设置。 

Visualize 可以通过多种图表展示数据。例如：我们使用饼图来查看银行账户样本数据中的账户余额。点击屏幕中间的 `Create a visualization` 按钮开始创建图表。
![](../../../../images/kibana/visualize_create.png)

选择 Pie
![](../../../../images/kibana/visualize_create_pie.png)

接下来为已保存的搜索建立可视化图表，或者输入新的搜索条件。使用后者时，首先需要选择一个索引模式来指定检索哪些索引。我们希望搜索账户数据，所以选择 `ba*` 这个索引模式
![](../../../../images/kibana/visualize_select_index.png)

默认搜索匹配所有的文档。初始饼图没有分区。
![](../../../../images/kibana/visualize_pie_init.png)

使用 Elasticsearch *桶聚合* 指定图表中显示哪些信息。桶聚合简单的把符合您搜索条件的文档分成不同类别，又叫做 buckets 。例如：包含每个账户的余额数据。通过使用桶聚合，您可以建立多个账户余额区间并找到每个区间内包含多少账户。

定义每个区间桶：

1.点击 **Split Slices** 桶类别。
2.从 **Aggregation** 列表中选择 **Range** 。
3.从 **Field** 列表中选择 **balance** 字段。
4.点击四次 **Add Range** 把区间总数增加到6个。
5.定义以下区间：

<blockquote>
<table>
<tr>
    <td>0</td><td>999</td>
</tr>
<tr>
    <td>1000</td><td>2999</td>
</tr>
<tr>
    <td>3000</td><td>6999</td>
</tr>
<tr>
    <td>7000</td><td>14999</td>
</tr>
<tr>
    <td>15000</td><td>30999</td>
</tr>
<tr>
    <td>31000</td><td>50000</td>
</tr>
</table>    
</blockquote>

6.点击 **Apply changes** ![](../../../../images/kibana/apply-changes-button.png) 更新图表。
现在您可以看到1000个账户根据余额区间划分的比例情况。
![](../../../../images/kibana/visualize_pie_stats.png) 

让我们看以下数据的另一方面：账户拥有者的年龄。通过添加另一个桶聚合，您可以看到每个余额区间的账户拥有者的年龄：

1.点击桶列表中的 **Add sub-buckets**。  
2.点击桶类型列表中的 **Split Slices**。  
3.在聚合列表中选择 **Terms**。  
4.在字段列表中选择 **age**。  
5.点击 **Apply changes** ![](../../../../images/kibana/apply-changes-button.png) 。

现在您可以看到根据账户持有者的年龄划分的环形结构显示在余额区间外侧
![](../../../../images/kibana/visualize_pie_stats01.png) 

点击 **Save** 然后输入名称 Pie Example 来保存这个图表供以后使用。

下一步，我们来看一下莎士比亚数据集中的数据。让我们找出每部剧中的台词数，然后通过柱状图来显示这些数据：

1.点击 **New** 然后选择 **Vertical bar chart** 。   
2.选择 `shakes*` 索引模式。因为目前并没有定义任何桶，您将会看到唯一的一个柱形，它代表着匹配默认通配请求的所有文档数。
![](../../../../images/kibana/visualize_col_init.png)
3.为了在y轴上显示每部剧里面的台词数，您需要通过<a>*指标聚合*</a>配置y轴。`指标聚合`检索结果，从中提取值做为基础数据并计算出相应的指标。为了得到每部剧中的台词数，选择 `Unique Count` 聚合然后从字段列表中选择 `speaker` 。您也可以给这个轴加上标签，例如 `Speaking Parts` 。    
4.为了在x轴上显示不同的剧目，选择X轴桶种类，然后在聚合列表中选择 `Terms` ，并从字段列表中选择 `play_name` 。选择 `Ascending` 使得剧目名称按照字母顺序排列。您也可以给这个轴加上标签，例如 Play Name 。 
5.点击 **Apply changes** ![](../../../../images/kibana/apply-changes-button.png)  来显示结果

![](../../../../images/kibana/visualize_col_stat.png)

注意每部剧名显示为短语，而不是以单词的形式分开。是因为我们在教程开始的时候做了映射的缘故，把 `play_name` 字段标记为 *not analyzed* 。

鼠标悬停在每个柱形图上可以tips信息的形式显示每部剧中的台词数。为了关闭提示信息并配置其它选项，选择可视化编辑器的 **Options** 选项。
现在，您已经拥有一个莎士比亚戏剧的最小演员表，您也许会想通过显示某部剧里面的最大台词数来了解哪部剧对一个演员要求最高。

1.点击 **Add metrics** 来添加一个Y轴聚合。  
2.选择 **Max** 聚合然后选择 **speech_number** 字段。  
3.选择 **Options** 然后把 **Bar Mode** 改为 **grouped** 。6.x中选择 **Metrics &Axes** 在 Metrics 下 **Mode** 中选择 normal   
4.点击 **Apply changes** ![](../../../../images/kibana/apply-changes-button.png) 。您的图表应该如下所示：

![](../../../../images/kibana/visualize_col_multi.png) 

如您所见，与其他剧目相比 *Love’s Labours Lost* 有着最高的台词数，因此也最考验演员的记忆力。

请注意 Number of speaking parts Y轴从0开始，但是柱形从18才开始有差别。为了让这种差别更明显，可以调整Y轴最小值，打开选项然后选择 **Scale Y-Axis to data bounds** 。（该选项6.3中未发现）

5.保存这个图表并命名为 Bar Example 

下一步，我们使用地图来可视化日志样本数据集中的地理标识信息。

1.点击 **New** 。    
2.选择 **Coordinate map** 。    
3.选择 `logstash-*` 索引模式。    
4.设置我们要查看的事件的时间窗口：    
5.在 Kibana 工具栏中点击时间控件选择。    
6.点击 **Absolute** 。    
7.设置开始时间为 May 18, 2015，结束时间为 May 20, 2015。
![](../../../../images/kibana/visualize_map_date.png) 

8.设置好时间范围后，点击 **Go** 按键并点击右下角向上的小箭头关闭时间控件。

因为目前没有定义任何桶，您将只会看到一幅世界地图：
![](../../../../images/kibana/viz-map-init.png) 

选择 **Geo Coordinates** 作为桶，(6.3.0版本 **Aggregation** 选择Geohash， **Field** 选择 geo.coordinates) 并点击 Apply changes ![](../../../../images/kibana/viz-map-data.png) 来显示日志文件中对应的地理坐标。您的图表应该如下所示：

您可以通过点击和拖动来浏览地图，通过 ![](../../../../images/kibana/images/viz-zoom.png) 进行缩放，或者点击 **Fit Data Bounds** ![](../../../../images/kibana/images/viz-fit-bounds.png) 来显示所有数据区域。通过 **Latitude/Longitude Filter** ![](../../../../images/kibana/images/viz-lat-long-filter.png) 在地图上画框来选择矩形区域。过滤器显示在查询栏下方。鼠标悬停在过滤器上方可以显示切换、固定、反转和删除该过滤器的操作选项。

最后，创建一个 Markdown 来显示其他信息：

1.点击 **New** 。  
2.选择 **Markdown widget** 。  
3.在输入框中输入如下内容：  

<blockquote>
# This is a tutorial dashboard! <br/>          
The Markdown widget uses **markdown** syntax. <br/>   
> Blockquotes in Markdown use the > character.    
</blockquote>

点击 **Apply changes** ![](../../../../images/kibana/apply-changes-button.png) 在预览框中显示该 Markdown 。

![](../../../../images/kibana/viz-md.png)


## 五、使用仪表板汇总数据总结 ##

仪表板用于集中管理或分享可视化控件集合。构建一个仪表板用以包含已保存的可视化控件，步骤如下：

1.在侧边导航栏点击 **Dashboard** 。
2.点击 **Add** 显示已保存的可视化控件列表。
3.单击 Markdown Example 、 Pie Example 、 Bar Example 和 Map Example ，然后通过点击列表底部向上的小箭头关闭可视化控件列表。
将鼠标悬停在一个可视化控件上可以显示允许您编辑、移动、删除和调整它的控制器。

您的样本仪表板最终看起来应该大概像这样：

![](../../../../images/kibana/dashboard.png)

要获取分享链接或获得可嵌入到网页中的 HTML 代码，请保存仪表板并点击工具栏中的 **Share** 。

## 六、总结 ##

开始使用 Kibana 定制您自己的数据了。

- Discover 查看更多关于搜索和过滤数据的信息。
- Visualize 查看所有 Kibana 提供的可视化控件种类。
- Management 查看如何配置 Kibana 和管理已保存的对象。
- Console 查看如何使用交互控制台向 Elasticsearch 提交 REST 请求。

# 数据探索 #

数据探索（Discover）页面提供交互式探索数据操作。访问选定索引模式匹配中每个索引中包含的文档。搜索请求、过滤搜索结果、查看文档数据。您还浏览与搜索查询匹配的文档数，获取字段值的统计信息。如果索引模式中配置了时间字段，还可以在这个页面的顶部看到基于时间分布的文档数量柱状图。
![](../../../../images/kibana/discover-start-annotated-6.3.0.png)

## 一、设置时间过滤器 ##

时间过滤器根据选定时间段展示搜索结果。包含 `index contains time-based events` 和 `time-field` 的索引模式可以加载时间过滤器。时间过滤器默认的时间段为最近15分钟。可以使用顶部工具栏中的 **Time Picker** 来调整时间段和刷新频率。

通过 **Time Picker** 设置时间过滤器：

1.点击 Kibana 工具栏中的 **Time Picker** ![](../../../../images/kibana/time-picker.png)。
2.选择时间段设置快速过滤条件。
![](../../../../images/kibana/visualize_map_date.png) 

3.**Quick** 选择一个给定时间进行设置。

4.**Relative** 基于当前时间来设置相对时间过滤器，选择数字和时间单位（秒、分、时、天、月、年）来指定当前时间多久之前是开始时间。同样的方式指定当前多久之后为结束时间。相对时间既可以是过往也可以是将来。

5.**Absolute** ，使用日历设置 From 和 To 指定开始时间和结束时间。

6.**Recent** 最近使用的日期设置。

7.选择 ![](../../../../images/kibana/up-close.png)  图标收回 **Time Picker** 。

通过直方图来快速设置时间过滤器：

1.直接点击直方图上的某根柱子来放大对应的时间段。    
2.通过拖拽的方式。当光标在图表的背景上变成一个加号时，代表这是可以选取的时间段。    
3.可以点击 **Time Picker** 左边和右边的箭头来选择上一个或下一个时间段。    
4.通过浏览器的返回按钮进行撤销操作。

时间段和刷新周期会在直方图上展示。默认情况下，刷新周期会根据时间段来自动设置。也可以手动设置刷新周期。

## 二、搜索数据 #

在搜索栏输入检索条件，可以在当前索引模式的索引中进行检索，检索条件支持简单的文本、[Lucene 语法](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html)、或基于 JSON 的 [Elasticsearch 查询 DSL](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/query-dsl.html) 。

提交一次搜请求后，直方图、文档列表、字段列表会根据最新搜索结果进行展示。工具栏上会展示命中（hits）的文档数量。<s>文档列表会展示前5条命中的文档。</s>文档列表默认按时间倒序进行排列，最新的文档优先展示。您可以点击时间字段的表头来调整顺序，或通过索引字段来指定列表的顺序。参考 *Sorting the Documents Table* 小节获取更多信息。

在搜索栏输入条件，回车或点击 Search ![](../../../../images/kibana/search-button.png) 向 Elasticsearch 提交搜索请求。

- 输入文本字符串来进行简单文本搜索。例如，查询 Web 服务器日志的时候，输入 `safari` 来搜索所有字段中包含词条 `safari` 的文档。
- 用字段名作为前缀来对指定字段进行搜索。例如，输入 `status:200` 来搜索字段 `status` 中包含词条`200`的文档。
- 中括号指定搜索范围， `[START_VALUE TO END_VALUE]` 。例如，搜索状态为 4xx 的条目，您可以输入 `status:[400 TO 499]` 。
- 使用布尔操作符 `AND`、`OR` 和 `NOT` 组合复杂的检索条件。例如，搜索状态为 4xx 且扩展名为 php 或 html 的条目，您可以输入 `status:[400 TO 499] AND (extension:php OR extension:html)` 。

>    注意
>    这些例子使用 Lucene 语法。您也可以通过 Elasticsearch 查询 DSL 来提交查询请求。请参考 Elasticsearch 手册中的 [query string syntax ](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/query-dsl-query-string-query.html#query-string-syntax)。

**保存搜索**

搜索保存后，在下次使用数据探索的时候可以重新载入并作为可视化的基础。保存搜索的时候既保存了查询条件，也保存了选择的索引模式。

保存当前的搜索:    
1.点击 Kibana 工具栏的 **Save** 。    
2.输入搜索的名称然后点击 **Save** 。    
可以在 **Management/Kibana/Saved Objects** 导入、导出或删除已经保存的搜索。

**载入已经保存的搜索**

载入已经保存的搜索：    
1.在 Kibana 工具栏点击 **Open** 。    
2.选择您要载入的搜索。    
如果载入的搜索使用的索引模式和当前索引模式不同，载入搜索的同时会同时重置当前选择的索引模式。

**更改要搜索的索引**

提交一个检索请求后，会在和当前索引模式匹配的索引中进行查询。当前的模式会展示在工具栏上。如果要使用其他索引模式，请选择另外一个。
参考 *创建索引模式* 小节获取更多有关搜索模式的信息。

**刷新搜索结果**
   
随着越来越多的文档被加入您要搜索的索引中，视图中的搜索结果会相对陈旧。通过设置刷新频率通过周期性的提交检索请求，以获取最新的结果。

开启自动刷新：    
1.点击 Kibana 工具栏中的 **Auto-refesh** 。    
2.点击 **OFF** 并选择右侧刷新频率。   
![](../../../../images/kibana/auto-refresh.png)

自动刷新开启后，刷新频率会和一个 **Pause** 按钮一起展示在 **Time Picker** 旁边。点击 **Pause** 可以暂停自动刷新请求的执行。

>    注意
>    如果自动刷新没有打开，您可以手动点击 **Refresh** 来刷新视图。

## 三、根据字段过滤 ##

添加过滤对查询结果进行过滤，显示包含特定字段值的文档。或创建否定过滤器，排除包含特定字段值的文档。

从 `Fields` 表或 `Documents` 表中选择过滤器使用的字段。除了可以创建积极和消极过滤器外，`Documents` 表还可以使用过滤条件判断某一字段是否存在。使用过的过滤器会在 Query 栏下方显示。消极过滤器用红色显示。

- 从 `Fields` 列表中添加一个过滤器：     
1.点击想要过滤的字段名。这里显示了该领域最常用的五个字段值。

![](../../../../images/kibana/filed-filter.png)    

2.添加积极过滤器，请点击 **Positive Filter** 按钮 ![](../../../../images/kibana/PositiveFilter.png)。这会只显示包含该字段值的文档。     
3.添加消极过滤器，请点击 **Negative Filter** 按钮 ![](../../../../images/kibana/NegativeFilter.png)。这会排除包含该字段值的文档。  

- 从 `Documents` 表中添加一个过滤器：

1.通过点击文档表条目左侧的 Expand 按钮 ![](../../../../images/kibana/ExpandButton.png) 展开 Documents 表中的一个文档。

![](../../../../images/kibana/document-filter.png)

2.添加积极过滤器，请点击 **Positive Filter** 按钮 ![](../../../../images/kibana/PositiveFilter.png)。这会只显示包含该字段值的文档。     
3.添加消极过滤器，请点击 **Negative Filter** 按钮 ![](../../../../images/kibana/NegativeFilter.png)。这会排除包含该字段值的文档。    
4.过滤文档是否包含某一字段，请点击该字段名右侧的 **Exists** 按钮 ![](../../../../images/kibana/ExistsButton.png)。这会只显示包含该字段的文档。

**管理过滤器**

修改一个过滤器，请将鼠标悬停该过滤器，然后点击某个操作按钮。
![](../../../../images/kibana/filter-allbuttons.png)

![](../../../../images/kibana/filter-enable.png) 启动过滤器      
禁用过滤器不会删除过滤器。再次点击会重启过滤器。斜条纹表示过滤器被禁用。    
![](../../../../images/kibana/filter-pin.png) 固定过滤器         
当把上下文切换为 Kibana 时，被固定的过滤器仍然有效。例如，在 **Discover** 中固定一个过滤器，若切换至 **Visualize**，该过滤器仍然存在。请注意，过滤器是基于某个特定的索引字段——如果搜索的索引不包含固定过滤器中的字段，将不会生效。   
![](../../../../images/kibana/filter-toggle.png) 切换筛选器         
在积极过滤器和消极过滤器之间转换。   
![](../../../../images/kibana/filter-delete.png) 移除过滤器    
移除过滤器。   
![](../../../../images/kibana/filter-custom.png) 编辑过滤器    
*编辑过滤器*定义。可用于手动更新过滤查询和为过滤器指定标签。

对所有已应用的过滤器进行一次过滤，点击 **Actions** 并选择过滤指令。
![](../../../../images/kibana/filter-actions.png)

**编辑过滤器**

编辑过滤器对查询结果进行微调。基于多个字段的创建更复杂的过滤器。

![](../../../../images/kibana/filter-custom-json.png)
 
例如，可以使用 [bool query](https://www.elastic.co/guide/en/elasticsearch/reference/6.0//query-dsl-bool-query.html) 为示例日志数据创建一个过滤器，该日志数据显示的是加拿大或中国导致404错误的匹配记录。

```
{
  "bool": {
    "should": [
      {
        "term": {
          "geoip.country_name.raw": "Canada"
        }
      },
      {
        "term": {
          "geoip.country_name.raw": "China"
        }
      }
    ],
    "must": [
      {
        "term": {
          "response": "404"
        }
      }
    ]
  }
}
```

![](../../../../images/kibana/filter-custom-json-result.png)


## 四、查看文档数据 ##

执行查询后，Documents 表中就会列出匹配的500个最新文档。可通过 *Advanced Settings* 中的 `discover:sampleSize` 设置表中显示的文档个数。默认情况下，该表显示的是由所选索引模式和文本 `_source` 配置的时间域的本地化版本。 您可以从 **Fields** 表中选择字段向 Documents 表中添加。也可以通过表中包含的任意索引字段对所列*文档进行排序*。

查看文档的字段数据，请击该文档表项目左侧的 **Expand** ![](../../../../images/kibana/ExpandButton.png) 按钮。

![](../../../../images/kibana/document-filter.png)

查看原始 JSON 文档（整齐打印），请点击 **JSON** 标签。

以单独页面查看文档数据，请点击 **View single document** 链接。可以通过收藏和分享本链接来实现对特定文档的直接访问。

显示或隐藏 Documents 表中的某一个字段所在的列，请点击 ![](../../../../images/kibana/add-column-button.png) **Toggle column in table** 按钮。
折叠文档细节，请点击 **Collapse** 按钮 ![](../../../../images/kibana/CollapseButton.png)。

**整理文档列表**

可以根据任意索引字段值对 Documents 表中的文档进行分类。如果为当前索引模式配置一个时间字段，文档将默认按照反向时间顺序排列。
若要改变排列顺序，可以在分类的字段名点击执行反序排列操作。

**向文档表中添加字段列**

默认情况下, Documents 表显示的是所选索引模式和 `_source` 文档配置的时间字段的本地化版本。 您可以从 **Fields** 列表或文档的字段数据中选择字段向文档表中添加列。

从 **Fields** 列表中添加字段列，将鼠标悬停该字段上，并点击 **add** 按钮。

从文档的字段数据中添加字段列，请展开文档并点击 ![](../../../../images/kibana/add-column-button.png) **Toggle column in table** 按钮。

新增的字段列会取代 Documents 表中的 `_source` 列。新增的字段也会被添加到 **Selected Fields** 列表中。

重新移动字段行列位置，鼠标悬停在列标题上，点击 **Move left** 或 **Move right** 按钮。
![](../../../../images/kibana/doc-position-change.png)

**从文档表中移除字段列**

从文档表中移除一个字段列，请将鼠标置于想要移除的列标题上，然后点击 Remove 按钮 ![](../../../../images/kibana/RemoveFieldButton.png)。

## 五、查看文档上下文 ##

对于某些应用来说，需要查看特定主题包含的多个文档。上下文视图能够帮助设置包含时序性事件的索引模式。想要显示与锚文档相关的上下文，点击文档表条目左侧的 **Expand** 按钮 ![](../../../../images/kibana/ExpandButton.png)，然后点击 **View surrounding documents** 链接。

上下文视图会显示锚文档前后的多个文档。锚文档会用蓝色突出显示。该视图是根据索引模式配置的时间字段而检索出的结果，并使用 Discover 浏览上下文时打开的组列。

![](../../../../images/kibana/discover-context-view.png)

>    默认显示的文档数量可以通过 **Management > Advanced Options** 中的 `context:defaultSize` 设置。

**改变上下文数量**

- 想要增加比锚文档更新文档的显示数量，点击文档列表上方的 **Load 5 more** 按钮，或者在该按钮右侧的输入框中输入所需的数量。
- 想要增加比锚文档更旧文档的显示数量，点击文档列表下方的 **Load 5 more** 按钮，或者在该按钮右侧的输入框中输入所需的数量。

>    注意
>    每次点击按钮默认加载的文档数量能够通过 **Management > Advanced Options** 中的 `context:step` 配置。


## 六、展示字段数据统计 ##

 **Fields** 列表，可以统计文档列表里面有多少文档包含特定的字段，这个字段排名前5的值是什么，包含每个值的文档所占的百分比是多少。
在字段列表里面点击字段名称，可以展示字段数据统计。

![](../../../../images/kibana/filed-top-total.png)


# 可视化 #

可视化 (Visualize) 功能使用 Elasticsearch 数据创建可视化控件。

Kibana 可视化控件基于 Elasticsearch 的查询结果。使用一系列的 Elasticsearch *查询聚合*功能来提取和处理数据，创建图表来呈现数据的分布和趋势。

可以基于在 Discover 页面保存的查询条件或者新建一个查询条件来创建可视化控件。

## 一、创建可视化视图 ##

1.点击左侧导航栏的 **Visualize** 。    
2.点击 **Create new visualization** 按钮或 + 按钮。    
3.选择视图类型。

- 基础图形

<table>
<tr>
    <td>Area，Line， Horizontal Bar，Vertical Bar</td>
    <td>在X/Y图中比较两个不同的序列。</td>
</tr>
<tr>
    <td>Heat maps</td>
    <td>使用矩阵的渐变单元格</td>
</tr>
<tr>
    <td>Pie chart</td>
    <td>显示每个来源的占比。</td>
</tr>
</table>

- 数据
<table>
<tr>
    <td>Data table</td>
    <td>显示一个组合聚合的原始数据。</td>
</tr>
<tr>
    <td>Gauge</td>
    <td>仪表盘的形式显示数字</td>
</tr>
<tr>
    <td>Goal</td>
    <td></td>
</tr>
<tr>
    <td>Metric</td>
    <td>显示单个数字。</td>
</tr>
</table>

- 地图
<table>
<tr>
    <td>Coordinate Map</td>
    <td>将聚合结果关联到地理位置。</td>
</tr>
<tr>
    <td>Region Map</td>
    <td></td>
</tr>
</table>

- 时间序列
<table>
<tr>
    <td>Timelion</td>
    <td>计算和合并来自多个时间序列数据集。</td>
</tr>
<tr>
    <td>Visual Builder</td>
    <td>使用管道聚合显示时间序列数据。</td>
</tr>
</table>

- 其他
<table>
<tr>
    <td>Controls</td>
    <td>控制面板。</td>
</tr>
<tr>
    <td>Markdown</td>
    <td>显示自由格式信息或说明。</td>
</tr>
<tr>
    <td>Tag cloud</td>
    <td>显示标签云，每个标签的字体大小表示其重要性。</td>
</tr>
<tr>
    <td>Vega</td>
    <td>使用Vega和VegaLite创建自定义可视化组件。</td>
</tr>
</table>

4.指定一个查询，为视图获取数据。    

- 输入数据查询条件，为需要可视化的数据的索引库选择索引模式。这将打开一个可视化视图编辑器，并关联从索引库里包含的文档使用通配符查询数据。
- 想要从一个已有的搜索来构建一个可视化视图，只需点击想使用的已有查询名称即可。这将打开一个视图编辑器并加载所选查询条件匹配的数据。

>    注意  当从一个已有的搜索来构建可视化视图时，随后对已有查询的任何修改都会自动反馈在视图中。想要禁止自动更新，您需要断开视图和已保存的搜索之间的连接。

5.在视图编辑器中设置Y轴指标聚合    

- **指标聚合(Metrics Aggregations)**
   - count
   - average
   - sum
   - min
   - max
   - standard deviation 标准方差
   - unique count
   - median (50th percentile) 中位数
   - percentiles
   - percentile ranks 百分等级
   - top hit
   - geo centroid

- **父类管道聚合(Parent Pipeline Aggregations)**
   - derivative
   - cumulative sum
   - moving average
   - serial diff

- **兄弟管道聚合(Sibling Pipeline Aggregations)**
   - average bucket
   - sum bucket
   - min bucket
   - max bucket

6.为视图X轴选择一个桶聚合：
   - date histogram
   - range
   - terms
   - filters
   - significant terms

如果正在索引 Apache 服务器日志，就可以构建一个柱状图，通过指定 geo.src(geo.src.keyword) 字段上的一个 term 聚合，来展示地理位置的请求分布：
![](../../../../images/kibana/bar-term-agg.png)

Y轴表示每个国家的请求数据，而X轴则表示国家。

饼图、线形或区域图的都使用*度量*指标作为Y轴，使用*桶*作为X轴。桶类似于SQL中的 `GROUP BY` 语句。Pie 图中使用分片大小作为指标，分片数量作为桶。

还可以进一步根据指定的子聚合来划分数据。第一个聚合决定任何子序列聚合的数据集。子聚合是有顺序的，可以通过拖拽聚合来改变。

比如，可以在 `geo.dest(geo.dest.keyword)` 字段增加一个 term 子聚合到原始国家条形图，来查看这些请求对应的位置。
![](../../../../images/kibana/bar-term-agg-sub.png)

## 二、线形图、区域图和条形图 ##

线形图，区域图和柱状图使用 X/Y 轴上描绘数据。

首先，您需要选择定义值轴的*指标* 。

##### **1. 指标** #####   
###### **1.1 指标聚合** ######    

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Standard Deviation</b></font>
*扩展统计* 聚合返回数字字段中数据的标准偏差。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Percentiles</b></font>
*百分数* 聚合将数字字段中的值分成您指定的百分数区间。从下拉列表中选择一个字段，然后在 Percentiles 输入域中指定一个或多个范围。点击 X 删除百分数字段。点击 + Add 添加百分数字段。

<font color="#2b4590"><b>Percentile Rank</b></font>
*百分位等级* 聚合返回指定的数值字段中的值的百分位等级。从下拉菜单中选择一个数字字段，然后在 Values 输入域中指定一个或多个百分比等级值。点击 **X** 删除值字段。点击 **+ Add** 添加值字段。

###### **1.2 父级管道聚合** ######    

对于每个父管道聚合，您必须定义用于计算聚合的指标。这可能是您现有的指标之一或新的指标。您也可以嵌套这些聚合（例如产生3阶导数）。

<font color="#2b4590"><b>Derivative</b></font>
*导数* 聚合计算特定指标的导数。

<font color="#2b4590"><b>Cumulative Sum</b></font>
*累计总和* 聚合计算父直方图中指定指标的累计总和。

<font color="#2b4590"><b>Moving Average</b></font>
*移动平均值* 聚合将动态移动数据窗口，生成该窗口数据的平均值。

<font color="#2b4590"><b>Serial Diff</b></font>
*串行差分* 是一种时间序列中的值在不同时间滞后或周期内从自身减去的技术。

###### **1.3 兄弟管道聚合** ######    

就像使用父级管道聚合一样，您需要提供一个用于计算同级聚合的指标。除此之外，还需要提供一个桶聚合，它将定义同级聚合将在其中运行的桶。

<font color="#2b4590"><b>Average Bucket</b></font>
*桶平均值* 计算同级聚合中指定指标的（中数）平均值

<font color="#2b4590"><b>Sum Bucket</b></font>
*桶总和* 计算同级聚合中指定指标值的总和

<font color="#2b4590"><b>Min Bucket</b></font>
*桶最小值* 计算同级聚合中指定指标的最小值

<font color="#2b4590"><b>Max Bucket</b></font>
*桶最大值* 计算同级聚合中指定指标的最大值

您可以通过单击 **+ Add Metrics** 按钮来添加聚合。
在 Custom Label 输入域中输入字符串以更改显示标签。

桶 聚合确定从数据集中检索哪些信息。

在选择桶聚合之前，请指定是在单个图表内拆分切片还是拆分为多个图表。多个图表拆分必须在任何其他聚合之前运行。在拆分图表时，可以通过单击 **Rows &#124; Columns** 选择器来更改拆分是显示在行中还是列中。

这个图表的 X 轴是 桶 轴。您可以为 X 轴定义桶，用于图表上的分割区域，也可以用于分割图表。
这个图表的 X 轴支持下面的聚合。单击每个聚合的链接名称以访问该聚合的 Elasticsearch 主文档。

<font color="#2b4590"><b>Date Histogram</b></font>
*日期直方图* 由数值字段汇总并按日期组织的。支持秒、分钟、小时、天、周、月或年为单位的时间间隔。您还可以通过选择 **Custom** 自定义事件间隔（在文本域中输入时间间隔和时间单位）。自定义时间间隔单位可以为 s 为秒， m 为分钟， h 为小时， d 为天， w 为周， y 为年。不同单位有不同级别的时间精度，最小时间精度为一秒。

<font color="#2b4590"><b>Histogram</b></font>
*标准直方图* 字段需要指定一个整数间隔。选择 **Show empty buckets** 复选框可以在直方图统计中包含空白区间。

<font color="#2b4590"><b>Range</b></font>
*区间聚合* 为数字字段设置数值的区间范围 **Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Date Range</b></font>
*日期区间* 统计指定的日期区间内的数据。您可以使用 *日期数学* 表达式来设置日期的区间。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>IPv4 Range</b></font>
*IPv4 区间* 根据 IPv4 地址的区间聚合数据。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Terms</b></font>
*词条* 聚合指定字段的 top 或 last 的 n 个元素，按数量或自定义指标进行排序。

<font color="#2b4590"><b>Filters</b></font>
*过滤器* 过滤器可设置为查询字符串或采用 JSON 格式，就像在 Discover 搜索栏中一样。**Add Filter** 添加过滤器。![](../../../../images/kibana/labelbutton.png) 按钮打开标签字段，并输入标签名。

<font color="#2b4590"><b>Significant Terms</b></font>
显示实验性的 *重要词项* 聚合的结果。

一旦设置了 X 轴聚合类型，就可以通过添加子聚合来定制可视化图表。**+ Add Sub Aggregation** 添加子聚合，选择 **Split Area** 或 **Split Chart** ，选择一个子聚合类型。

在图表轴上定义多个聚合时，可以使用聚合类型右侧的上或下箭头按钮来变更聚合的优先级。在 **Custom Label** 设置显示标签。
点击每个标签旁边的色点从 **颜色选择器** 自定义视图的颜色。
![](../../../../images/kibana/color-picker.png)


在 **Custom Label** 输入框中修改标签。
点击 **Advanced** 展开更多更多自定义选项：

###### **1.4 Advanced选项** ######  

- <font color="#2b4590"><b>Exclude Pattern</b></font>
指定一个模式以从结果中排除。

- <font color="#2b4590"><b>Include Pattern</b></font>
指定一个模式以包含在结果中。

- <font color="#2b4590"><b>JSON Input</b></font>
在其中添加特定的 JSON 格式的自定义聚合语句，如下例所示：
>    { "script" : "doc['grade'].value * 1.2" }

>    注意
>    在 Elasticsearch 版本1.4.3及更高版本中，此功能要求您启用 [动态 Groovy 脚本](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting.html)。

这些选项的可用性取决于您选择的聚合。

##### **2.指标 & 轴** #####

选择 **Metrics & Axes** 选项卡可以更改图表上每个指标的显示方式。数据系列样式在 *指标* 部分中进行设置，而轴样式在 X 和 Y 轴部分进行设置。

###### **2.1 指标** ######  

修改数据面板中的每个指标在图表上的可视化方式。

- <font color="#2b4590"><b>Chart type</b></font>
在 Area、Line 和 Bar 类型之间进行选择。

- <font color="#2b4590"><b>Mode</b></font>
堆叠样式，normal、stacked。

- <font color="#2b4590"><b>Value Axis</b></font>
选择要绘制此数据的轴（属性在 Y 轴下配置）。

- <font color="#2b4590"><b>Line mode</b></font>
线条或柱条的轮廓是 smooth（平滑）、smooth（笔直）、或 stepped（阶梯）的。

###### **2.2 Y 轴** ######  

调整图表的所有 Y 轴。

- <font color="#2b4590"><b>Position</b></font>
Y 轴的位置（垂直图表为 left 或 right，水平图表为 top 或 bottom）。

- <font color="#2b4590"><b>Scale Type</b></font>
数值缩放类型（linear、log 或 square root）。

- <font color="#2b4590"><b>高级选项</b></font>

    - <font color="#2b4590"><b>Labels</b></font>
        - <font color="#2b4590"><b>Show Labels</b></font>
        允许您隐藏轴标签。

        - <font color="#2b4590"><b>Filter Labels</b></font>
        如果启用了标签过滤，则在没有足够空间显示它们的情况下，会隐藏一些标签。

        - <font color="#2b4590"><b>Rotate</b></font>
        您可以以度数为单位输入您想要标签旋转的角度。

        - <font color="#2b4590"><b>Truncate</b></font>
        您可以输入标签被截断的像素大小。

    - <font color="#2b4590"><b>Custom Extents</b></font>
    
        - [ ] <font color="#2b4590"><b>Scale to Data Bounds</b></font>
        默认的Y轴界限为零和数据中返回的最大值。选中此框可更改上限和下限以匹配数据中返回的值。
    
        - [ ] <font color="#2b4590"><b>Set Axis Extents</b></font>
       您可以为每个轴定义自定义的最小值和最大值。

###### **2.3 X 轴** ######  

图表默认只加载一个 X 轴，不过可以根据需要添加多个 X 轴。点击 + 号创建一个新的 X 轴。

- <font color="#2b4590"><b>Show</b></font>
显示隐藏 X 轴

- <font color="#2b4590"><b>Position</b></font>
X 轴的位置 (水平图表为 **left** 或 **right**，垂直图表为 **top** 或 **bottom**)。

- <font color="#2b4590"><b>高级选项</b></font>
    - <font color="#2b4590"><b>Labels</b></font>
        - <font color="#2b4590"><b>Show Labels</b></font>
        允许您隐藏轴标签。

        - <font color="#2b4590"><b>Filter Labels</b></font>
        如果启用了标签过滤，则在没有足够空间显示它们的情况下，会隐藏一些标签。

        - <font color="#2b4590"><b>Rotate</b></font>
        您可以以度数为单位输入您想要标签旋转的角度。

        - <font color="#2b4590"><b>Truncate</b></font>
        您可以输入标签被截断的像素大小。。

###### **2.4 面板设置（Panel Settings）** ######  

这些选项适用于整个图表，而不仅仅是单个数据系列。

**通用选项**
- <font color="#2b4590"><b>Legend Position</b></font>
将您的图例移动到 left、right、top 或 bottom。

- <font color="#2b4590"><b>Show Tooltip</b></font>
启用或禁止显示鼠标悬停在图表对象上时的工具提示。

- <font color="#2b4590"><b>Order Buckets by Sum</b></font>
根据 sum 对桶数据进行排序

- <font color="#2b4590"><b>Current Time Marker</b></font>
显示一条线表示当前时间。

**网格选项**

您可以在图表上启用网格。 默认情况下，网格仅显示在类别轴上。

- <font color="#2b4590"><b>X-axis</b></font>
您可以禁止显示类别轴上的网格线。

- <font color="#2b4590"><b>Y-axis</b></font>
您可以选择要显示网格线的数值轴（如果有）。

## 三、数据表 ##

##### **1. 指标** #####   
###### **1.1 指标聚合** ######    

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Standard Deviation</b></font>
*扩展统计* 聚合返回数字字段中数据的标准偏差。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Percentiles</b></font>
*百分数* 聚合将数字字段中的值分成您指定的百分数区间。从下拉列表中选择一个字段，然后在 Percentiles 输入域中指定一个或多个范围。点击 X 删除百分数字段。点击 + Add 添加百分数字段。

<font color="#2b4590"><b>Percentile Rank</b></font>
*百分位等级* 聚合返回指定的数值字段中的值的百分位等级。从下拉菜单中选择一个数字字段，然后在 Values 输入域中指定一个或多个百分比等级值。点击 **X** 删除值字段。点击 **+ Add** 添加值字段。

###### **1.2 父级管道聚合** ######    

对于每个父管道聚合，您必须定义用于计算聚合的指标。这可能是您现有的指标之一或新的指标。您也可以嵌套这些聚合（例如产生3阶导数）。

<font color="#2b4590"><b>Derivative</b></font>
*导数* 聚合计算特定指标的导数。

<font color="#2b4590"><b>Cumulative Sum</b></font>
*累计总和* 聚合计算父直方图中指定指标的累计总和。

<font color="#2b4590"><b>Moving Average</b></font>
*移动平均值* 聚合将动态移动数据窗口，生成该窗口数据的平均值。

<font color="#2b4590"><b>Serial Diff</b></font>
*串行差分* 是一种时间序列中的值在不同时间滞后或周期内从自身减去的技术。

###### **1.3 兄弟管道聚合** ######    

就像使用父级管道聚合一样，您需要提供一个用于计算同级聚合的指标。除此之外，还需要提供一个桶聚合，它将定义同级聚合将在其中运行的桶。

<font color="#2b4590"><b>Average Bucket</b></font>
*桶平均值* 计算同级聚合中指定指标的（中数）平均值

<font color="#2b4590"><b>Sum Bucket</b></font>
*桶总和* 计算同级聚合中指定指标值的总和

<font color="#2b4590"><b>Min Bucket</b></font>
*桶最小值* 计算同级聚合中指定指标的最小值

<font color="#2b4590"><b>Max Bucket</b></font>
*桶最大值* 计算同级聚合中指定指标的最大值

您可以通过单击 **+ Add Metrics** 按钮来添加聚合。
在 Custom Label 输入域中输入字符串以更改显示标签。
数据表的行叫做 *桶* 。可以通过定义桶把表格划分为多行或者拆分表格到另外的表中。

每个桶类型支持以下聚合：

<font color="#2b4590"><b>Date Histogram</b></font>
*日期直方图* 由数值字段汇总并按日期组织的。支持秒、分钟、小时、天、周、月或年为单位的时间间隔。您还可以通过选择 **Custom** 自定义事件间隔（在文本域中输入时间间隔和时间单位）。自定义时间间隔单位可以为 s 为秒， m 为分钟， h 为小时， d 为天， w 为周， y 为年。不同单位有不同级别的时间精度，最小时间精度为一秒。

<font color="#2b4590"><b>Histogram</b></font>
*标准直方图* 字段需要指定一个整数间隔。选择 **Show empty buckets** 复选框可以在直方图统计中包含空白区间。

<font color="#2b4590"><b>Range</b></font>
*区间聚合* 为数字字段设置数值的区间范围 **Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Date Range</b></font>
*日期区间* 统计指定的日期区间内的数据。您可以使用 *日期数学* 表达式来设置日期的区间。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>IPv4 Range</b></font>
*IPv4 区间* 根据 IPv4 地址的区间聚合数据。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Terms</b></font>
*词条* 聚合指定字段的 top 或 last 的 n 个元素，按数量或自定义指标进行排序。

<font color="#2b4590"><b>Filters</b></font>
*过滤器* 过滤器可设置为查询字符串或采用 JSON 格式，就像在 Discover 搜索栏中一样。**Add Filter** 添加过滤器。![](../../../../images/kibana/labelbutton.png) 按钮打开标签字段，并输入标签名。

<font color="#2b4590"><b>Significant Terms</b></font>
显示实验性的 *重要词项* 聚合的结果。**Size** 参数的值定义该聚合返回的实体数量。

<font color="#2b4590"><b>Geohash</b></font>
*geohash 聚合 *根据 geohash 坐标来显示点。

一旦指定了一个桶类型的聚合，就可以定义子桶来优化视图。点击 **+ Add sub-buckets** 新增一个子桶，然后选择 **Split Rows** 或 **Split Table**，再从类型列表中选择一种聚合。

可以使用向上或向下键翻到合适的聚合类型，以更改聚合优先级。在 Custom Label 字段中输入一个字符串来修改显示标签。可以点击 Advanced 链接显示指标或桶聚合的更多自定义选项

###### **1.4 Advanced选项** ######  

- <font color="#2b4590"><b>Exclude Pattern</b></font>
指定一个模式以从结果中排除。

- <font color="#2b4590"><b>Include Pattern</b></font>
指定一个模式以包含在结果中。

- <font color="#2b4590"><b>JSON Input</b></font>
在其中添加特定的 JSON 格式的自定义聚合语句，如下例所示：
>    { "script" : "doc['grade'].value * 1.2" }

>    注意
>    在 Elasticsearch 版本1.4.3及更高版本中，此功能要求您启用 [动态 Groovy 脚本](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting.html)。

这些选项的可用性取决于您选择的聚合。

###### **1.5 Options标签** ###### 

- <font color="#2b4590"><b>Per Page</b></font>
该字段控制表格的分页，默认每页10行。

复选框用于打开或关闭下列行为：

- <font color="#2b4590"><b>Show metrics for every bucket/level</b></font>
勾选该选项，将为每个 bucket 聚合显示中间结果。

- <font color="#2b4590"><b>Show partial rows</b></font>
勾选该选项，即使没有结果也会显示一行。

- <font color="#2b4590"><b>Calculate metrics for every bucket/level</b></font>
勾选该选项，计算每个 bucket 聚合显示中间结果

- <font color="#2b4590"><b>Show total</b></font>
开启禁用统计函数

- <font color="#2b4590"><b>Total function</b></font>
show total选中时，可选择统计函数sum、svg、min、max、count

>    注意
>    支持这些行为可能对性能会有较大影响。

## 四、Markdown控件 ##

Markdown 支持 Github 风格的 Markdown 文本。Kibana 会渲染输入的文本，并把结果展示在仪表板上。点击 Help 链接可以跳转到 Github 风格 Markdown 的[帮助页面](https://help.github.com/articles/github-flavored-markdown/)，点击 **Apply** 在预览窗格中显示渲染文本，或点击 **Discard** 回退到之前的版本。

## 五、指标（Metric） ##

##### **1. 指标** #####   
###### **1.1 指标聚合** ######    

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Standard Deviation</b></font>
*扩展统计* 聚合返回数字字段中数据的标准偏差。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Percentiles</b></font>
*百分数* 聚合将数字字段中的值分成您指定的百分数区间。从下拉列表中选择一个字段，然后在 Percentiles 输入域中指定一个或多个范围。点击 X 删除百分数字段。点击 + Add 添加百分数字段。

<font color="#2b4590"><b>Percentile Rank</b></font>
*百分位等级* 聚合返回指定的数值字段中的值的百分位等级。从下拉菜单中选择一个数字字段，然后在 Values 输入域中指定一个或多个百分比等级值。点击 **X** 删除值字段。点击 **+ Add** 添加值字段。

###### **1.2 父级管道聚合** ######    

对于每个父管道聚合，您必须定义用于计算聚合的指标。这可能是您现有的指标之一或新的指标。您也可以嵌套这些聚合（例如产生3阶导数）。

<font color="#2b4590"><b>Derivative</b></font>
*导数* 聚合计算特定指标的导数。

<font color="#2b4590"><b>Cumulative Sum</b></font>
*累计总和* 聚合计算父直方图中指定指标的累计总和。

<font color="#2b4590"><b>Moving Average</b></font>
*移动平均值* 聚合将动态移动数据窗口，生成该窗口数据的平均值。

<font color="#2b4590"><b>Serial Diff</b></font>
*串行差分* 是一种时间序列中的值在不同时间滞后或周期内从自身减去的技术。

###### **1.3 兄弟管道聚合** ######    

就像使用父级管道聚合一样，您需要提供一个用于计算同级聚合的指标。除此之外，还需要提供一个桶聚合，它将定义同级聚合将在其中运行的桶。

<font color="#2b4590"><b>Average Bucket</b></font>
*桶平均值* 计算同级聚合中指定指标的（中数）平均值

<font color="#2b4590"><b>Sum Bucket</b></font>
*桶总和* 计算同级聚合中指定指标值的总和

<font color="#2b4590"><b>Min Bucket</b></font>
*桶最小值* 计算同级聚合中指定指标的最小值

<font color="#2b4590"><b>Max Bucket</b></font>
*桶最大值* 计算同级聚合中指定指标的最大值

您可以通过单击 **+ Add Metrics** 按钮来添加聚合。
在 Custom Label 输入域中输入字符串以更改显示标签。

## 六、饼图 ##

饼图的切片大小由 *metrics* 聚合决定，下列聚合可用于饼图

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

在 Custom Label 字段中输入一个字符串来修改显示标签。
*桶* 聚合用于决定从数据集抽取何种信息。
在选择一个桶聚合之前，需要知道是否为单个图或组合图的X轴或Y轴定义桶。一个组合图必须在所有其他聚合之前执行。当划分一个图时，可以通过点击 Rows &#124; Columns 选择器，来改变划分是显示为一行还是一列。

可以为饼图指定下列任意桶聚合

<font color="#2b4590"><b>Date Histogram</b></font>
*日期直方图* 由数值字段汇总并按日期组织的。支持秒、分钟、小时、天、周、月或年为单位的时间间隔。您还可以通过选择 **Custom** 自定义事件间隔（在文本域中输入时间间隔和时间单位）。自定义时间间隔单位可以为 s 为秒， m 为分钟， h 为小时， d 为天， w 为周， y 为年。不同单位有不同级别的时间精度，最小时间精度为一秒。

<font color="#2b4590"><b>Histogram</b></font>
*标准直方图* 字段需要指定一个整数间隔。选择 **Show empty buckets** 复选框可以在直方图统计中包含空白区间。

<font color="#2b4590"><b>Range</b></font>
*区间聚合* 为数字字段设置数值的区间范围 **Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Date Range</b></font>
*日期区间* 统计指定的日期区间内的数据。您可以使用 *日期数学* 表达式来设置日期的区间。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>IPv4 Range</b></font>
*IPv4 区间* 根据 IPv4 地址的区间聚合数据。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Terms</b></font>
*词条* 聚合指定字段的 top 或 last 的 n 个元素，按数量或自定义指标进行排序。

<font color="#2b4590"><b>Filters</b></font>
*过滤器* 过滤器可设置为查询字符串或采用 JSON 格式，就像在 Discover 搜索栏中一样。**Add Filter** 添加过滤器。![](../../../../images/kibana/labelbutton.png) 按钮打开标签字段，并输入标签名。

<font color="#2b4590"><b>Significant Terms</b></font>
显示实验性的 *重要词项* 聚合的结果。

一旦设置了 X 轴聚合类型，就可以通过添加子聚合来定制可视化图表。**+ Add Sub Aggregation** 添加子聚合，选择 **Split Area** 或 **Split Chart** ，选择一个子聚合类型。

在图表轴上定义多个聚合时，可以使用聚合类型右侧的上或下箭头按钮来变更聚合的优先级。在 **Custom Label** 设置显示标签。
点击每个标签旁边的色点从 **颜色选择器** 自定义视图的颜色。
![](../../../../images/kibana/color-picker.png)

在 **Custom Label** 输入框中修改标签。
点击 **Advanced** 展开更多更多自定义选项：

- <font color="#2b4590"><b>Exclude Pattern</b></font>
指定一个模式以从结果中排除。

- <font color="#2b4590"><b>Include Pattern</b></font>
指定一个模式以包含在结果中。

- <font color="#2b4590"><b>JSON Input</b></font>
在其中添加特定的 JSON 格式的自定义聚合语句，如下例所示：
>    { "script" : "doc['grade'].value * 1.2" }

>    注意
>    在 Elasticsearch 版本1.4.3及更高版本中，此功能要求您启用 [动态 Groovy 脚本](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting.html)。

这些选项的可用性取决于您选择的聚合。

**Options标签**
- **Pie Settings**

    - <font color="#2b4590"><b>Donut</b></font>
    在环状图和饼状图显示样式之间切换。

    - <font color="#2b4590"><b>Legend Position</b></font>
    图例位置设置。

    - <font color="#2b4590"><b>Show Tooltip</b></font>
    勾选此项开启显示提示语。

- **Labels Settings**

    - <font color="#2b4590"><b>Show Labels</b></font>
    显示图标说明

    - <font color="#2b4590"><b>Show Top Level Only</b></font>
    
  
    - <font color="#2b4590"><b>Show Values</b></font>
    显示具体统计数值

    - <font color="#2b4590"><b>Truncate</b></font>
    数据超出后进行截断显示    

在修改选项后，点击 **Apply changes** 按钮更新视图，或者点击 **Discard changes** 按钮保持视图为当前状态。


## 七、Tile地图 ##

##### **1. 指标** #####   
 
坐标地图的默认指标聚合是 **Count** 聚合。可以选择以下任何一项聚合作为指标聚合

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

##### **2. 桶** ##### 

Tile 地图使用 `geohash` 聚合。下拉菜单中选择字段，通常是坐标（coordinates）字段。

- *Change precision on map zoom*（更改地图缩放的精度）选项框默认是选中的。取消选中该选项框以禁用此行为。Precision（精度）滑块决定了地图上显示的结果的粒度。调整指定的区域的精度级别的详细信息，请参阅[geohash grid](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/search-aggregations-bucket-geohashgrid-aggregation.html#_cell_dimensions_at_the_equator) 聚合的文档。

>    注意
>    更高的精度会增加显示 Kibana 的浏览器以及底层 Elasticsearch 集群的内存使用量。

- *place markers off grid* 不将标记放置在网格上 (use geocentroid)选项框默认是选中的。选中此选框时，标记将放置在该桶中所有文档的中心。未选中时，标记将放置在 geohash 网格单元的中心。保持此项选中通常会产生更准确的可视化。

您可以点击 Advanced 链接为您的度量或桶聚合显示更多自定义选项：

- <font color="#2b4590"><b>Exclude Pattern</b></font>
指定一个模式以从结果中排除。

- <font color="#2b4590"><b>Include Pattern</b></font>
指定一个模式以包含在结果中。

- <font color="#2b4590"><b>JSON Input</b></font>
在其中添加特定的 JSON 格式的自定义聚合语句，如下例所示：
>    { "script" : "doc['grade'].value * 1.2" }

>    注意
>    在 Elasticsearch 版本1.4.3及更高版本中，此功能要求您启用 [动态 Groovy 脚本](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting.html)。

这些选项的可用性取决于您选择的聚合


##### **2. 选项** ##### 

**Map type**

从下拉列表中选择以下选项之一。
- <font color="#2b4590"><b>Scaled Circle Markers（缩放的圆圈标记）</b></font>
根据度量聚合的值缩放标记的大小。

- <font color="#2b4590"><b>Shaded Circle Markers（带阴影的圆圈标记）</b></font>
根据度量聚合的值显示具有不同阴影的标记。

- <font color="#2b4590"><b>Shaded Geohash Grid（带阴影的 Geohash 网格）</b></font>
显示 geohash 网格的矩形单元格，而不是圆形标记，并根据度量聚合的值显示不同的阴影。

- <font color="#2b4590"><b>Heatmap（热点图）</b></font>
热点图将模糊应用于圆形标记，并根据重叠量应用阴影。 热点图有以下选择：

    - Radius（半径）： 设置单个热点图像点的大小。
    - Blur（模糊）： 设置热点图像点的模糊量。
    - Maximum zoom（最大缩放）： Kibana中的Tilemaps支持18个缩放级别。 此滑块定义当热点图像点以全强度出现时的最大缩放级别。
    - Minimum opacity（最小不透明度）： 设置像点的不透明度的最小值。
    - Show Tooltip（显示工具提示）： 选中此选框可在光标位于点上时提供该点的值提示。

- <font color="#2b4590"><b>Desaturate map tiles（地图图块去饱和）</b></font>
对地图颜色进行去饱和处理，以使标记更加清晰。

- <font color="#2b4590"><b>WMS compliant map server（符合WMS的地图服务器）</b></font>
选中此选框可启用符合 Web 地图服务（WMS）标准的第三方地图服务。 指定以下元素：

    - WMS URL： WMS 地图服务的 URL。
    - WMS layers（WMS 图层）： 在此可视化中使用的图层的逗号分隔列表。每个地图服务器都提供自己的图层列表。
    - WMS version（WMS 版本）： 此地图服务使用的 WMS 版本。
    - WMS format（WMS 格式）： 此地图服务使用的图像格式。两种最常见的格式是 image/png 和 image/jpeg 。
    - WMS attribution（WMS 来源）： 用于标识地图来源的可选用户定义字符串。地图在右下角显示来源字符串。
    - WMS styles（WMS 样式）： 此可视化中使用的样式的逗号分隔列表。每个地图服务器都提供自己的样式选项。
更改选项后，单击 Apply changes 按钮更新可视化效果，或单击灰色的 Discard changes 按钮以将可视化保持在当前状态。

##### **2. 浏览地图** ##### 

当您的 Tile 地图可视化准备就绪了，您可以通过几种方式浏览地图：

- 点击并按住地图上的任意位置并移动光标以移动地图中心。 按住 Shift 键并在地图上拖出一个边界框以放大选区。
- **Zoom In/Out（缩小/放大）** ![](../../../../images/kibana/viz-zoom.png) 按钮手动更改缩放级别。
- **Fit Data Bounds（适应数据边界）** ![](../../../../images/kibana/viz-fit-bounds.png) 按钮自动将地图边界裁剪为至少有一个结果的 geohash 桶。
- **Latitude/Longitude Filter（经度/纬度过滤器）** ![](../../../../images/kibana/viz-lat-long-filter.png) 按钮，然后在地图上拖出一个边界框，为框住的坐标创建过滤器。

## 八、时间序列可视化生成器 ##

时间序列可视化生成器是一个时间序列数据可视化工具，可以使用 Elasticsearch 聚合框架的全部功能。时间序列可视化生成器允许您组合无限数量的聚合和管道聚合，以显示复杂的数据。

![](../../../../images/kibana/tsvb-screenshot.png)

###### 8.1 特色可视化 ######

时间序列支持5种不同的可视化展示。不同可视化类型展示，可以通过界面上部的选项卡进行切换。

**时间序列**

直方图可，支持包含多个 y 轴的区域图、线形图、条形图和步骤图。您可以完全自定义颜色、点、线条粗细和填充不透明度。该可视化还支持时间偏移来比较两个时间段。该可视化还支持注解（annotations），该注解可以基于查询从单独的索引加载。
![](../../../../images/kibana/tsvb-timeseries.png)

**指标**

用于显示系列中最新数值的可视化。该可视化支持2个指标：主要指标和次要指标。标签和背景可以根据一组规则完全自定义。
![](../../../../images/kibana/tsvb-metric.png)

**Top N**

这是一个水平柱状图，其中 y 轴是基于一个系列的指标，x 轴是这些系列中的最新值，按降序排列。条形的颜色可以根据一组规则完全自定义。
![](../../../../images/kibana/tsvb-top-n.png)

**测量仪（Gauge）**

这是基于系列中最新值的单值计量可视化。测量仪的面貌可以是半圆表或全圆表。您可以自定义内线和外线的厚度以达到所需的设计美学效果。测量仪和文本的颜色可根据一组规则完全自定义。
![](../../../../images/kibana/tsvb-gauge.png)

**Markdown**

此可视化允许您输入 Markdown 文本并嵌入 Mustache 模板语法，以基于一组系列数据自定义 Markdown。该可视化还支持 HTML 标记以及自定义样式表的功能。

###### 8.2 界面概述 ######

可视化的界面由 **Data** 标签页和 **Pannel Options** 组成。时间序列和 Markdown 可视化稍有不同，时间序列具有用于 Annotations 的标签页，Markdown 具有用于编辑器的标签页

**数据标签页**

数据标签页用于配置每个可视化的序列。此选项卡允许您根据可视化支持的内容添加多个序列，并将多个聚合组合在一起以创建单个指标。以下是数据标签页 UI 重要组件的细分。

**序列标签和颜色**

每个序列都支持一个标签，该标签将用于图例和标题，具体取决于所选的可视化类型。对于按词项分组的序列，可以指定 `{{key}}` 的 mustache 变量以替换该词项。对于大多数可视化，您还可以通过点击色板打开颜色选择器选择一种颜色。
![](../../../../images/kibana/tsvb-data-tab-label.png)

**指标**

每个序列支持多个指标（聚合）; 最后一个指标（聚合）是将为该序列显示的值，用指标左侧的“眼睛”图标表示。指标可以使用管道聚合进行组合。一个常见的用例是创建一个带有“最大值”聚合的指标，然后创建一个“导数”指标，并选择之前的“最大值”指标作为源，这将会创造一个比率。
![](../../../../images/kibana/tsvb-data-tab-derivative-example.png)

**序列选项**

每个系列还支持一组选项，这些选项取决于您选择的可视化类型。每个可视化类型通用的配置项有：

- 数据格式
- 时间区间
- 索引模式、时间戳和区间覆盖
![](../../../../images/kibana/tsvb-data-tab-series-options.png)

对于时间序列可视化，您还可以配置：

- 图表类型
- 每种图表类型的选项
- 图例可见性
- Y 轴选项
- 分色主题
![](../../../../images/kibana/tsvb-data-tab-series-options-time-series.png)

**分组控件**

在指标的底部有一组“分组依据”控件，允许您指定该序列应该如何分组或拆分。有四种选择：

- 所有
- 过滤器（单个）
- 过滤器（可配置颜色的多个）
- 词项

默认情况下，系列按照所有进行分组。

**面板选项标签页**

面板选项标签页用于配置整个面板，可用选项集取决于您选择的可视化。以下是每个可视化可用的选项列表：

**时间序列**

- 索引模式、时间戳和区间
- Y 轴最小值和最大值
- Y 轴位置
- 背景颜色
- 图例可见性
- 图例位置
- 面板过滤器

**指标**

- 索引模式、时间戳和区间
- 面板过滤器
- 背景和主要值的颜色规则

**Top N**

- 索引模式、时间戳和区间
- 面板过滤器
- 背景颜色
- 项目 URL
- 条形的颜色规则

**测量仪**

- 索引模式、时间戳和区间
- 面板过滤器
- 背景颜色
- 测量仪最大值
- 测量仪样式
- 内规颜色
- 内规宽度
- 规线宽
- 规线颜色规则

**Markdown**

- 索引模式、时间戳和区间
- 面板过滤器
- 背景颜色
- 滚动条可见性
- 内容垂直对齐
- 自定义面板 CSS 支持 Less 语法

**Annotations 标签页**

注解标签页用于将注解数据源添加到时间序列可视化中。您可以配置以下选项：

- 索引模式和时间字段
- 注解颜色
- 注解图标
- 包含在消息中的字段
- 消息的格式
- 面板和全局级别的过滤选项
![](../../../../images/kibana/tsvb-annotations.png)

**Markdown 选项卡**

Markdown 标签页用于编辑 Markdown 可视化的源代码。用户界面左侧有一个编辑器，右侧有数据标签页中的可用变量。您可以单击变量名称将 Mustache 模板变量插入到光标位置的标记中。Mustache 语法使用 Handlebar.js 处理器，它是 Mustache 模板语言的扩展版本。
![](../../../../images/kibana/tsvb-markdown-tab.png)

## 九、标签云 ##

标签云视图是文本数据的一种可视化表示，通常用来可视化自由形式的文本。标签一般是单独的词，每个标签的重要程度通过字体大小或颜色来表示。

每个词的字体大小，是由 指标 聚合来决定的。下列聚合可用于这个图

###### **1.1 指标聚合** ######    

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Standard Deviation</b></font>
*扩展统计* 聚合返回数字字段中数据的标准偏差。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Percentiles</b></font>
*百分数* 聚合将数字字段中的值分成您指定的百分数区间。从下拉列表中选择一个字段，然后在 Percentiles 输入域中指定一个或多个范围。点击 X 删除百分数字段。点击 + Add 添加百分数字段。

<font color="#2b4590"><b>Percentile Rank</b></font>
*百分位等级* 聚合返回指定的数值字段中的值的百分位等级。从下拉菜单中选择一个数字字段，然后在 Values 输入域中指定一个或多个百分比等级值。点击 **X** 删除值字段。点击 **+ Add** 添加值字段。

###### **1.2 父级管道聚合** ######    

对于每个父管道聚合，您必须定义用于计算聚合的指标。这可能是您现有的指标之一或新的指标。您也可以嵌套这些聚合（例如产生3阶导数）。

<font color="#2b4590"><b>Derivative</b></font>
*导数* 聚合计算特定指标的导数。

<font color="#2b4590"><b>Cumulative Sum</b></font>
*累计总和* 聚合计算父直方图中指定指标的累计总和。

<font color="#2b4590"><b>Moving Average</b></font>
*移动平均值* 聚合将动态移动数据窗口，生成该窗口数据的平均值。

<font color="#2b4590"><b>Serial Diff</b></font>
*串行差分* 是一种时间序列中的值在不同时间滞后或周期内从自身减去的技术。

###### **1.3 兄弟管道聚合** ######    

就像使用父级管道聚合一样，您需要提供一个用于计算同级聚合的指标。除此之外，还需要提供一个桶聚合，它将定义同级聚合将在其中运行的桶。

<font color="#2b4590"><b>Average Bucket</b></font>
*桶平均值* 计算同级聚合中指定指标的（中数）平均值

<font color="#2b4590"><b>Sum Bucket</b></font>
*桶总和* 计算同级聚合中指定指标值的总和

<font color="#2b4590"><b>Min Bucket</b></font>
*桶最小值* 计算同级聚合中指定指标的最小值

<font color="#2b4590"><b>Max Bucket</b></font>
*桶最大值* 计算同级聚合中指定指标的最大值

您可以通过单击 **+ Add Metrics** 按钮来添加聚合。
在 Custom Label 输入域中输入字符串以更改显示标签。

桶 聚合决定了需要从数据集中抽取哪些信息。在选择一个桶聚合前，要勾选 **Split Tags** 选项。

可以为标签云视图指定下列桶聚合：

<font color="#2b4590"><b>Terms</b></font>

一个 terms 聚合支持显示给定字段的前面或后面的 n 个元素，并按数量或自定义指标排序。
点击 Advanced 链接可以显示该指标或桶聚合的更多自定义选项：

<font color="#2b4590"><b>JSON Input</b></font>

这是一个文本字段，支持增加特定的 JSON 格式属性合并到聚合定义中，见下述例子：

>    { \"script\" : \"doc[\'grade\'].value * 1.2\" }

注意：在 Elasticsearch 1.4.3及以后的版本中，这个功能需要打开 动态 Groovy 脚本 。

选择 Options 标签来改变下列图形的方向：

<font color="#2b4590"><b>Text Scale</b></font>

可以选择 linear*、 *log 或 square root 作为文本比例。可以使用对数比例来显示指数变化的数据，或者使用平方根比例来归一化显示包含自身波动很大的变量的数据集。

<font color="#2b4590"><b>Orientation</b></font>

支持选择在标签云中如何定位文本，可以选择下列选项之一：
单个、直角和多个。

<font color="#2b4590"><b>Font Size</b></font>

支持设置视图的最小和最大字体大小。

## 十、热点图 ##

热点图是数据的一种图形化表示，该图中使用颜色来表示矩阵所包含的单个数值。每个矩阵位置的颜色由 （指标）metrics 聚合来决定。热点图支持以下聚合

###### **1.1 指标聚合** ######    

<font color="#2b4590"><b>Count</b></font>
*计数* 聚合返回所选索引模式中元素的原始计数。

<font color="#2b4590"><b>Average</b></font>
*平均值* 从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Sum</b></font>
*总和* 聚合返回数字字段的总和。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Min</b></font>
*最小值* 聚合返回数字字段的最小值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Max</b></font>
*最大值* 聚合返回数字字段的最大值。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Unique Count</b></font>
*基数* 聚合返回字段中唯一值的数量。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Standard Deviation</b></font>
*扩展统计* 聚合返回数字字段中数据的标准偏差。从下拉菜单中选择一个字段。

<font color="#2b4590"><b>Percentiles</b></font>
*百分数* 聚合将数字字段中的值分成您指定的百分数区间。从下拉列表中选择一个字段，然后在 Percentiles 输入域中指定一个或多个范围。点击 X 删除百分数字段。点击 + Add 添加百分数字段。

<font color="#2b4590"><b>Percentile Rank</b></font>
*百分位等级* 聚合返回指定的数值字段中的值的百分位等级。从下拉菜单中选择一个数字字段，然后在 Values 输入域中指定一个或多个百分比等级值。点击 **X** 删除值字段。点击 **+ Add** 添加值字段。

###### **1.2 父级管道聚合** ######    

对于每个父管道聚合，您必须定义用于计算聚合的指标。这可能是您现有的指标之一或新的指标。您也可以嵌套这些聚合（例如产生3阶导数）。

<font color="#2b4590"><b>Derivative</b></font>
*导数* 聚合计算特定指标的导数。

<font color="#2b4590"><b>Cumulative Sum</b></font>
*累计总和* 聚合计算父直方图中指定指标的累计总和。

<font color="#2b4590"><b>Moving Average</b></font>
*移动平均值* 聚合将动态移动数据窗口，生成该窗口数据的平均值。

<font color="#2b4590"><b>Serial Diff</b></font>
*串行差分* 是一种时间序列中的值在不同时间滞后或周期内从自身减去的技术。

###### **1.3 兄弟管道聚合** ######    

就像使用父级管道聚合一样，您需要提供一个用于计算同级聚合的指标。除此之外，还需要提供一个桶聚合，它将定义同级聚合将在其中运行的桶。

<font color="#2b4590"><b>Average Bucket</b></font>
*桶平均值* 计算同级聚合中指定指标的（中数）平均值

<font color="#2b4590"><b>Sum Bucket</b></font>
*桶总和* 计算同级聚合中指定指标值的总和

<font color="#2b4590"><b>Min Bucket</b></font>
*桶最小值* 计算同级聚合中指定指标的最小值

<font color="#2b4590"><b>Max Bucket</b></font>
*桶最大值* 计算同级聚合中指定指标的最大值

您可以通过单击 **+ Add Metrics** 按钮来添加聚合。
在 Custom Label 输入域中输入字符串以更改显示标签。

桶 聚合决定了需要从数据集中抽取哪些信息。

在选择一个桶聚合之前，需要知道是否为单个图或组合图的X轴或Y轴定义桶。一个组合图必须在所有其他聚合之前执行。当划分一个图时，可以通过点击 Rows &#124; Columns 选择器，来改变划分是显示为一行还是一列。

该图的X轴和Y轴支持下面的聚合，点击每个聚合的链接名称查看对应聚合的 Elasticsearch 文档。

<font color="#2b4590"><b>Date Histogram</b></font>
*日期直方图* 由数值字段汇总并按日期组织的。支持秒、分钟、小时、天、周、月或年为单位的时间间隔。您还可以通过选择 **Custom** 自定义事件间隔（在文本域中输入时间间隔和时间单位）。自定义时间间隔单位可以为 s 为秒， m 为分钟， h 为小时， d 为天， w 为周， y 为年。不同单位有不同级别的时间精度，最小时间精度为一秒。

<font color="#2b4590"><b>Histogram</b></font>
*标准直方图* 字段需要指定一个整数间隔。选择 **Show empty buckets** 复选框可以在直方图统计中包含空白区间。

<font color="#2b4590"><b>Range</b></font>
*区间聚合* 为数字字段设置数值的区间范围 **Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Date Range</b></font>
*日期区间* 统计指定的日期区间内的数据。您可以使用 *日期数学* 表达式来设置日期的区间。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>IPv4 Range</b></font>
*IPv4 区间* 根据 IPv4 地址的区间聚合数据。**Add Range** 添加一组统计区间。红色的 **(x)** 按钮可以删除一个区间。

<font color="#2b4590"><b>Terms</b></font>
*词条* 聚合指定字段的 top 或 last 的 n 个元素，按数量或自定义指标进行排序。

<font color="#2b4590"><b>Filters</b></font>
*过滤器* 过滤器可设置为查询字符串或采用 JSON 格式，就像在 Discover 搜索栏中一样。**Add Filter** 添加过滤器。![](../../../../images/kibana/labelbutton.png) 按钮打开标签字段，并输入标签名。

<font color="#2b4590"><b>Significant Terms</b></font>
显示实验性的 *重要词项* 聚合的结果。

击 Advanced 链接为您的度量或桶聚合显示更多自定义选项：

- <font color="#2b4590"><b>Exclude Pattern</b></font>
指定一个模式以从结果中排除。

- <font color="#2b4590"><b>Include Pattern</b></font>
指定一个模式以包含在结果中。

- <font color="#2b4590"><b>JSON Input</b></font>
在其中添加特定的 JSON 格式的自定义聚合语句，如下例所示：
>    { "script" : "doc['grade'].value * 1.2" }

这些选项是否可用取决于所选的聚合。

选择 Options 标签来改变表格的下列方面：

<font color="#2b4590"><b>Show Tooltips</b></font>
勾选此项支持显示提示语。

<font color="#2b4590"><b>Highlight</b></font>
勾选此项支持高亮相同标签的原色。

<font color="#2b4590"><b>Legend Position</b></font>
选择在何处显示图例（上、左、右、下）。

<font color="#2b4590"><b>Color Schema</b></font>
可以选择已有配色方案，或者自定义自己的颜色图例。

<font color="#2b4590"><b>Reverse Color Schema</b></font>
勾选此项将翻转配色方案。

<font color="#2b4590"><b>Color Scale</b></font>
可以切换为 linear、log 及 sqrt 的颜色范围。

<font color="#2b4590"><b>Scale to Data Bounds</b></font>
默认的Y轴边界是0到返回数据中的最大值。勾选此项可以更新上下边界来适应实际数值。

<font color="#2b4590"><b>Number of Colors</b></font>
创建的颜色桶数量。最小为2最大为10。

<font color="#2b4590"><b>Percentage Mode</b></font>
打开时将会以百分比形式显示图例值。

<font color="#2b4590"><b>Custom Range</b></font>
可以为颜色桶自定义范围。对于每个颜色桶，需要指定一个范围的最小值（包括）和最大值（不包括）。

<font color="#2b4590"><b>Show Label</b></font>
在每个单元格中与数值一起显示标签。

<font color="#2b4590"><b>Rotate</b></font>
将单元格数值的标签旋转90度

## 十一、可视化监测 ##

为了查看可视化容器背后的原始数据，点击容器左下方 ![](../../../../images/kibana/spy-open-button.png) 按钮，可视化监测窗口将会打开。可以选中查看原始数据详情。

**表格.** 分页表格形式呈现的基础数据。可以点击表头每行字段名的上下箭头来按照该列排序。

**请求.** 服务器原始请求数据，以 JSON 形式呈现。

**响应.** 服务器原始响应数据，以 JSON 形式呈现。

**统计.** 请求和响应的统计汇总数据，以表格形式呈现。包括查询周期，请求周期，查询到的记录数以及用于查询的索引模板。

**调试.** 以 JSON 形式保存的可视化容器的状态。

将可视化数据以逗号分割值的形式导成（cvs）文件，点击数据表底部的 Raw 或者 Formatted 链接。 Raw 导出 Elasticsearch 存储格式的数据。 Formatted 导出格式化好的数据，详情参考[field formatters](https://www.elastic.co/guide/cn/kibana/current/managing-fields.html)。

# 仪表板 #

## 一、创建一个仪表板 ##

**创建一个仪表板**

1.导航菜单中选择 Dashboard 。您如果没有设置过仪表板，Kibana 显示一个默认页，使用 **+** 或者 **+ Create a dashboard **创建新的仪表板。否则，点击 Dashboard 返回起始页。

Dashboard Landing Page

2.添加可视化结果到仪表板，点击 Edit 进入编辑模式。仪表板切换到编辑模式。
![](../../../../images/kibana/dashboad-edit.png)

3.在编辑，通过 Add 选择并新增一个可视化结果。可以使用 过滤条件 过滤对多个可视化列表结果进行过滤。

Kibana 在仪表板上的容器中使用默认大小显示选择的可视化控件。如果弹出容器太小的提示消息，可以通过拖拽组件调整其大小。

>    注意
>    Kibana 仪表板缺省使用的是浅色主题。 更改为深色主题，点击 **Options** 并选择 **Use dark theme** 。想修改默认主题，到 **Management/Kibana/Advanced Settings **并设置 `dashboard:defaultDarkTheme` 为 true 。

4.当您完成添加和排列可视化操作后，点击 Save 以保存仪表板：

a.输入仪表板的名称。    
b.要使用仪表板存储时间过滤器中指定的时间段，请选择 **Store time with dashboard** 。    
c.点击 Save 按钮将其存储为 Kibana 保存项。    

**仪表板元素布局**

编辑模式下，仪表板中的可视化结果保存在一个可移动的且可调整大小的容器中。

- **移动可视化结果**

1.将鼠标悬停在上方以显示容器控件。    
2.点击并长按容器右上角的 Move 按钮。    
3.将容器拖到新的位置。    
4.释放 Move 按钮。    

- **调整可视化结果的大小**

1.将鼠标悬停在上方以显示容器控件。    
2.点击且长按容器右下角的 Resize 按钮。    
3.拖动以更改容器的尺寸。    
4.释放 Resize 按钮。    

- **删除可视化结果**
从仪表板中移除一个可视化结果：

1.将鼠标悬停在上方以显示容器控件。   
2.点击右上角 Delete 按钮。   

>    注意
>    从仪表板中删除可视化 不会 删除已保存的可视化。

- **查看可视化数据**

显示可视化使用的原始数据：

1.将鼠标悬停在上方以显示容器控件。    
2.点击容器左下角的 Expand 按钮，这将展示包含基础数据的表格、JSON 格式的 Elasticsearch 请求和响应以及请求统计信息数据。请求统计信息显示查询持续时间、请求持续时间、匹配记录总数以及搜索的索引（或索引正则）。

![](../../../../images/kibana/dashboard-datas.png)

可视化数据支持以 CVS 格式导出，请点击数据表底部的 Raw 或者 Formatted 进行导出操作。 Raw 原样导出存储在 Elasticsearch 中的数据。 Formatted 导出格式化好的数据，请参考 *field formatters* 小节。

点击容器左下角的 Collapse 按钮返回可视化结果。

- **修改可视化结果**

在可视化编辑器中打开可视化结果：

1.进入编辑模式。   
2.将鼠标悬停在上方以显示容器控件。     
3.点击容器右上角的 Edit 按钮。  

## 二、加载仪表板 ##

1.点击侧边导航栏中的 Dashboard 。   
2.从列表中选择一个仪表板并点击仪表板名称，可以使用 Filter 来过滤显示仪表板列表。

>    提示
>    要导入、导出和删除仪表板，请点击 Manage Dashboards 链接打开 Management/Kibana/Saved Objects/Dashboards 。

## 三、共享仪表板 ##

向其他用户分享一个 Kibana 仪表板，或者将仪表板嵌入到网页中。用户必须具有 Kibana 权限才能访问嵌入式仪表板。

如何分享一个仪表板：

1.点击侧边导航栏中的 Dashboard。    
2.打开您想共享的仪表板。    
3.点击 Share。    
4.复制您想分享的链接或者您想嵌套的 iframe。您可以分享动态仪表板或者当前时间点的静态快照。

>    提示
>    当共享仪表板快照链接的时候，请使用 Short URL 。 快照 URLs 很长，对于 IE 用户或者其他工具可能会有问题


# 时序控件 #

时序控件（Timelion）是一款时间序列数据可视化工具，可以将多种独立的数据源合并呈现到一张视图上。它是由一个简单的表达式语言驱动的，用来检索时间序列数据，执行计算得出复杂问题的答案，并可视化结果。

例如，Timelion 可以让您轻松获得如下问题的答案：

- 过去某段时间页面的 UV 量是多少？
- 本周五和上周五的流量有多少差异？
- 本站今天来自日本的访客占多少百分比？
- 标普500指数过去10天的移动平均值是多少？
- 过去两年所有的搜索请求总量有多少？  

您还可能对以下视频教程感兴趣：

- [Timelion: 魔法、数学，一切尽在其中](https://www.elastic.co/elasticon/conf/2017/sf/timelion-magic-math-and-everything-in-the-middle)
- [Timelion 插件为 Kibana 提供了时间序列分析工具](https://www.elastic.co/videos/timelion-plugin-for-kibana-enables-times-series-paris-meetup)
- [利用 Kibana 和 Timelion 分析地震数据](https://www.elastic.co/videos/using-kibana-and-timelion-to-analyze-earthquake-data)

## 一、基础入门 ##

###### 1.1 创建基于时间序列的可视化控件 ######

本小节使用来自 [Metricbeat](https://www.elastic.co/guide/en/beats/metricbeat/current/index.html) 的时间序列数据为您示例 Timelion 所能提供的功能。可以先下载 Metricbeat 并根据[使用向导](https://www.elastic.co/downloads/beats/metricbeat)在本地抽取数据。

第一个可视化控件将会对比系统用户空间 CPU 实时使用百分比和其每小时的平均偏移量。为了创建这个控件，我们需要创建两个 Timelion 表达式。第一个是实时的 system.cpu.user.pct 平均值，第二个是每小时的平均偏移量。

您需要在第一个表达式中定义 index 、 timefield 和 metric 。然后紧接着在 Timelion 查询框中输入如下表达式

```
.es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct')
```


现在您需要添加前一个小时的数据用来对比。您需要添加一个 offset 参数到 .es() 函数。 offset 将会利用表达式来指定时间序列偏移量。举个例子，如果您想让时间偏移一个小时那么将会使用时间表达式 -1h 。 使用逗号分隔两个时间序列表达式，例如在 Timelion 查询框中输入如下表达式：

```
.es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct'), .es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct'
```

图形上有点难区分上述两个序列表达式。我们可以通过给每个序列自定义标签来区分它们。您可以在任何一个序列后面添加 .label() 表达式来自定义标签。我们来看看如下自定义标签的例子

```
.es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('last hour'), .es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('current hour')
```

保存整个 Timelion 表格为 Metricbeat Example 。Timelion 是一个非常强大的基于时间序列的控件，您可以对本教程中的一些关键点多加练习来熟悉 Timelion

###### 1.2 自定义格式化控件 ######

Timelion 有大量的自定义选项。您可以利用这些功能根据定制每个图表的各个细节。在本节教程中，您将会进行以下修改：

- 添加一个标题
- 修改一个序列图表的类型
- 修改序列图表的颜色和透明度
- 调整布局

在上一节创建 Timelion 中，您创建了有两个序列图表的 Timelion 控件。让我们继续自定义这些可视化控件。

在进行任何修改之前，我们可以利用 `title()` 函数在表达式结尾添加一个有意义的标题。这将会使不熟悉的用户更容易理解这个可视化控件的目的。如下示例添加了 `title('CPU usage over time')` 到原始的序列表达式中。

```
.es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('last hour'), .es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('current hour').title('CPU usage over time')
```


为了区分前一个小时数据的序列图，您可以修改图表的类型为一个填充的区域图表。为了实现这个目的，您需要使用 .lines() 函数来自定义原有的图表。可以设置 fill 和 width 参数来定义填充级别和线宽。如下示例通过 `.lines(fill=1,width=0.5)` 定义了填充级别为1，线宽为0.5的样式：

```
.es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('last hour').lines(fill=1,width=0.5), .es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('current hour').title('CPU usage over time')
```
 
接下来我们用颜色来凸显当前小时的序列图表。color() 函数可以用来改变颜色，它接受标准的颜色命名，十六进制的值或者直接用标准的颜色命名。例如我们可以使用 .color(gray) 来标记上一个小时的数据，用 .color(#1E90FF) 来标记当前小时的数据。完整的输入如下表达式到 Timelion 查询框来调整：

```
.es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('last hour').lines(fill=1,width=0.5).color(gray), .es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('current hour').title('CPU usage over time').color(#1E90FF)
images/timelion-customize03.png
```

最后，调整控件布局合理利用空间。您可以利用 .legend() 函数设置位置和样式。例如可以通过设置 `.legend(columns=2, position=nw)· 使控件位于西北方向并占用两列。利用如下的表达式进行调整：

```
.es(offset=-1h,index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('last hour').lines(fill=1,width=0.5).color(gray), .es(index=metricbeat-*, timefield='@timestamp', metric='avg:system.cpu.user.pct').label('current hour').title('CPU usage over time').color(#1E90FF).legend(columns=2, position=nw)
```

保存您的修改并继续学习下一节的数学函数。

###### 1.3 使用数学函数 ######

前面两节您学会了如何创建和自定义 Timelion 可视化控件。这一节带您领略 Timelion 数学函数的风采。我们继续使用 Metricbeat 数据来创建基于网络上下行链路数据的新的 Timelion 可视化控件。您可以先添加一个新的 Timelion 可视化控件。

在菜单的顶层，点击 Add 添加第二个控件。添加到当前工作表的时候，您可以注意到查询输入框会被替换成默认的 .es(*) 表达式。因为这个查询是和您当前选中的控件相关联的。

为了便于追踪网络上下行流量，您的第一个表达式将会计算 system.network.in.bytes 下行数据的最大值。在 Timelion 查询框输入如下表达式：

```
.es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.in.bytes)
```
 
监控网络流量对于评估网络速率来说是非常有价值的。derivative() 函数就可以用来做这种随着时间而变化的数据。我们可以简单的将该函数添加至表达式的末尾。使用如下表达式来更新您的控件：

```
.es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.in.bytes).derivative()
```

针对上行数据，您需要添加类似的指标 system.network.out.bytes 。因为上行数据是从您的设备发出去的，一般我们用负数来表达这一指标。.multiply() 函数将会利用一个数来乘以一个序列的数据。结果也将是一个序列或者一个链表的序列数据。例如，您可以使用 .multiply(-1) 来将上行线路转换成负数。使用如下表达式来更新您的控件：

```
.es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.in.bytes).derivative(), .es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.out.bytes).derivative().multiply(-1)
```

为了使该可视化控件可读性更强，可以将数据单位从 bytes 转换为 megabytes(MB)。Timelion 有一个 .divide() 函数可以使用。该函数接收和 .multiply() 类似的数据参数，会利用整个序列的数据来除以定义好的参数。使用如下表达式来更新您的控件：

```
.es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.in.bytes).derivative().divide(1048576), .es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.out.bytes).derivative().multiply(-1).divide(1048576)
```

我们可以利用前面章节学过的样式定制函数 .title()、.label()、.color()、.lines()和.legend()将我们的控件变的更美观。使用如下表达式来更新您的控件：

```
.es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.in.bytes).derivative().divide(1048576).lines(fill=2, width=1).color(green).label("Inbound traffic").title("Network traffic (MB/s)"), .es(index=metricbeat*, timefield=@timestamp, metric=max:system.network.out.bytes).derivative().multiply(-1).divide(1048576).lines(fill=2, width=1).color(blue).label("Outbound traffic").legend(columns=2, position=nw)
```
保存所有的修改继续学习下一节关于条件逻辑和趋势跟踪的内容。

###### 1.4 使用条件逻辑和趋势追踪 ######

这一节您将学会如何使用条件逻辑修改时间序列数据和创建移动平均趋势。这样可以非常方便的发现随着时间推移的异常数据。

为了便于本节内容的学习，我们可以基于 Metricbeat 数据利用可视化控件监控内存消耗情况。可以使用如下表达式在图表中呈现 `system.memory.actual.used.bytes` 的最大值。

```
.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes')
```

我们为内存使用总量创建两个阈值。例如您的告警阈值是12.5GB，严重告警阈值是15GB。当内存使用总量超过其中任何一个，序列图将会在阈值点后用不同的颜色展示。

>    注意
>    如果上述阈值相对您的机器过高或过低，可以自行调节。

您可以使用 Timelion 的条件逻辑配置这两个阈值。可以使用 if() 去比较每个点的值和某个数值的大小，如果数值超过阈值则使用不同的样式，如果未超过阈值，则使用默认样式。Timelion 提供以下六种比较操作：

eq    等于
ne    不等于
lt    小于
lte   小于等于
gt    大于
gte   大于等于

因为有两个阈值，我们需要配置两种不同的样式。使用 gt 操作符和 .color('#FFCC11') 函数将高于告警阈值的标记为黄色，用 .color('red') 函数将严重告警标记为红色。在 Timelion 查询框里面输入以下表达式来配置条件逻辑和阈值类型：

```
.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,12500000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('warning').color('#FFCC11'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,15000000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('severe').color('red')
```

参考 [I have but one .condition()](https://www.elastic.co/blog/timeseries-if-then-else-with-timelion) 博文查看更多关于 Timelion 的用法。

现在我们有阈值控制可以轻松的识别错误数据，接下我们创建一个新的时序图来呈现真正的趋势。Timelion 的 mvavg() 方法可以方便的计算给定时间窗口的移动平均值。这对于分析有很多噪音数据的时序图非常有帮助。这里，您可以使用 .mvavg(10) 创建有10个数据点的移动平均窗口。使用如下表达式创建最大内存使用量的移动平均趋势。

```
.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,12500000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('warning').color('#FFCC11'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,15000000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('severe').color('red'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').mvavg(10)
```
 
现在我们有了阈值控制和移动平均，我们来利用上一节描述过的 .color() 、 .line() 、 .title() 和 .legend() 方法来丰富我们的图表以便于更好的查看：

```
.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').label('max memory').title('Memory consumption over time'), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,12500000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('warning').color('#FFCC11').lines(width=5), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').if(gt,15000000000,.es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes'),null).label('severe').color('red').lines(width=5), .es(index=metricbeat-*, timefield='@timestamp', metric='max:system.memory.actual.used.bytes').mvavg(10).label('mvavg').lines(width=2).color(#5E5E5E).legend(columns=4, position=nw)
```
 
保存您的 Timelion 工作表，继续学习下一章节将这些工作表添加到您的仪表板上。

###### 1.5 添加至仪表板 ######

您已经领略了 Timelion 创建时间序列可视化控件的强大功能。在本章节教程的最后一步是将新的可视化控件添加到一个仪表板上。这一节将向您展示如何保存一个可视化控件至 Timelion 表单并添加至已经存在的仪表板。

按照如下步骤来保存一个 Timelion 控件至仪表板：

选择需要添加至仪表板的一个或多个可视化控件。点击上面菜单中的 Save 选项。选择 Save current expression as Kibana dashboard panel 。定义控件的名称并点击 Save 来保存成一个仪表板可视化控件。

 
现在您可以添加这个仪表板控件到任何一个您喜欢的仪表板上。这个控件将会在控件列表中呈现。继续按照相同的步骤来处理您创建的剩下的可视化控件。

创建一个新的仪表板或者打开一个已经存在的，然后添加您喜欢的其它 Timelion 控件。

 

>    提示
>    您也可以在可视化控件列表 Timeseries 中用 Timelion 表达式直接创建时间序列控件。

## 二、内嵌的帮助文档 ##

记不住一些函数或者搜索方法？随时可以参考 Timelion 内嵌的帮助文档。

Timelion 表达式语言是嵌入式的。点击页面顶部的 Docs 菜单查看可用函数和详细内嵌手册。在查询命令行中输入函数， Timelion 就会实时显示参数提示

![](../../../../images/kibana/timelion-help.png)

# 控制台 #

控制台插件提供一个用户界面来和 Elasticsearch 的 REST API 交互。控制台有两个主要部分： editor ，用来编写提交给 Elasticsearch 的请求； response 面板，用来展示请求结果的响应。在页面顶部的文本框中输入 Elasticsearch 服务器的地址。默认地址是：“localhost:9200”。

![](../../../../images/kibana/dev-tools.png)

控制台支持 cURL 语句。例如以下控制台命令

```
GET /_search
{
  "query": {
    "match_all": {}
  }
}
```

下面是等效的 Elasticsearch _search API 的简单 GET 命令。

```
curl -XGET "http://localhost:9200/_search" -d'
{
  "query": {
    "match_all": {}
  }
}'
```

实际上，复制粘贴上面的命令到控制台，它会自动转换成控制台语句。

当敲入一行命令，控制台会给出上下文相关的提示。这些提示可以帮助您探索每条 API 参数，或者用于提高输入速度。控制台会提示 APIs 、索引和字段名。

![](../../../../images/kibana/introduction_suggestion.png)

一旦您在左边的面板中敲入命令，您可以点击 URL 行边上的绿色小三角提交这条请求到 Elasticsearch。注意，当您移动光标的时候，会有一个小三角和扳手图标跟随着您。我们把这个叫做动作菜单。您也可以选择写多条请求并一起提交它们。

动作菜单
![](../../../../images/kibana/introduction_action_menu.png)

当请求响应后，您可以在侧面的面板中看到它：

输出面板
![](../../../../images/kibana/introduction_output.png)

## 一、多请求支持 ##

控制台编辑器允许您编写多个请求，像在控制台章节展示中那样，您可以通过定位光标并使用动作菜单向 Elasticsearch 提交请求。类似的，您可以一次选择多个请求：

多请求支持
![](../../../../images/kibana/multiple_requests.png)

控制台会依次提交请求到 Elasticsearch ，并将 Elasticsearch 返回的结果显示在右边窗口。这在调试问题或在多个场景中尝试查询组合时会非常方便。

选择多个请求还允许您自动格式化并将其复制为 cURL 命令。

## 二、自动格式化 ##

控制台允许您自动格式化复杂的请求。为此，请将光标置于您想格式化的请求上，并从操作菜单中选择自动缩进：

自动缩进一个请求
![](../../../../images/kibana/auto_format_before.png)

控制台将调整请求的 JSON 体，调整之后的请求如下所示：

格式化的请求
![](../../../../images/kibana/auto_format_after.png)

如果在已完全格式化的请求上选择自动缩进，控制台将把每个文档的请求体折叠到一行，这在使用 Elasticsearch 的批量 API 的时候会非常方便。

每个文档一行
![](../../../../images/kibana/auto_format_bulk.png)

## 三、键盘快捷键 ##

控制台配备了一套非常方便的键盘快捷键，使其工作效率更高。下面是一段概述：

**一般编辑**
Ctrl/Cmd + I
当前请求自动缩进。
Ctrl + Space      
    打开自动补全 （即使没有打字也可以）。    
Ctrl/Cmd + Enter    
    提交请求。    
Ctrl/Cmd + Up/Down    
    跳转到上一个/下一个请求的开始或结束。    
Ctrl/Cmd + Alt + L    
    折叠或展开当前代码块。    
Ctrl/Cmd + Option + 0    
    折叠除当前代码块之外的所有代码块，通过添加 shift 来展开。   

**自动补全可见时**
Down arrow    
    光标切换到自动补全菜单，使用方向键选择下一个选项。    
Enter/Tab    
    在自动补全菜单中选择当前或最上面的选项。    
Esc    
关闭自动补全菜单。

## 四、历史记录 ##

控制台维护 Elasticsearch 成功执行的最后500个请求列表。点击窗口右上角的时钟图标即可查看历史记录。这个图标会打开历史记录面板，您可以在其中查看历史请求。您也可以在这里选择一个请求，它将被添加到编辑器中当前光标所在的位置。

![](../../../../images/kibana/dev-tools-history.png)

## 五、设置 ##

控制台有很多设置，这些设置都可以在控制面板中找到。点击右上角的齿轮按钮就能打开设置面板。
![](../../../../images/kibana/dev-tools-setting.png)

## 六、设置控制台 ##

您可以在 `config/kibana.yml` 文件中添加以下配置：

`console.enabled`
    默认: true 。设置为 false 以禁用控制台。切换此配置将导致服务器在下次启动时重新生成资源，这可能会造成页面开始服务之前有些延迟。

# 管理 #

这里是用来管理您的 kibana 运行时配置的地方，包括初始化配置和后续的索引模式配置、高级设置等。您可以调整 kibana 自身的行为，也可以编辑您通过 kibana 保存的查询、视图、仪表板等各种 "对象“ 。

这部分功能是通过插件实现的，所以除了开箱即用的功能外，诸如 X-Pack 之类的扩展也可以为 Kibana 增加额外的管理能力。

## 一、索引模式 ##

**索引模式**
要使用Kibana，您需要通过配置一个或多个索引模式来告诉它您想探索的 Elasticsearch 索引。您也可以：

1.通过对您数据的实时计算创建脚本化字段，您可以浏览和可视化脚本化字段，但是不能搜索它们。    
2.设置高级选项，例如要在表格中显示的行数以及要显示多少个最受关注的字段。修改高级选项时需要格外注意，避免设置彼此不兼容的值。    
3.为生产环境配置 Kibana。    

***创建索引模式连接 Elasticsearch**

一个 索引模式 标识一个或者多个您想要通过 kiabna 探索的 Elasticsearch 索引。Kibana 会查找与指定模式匹配的索引名称。模式中的星号 (*) 匹配0个或者多个字符。例如，模式 myindex-* 匹配所有名称中以 myindex- 开头的索引，如 myindex-1 和 myindex-2 。

一个索引模式也可以简单地作为单个索引的名称。

要创建一个连接到 Elasticsearch 的索引模式：

1.点击 **设置 > 索引** 标签页。

2.指定与一个或多个 Elasticsearch 索引名称匹配的索引模式。默认情况下，Kibana 会认为您正在处理通过 Logstash 送到 Elasticsearch 的日志数据。

>    注意
>    当您在顶层标签页中切换时，Kibana 会记住您在每个标签页中的位置。例如，如果您在设置标签页中查看了一个特定的索引模式，然后切换到探索标签页，接着再回到设置标签页，Kibana 会显示您刚才看过的那个索引模式。想创建新的索引模式，点击索引模式列表上的 *添加* 按钮。

3.如果您的索引中含有一个时间戳字段，并且您想将这个字段用于执行基于时间比较的操作，请选择 **索引含有带时间戳的事件** 选项，Kibana 会读取索引映射并列出包含时间戳的所有字段，从中选择您需要的字段即可。

4.默认情况下，Kibana 会限制基于时间的索引模式的通配符扩展，范围为当前选定时间内的索引数据。点击 **当搜索时不要展开索引模式** 选项来禁用此行为。

5.点击 **创建** 添加新的索引模式。

6.要指定新模式作为查看探索标签页时加载的默认模式，请单击 **收藏** 按钮。

>    注意
>    当您定义一个索引模式时，Elasticsearch 中必须存在匹配该模式的索引，并且这些索引必须包含数据。

要在索引名称中使用事件时间，需要使用下表中指定的日期格式语汇单元，并将其作为为静态文本放在模式名称中。

例如，`[logstash-]YYYY.MM.DD `匹配所有前缀是 `logstash-` 并且后接 `YYYY.MM.DD` 这种时间戳格式的索引，如 logstash-2015.01.31 和 logstash-2015-02-01 。

**表： 日期格式语汇单元**

<table summary="日期格式语汇单元" cellpadding="4px" border="0"><colgroup><col><col></colgroup><tbody valign="top"><tr><td valign="top">
<p>
<code class="literal">M</code>
</p>
</td><td valign="top">
<p>
Month - cardinal: 1 2 3 … 12
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">Mo</code>
</p>
</td><td valign="top">
<p>
Month - ordinal: 1st 2nd 3rd … 12th
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">MM</code>
</p>
</td><td valign="top">
<p>
Month - two digit:   01 02 03 … 12
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">MMM</code>
</p>
</td><td valign="top">
<p>
Month - abbreviation: Jan Feb Mar … Dec
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">MMMM</code>
</p>
</td><td valign="top">
<p>
Month - full: January February March … December
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">Q</code>
</p>
</td><td valign="top">
<p>
Quarter: 1 2 3 4
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">D</code>
</p>
</td><td valign="top">
<p>
Day of Month - cardinal: 1 2 3 … 31
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">Do</code>
</p>
</td><td valign="top">
<p>
Day of Month - ordinal: 1st 2nd 3rd … 31st
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">DD</code>
</p>
</td><td valign="top">
<p>
Day of Month - two digit:  01 02 03 … 31
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">DDD</code>
</p>
</td><td valign="top">
<p>
Day of Year - cardinal: 1 2 3 … 365
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">DDDo</code>
</p>
</td><td valign="top">
<p>
Day of Year - ordinal: 1st 2nd 3rd … 365th
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">DDDD</code>
</p>
</td><td valign="top">
<p>
Day of Year - three digit: 001 002 … 364 365
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">d</code>
</p>
</td><td valign="top">
<p>
Day of Week - cardinal: 0 1 3 … 6
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">do</code>
</p>
</td><td valign="top">
<p>
Day of Week - ordinal: 0th 1st 2nd … 6th
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">dd</code>
</p>
</td><td valign="top">
<p>
Day of Week - 2-letter abbreviation: Su Mo Tu … Sa
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">ddd</code>
</p>
</td><td valign="top">
<p>
Day of Week - 3-letter abbreviation: Sun Mon Tue … Sat
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">dddd</code>
</p>
</td><td valign="top">
<p>
Day of Week - full: Sunday Monday Tuesday … Saturday
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">e</code>
</p>
</td><td valign="top">
<p>
Day of Week (locale): 0 1 2 … 6
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">E</code>
</p>
</td><td valign="top">
<p>
Day of Week (ISO): 1 2 3 … 7
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">w</code>
</p>
</td><td valign="top">
<p>
Week of Year - cardinal (locale): 1 2 3 … 53
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">wo</code>
</p>
</td><td valign="top">
<p>
Week of Year - ordinal (locale): 1st 2nd 3rd … 53rd
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">ww</code>
</p>
</td><td valign="top">
<p>
Week of Year - 2-digit (locale): 01 02 03 … 53
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">W</code>
</p>
</td><td valign="top">
<p>
Week of Year - cardinal (ISO): 1 2 3 … 53
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">Wo</code>
</p>
</td><td valign="top">
<p>
Week of Year - ordinal (ISO): 1st 2nd 3rd … 53rd
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">WW</code>
</p>
</td><td valign="top">
<p>
Week of Year - two-digit (ISO): 01 02 03 … 53
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">YY</code>
</p>
</td><td valign="top">
<p>
Year - two digit:  70 71 72 … 30
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">YYYY</code>
</p>
</td><td valign="top">
<p>
Year - four digit: 1970 1971 1972 … 2030
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">gg</code>
</p>
</td><td valign="top">
<p>
Week Year - two digit (locale):  70 71 72 … 30
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">gggg</code>
</p>
</td><td valign="top">
<p>
Week Year - four digit (locale): 1970 1971 1972 … 2030
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">GG</code>
</p>
</td><td valign="top">
<p>
Week Year - two digit (ISO): 70 71 72 … 30
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">GGGG</code>
</p>
</td><td valign="top">
<p>
Week Year - four digit (ISO): 1970 1971 1972 … 2030
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">A</code>
</p>
</td><td valign="top">
<p>
AM/PM: AM PM
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">a</code>
</p>
</td><td valign="top">
<p>
am/pm: am pm
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">H</code>
</p>
</td><td valign="top">
<p>
Hour: 0 1 2 … 23
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">HH</code>
</p>
</td><td valign="top">
<p>
Hour - two digit: 00 01 02 … 23
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">h</code>
</p>
</td><td valign="top">
<p>
Hour - 12-hour clock: 1 2 3 … 12
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">hh</code>
</p>
</td><td valign="top">
<p>
Hour - 12-hour clock, 2 digit: 01 02 03 … 12
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">m</code>
</p>
</td><td valign="top">
<p>
Minute: 0 1 2 … 59
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">mm</code>
</p>
</td><td valign="top">
<p>
Minute - two-digit:  00 01 02 … 59
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">s</code>
</p>
</td><td valign="top">
<p>
Second: 0 1 2 …  59
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">ss</code>
</p>
</td><td valign="top">
<p>
Second - two-digit: 00 01 02 … 59
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">S</code>
</p>
</td><td valign="top">
<p>
Fractional Second - 10ths: 0 1 2 … 9
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">SS</code>
</p>
</td><td valign="top">
<p>
Fractional Second - 100ths:  0 1 … 98 99
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">SSS</code>
</p>
</td><td valign="top">
<p>
Fractional Seconds - 1000ths: 0 1 … 998 999
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">Z</code>
</p>
</td><td valign="top">
<p>
Timezone - zero UTC offset (hh:mm format): -07:00 -06:00 -05:00 .. +07:00
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">ZZ</code>
</p>
</td><td valign="top">
<p>
Timezone - zero UTC offset (hhmm format):  -0700 -0600 -0500 … +0700
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">X</code>
</p>
</td><td valign="top">
<p>
Unix Timestamp: 1360013296
</p>
</td></tr><tr><td valign="top">
<p>
<code class="literal">x</code>
</p>
</td><td valign="top">
<p>
Unix Millisecond Timestamp: 1360013296123
</p>
</td></tr></tbody></table>


**设置默认的索引模式**

当您查看 **探索** 标签页时，默认索引模式将会自动加载。在 **设置 > 索引** 标签页的索引模式列表中，Kibana 会在默认模式名称的左侧显示一颗星。您创建的第一个模式将会被自动指定为默认模式。

设置其他模式作为默认索引模式：

1.点击 设置 > 索引 标签页。   
2.在索引模式列表中选择您想要默认加载的模式。  
3.点击模式的 收藏 按钮。

>    注意
>    您也可以在 高级 > 设置 中手动设定默认索引模式。

**重新加载索引字段列表**

当您新增了一个索引映射，Kibana 会自动扫描匹配模式的索引，并显示索引字段的清单。您可以重新载入索引字段列表以便能选择新增的字段。

重载索引字段列表会导致 Kibana 的字段流行度计数器重置。流行度计数器是用来跟踪您在 Kibana 中经常使用的字段，并被用于对列表中的字段进行排序。

要重新加载索引字段列表：

1.点击 **设置 > 索引** 标签页。   
2.从索引模式列表中选择一个索引模式。    
3.点击该模式的 **重载** 按钮。    

**删除索引模式**

要删除一个索引模式：

1.点击 **设置 > 索引** 标签页。         
2.从索引模式列表中选择您想要删除的索引模式。        
3.点击该模式的 **删除** 按钮。      
4.确认您想要删除该模式。

## 二、字段管理 ##

索引模式中的字段会以列表的方式显示，点击列标题可以按列对表格排序，点击最右边列的 **控制** 按钮可以编辑指定字段的属性。您可以从 **格式** 下拉菜单中手动设置字段的格式。具体格式选项依赖于字段类型。

您也可以在 **流行度** 文本框中设置您需要的该字段的流行度值。点击 **更新字段** 按钮确认更改，或者点击 **取消** 返回字段列表。

Kibana 有以下字段类型的格式化：

- 字符串
- 日期
- 地理位置
- 数字

###### 2.1 字符串字段格式化 ######

字符串字段支持 String 和 Url 的格式化。字符串 字段格式化可以对字段内容做如下转换：

- 转换为小写
- 转换为大写
- 转化为标题 （单词的第一个字母大写）
- 应用短点转换，对于 . 字符之前的内容，它将用其第一个字符替换整个字符串。如下所示

<table cellpadding="4px" border="0">
<tr>
    <td valign="middle" align="center"> <strong>原始字符串</strong> </td>
    <td valign="middle" align="center"> <strong>转换后</strong>     </td>
</tr>
<tr>
    <td>com.organizations.project.ClassName</td>
    <td>c.o.p.ClassName</td>
</tr>
</table>


Url 字段格式化支持如下类型：

- **链接** 类型可以将字段的内容转化为一个 URL 。
- **图片** 类型可以用于指定一张特定图片所在的图片目录。

您可以用模板来自定义任意类型的 URL 字段格式。一个 URL 模板 可以让您添加特定的值作为 URL 的一部分。使用字符串 <code>&#123;&#123;value&#125;&#125;</code> 可以将其值添加到指定的 URL。

例如，当:

- 一个字段含有一个用户 ID
- 对该字段使用了 Url 字段格式化
- URI 模板为 http://company.net/profiles?user_id={­{value}­}

生成的 URL 会用来自该字段的用户 ID 替换 <code>&#123;&#123;value&#125;&#125;</code> 。

<code>&#123;&#123;value&#125;&#125;</code> 模板字符串会对字段内容做 URL 编码。当一个字段编码为 URL 出现非 ASCII 字符时，这些字符会被替换为由 % 字符加上相对应的十六进制代码。例如，字段值 users/admin 编码到 URL 模板中会变为 users%2Fadmin 。

当格式化的类型为 图片 时， <code>&#123;&#123;value&#125;&#125;</code> 模板字符串会被替换为对应 URI 图片的名称。

如果想要将未转义的值直接传递给URL，需要使用 <code>&#123;&#123;rawValue&#125;&#125;</code> 字符串。

*标签模板* 可以让您显示一段文本而不是直接显示 URL，您可以在标签模板中使用普通的模板字符串 <code>&#123;&#123;value&#125;&#125;</code> 。也可以使用 <code>&#123;&#123;url&#125;&#125;</code> 模板字符串来显示格式化的 URL。

###### 2.2 日期字段格式化 ######

日期字段支持 Date、Url 和 String 格式化。

Date 格式化能让您使用 moment.js 标准格式定义来选择日期的显示格式。

字符串 字段格式化可以对字段内容做如下转换：

- 转换为小写
- 转换为大写
- 转化为标题 （单词的第一个字母大写）
- 应用短点转换，对于 . 字符之前的内容，它将用其第一个字符替换整个字符串。如下所示：

<table cellpadding="4px" border="0">
<tr>
    <td valign="middle" align="center"> <strong>原始字符串</strong> </td>
    <td valign="middle" align="center"> <strong>转换后</strong>     </td>
</tr>
<tr>
    <td>com.organizations.project.ClassName</td>
    <td>c.o.p.ClassName</td>
</tr>
</table>

Url 字段格式化支持如下类型：

- **链接** 类型可以将字段的内容转化为一个 URL 。
- **图片** 类型可以用于指定一张特定图片所在的图片目录。

您可以用模板来自定义任意类型的 URL 字段格式。一个 URL 模板 可以让您添加特定的值作为 URL 的一部分。使用字符串 <code>&#123;&#123;value&#125;&#125;</code> 可以将其值添加到指定的 URL。

例如，当:

- 一个字段含有一个用户 ID
- 对该字段使用了 Url 字段格式化
- URI 模板为 http://company.net/profiles?user_id={­{value}­}

生成的 URL 会用来自该字段的用户 ID 替换 <code>&#123;&#123;value&#125;&#125;</code> 。

<code>&#123;&#123;value&#125;&#125;</code> 模板字符串会对字段内容做 URL 编码。当一个字段编码为 URL 出现非 ASCII 字符时，这些字符会被替换为由 % 字符加上相对应的十六进制代码。例如，字段值 users/admin 编码到 URL 模板中会变为 users%2Fadmin 。

当格式化的类型为 图片 时， <code>&#123;&#123;value&#125;&#125;</code> 模板字符串会被替换为对应 URI 图片的名称。

如果想要将未转义的值直接传递给URL，需要使用 <code>&#123;&#123;rawValue&#125;&#125;</code> 字符串。

*标签模板* 可以让您显示一段文本而不是直接显示 URL，您可以在标签模板中使用普通的模板字符串 <code>&#123;&#123;value&#125;&#125;</code> 。也可以使用 <code>&#123;&#123;url&#125;&#125;</code> 模板字符串来显示格式化的 URL。

###### 2.3 地理坐标字段格式化 ######

地理坐标字段支持 String 格式化。

字符串 字段格式化可以对字段内容做如下转换：

- 转换为小写
- 转换为大写
- 转化为标题 （单词的第一个字母大写）
- 应用短点转换，对于 . 字符之前的内容，它将用其第一个字符替换整个字符串。如下所示：

<table cellpadding="4px" border="0">
<tr>
    <td valign="middle" align="center"> <strong>原始字符串</strong> </td>
    <td valign="middle" align="center"> <strong>转换后</strong>     </td>
</tr>
<tr>
    <td>com.organizations.project.ClassName</td>
    <td>c.o.p.ClassName</td>
</tr>
</table>

###### 2.4 数字字段格式化 ######

数字字段支持 Url 、 Bytes 、 Duration 、 Number 、 Percentage 、 String 和 Color 格式化

Url 字段格式化支持如下类型：

- **链接** 类型可以将字段的内容转化为一个 URL 。
- **图片** 类型可以用于指定一张特定图片所在的图片目录。

您可以用模板来自定义任意类型的 URL 字段格式。一个 URL 模板 可以让您添加特定的值作为 URL 的一部分。使用字符串 <code>&#123;&#123;value&#125;&#125;</code> 可以将其值添加到指定的 URL。

例如，当:

- 一个字段含有一个用户 ID
- 对该字段使用了 Url 字段格式化
- URI 模板为 http://company.net/profiles?user_id={­{value}­}

生成的 URL 会用来自该字段的用户 ID 替换 <code>&#123;&#123;value&#125;&#125;</code> 。

<code>&#123;&#123;value&#125;&#125;</code> 模板字符串会对字段内容做 URL 编码。当一个字段编码为 URL 出现非 ASCII 字符时，这些字符会被替换为由 % 字符加上相对应的十六进制代码。例如，字段值 users/admin 编码到 URL 模板中会变为 users%2Fadmin 。

当格式化的类型为 图片 时， <code>&#123;&#123;value&#125;&#125;</code> 模板字符串会被替换为对应 URI 图片的名称。

如果想要将未转义的值直接传递给URL，需要使用 <code>&#123;&#123;rawValue&#125;&#125;</code> 字符串。

*标签模板* 可以让您显示一段文本而不是直接显示 URL，您可以在标签模板中使用普通的模板字符串 <code>&#123;&#123;value&#125;&#125;</code> 。也可以使用 <code>&#123;&#123;url&#125;&#125;</code> 模板字符串来显示格式化的 URL。

字符串 字段格式化可以对字段内容做如下转换：

- 转换为小写
- 转换为大写
- 转化为标题 （单词的第一个字母大写）
- 应用短点转换，对于 . 字符之前的内容，它将用其第一个字符替换整个字符串。如下所示：

<table cellpadding="4px" border="0">
<tr>
    <td valign="middle" align="center"> <strong>原始字符串</strong> </td>
    <td valign="middle" align="center"> <strong>转换后</strong>     </td>
</tr>
<tr>
    <td>com.organizations.project.ClassName</td>
    <td>c.o.p.ClassName</td>
</tr>
</table>

`持续时间` 字段格式化可以以如下增量显示字段的数值：

- Picoseconds 皮秒
- Nanoseconds 纳秒
- Microseconds 微秒
- Milliseconds 毫秒
- Seconds 秒
- Minutes 分钟
- Hours 小时
- Days 天
- Weeks 星期
- Months 月
- Years 年

对于输入和输出，您都可以指定最多20位数字的增量。

`颜色` 字段格式化可以让您为数值型字段的某一段值区间指定特定颜色。

当您选择 颜色 字段格式化时，Kibana 会显示**区间、字体颜色、背景颜色和范例**字段。

点击 **添加颜色** 按钮将一段区间值与一个特定颜色关联。您可以点击 **字体颜色** 和 **背景颜色** 字段来显示颜色选择器，也可以在该字段中输入十六进制的颜色码。最后您可以在 **范例** 字段中看到所选颜色的效果。

![](../../../../images/kibana/index-pattern-color.png)

###### 2.5 脚本化字段 ######

脚本化字段是依据 Elasticsearch 索引中的数据即时计算得到的。其作为文档数据的一部分显示在 **发现** 标签页上，您可以将其可视化，但是因为脚本化字段的值是在查询时实时计算产生的，所以它们不能被索引和查询。

>    注意
>    Kibana 不能查询脚本化字段

>    警告
>    脚本化字段因为实时计算数据，所以有可能非常耗费资源，并对 Kibana 的性能产生直接的影响。请记住，脚本化字段是没有内置校验的。如果脚本有问题，每当您试图去查看动态生成的数据时都会得到异常。

当您在 Kibana 中定义一个脚本化字段时，您可以选择使用的脚本语言。从 5.0 版本开始，默认的选项是 [Lucene](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting-expression.html) 表达式 和 [Painless](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting-painless.html)。如果您在 Elasticsearch 中启用了其它动态脚本语言，也可以在 Kibana 中使用，但是不建议这样做。因为它们不能确保[沙箱安全](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting-security.html)。

>    警告
>    从 Elasticsearch 5.0 开始，不推荐使用 Groovy、 Javascript 和 Python 脚本，未来的版本中将不再支持这些脚本语言。

您可以在表达式中引用任何单值的数值字段，例如：

>    doc['field_name'].value
有关脚本化字段和其他范例的更多背景信息，请参阅此博客： [Using Painless in Kibana scripted fields](https://www.elastic.co/blog/using-painless-kibana-scripted-fields)

**创建一个脚本化字段**

要创建脚本化字段:

1.进入 **设置 > 索引**    
2.选择您要添加脚本化字段的索引模式。    
3.进入模式的 **脚本化字段** 标签页。    
4.点击 **添加脚本化字段** 。    
5.输入脚本化字段的名称。    
6.输入您想要通过索引数据即时计算值的表达式。    
7.点击 **保存脚本化字段** 。

有关 Elasticsearch 中脚本化字段的更多信息，请参考 [Scripting](https://www.elastic.co/guide/en/elasticsearch/reference/6.0/modules-scripting.html)。

**更新一个脚本化字段**

要修改一个脚本化字段：

1.进入 **设置 > 索引 **。    
2.点击您想要修改的脚本化字段的 **编辑** 按钮。   
3.修改并点击 **保存脚本化字段** 以更新字段。   

>    警告
>    请注意，脚本化字段没有内置验证。如果您的脚本有问题，每次当您尝试查看动态生成的数据时，都会遇到异常。

**删除一个脚本化字段**

要删除一个脚本化字段：

1.进入 **设置 > 索引** 。
2.点击要删除的脚本化字段的 **删除** 按钮。
3.确认您确实要删除该字段。

## 三、设置高级选项 ##

您可以通过直接编辑 **高级设置** 页面中的选项来控制 Kibana 应用程序的行为。例如，您可以更改日期的显示格式，指定默认的索引模式，或者设置数值的显示精度等。

要设置高级选项：

1.进入 **设置 > 高级** 。
2.点击您想要修改选项的 **编辑** 按钮。
3.为该选项输入一个新的值。
4.点击 **保存** 按钮。

>    警告
>    修改以下的设置会显著的影响 Kibana 的性能，并且有可能导致难以诊断的问题。如果想恢复默认设置，将属性值设置为空字段即可，这可能会造成与其他配置不兼容的情况。如果删除一个自定义的设置，则会将其从 Kibana 中永久删除。

<table>
    <tbody>
        <tr>
            <td>query:queryString:options</td>
            <td>Lucene 查询字符串解析器选项。</td>
        </tr>
        <tr>
            <td>sort:options</td>
            <td>Elasticsearch 排序参数选项 <a class="ulink"
                href="https://www.elastic.co/guide/en/elasticsearch/reference/6.0/search-request-sort.html"
                target="_top">sort</a> 。
            </td>
        </tr>
        <tr>
            <td>dateFormat</td>
            <td>指定日期的显示格式。</td>
        </tr>
        <tr>
            <td>dateFormat:tz</td>
            <td> Kibana 使用的时区。默认值 Browser 表示使用用户浏览器检测到的时区。</td>
        </tr>
        <tr>
            <td> dateFormat:scaled</td>
            <td>这些值定义用于呈现基于时间的有序数据的格式，格式化的时间戳必须适配测量间隔。参考： <a
                        class="ulink"
                        href="http://en.wikipedia.org/wiki/ISO_8601#Time_intervals"
                        target="_top">ISO8601 intervals</a> </td>
        </tr>
        <tr>
            <td> dateFormat:dow </td>
            <td> 这个属性定义了一周应该从哪一天开始。</td>
        </tr>
        <tr>
            <td> defaultIndex </td>
            <td>默认值是  null。这个属性指定了默认索引。</td>
        </tr>
        <tr>
            <td> defaultColumns </td>
            <td> 默认值是 _source。定义“发现”标签页上默认显示的列。</td>
        </tr>
        <tr>
            <td> metaFields</td>
            <td>定义 _source 之外的字段数组。Kibana 会将这些字段合并到文档中一起显示。</td>
        </tr>
        <tr>
            <td> discover:sampleSize </td>
            <td> 定义“发现”标签页中表格要显示的文档行数。</td>
        </tr>
        <tr>
            <td> discover:aggs:terms:size</td>
            <td>定义在“发现”边栏中点击”可视化“按钮时，下拉列表中要显示多少条目。默认值是20。</td>
        </tr>
        <tr>
            <td> doc_table:highlight </td>
            <td> “发现”标签页和保存的搜索仪表板中会高亮显示搜索结果。但是如果遇到超大文档可能会导致请求响应变慢。将此属性设置为 false  可禁用高亮显示。</td>
        </tr>
        <tr>
            <td> doc_table:highlight:all_fields </td>
            <td> 通过在 query_string 查询上使用  all_fields 模式的单独 highlight_query 来改进高亮显示性能。如果您在索引中使用  default_field字段，则设置为 false</td>
        </tr>
        <tr>
            <td>courier:maxSegmentCount </td>
            <td>  Kibana 将”发现“功能中的请求拆分成多个段，以限制发送到 Elasticsearch集群请求的大小。该设置限制了段列表的长度。太长的段列表会显著增加请求处理的时间。 </td>
        </tr>
        <tr>
            <td> courier:ignoreFilterIfFieldNotInIndex</td>
            <td> 设置这个属性为  true 可以跳过那些可视化索引中不存在字段的过滤器。在组成仪表板的可视化组件来自于多个索引模式时特别有用。</td>
        </tr>
        <tr>
            <td> fields:popularLimit</td>
            <td> 这个设置控制显示多少个热门字段。</td>
        </tr>
        <tr>
            <td> histogram:barTarget </td>
            <td> 当日期直方图使用 auto 间隔时，Kibana 试图产生条块的数量。 </td>
        </tr>
        <tr>
            <td> histogram:maxBars</td>
            <td> 日期直方图不会生成超过此属性值的条块数量，并在需要时自动缩放。</td>
        </tr>
        <tr>
            <td> visualization:tileMap:maxPrecision </td>
            <td>
                    tile 地图上显示的最大 geoHash 精度：7表示高，10表示非常高，12是最大值。 <a
                        class="ulink"
                        href="https://www.elastic.co/guide/en/elasticsearch/reference/6.0/search-aggregations-bucket-geohashgrid-aggregation.html#_cell_dimensions_at_the_equator"
                        target="_top">Explanation of cell
                        dimensions</a>.
            </td>
        </tr>
        <tr>
            <td> visualization:tileMap:WMSdefaults  </td>
            <td>  坐标图中 WMS MAP 服务器支持的默认属性。  </td>
        </tr>
        <tr>
            <td> visualization:colorMapping </td>
            <td> 在可视化组件内映射值到指定颜色。</td>
        </tr>
        <tr>
            <td> visualization:loadingDelay </td>
            <td> 在载入可视化组件查询时的等待时长。 </td>
        </tr>
        <tr>
            <td>  visualization:dimmingOpacity </td>
            <td>  当一个可视化组件的一部分通过悬停其上而突出显示时，其他元素会产生不透明效果，数值越大意味着其他元素越不透明。 </td>
        </tr>
        <tr>
            <td> csv:separator </td>
            <td> 设置导出数据时用作分隔符的字符串。</td>
        </tr>
        <tr>
            <td> csv:quoteValues </td>
            <td> 设置这个属性为  true 以引用导出的值。</td>
        </tr>
        <tr>
            <td> history:limit</td>
            <td>  一些字段具有历史数据，比如查询时的输入内容，此属性的值可以限制显示多少条最近的记录。 </td>
        </tr>
        <tr>
            <td> shortDots:enable </td>
            <td> 设置这个属性为  true 可以缩短可视化组件中的字段名称。例如，显示 f.b.baz 替代   foo.bar.baz。 </td>
        </tr>
        <tr>
            <td> truncate:maxHeight </td>
            <td> 这个属性指定了表格中单元格显示时占用的最大高度，设置为0则不限制。</td>
        </tr>
        <tr>
            <td> indexPattern:fieldMapping:lookBack</td>
            <td>此属性设置最近匹配模式的数量，以便查询名称中包含时间戳的索引模式的字段映射。</td>
        </tr>
        <tr>
            <td> indexPattern:placeholder</td>
            <td> 当添加一个新的索引模式到 Kibana 时默认使用的占位符。</td>
        </tr>
        <tr>
            <td> format:defaultTypeMap</td>
            <td>每个字段类型默认格式名称的映射，没有明确提到的字段类型使用 "<span
                        class="emphasis"><em>default</em></span>" 。
            </td>
        </tr>
        <tr>
            <td> format:number:defaultPattern</td>
            <td> "number" 格式的默认数字格式。 </td>
        </tr>
        <tr>
            <td> format:bytes:defaultPattern </td>
            <td>"bytes" 格式的默认数字格式。 </td>
        </tr>
        <tr>
            <td> format:percent:defaultPattern</td>
            <td> "percent" 格式的默认数字格式。 </td>
        </tr>
        <tr>
            <td> format:currency:defaultPattern</td>
            <td> "currency" 格式的默认数字格式。</td>
        </tr>
        <tr>
            <td> savedObjects:perPage </td>
            <td>保存对象列表中每个页面上显示的对象数量。默认值是 5。</td>
        </tr>
        <tr>
            <td> timepicker:timeDefaults </td>
            <td>   默认选择的时间过滤器。</td>
        </tr>
        <tr>
            <td> timepicker:refreshIntervalDefaults</td>
            <td> 时间过滤器的默认刷新间隔。 </td>
        </tr>
        <tr>
            <td> dashboard:defaultDarkTheme</td>
            <td>设置此属性为 true可以使新建仪表板默认使用 dark 主题。</td>
        </tr>
        <tr>
            <td> filters:pinnedByDefault</td>
            <td> 将此属性设置为  true   以使默认情况下过滤器具有全局状态。 </td>
        </tr>
        <tr>
            <td> notifications:banner </td>
            <td> 您可以指定一段自定义内容临时通知给所有用户。该字段支持 Markdown 。 </td>
        </tr>
        <tr>
            <td> notifications:lifetime:banner</td>
            <td> 指定自定义通知显示的持续时间（以毫秒为单位）。默认值为3000000。将此字段设置为 Infinity 可禁用此通知。 </td>
        </tr>
        <tr>
            <td> notifications:lifetime:error </td>
            <td> 指定警告通知显示的持续时间（以毫秒为单位）。默认值为3000000。将此字段设置为  Infinity 可禁用错误通知。 </td>
        </tr>
        <tr>
            <td>notifications:lifetime:warning </td>
            <td> 指定错误通知显示的持续时间（以毫秒为单位）。默认值为3000000。将此字段设置为 Infinity 可禁用警告通知。</td>
        </tr>
        <tr>
            <td> notifications:lifetime:info </td>
            <td>  指定信息通知显示的持续时间（以毫秒为单位）。默认值为3000000。将此字段设置为 Infinity 可禁用信息通知。 </td>
        </tr>
        <tr>
            <td> metrics:max_buckets </td>
            <td> 设置桶的最大数量阈值。例如，避免当用户选择了超长时间（比如1年）和超短的时间间隔（比如1秒）时产生超过上限的桶。 </td>
        </tr>
        <tr>
            <td> timelion:showTutorial</td>
            <td>设置这个属性为 true 以便在用户第一次使用 Timelion 时显示 Timelion 教程。 </td>
        </tr>
        <tr>
            <td> timelion:es.timefield </td>
            <td> 当使用 .es() 查询时，默认字段包含时间戳。</td>
        </tr>
        <tr>
            <td> timelion:es.default_index</td>
            <td>当使用.es() 查询时，默认的索引。</td>
        </tr>
        <tr>
            <td> timelion:target_buckets</td>
            <td> 用于计算可视化中的自动间隔，这是试图表示的桶的数量 </td>
        </tr>
        <tr>
            <td>timelion:max_buckets </td>
            <td> 用于计算可视化中的自动间隔，这是试图表示的桶的最大数量。 </td>
        </tr>
        <tr>
            <td> timelion:default_columns </td>
            <td>  在 timelion 工作表上使用的默认列数。  </td>
        </tr>
        <tr>
            <td>  timelion:default_rows</td>
            <td>
                在 timelion 工作表上使用的默认行数。
            </td>
        </tr>
        <tr>
            <td> timelion:graphite.url</td>
            <td> [试验的] 用于 graphite 查询，这里设置其主机的 URL </td>
        </tr>
        <tr>
            <td> timelion:quandl.key
            </td>
            <td>  [试验的] 用于 quandl 查询，值来自于 www.quandl.com 上您的  API key。</td>
        </tr>
        <tr>
            <td> state:storeInSessionStorage</td>
            <td> [试验的] Kibana 跟踪 URL 中的 UI 状态，当存在大量信息并且 URL 变得非常长的时候，可能会导致问题。启用这个功能会将部分状态保存在浏览器会话中，以保持较短的  URL。 </td>
        </tr>
        <tr>
            <td> context:defaultSize</td>
            <td> 指定在上下文视图中显示的环绕条目的初始数量。默认值是5。 </td>
        </tr>
        <tr>
            <td> context:step </td>
            <td>使用上下文视图中的按钮时，指定用于递增或递减上下文大小的数字。默认值是5。</td>
        </tr>
    </tbody>
</table>


## 四、管理保存的搜索、可视化组件和仪表板 ##

您可以在 **设置 > 对象** 中查看、编辑和删除保存的搜索、可视化组件以及仪表板。您也可以导入或者导出搜索、可视化组件和仪表板的集合。

保存的对象会显示在** 发现、可视化组件** 或者 **仪表板** 页面的待选列表中。要查看保存的对象：

1.进入 **设置 > 对象** 。    
2.选择您想要查看的对象。    
3.点击 **查看** 按钮。   

编辑一个保存的对象能够让您直接修改对象的定义。您可以改变对象的名称、添加说明并修改定义对象属性的 JSON 。

如果您试图访问一个对象，但是其关联的索引已经被删除，Kibana 将显示其“编辑对象”页面。您可以：

- 重新创建索引，以便您可以继续使用该对象。
- 删除该对象并使用不同的索引重新创建它。
- 修改该对象的 `kibanaSavedObjectMeta.searchSourceJSON` 属性，将其引用的索引名称更改为指向一个现存的索引模式。如果您正在使用的索引被重命名，这种方法就非常适用。

>    警告
>    对象属性的修改是没有校验的，提交无效更改将会导致对象不可用。通常您应该使用 发现 、 可视化组件 或者 仪表板 页面来创建新的对象，而不是直接编辑现有的对象。

要编辑一个保存的对象：

1.进入 **设置 > 对象 **。
2.选择您想要编辑的对象。
3.点击 **编辑** 按钮。
4.修改对象的定义。
5.点击 **保存对象** 按钮。

要删除一个保存的对象：

1.进入 **设置 > 对象** 。    
2.选择您想要删除的对象。    
3.点击 **删除** 按钮。    
4.确认您要删除该对象。    

要导出对象的集合：

1.进入 **设置 > 对象** 。    
2.选择要导出的对象的类型。您可以导出一组仪表板、搜索或可视化组件。    
3.选择您想要导出的对象的选择框，或者点击 **选择全部** 。    
4.点击 **导出** 然后选择要导出 JSON 数据的存储位置。   

>    警告
>    导出的仪表板并不包含其关联的索引模式。要将保存的仪表板导入运行在另一个 Elasticsearch 集群上的 Kibana 实例，需要提前手动重新创建索引模式。

要导入对象的集合：

1.进入 **设置 > 对象** 。
2.点击 **导入** ，然后导航到存有要导入对象集合的 JSON 文件所在位置。
3.选择 JSON 文件后点击 **打开** 。
4.如果集合中的对象有可能会覆盖 kibana 中已经存在的对象，需要确认是否覆盖。

# 插件 #

附加的功能在 Kibana 中是以插件的形式提供的。您可以利用 bin/kibana-plugin 命令来管理这些模块。您也可以手动安装这些插件，只需要将这些插件包放到 plugins 目录并解压到新的目录就可以了。

>    重要
>    插件兼容性
>    Kibana 插件接口在不断的发展变化。由于插件更新很快，因此很难向后兼容。Kibana 强制要求安装的插件版本必须和 Kibana 版本一致。插件开发者必须为每个新的 Kibana 版本发布新的插件版本。

## 一、安装插件 ##

使用以下命令安装插件：

```
bin/kibana-plugin install <package name or URL>
```
当您指定的插件名没有带 URL，插件工具将会尝试去下载 Elastic 官方插件。例如：

```
$ bin/kibana-plugin install x-pack
```

**通过指定的 URL 地址安装插件**

您可以简单的指定插件名称来下载 Elastic 官方插件。也可以指定插件具体的 URL 来下载安装，例如：

```
$ bin/kibana-plugin install https://artifacts.elastic.co/downloads/packs/x-pack/x-pack-6.0.0.zip
```

您可以在 URL 中指定多种协议，例如 HTTP 、 HTTPS 或者 文件 协议。

**向指定的目录安装插件**

在 `install` 命令后面通过 `-d` 或者 `--plugin-dir` 选项指定插件安装目录，例如：

```
$ bin/kibana-plugin install file:///some/local/path/x-pack.zip -d path/to/directory
```

>    注意
>    如果目录不存在，这条命令会创建这个目录。

**通过 Linux 安装包安装插件**

Kibana 服务需要有 `optimize` 目录的写权限。如果您使用 sudo 或者 su 安装插件，您需要确保这些命令使用 kibana 用户执行。这个用户已经默认为您添加了，它用于包的安装。

```
$ sudo -u kibana bin/kibana-plugin install x-pack
```

如果插件使用了不同的用户安装且服务又没有运行起来，您就需要修改这些文件的所属用户：

```
$ chown -R kibana:kibana /path/to/kibana/optimize
```

## 二、升级和移除插件 ##

通过删除当前版本重装新的插件来升级插件。

通过 `remove` 命令来删除插件：

```
$ bin/kibana-plugin remove x-pack
```
您也可以通过手动删除 `plugins/` 目录下的插件子目录来手动删除插件。

>    注意
>    删除插件之后将会在下一次 Kibana 启动的时候触发一次 “优化（optimize）” 动作，可能会使启动有点延迟。

## 三、关闭插件 ##

使用如下命令来关闭插件：

```
./bin/kibana --<plugin ID>.enabled=false 
```

>    注意
>    关闭或打开插件将会在下一次 Kibana 启动的时候触发一次 “优化（optimize）” 动作，可能会使启动有点延迟。

您可以在 package.json 文件中通过 name 属性查看插件的 ID。

## 四、配置插件管理器 ##

默认情况下，插件管理器会为您的插件管理动作做出信息反馈。您可以通过添加 `--quiet` 和 `--silen`t 选项为 `install` 和 `remove` 命令控制反馈信息的级别。使用 `--quiet` 选项屏蔽除错误信息以外的日志输出。使用 `--silent` 选项屏蔽所有输出。

默认情况下，插件管理器安装插件不会超时。使用 `--timeout` 选项并添加一个时间来指定安装超时时间：

设定30秒安装超时. 

```
bin/kibana-plugin install --timeout 30s sample-plugin
```

设定1分钟安装超时. 

```
bin/kibana-plugin install --timeout 1m sample-plugin
```

**插件及自定义 Kibana 的配置**

在 `install` 和 `remove` 命令中使用 `-c` 或者 `--config` 选项来指定启动 Kibana 的配置文件的路径。默认情况下，Kibana 使用 config/kibana.yml 配置文件。当您需要修改已安装好的插件配置时，使用 `bin/kibana-plugin` 命令来重启 Kibana 服务。当您使用自定义的配置文件时，每次使用 bin/kibana-plugin 命令必须指定配置文件的路径。

**插件管理器退出代码**
<table>
    <tr>
        <td>0</td>
        <td>成功</td>
    </tr>
    <tr>
        <td>64</td>
        <td>未知命令或错误的参数</td>
    </tr>
    <tr>
        <td>74</td>
        <td>I/O 错误</td>
    </tr>
    <tr>
        <td>70</td>
        <td>其它错误</td>
    </tr>
</table>


## 五、已知的插件 ##

>    重要
>    **插件兼容性**
>    Kibana 插件接口一直在不断发展中，由于变化太快我们无法为插件提供向后的兼容性。Kibana 会强制要安装的插件与 Kibana 当前版本相匹配。因此，插件的开发者需要不断为每个 Kibana 的新版本发布他们所提供插件的新版本。

这个插件列表不保证适用于您的 Kibana 版本。不过它们是可以在 Kibana 5.x 上正常工作的。Kibana 安装程序将拒绝安装任何尚未针对您当前版本 Kibana 发布的插件。

**包**

[X-Pack](https://www.elastic.co/downloads/x-pack) - 安全、监控、报告、告警、图形

**应用**

- [LogTrail](https://github.com/sivasamyk/logtrail) - 为开发者/系统管理员提供实时查看、分析、搜索事件的易用接口
- [Own Home (wtakase)](https://github.com/wtakase/kibana-own-home) - 支持多租户
- [Shard Allocation (asileon)](https://github.com/asileon/kibana_shard_allocation) - 可视化 elasticsearch 分片的分配

**Timelion 扩展**

[mathlion (fermiumlabs)](https://github.com/fermiumlabs/mathlion) - 为 Timelion 增加方程解析和高数能力

**可视化组件**

- [Swimlanes (prelert)](https://github.com/prelert/kibana-swimlane-vis)
- [Line (sbeyn)](https://github.com/sbeyn/kibana-plugin-line-sg)
- [Gauge (sbeyn)](https://github.com/sbeyn/kibana-plugin-gauge-sg)
- [Traffic (sbeyn)](https://github.com/sbeyn/kibana-plugin-traffic-sg)
- [3D Graph (JuanCarniglia)](https://github.com/JuanCarniglia/area3d_vis)
- [Enhanced Tilemap (nreese)](https://github.com/nreese/enhanced_tilemap)
- [Network Plugin (dlumbrer)](https://github.com/dlumbrer/kbn_network)
- [C3JS Visualizations (mstoyano)](https://github.com/mstoyano/kbn_c3js_vis)
- [Health Metric (clamarque)](https://github.com/clamarque/Kibana_health_metric_vis)
- [Extended Metric (ommsolutions)](https://github.com/ommsolutions/kibana_ext_metrics_vis)
- [3D Charts (virusu)](https://github.com/virusu/3D_kibana_charts_vis)
- [Colored Metric Visualization (deanf)](https://github.com/DeanF/health_metric_vis)
- [Cohort analysis (elo7)](https://github.com/elo7/cohort)
- [Percent (amannocci)](https://github.com/amannocci/kibana-plugin-metric-percent)
- [Funnel Visualization (roybass)](https://github.com/outbrain/ob-kb-funnel)
- [Transform Visualization (PhaedrusTheGreek)](https://github.com/PhaedrusTheGreek/transform_vis)
- [Search-Tables (dlumbrer)](https://github.com/dlumbrer/kbn_searchtables)

**其他**

[Time picker as a dashboard panel](https://github.com/nreese/kibana-time-plugin) 可以在仪表板内查看和编辑时间范围的小组件

>    注意
>    如果您希望将您的插件也添加到此页面，请打开 [pull request](https://github.com/elastic/kibana/tree/6.0/docs/plugins/known-plugins.asciidoc)。

# 贡献 #

我们非常欢迎您为 Kibana 做贡献，如果您想提交 pull request 到 Kibana 仓库，您可以参考[核心开发](https://www.elastic.co/guide/cn/kibana/current/core-development.html)。

如果您想使用 Kibana 内部的插件 API，您可以查看[插件开发](https://www.elastic.co/guide/cn/kibana/current/plugin-development.html)。

## 一、核心开发 ##

- basePath 注意事项
- 管理依赖
- 模块和自动加载
- 与 Elasticsearch 通信
- 功能测试

###### 1.1 basePath注意事项 ######

所有从 Kibana UI 到服务端的通信，都要遵守 `server.basePath`。下面是一些基于上下文处理该问题的建议：

**&lt;img&gt; 和 &lt;a&gt; 元素**

如您所愿，可以不写基本路径而直接写上 src 或者 href urls，然后用 kbn-src 或 kbn-href 替换 src 或 href 。

```
<img kbn-src="plugins/kibana/images/logo.png">
```

**获取一个静态的 asset url**

用 webpack 导入 asset 到 build 中。这会给您一个 JavaScript 的 URL，并给 webpack 一个机会去执行优化及中断缓冲。

```
// in plugin/public/main.js
import uiChrome from 'ui/chrome';
import logoUrl from 'plugins/facechimp/assets/banner.png';

uiChrome.setBrand({
  logo: `url(${logoUrl}) center no-repeat`
});
```

**前端 API 请求**

使用 `chrome.addBasePath()` 将 basePath 添加到 url 的前面。

```
import chrome from 'ui/chrome';
$http.get(chrome.addBasePath('/api/plugin/things'));
```

**服务器端**

在每个绝对 URL 路径上添加 `config.get('server.basePath')`

```
const basePath = server.config().get('server.basePath');
server.route({
  path: '/redirect',
  handler(req, reply) {
    reply.redirect(`${basePath}/otherLocation`);
  }
});
```

**开发模式中的 BasePathProxy**

Kibana 开发服务器在一个有随机 server.basePath 的代理之后自动运行。这样，当开发者编写代码时，他们会不断地确认他们的代码是否与 basePath 一起工作。

为了达到这个效果， serve 任务做了如下一些事情：

1.根据 `dev.basePathProxyTarge`t 配置服务器的端口（默认 5603 ）
2.在 `server.port` 启动一个 `BasePathProxy`

- 为 `randomBasePath` 挑选一个三位数的值
- 从 `/{any}/app/{appName}` 重定向到 `/{randomBasePath}/app/{appName}`，从而使刷新起作用
- 将以 `/{randomBasePath}/` 开头的所有请求代理到 Kibana 服务器

有时候，在开发环境中代理会产生意想不到的副作用。因此，当需要的时候您可以通过传递 `--no-base-path` 选项到 serve 任务或者 npm start 以退出代理。

```
npm start -- --no-base-path
```

###### 1.2 管理依赖 ######

在开发 Kibana 前端环境中使用的插件时，您可能想要包含（至少）一个或两个库。虽然这在90%的情况下都是很简单的，但总会有一些异常值，而其中一些异常值还是在非常受欢迎的项目中。

在 Kibana 中使用外部库之前，您要先安装它。您可以通过如下方式安装：

**npm （首选方法）**
一旦您[发现](http://npmsearch.com/)想要添加的依赖，您可以像这样安装它：

``` js
npm install --save some-neat-library
```

在 javascript 文件的顶部，只需要使用它的名称来导入库：

```
import someNeatLibrary from 'some-neat-library';
```

就像在 node.js 中一样，前端代码无需进行扩展配置就能请求 npm 节点模块安装。

**webpackShims**

当您想要用的库使用 es6 或 common.js 模块，但在 npm 上不可用时，您可以复制库的源文件到 webpackShim。

```
# 为新的库创建一个目录
mkdir -p webpackShims/some-neat-library
# 将您想使用的库下载到该目录
curl https://cdnjs.com/some-neat-library/library.js > webpackShims/some-neat-library/index.js
```

然后，像往常一样在您的 JavaScript 代码中包含该库：

``` js
import someNeatLibrary from 'some-neat-library';
```

**桥接第三方代码**

一些 JavaScript 库声明它们依赖的方式并不会被诸如 webpack 的工具所理解。通常情况下，库不会导出它们提供的值，而只是将它们写入到全局变量里（或者某种意义上的变量）。

当将这样的代码拉入到 Kibana 中时，我们要编写 “桥接代码（shims）” 来整合第三方代码，以便与我们的应用、其他库和模块系统一起工作。我们可以使用 `webpackShims` 目录来做到这一点。

示例是解释如何编写桥接代码的最简单方式。下面是我们用于 jQuery 的 webpack 桥接代码。

``` js
// webpackShims/jquery.js

module.exports = window.jQuery = window.$ = require('node_modules/jquery/dist/jquery');
require('ui/jquery/findTestSubject')(window.$);
```

由于 `webpackShims` 的行为类似于 `node_modules`，一旦 webpack 发现 `import 'jquery';` 语句，桥接代码会被加载。当它发生时，桥接代码会做两件事：

1.将实际 jQuery 模块的导出值分配给 `$` 和 `jQuery` ，允许像 angular 这样的库检测 jQuery 是否可用，并将其作为模块的导出变量使用。
2.最终，我们编写的 jQuery 插件会被引入，因此每次有文件引入 jQuery 时，该文件会同时得到 jQuery 和 `$.findTestSubject` 的帮助模块。

下面是我们用于 angular 的 webpack 桥接代码：

``` js
// webpackShims/angular.js

require('jquery');
require('node_modules/angular/angular');
require('node_modules/angular-elastic/elastic');
require('ui/modules').get('kibana', ['monospaced.elastic']);
module.exports = window.angular;
```

如果您一行一行的看，会发现桥接代码做的很简单：

1.确保 jQuery 在 angular（实际运行上述的 shim） 之前加载。
2.从 npm 安装中加载 angular.js 。
3.加载 angular-elastic 插件，每次导入 angular 都需要包含 angular-elastic 插件。
4.使用 `ui/modules` 模块添加被 angular-elastic 导入进来的模块作为 kibana angular 模块的依赖。
5.最后，导出 window.angular 变量。这意味着当写下 `import angular from 'angular';` 时会恰当地设置 angular 库中的 angular 变量，而不是未定义的默认配置。

###### 1.3 模块和自动加载 ######

**自动加载**

由于 JS 模块与指令、过滤器和服务的脱节，很难知道要导入哪些内容。更难的是，您不知道自己移除的看似无用的模块是否会对其他地方产生影响。

为了防止其成为一个问题，ui 模块提供了 “自动加载（autoloading）” 模块。这些模块的唯一目的是使用某些组件拓展环境。以下是这些模块的分解：

- `import 'ui/autoload/styles'` 在 `src/ui/public/styles` 导入所有样式。
- `import 'ui/autoload/directives'` 在 `src/ui/public/directives` 导入所有指令。
- `import 'ui/autoload/filters'` 在 `src/ui/public/filters` 导入所有过滤器。
- `import 'ui/autoload/modules'` 导入 Kibana 依赖没有导入的 angular、一些 ui 服务和 “组件”。需要导入的全量列表被硬编码在模块中。随着我们正确地定位出所需模块并将其导入到需要它们的位置，这个列表可能会逐渐缩小。
- `import 'ui/autoload/all'` 导入所有上述模块

**解析所需路径**

Kibana 用 Webpack 管理依赖。

下面是如何将 import/require 语句解析为一个文件：

1.检查模块路径的开头
- 如果路径以 . 开头
    - 添加当前文件的目录
    - 转到 3

- 如果路径以 / 开头
    - 搜索这条精确路径
    - 转到 3
- 转到 2

2.搜索已命名模块
- `moduleName = dirname(require path)`
- 如果 `moduleName` 是下面别名中的一个，或者以下面中的别名开头，则匹配
    - 用匹配替换别名，继续 3

- 当满足这些条件时，匹配：
    - `./webpackShims/${moduleName}` 是一个目录
    - `./node_modules/${moduleName}` 是一个目录

- 如果没有找到匹配
    - 转到上层目录
    - 从 2.iii 重新开始，直至找到匹配或者到达根目录

- 如果找到匹配
    - 以匹配的全路径替换 requite 语句中的 `moduleName` 前缀，然后转到 3

3.搜索文件
- 下列路径中第一个解析为一个 file 的是我们的匹配
    - path + .js
    - path + .json
    - path + .jsx
    - path + .less
    - path
    - path/${basename(path)} + .js
    - path/${basename(path)} + .json
    - path/${basename(path)} + .jsx
    - path/${basename(path)} + .less
    - path/${basename(path)}
    - path/index + .js
    - path/index + .json
    - path/index + .jsx
    - path/index + .less
    - path/index

- 如果以上路径均不匹配则抛出错误

###### 1.4 与Elasticsearch通信 ######

Kibana 在服务器和浏览器上暴露了两个客户端用于和 elasticsearch 通信。其中一个为管理客户端，用于管理 Kibana 的状态；另外一个为数据客户端，用于处理其它所有的请求。客户端使用 elasticsearch.js 库。

**服务器客户端**

服务器客户端通过 elasticsearch 插件暴露。

```js
  const adminCluster = server.plugins.elasticsearch.getCluster('admin);
  const dataCluster = server.plugins.elasticsearch.getCluster('data);

  //ping as the configured elasticsearch.user in kibana.yml
  adminCluster.callWithInternalUser('ping');

  //ping as the user specified in the current requests header
  adminCluster.callWithRequest(req, 'ping');
```

**浏览器客户**

浏览器客户端通过 AngularJS 服务暴露。

```js
uiModules.get('kibana')
    .run(function (esAdmin, es) {
        es.ping()
          .then(() => esAdmin.ping())
          .catch(err => {
              console.log('error pinging servers');
          });
    });
```


###### 1.5 功能测试 ######

我们通过功能测试确保 Kibana UI 按照预期方式运行。该功能测试通过自动化用户交互，取代了长达数小时的人工测试。Kibana 使用的工具叫做 `FunctionalTestRunner`，能够更好的控制功能测试环境，更便于插件作者使用。

**运行功能测试**

`FunctionalTestRunner` 结构非常简单，大部分功能主要源自位于[ test/functional/config.js](https://github.com/elastic/kibana/blob/6.0/test/functional/config.js) 的配置文件。如果您正在编写一个插件，就会拥有自己的配置文件。有关更多信息，请参见 [插件功能测试](https://www.elastic.co/guide/cn/kibana/current/development-plugin-functional-tests.html) 。

使用 node.js 执行 `FunctionalTestRunner` 脚本运行测试，使用 Kibana 的默认配置：

```shell
node scripts/functional_test_runner
```

在没有任何参数的情况下运行时， `FunctionalTestRunner` 会自动加载位于标准位置的配置，但是您可以用 `--config` 标记来覆盖这个行为。 `--bail` 和 `--grep` 也有命令行标记，功能与 mocha 类似。 日志也可以通过使用 `--quiet`、`--debug` 或 `--verbose` 标记进行自定义设置。

使用 `--help` 标记获得更多选项。

**编写功能测试**

- **环境**

测试位于 [mocha](https://mochajs.org/) ，使用 [expect](https://github.com/Automattic/expect.js) 作断言。

我们使用 [chromedriver](https://sites.google.com/a/chromium.org/chromedriver/)、[leadfoot](https://theintern.github.io/leadfoot) 和 [digdug](https://github.com/theintern/digdug) 在 Chrome 上做自动化测试。 FunctionalTestRunner 启动后，digdug 会打开一个启动 chromedriver 的 Tunnel 和一个 Chrome 的精简用例。digdug 还会创建一个 [Leadfoot’s](https://theintern.github.io/leadfoot/module-leadfoot_Command.html) Command 类的用例，该用例可以通过 remote 服务器获取。 remote 通过 digdug Tunnel 与 Chrome 进行通讯。 remote 涉及的所有命令详见 [leadfoot/Command API](https://theintern.github.io/leadfoot/module-leadfoot_Command.html)。

`FunctionalTestRunner` 使用 babel 语言自动编译功能测试，因此测试可以使用 Kibana 源代码使用的 ECMAScript 特性。详见 [style_guides/js_style_guide.md](https://github.com/elastic/kibana/blob/6.0/style_guides/js_style_guide.md)。

- **术语**

**Provider(提供者):**

`FunctionalTestRunner` 运行的代码会被打包进一个函数中，这样它就可以通过配置文件传递，并且能被参数化。这些提供者函数中的任何一个都有可能是异步的，并需要返回或重新获取他们想要的 值 。提供者函数总通过单一参数：API Provider（参见 [Provider API](https://www.elastic.co/guide/cn/kibana/current/development-functional-tests.html#functional_test_runner_provider_api) 章节）来调用。

提供者配置示例

```yml
// config and test files use `export default`
export default function (/* { providerAPI } */) {
    return {
        // ...
    }
}
```

<font color="#2b4590"><b>Services(服务)</b></font>
服务根据服务提供者产生的单一值命名。测试和其他服务能够通过请求服务的名称来检索服务实例。除 mocha API 以外的所有功能都是通过服务公开的。

<font color="#2b4590"><b>Page objects(页对象)</b></font>
页对象是一种将通常行为封装进特定页面或插件的特殊服务。当您编写自己的插件时，您可能想要添加一个（或多个）用于描述测试所需执行的常见交互的页面对象。

<font color="#2b4590"><b>Test Files(测试文件)</b></font>
`FunctionalTestRunner` 的主要目的是执行测试文件。这些文件导出一个提供者 API 调用的测试提供者（Test Provider），但并不会返回数值。相反，测试提供者用 [mocha’s BDD interface](https://mochajs.org/#bdd) 定义一个程序组。

<font color="#2b4590"><b>Test Suite(测试套件)</b></font>
测试套件是调用 `describe()` 的测试集，然后通过调用 `it()`、 `before()`、`beforeEach()` 等填充测试和 setup/teardown hooks。每个测试文件都必须定义唯一一个顶级测试套件，但测试套件可以拥有任意多个嵌套测试套件。

- **测试文件剖析**

下列带注释的示例文件展示了每个测试套件所使用的基本结构。它首先导入 [expect.js](https://github.com/Automattic/expect.js)，然后定义其默认输出：一个匿名的测试提供者。该测试提供者为 `getService()` 和 `getPageObjects()` 函数拆解提供者 API。它使用这些函数来收集本套件的依赖。对于 mocha.js 用户，其他测试文件看起来就很普通了。

```js
import expect from 'expect.js';
// test files must `export default` a function that defines a test suite
export default function ({ getService, getPageObject }) {

    // most test files will start off by loading some services
    const retry = getService('retry');
    const testSubjects = getService('testSubjects');
    const esArchiver = getService('esArchiver');

    // for historical reasons, PageObjects are loaded in a single API call
    // and returned on an object with a key/value for each requested PageObject
    const PageObjects = getPageObjects(['common', 'visualize']);

    // every file must define a top-level suite before defining hooks/tests
    describe('My Test Suite', () => {

        // most suites start with a before hook that navigates to a specific
        // app/page and restores some archives into elasticsearch with esArchiver
        before(async () => {
            await Promise.all([
                // start with an empty .kibana index
                esArchiver.load('empty_kibana'),
                // load some basic log data only if the index doesn't exist
                esArchiver.loadIfNeeded('makelogs')
            ]);
            // go to the page described by `apps.visualize` in the config
            await PageObjects.common.navigateTo('visualize');
        });

        // right after the before() hook definition, add the teardown steps
        // that will tidy up elasticsearch for other test suites
        after(async () => {
            // we unload the empty_kibana archive but not the makelogs
            // archive because we don't make any changes to it, and subsequent
            // suites could use it if they call `.loadIfNeeded()`.
            await esArchiver.unload('empty_kibana');
        });

        // This series of tests illustrate how tests generally verify
        // one step of a larger process and then move on to the next in
        // a new test, each step building on top of the previous
       it('Vis Listing Page is empty');
       it('Create a new vis');
       it('Shows new vis in listing page');
       it('Opens the saved vis');
       it('Respects time filter changes');
       //it(...
    });

}
```

- **提供者 API**

提供者 API 对象（Provider API Object）是所有提供者的第一个也是唯一一个参数。这个对象可以用于加载服务、页面对象和配置、测试文件。

在配置文件中，API具有以下属性

<table class="flex">
    <tr>
        <td>log</td>
        <td>
            <code>
                <a href="https://github.com/elastic/kibana/blob/6.0/src/utils/tooling_log/tooling_log.js">ToolingLog</a>
            </code>的一个准备使用的实例
        </td>
    </tr>
    <tr>
        <td>readConfigFile(path)</td>
        <td>返回一个解析为配置实例的承诺，提供 path 路径下的配置文件值</td>
    </tr>
</table>

在服务和 PageObject 提供者中，API 是

<table>
    <tr>
        <td>getService(name)</td>
        <td>根据名称，加载并返回服务的一个单例实例</td>
    </tr>
    <tr>
        <td>getPageObjects(names)</td>
        <td>加载 <code>PageObject</code> 的单例实例，收集它们到一个对象，名字是 PageObject 中每个对象的 key</td>
    </tr>
</table>

测试提供者中的 API 与服务提供者 API 相同，但是具有附加方法：

`loadTestFile(path)` 加载路径上的测试文件。使用此方法将其他文件中的套件嵌套到更高级的套件中。

**服务指标**

- **内置服务**

`FunctionalTestRunner` 自带三种内置 service：

<font color="#2b4590"><b>config:</b></font>
- 源码： src/functional_test_runner/lib/config/config.js
- 概要： src/functional_test_runner/lib/config/schema.js
- 使用 config.get(path) 查看配置文件中的任意值


<font color="#2b4590"><b>log:</b></font>
- 源码： src/utils/tooling_log/tooling_log.js
- `ToolingLog` 实例是可读流。此服务提供的实例由 `FunctionalTestRunner CLI` 自动传输到 stdout
- `log.verbose()`、`log.debug()`、`log.info()`、`log.warning()` 像 console.log 那样工作，只不过产生结构化更好的输出

<font color="#2b4590"><b>lifecycle:</b></font>
- 源码： src/functional_test_runner/lib/lifecycle.js
- 设计主要用于 service 中
- 公开生命周期事件以进行基本协调。处理程序可以返回承诺并异步地解析、失败
- 包括 `beforeLoadTests`、`beforeTests`、`beforeEachTest`、`cleanup`、`phaseStart`、`phaseEnd` 阶段

- **Kibana 服务**

Kibana 功能测试定义了绝大部分测试会使用的实际功能。

<font color="#2b4590"><b>retry:</b></font>
- 源码： test/functional/services/retry.js
- 重试操作辅助器
- 常用方法：
    - `retry.try(fn)` - 在 loop 中执行 fn 直至成功或超过默认重试时间
    - `retry.tryForTime(ms, fn)` 在 loop 中执行，直至成功或超过 ms 毫秒

<font color="#2b4590"><b>testSubjects:</b></font>
- 源码： test/functional/services/test_subjects.js
- 测试主题是从测试中选出的被专门标记过的要素
- 可能的情况下，在 CSS 选择器中使用 `testSubjects`
- 使用：

    - 用 `data-test-subj` 属性标记您的测试对象：

>    <div id="container”>
>        <button id="clickMe” data-test-subj=”containerButton” />
>    </div>

    - 使用 testSubjects 帮助器点击这个按钮

>    await testSubjects.click(‘containerButton’);

- 常用方法：
    - `testSubjects.find(testSubjectSelector)` - 在页面中寻找一个测试对象；如果过一段时间没有找到，抛出异常
    - `testSubjects.click(testSubjectSelector)` - 在页面中点击一个测试主题；如果过一段时间没有找到，抛出异常

<font color="#2b4590"><b>find:</b></font>
- 源码： test/functional/services/find.js
- remote.findBy 方法帮助器，用于记录日志和管理超时
- 常用方法：
    - find.byCssSelector()
    - find.allByCssSelector()
    - 
<font color="#2b4590"><b>kibanaServer:</b></font>
- 源码： test/functional/services/kibana_server/kibana_server.js
- 与 Kibana 服务器交互的帮助器
- 常用方法：
    - kibanaServer.uiSettings.update()
    - kibanaServer.version.get()
    - kibanaServer.status.getOverallState()

<font color="#2b4590"><b>esArchiver:</b></font>
- 源码： test/functional/services/es_archiver.js
- 用 esArchiver 创建的加载、卸载文件
- 常用方法：
    - esArchiver.load(name)
    - esArchiver.loadIfNeeded(name)
    - esArchiver.unload(name)

<font color="#2b4590"><b>docTable:</b></font>
- 源码： test/functional/services/doc_table.js
- 与 doc 表格交互的帮助器

<font color="#2b4590"><b>pointSeriesVis:</b></font>
- 源码： test/functional/services/point_series_vis.js
- 与点序列可视化交互的帮助器

<font color="#2b4590"><b>Low-level utilities:</b></font>
- es
    -源码： test/functional/services/es.js
    -Elasticsearch 客户端
    -高级选项： kibanaServer.uiSettings 或 esArchiver

- remote
    -源码: test/functional/services/remote/remote.js
    -https://theintern.github.io/leadfoot/module-leadfoot_Command.html[Leadfoot’s Command] 类实例
    -负责与浏览器的所有通信
    -高级选项： testSubjects 、 find 和 PageObjects.common
    -完整 API 参见 [leadfoot/Command API](https://theintern.github.io/leadfoot/module-leadfoot_Command.html)

**自定义服务**

服务是有意通用的。它们可以是任何东西（甚至什么都不是）。有些服务有助于与特定类型的 UI 元素（如 PooSosieServices ）交互，而其他服务则更为基础，如日志或配置。每当您想在可重用包中提供一些功能时，请考虑制作自定义服务。

为了创建一个自定义的 `somethingUseful` service：

- 创建一个如下的 `test/functional/services/something_useful.js` 文件:

```js
// Services are defined by Provider functions that receive the ServiceProviderAPI
export function SomethingUsefulProvider({ getService }) {
    const log = getService('log');

    class SomethingUseful {
        doSomething() {
        }
    }
    return new SomethingUseful();
}
```

- 从 `services/index.js` 重新导出您的 provider
- 将它导入到 `src/functional/config.js` 并添加到服务配置中：

```js
import { SomethingUsefulProvider } from './services';

export default function () {
    return {
        // … truncated ...
        services: {
            somethingUseful: SomethingUsefulProvider
        }
    }
}
```

**PageObjects**
PageObject 的目的只是自我解释。可视化的 PageObject 提供与可视化 app 交互的助手，相当于仪表板对于仪表板 app。

"common" PageObject 是一个例外。作为一个延缓的实验性的实现，common PageObject 是有用的跨页面的帮助器集合。现在我们有了共享服务，并且这些服务可以与其他的 `FunctionalTestRunne`r 共享，我们会继续将功能从 common PageObject 转移到服务中。

请在已有或新服务中添加新的方法，而不是进一步扩展 CommonPage 类。

**Gotchas**

记住您不能运行文件（ it 块）中一个单独的测试，因为整个 describe 需要按顺序执行。在一个文件中应该只有一个顶级的 describe 。

**功能测试计时**

另一个重要的 gotcha 是通过注意时间来编写稳定的测试。所有 remote 方法异步运行。最好在进入下一步之前，在 UI 上添加等待变化的交互。

例如，与其简单的编写点击按钮的交互，不如在头脑中编写更高级目的的交互：

不好的例子： `PageObjects.app.clickButton()`

```js
class AppPage {
    // what can people who call this method expect from the
    // UI after the promise resolves? Since the reaction to most
    // clicks is asynchronous the behavior is dependant on timing
    // and likely to cause test that fail unexpectedly
    async clickButton () {
        await testSubjects.click(‘menuButton’);
    }
}
```

好的例子： `PageObjects.app.openMenu()`

```js
class AppPage {
    // unlike `clickButton()`, callers of `openMenu()` know
    // the state that the UI will be in before they move on to
    // the next step
    async openMenu () {
        await testSubjects.click(‘menuButton’);
        await testSubjects.exists(‘menu’);
    }
}
```

这样写将确保您的测试时间不是片状的，或者基于交互后UI更新的假设。

**调试**
在命令行运行：

```js
node --debug-brk --inspect scripts/functional_test_runner
```

该命令会输出一个URL，通过在 Chrome 浏览器中访问该URL，您可以调试您的功能测试用例。

您也可以在运行 `FunctionalTestRunner` 时增加 `--debug` 或 `--verbose` 参数，从而在命令行看额外的日志信息。您可以像下面这样，在您的测试用例中增加日志：

```js
// load the log service
const log = getService(‘log’);

// log.debug only writes when using the `--debug` or `--verbose` flag.
log.debug(‘done clicking menu’);
```

## 二、插件开发 ##

>    重要
>    Kibana 插件接口在不断的发展变化。由于插件更新很快，因此很难向后兼容。Kibana 强制要求安装的插件版本必须和 Kibana 版本一致。插件开发者必须为每个新的 Kibana 版本发布新的插件版本。

- [插件资源](https://www.elastic.co/guide/cn/kibana/current/development-plugin-resources.html)
- [UI Exports](https://www.elastic.co/guide/cn/kibana/current/development-uiexports.html)
- [插件功能测试](https://www.elastic.co/guide/cn/kibana/current/development-plugin-functional-tests.html)

###### 2.1 插件资源 ######

这里有一些资源可以帮助您开发插件

**我们的 IRC 频道**

很多 Kibana 开发者都在 `#kibana` 频道上的 irc.freenode.net 上玩。我们 想 帮助您开发插件。更重要的，我们 想要您的帮助 来理解您使用插件的目标，借此我们可以为您创建一个更好的插件系统。如果您从来没有用过 IRC，欢迎来玩。您可以从 [Freenode 网页客户端](http://webchat.freenode.net/?channels=kibana)开始。

**一些有用的文章**

- [贡献指南](https://github.com/elastic/kibana/blob/master/CONTRIBUTING.md)可以帮助您获得一个开发环境
- Tim Roes' 系列博客 [编写 Kibana](https://www.timroes.de/2016/02/21/writing-kibana-plugins-custom-applications/) 插件

**视频**

- [Kibana Galaxy 指南](https://www.elastic.co/elasticon/2015/sf/contributors-guide-to-the-kibana-galaxy)
- [Kibana 插件开发 - Elasticon 2016](https://www.elastic.co/elasticon/conf/2016/sf/how-to-build-your-own-kibana-plugins)

**插件生成器**

下载 [插件生成器](https://github.com/elastic/generator-kibana-plugin) 以快速生成您的插件。

**代码中的引用**

[Plugin class](https://github.com/elastic/kibana/blob/6.0/src/server/plugins/plugin.js): kibana.Plugin 类接收哪些选项？
[UI Exports](https://www.elastic.co/guide/cn/kibana/current/development-uiexports.html): 什么类型的导出是可用的？

###### 2.2 UI Exports ######

可用的 UiExport 类型列表
<table>
    <thead>
        <tr>
            <th align="left" valign="top">类型</th>
            <th align="left" valign="top">用途</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>hacks</strong></span>
                </p>
            </td>
            <td align="left" valign="top"><p>每个应用都需要包含的模块。</p></td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>visTypes</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p> 注册器通过
                    <code>ui/registry/vis_types</code> 提供的模块。
                </p>
            </td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>fieldFormats</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p> 注册器通过 <code>ui/registry/field_formats</code> 提供的模块。</p>
            </td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>chromeNavControls</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p> 注册器通过 <code>ui/registry/chrome_nav_controls</code> 提供的模块。
                </p>
            </td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>navbarExtensions</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p> 注册器通过 <code>ui/registry/navbar_extensions</code> 提供的模块。</p>
            </td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>docViews</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p> 注册器通过 <code>ui/registry/doc_views</code> 提供的模块。</p>
            </td>
        </tr>
        <tr>
            <td align="left" valign="top">
                <p>
                    <span><strong>app</strong></span>
                </p>
            </td>
            <td align="left" valign="top">
                <p>向系统添加一个应用。这个  uiExport 类型被定义为元数据的一个对象，而不仅仅是一个模块 id。</p>
            </td>
        </tr>
    </tbody>
</table>


###### 2.3 插件功能测试 ######

插件在 Kibana repo 外部运行并使用 `FunctionalTestRunner` 。在继续之前，请确认您的 Kibana 开发环境配置正确。

**编写您自己的配置**

每个工程或插件应该有自己的 `FunctionalTestRunner` 配置文件。就像 Kibana，配置文件会定义所有要加载的测试文件、服务提供者和 PageObjects，还有某些服务的配置选项。

通过复制下面的例子到 `test/functional/config.js` 文件开始测试：

```js
import { resolve } from 'path';
import { MyServiceProvider } from './services/my_service';
import { MyAppPageProvider } from './services/my_app_page;

// 允许重写默认的 kibana 目录
// 使用 KIBANA_DIR 环境变量
const KIBANA_CONFIG_PATH = resolve(process.env.KIBANA_DIR || '../kibana', 'test/functional/config.js');

// 配置文件的默认导出必须是一个配置提供程序（config provider）
// 它返回带有项目配置值的对象
export default async function ({ readConfigFile }) {

    // 读取 Kibana 配置文件，这样我们可以使用它的一些服务和 PageObjects
    const kibanaConfig = await readConfigFile(KIBANA_CONFIG_PATH);

    return {
        // 列出包含您插件测试用例的文件路径
        testFiles: [
            resolve(__dirname, './my_test_file.js'),
        ],

        // 定义在您的测试中可用的服务和提供程序，
        // 否则，只有内置的服务可用
        services: {
            ...kibanaConfig.get('services'),
            myService: MyServiceProvider,
        },

        // 就像服务那样，PageObjects 定义为提供者的名称映射
        // 在 Kibana 中合并或选择指定一个
        pageObjects: {
            management: kibanaConfig.get('pageObjects.management'),
            myApp: MyAppPageProvider,
        },

        // apps 部分定义 PageObjects.common.navigateTo(appKey) 使用的 urls
        // 为您的插件合并 Kibana 配置中定义的 url，以便使用帮助
        apps: {
            ...kibanaConfig.get('apps'),
            myApp: {
                pathname: '/app/my_app',
            }
        },

        // 选择 esArchiver 从哪里加载
        esArchiver: {
            directory: resolve(__dirname, './es_archives'),
        },

        // 选择 screenshots 保存到哪里
        screenshots: {
            directory: resolve(__dirname, './tmp/screenshots'),
        }

        // 更多设置，例如 timeouts、 mochaOpts 等定义在配置模式。参见 {blob}src/functional_test_runner/lib/config///////schema.js[src/functional_test_runner/lib/config/schema.js]
    };
}
````

现在可以在 repo 的根目录运行您插件工程的 FunctionalTestRunner 脚本。

```js
node ../kibana/scripts/functional_test_runner
````

**使用 esArchiver**

我们正在为这部分准备文档，但目前最好的资料是原始的 [pull request](https://github.com/elastic/kibana/pull/10359)。

# 限制 #

Kibana 目前有以下限制：

[嵌套字段](https://www.elastic.co/guide/cn/kibana/current/nested-objects.html)

## 嵌套字段 ##

Kibana 不能执行带嵌套字段（nested objects）的聚合操作。再查询框中执行 Lucene 查询语句的时候也不能有嵌套对象。

>    重要
>    使用 include_in_parent 和 copy_to 属性作为临时解决方案已经不再支持了。

# 版本说明 #

6.3.0
