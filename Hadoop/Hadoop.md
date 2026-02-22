# Hadoop完全分布式搭建

**版本介绍：**

> Hadoop版本：3.1.3
>
> Hbase版本：2.4.17
>
> Hive版本：3.1.3
>
> Pig版本：0.17.0
>
> Flume版本：1.9.0
>
> Sqoop版本：1.4.7
>
> ZooKeeper版本：3.6.4

## 壹、Hadoop环境搭建

### 一、虚拟机的安装

**VM VirtualBox**官网下载地址：[Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)

![6c3957d4f6ef475afd5462fc6ba1bd6](./Asset/6c3957d4f6ef475afd5462fc6ba1bd6.png)

由于最新的版本的软件安装位置只能是系统盘下，为了额外占用系统盘的空间，我使用历史版本：`7.0.12`

历史版本链接：[Download_Old_Builds_7_0 – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds_7_0)

![6dca8b6d4e52b5e8e43d17f82c0cd71](./Asset/6dca8b6d4e52b5e8e43d17f82c0cd71.png)

安装VM VirtualBox：

![f2926a8a119fb2237eac562f3c63830](./Asset/f2926a8a119fb2237eac562f3c63830.png)

**指定安装位置**，下一步：

![4d1e3cfa31398e94d1bc75fdf35370d](./Asset/4d1e3cfa31398e94d1bc75fdf35370d.png)

![7a37d7b7ec33e83e0b7137cb3508288](./Asset/7a37d7b7ec33e83e0b7137cb3508288.png)

![1834efa403d4e539488527d754be836](./Asset/1834efa403d4e539488527d754be836.png)

![0cbf3e81b778c8bc8ae67ce72c3d24b](./Asset/0cbf3e81b778c8bc8ae67ce72c3d24b.png)

等待安装：

![e7f4392966fc34cc0054bab32e0dda0](./Asset/e7f4392966fc34cc0054bab32e0dda0.png)

勾选安装后运行可以直接运行软：

![d43807dd8455123112d7328b64e16f1](./Asset/d43807dd8455123112d7328b64e16f1.png)

### 二、Linux系统镜像下载

Linux镜像文件是：`ubuntukylin-16.04desktop-amd64.iso`。

官方网址：[Ubuntu Releases](https://releases.ubuntu.com/)

下载`16.04/`版本的Linux镜像。

![3c1e0728ffb600bb65982cc07776102](./Asset/3c1e0728ffb600bb65982cc07776102.png)

选择`64`位的Linux桌面版的操作系统：

![69101852bed3648adeef5a049e754b7](./Asset/69101852bed3648adeef5a049e754b7.png)

### 三、创建虚拟机

打开`VM VirtualBox`进行新建虚拟机：

![4b4743bf766fc605ad0912bd196696f](./Asset/4b4743bf766fc605ad0912bd196696f.png)

设置虚拟机名称为`master`（主节点），设置存放路径，虚拟光盘可以暂时先不指定，类型选择`Linux`，版本选择`Ubuntu64`位的版本：

![98b480cf2729555cf2e175b43eec3f7](./Asset/98b480cf2729555cf2e175b43eec3f7.png)

因为创建的是主节点，所以分配了较多的内存空间`（4GB）`和`2`个CPU内核：

![07a4c130579929f65f952d63ded9e5b](./Asset/07a4c130579929f65f952d63ded9e5b.png)

同样为主节点分配`25GB`的硬盘空间：

![8b609af3452d33a947f8389c6e7605c](./Asset/8b609af3452d33a947f8389c6e7605c.png)

完成：

![576020265d250efed477b895570051a](./Asset/576020265d250efed477b895570051a.png)

打开`master`虚拟机的设置：

![cd49aa70f4b52ec95769806a79a04e6](./Asset/cd49aa70f4b52ec95769806a79a04e6.png)

打开存储选项：

![d98b66482b981e6bf569567ca085a3f](./Asset/d98b66482b981e6bf569567ca085a3f.png)

指定虚拟盘：

1. 点击`‘没有盘片’`
2. 选择属性中的蓝色光盘图片
3. 点击`选择虚拟盘...`

![8367bcc085c16e3e1970927ee9cfcad](./Asset/8367bcc085c16e3e1970927ee9cfcad.png)

系统配置：

1. 点击系统选项
2. 将`启动顺序`中的`软驱`取消勾选
3. 将`指点设备`更改为`PS/2鼠标`

![a24c388383e06fef767c7d0d36ef2d1](./Asset/a24c388383e06fef767c7d0d36ef2d1.png)

网络配置：

1. 点击`网络`选项
2. 启用`网卡1`
3. 将`网卡1`的连接方式设置为`仅主机（Host-Only）网络`
4. 将`混杂模式`更改为`全部允许`

![0ae5de4ebe0c108ce37cd97afa4ecf9](./Asset/0ae5de4ebe0c108ce37cd97afa4ecf9.png)

1. 启用`网卡2`
2. 将`连接方式`设置为`网络地址转换（NAT）`
3. 确定

![a1760000dc725d15b621884865982d6](./Asset/a1760000dc725d15b621884865982d6.png)

### 四、安装Linux系统

启动`master`虚拟机： 	

![09f3be860111d3197f1f743c7708bf5](./Asset/09f3be860111d3197f1f743c7708bf5.png)

选择`中文（简体）`，安装Ubuntu：

![f6fd0d0c5a73c02e710da6c3c596946](./Asset/f6fd0d0c5a73c02e710da6c3c596946.png)

继续：

![0fe4187a9031abb92df4ea42bde50aa](./Asset/0fe4187a9031abb92df4ea42bde50aa.png)

默认`清除整个磁盘并安装Ubuntu`，这里说的清楚整个磁盘并不是windows中的磁盘，而是你为虚拟机分配的磁盘空间，不会影响到windows磁盘上的其他文件，点击`现在安装`：

![9d2a145b1513cf739749ec3486f7819](./Asset/9d2a145b1513cf739749ec3486f7819.png)

继续：

![a1edbca6928d7ce65189ab474ec1207](./Asset/a1edbca6928d7ce65189ab474ec1207.png)

选择时区为`Shanghai`（上海），继续 ：

![9693245fd34ebaca815b22b9c4c601a](./Asset/9693245fd34ebaca815b22b9c4c601a.png)

选择`汉语`，继续：

![95f8ba8a166df313d640a75a8137dd9](./Asset/95f8ba8a166df313d640a75a8137dd9.png)

用户设置：

- `您的姓名`：这个原则上是写你的真实姓名，实际上可以按照自己的习惯起名即可。
- `您的计算机名`：这个是这个系统的名称，也就是你master虚拟机中Linux系统的名称。
- `选择一个用户名`：这个是使用Linux系统的用户名，设置为**hadoop**。
- `选择一个密码`：设置用户密码。
- `确认您的密码`：确认用户密码。

![5fe761308f1e8d03293d3dc5ee2288f](./Asset/5fe761308f1e8d03293d3dc5ee2288f.png)

等待系统安装：

![f6ed4334e490d419cc7a3ad4c9949bf](./Asset/f6ed4334e490d419cc7a3ad4c9949bf.png)

现在重启：

![2c69fa8c97c42a1606728a0ae24b9e2](./Asset/2c69fa8c97c42a1606728a0ae24b9e2.png)

> **重启后，可能会停留在某一个界面，如果长时间停留在一个界面，按任意键即可进入到系统中。**

输入密码，登录`hadoop`用户：

![ee74edaec0ecee5e7c680e5575a3bc3](./Asset/ee74edaec0ecee5e7c680e5575a3bc3.png)

### 五、配置增强功能

为了能更加方便的使用虚拟机，我们进行安装增强功能，然后打开共享粘贴板功能。

安装增强功能：

1. 点击`设备`。
2. 选择`安装增强功能`。
3. 在弹出的窗口中选择`运行`。

![0f1ee9b57897038b277db08da3f8264](./Asset/0f1ee9b57897038b277db08da3f8264.png)

输入用户密码，给予权限：

![625d71ee3484796b48b1e55134942b7](./Asset/625d71ee3484796b48b1e55134942b7.png)

进行等待，出现`Press Return to close this windows...`时，重启系统即可。

![222b367d20ba7a4c292c878b84414f7](./Asset/222b367d20ba7a4c292c878b84414f7.png)

1. 点击`设备`。
2. 选择`共享粘贴板`。
3. 选择`双向`。

![c74876c6dbb8dd1a2fa9cc80f25707c](./Asset/c74876c6dbb8dd1a2fa9cc80f25707c.png)

### 六、配置从节点虚拟机

从节点虚拟机，我们直接对主节点（`master`）虚拟机进行拷贝即可。

在`master`虚拟机上直接进行右键，选择复制：

![0b464425fa8e1ba2c42ece9ea6e0e74](./Asset/0b464425fa8e1ba2c42ece9ea6e0e74.png)

设置第一个从节点的虚拟机的名称为`slave1`，选择存储路径，将`MAC地址设定（O）`选项设置为：`为所有网卡从新生成MAC地址`，下一步：

![3e5d6c9c346e6f8aee661b6a5605977](./Asset/3e5d6c9c346e6f8aee661b6a5605977.png)

选择`完全复制`，完成：

![17e80850fa0f424148482545757cbf5](./Asset/17e80850fa0f424148482545757cbf5.png)

同样的操作，从master上复制第二个从节点虚拟机，名称设置为`slave2`，设定存储路径，将`MAC地址设定（O）`选项设置为：`为所有网卡从新生成MAC地址`，下一步：

![068b35de5608269642950f2292da39d](./Asset/068b35de5608269642950f2292da39d.png)

选择`完全复制`，完成：

![7fb54808d8d3d050cba068cf9edfcba](./Asset/7fb54808d8d3d050cba068cf9edfcba.png)

因为是从节点，需要的资源并没有主节点多，因此我们调整从节点的资源，将内存设置为`2GB`：

![56140be8c452d10f7de347baf2dfa6b](./Asset/56140be8c452d10f7de347baf2dfa6b.png)

将CPU设置为1个CPU核心：

![cd1cc54d53b04d0ff09078eccff5e67](./Asset/cd1cc54d53b04d0ff09078eccff5e67.png)

### 七、系统初始化配置

为三台虚拟机安装vim编译器，这样方便进行文件的操作：

```shell
sudo apt install vim
```



![703a6fb47586da4b28b221a3764fe79](./Asset/703a6fb47586da4b28b221a3764fe79.png)

#### 1. 修改主机名称

修改`/etc/hostname`文件内容：

```shell
sudo vim /etc/hostname
```

![c5ef7ca07837685490569e4ade39a87](./Asset/c5ef7ca07837685490569e4ade39a87.png)

设置主机名称为`master`：

*tips：刚进入文本时，按下`i`键进入插入模式，然后进行编辑文本；编辑结束时，按下`esc`键进入底行模式，键入`wq`进行保存并退出。*

![575db0507af3217e3b59d161bab138e](./Asset/575db0507af3217e3b59d161bab138e.png)

> 其他两个节点也进行`主机名的修改`，要将主机名称设置为相应的`slave1`和`slave2`。

重启Linux：

```shell
reboot
```

![b919fea60a6e882890a0961758a2395](./Asset/b919fea60a6e882890a0961758a2395.png)

#### 2. 添加域名映射

查看每一个节点的`IP地址`：

```shell
ifconfig
```

![460152ae18a9d440ad33cbd4d33e473](./Asset/460152ae18a9d440ad33cbd4d33e473.png)

进行编辑`\etc\hosts`文件：

![aeff309b24df681ae37d1e366a38aa2](./Asset/aeff309b24df681ae37d1e366a38aa2.png)

`hosts`内容如下，将三个节点的IP地址以及对应的系统名称添加到如下位置：

![1aec025530e735adce6391e64f2fc4e](./Asset/1aec025530e735adce6391e64f2fc4e.png)

> **每个节点都进行`域名映射`的配置。**

#### 3. 配置静态IP

查看IP地址，广播，掩码 ：

![49dddd6914550ad890339f927b736ea](./Asset/49dddd6914550ad890339f927b736ea.png)



编辑`interfaces文件`：

![0cdba9db57a6eecde1bc6eafd64f334](./Asset/0cdba9db57a6eecde1bc6eafd64f334.png)

将上面查看到的信息（包括`网卡名`、`IP地址`、`掩码`、`广播`等），这里的**网关是将IP地址的最后一位设置为1**即可，原则上写为任意的都可以，但通常情况下设置为1。

![1dba3ae5b1831454f79d685491d1435](./Asset/1dba3ae5b1831454f79d685491d1435.png)

> **每个节点都进行`静态IP`的配置。**

#### 4. 配置DNS服务

编辑`\etc\systemd\resolved.conf`文件：

![6cb3fa022d7d2c2e19aba5523a4d8de](./Asset/6cb3fa022d7d2c2e19aba5523a4d8de.png)

将`DNS`的值设置为`114.114.114.114`：

![726fb0dcf3a49aa951eafc64428eee4](./Asset/726fb0dcf3a49aa951eafc64428eee4.png)

> **每个节点都进行`DNS服务`的配置。**

#### 5. 关闭防火墙

查看防火墙：

```shell
sudo ufw status
```



![7ac05917137942c611eed934d5e0967](./Asset/7ac05917137942c611eed934d5e0967.png)

如果防火墙的状态显示`激活`，那么需要将防火墙进行关闭：

```shell
sudo  ufw disable      # 关闭防火墙
sudo ufw enable    	   # 启动防火墙
```

![2eee38a31d413d2b25084cd3c7581b4](./Asset/2eee38a31d413d2b25084cd3c7581b4.png)

> 每一个节点都需要`关闭防火墙`

#### 6. SSH免密登录

安装ssh服务端：

![31658136cad6f2771c53a777776887d](./Asset/31658136cad6f2771c53a777776887d.png)

登录本机，检验是否可以使用SSH服务：

![bb3c2b831bd7089a1ccd2ba88e1ffc8](./Asset/bb3c2b831bd7089a1ccd2ba88e1ffc8.png)

出现如下情况表示可以登录本机：

![341e957d39ccd96a359dbbc5944c720](./Asset/341e957d39ccd96a359dbbc5944c720.png)

退出本机：

![04d4b9dab0c801c31d29ba71dd163aa](./Asset/04d4b9dab0c801c31d29ba71dd163aa.png)

生成密钥：

```shell
ssh-keygen -t rsa
```

![55668df221cda10ce7060899b13f6d7](./Asset/55668df221cda10ce7060899b13f6d7.png)

将生成的密钥通过`管道`传输到文件`authorized_keys`中：

![80b4f489bac7ecbb159d5ee3f380f03](./Asset/80b4f489bac7ecbb159d5ee3f380f03.png)

传送公钥给master节点：

![43ec69154edb0067c0c936c30ab5156](./Asset/43ec69154edb0067c0c936c30ab5156.png)

> **传送公钥给`slave1`和`slave2`的前提是`slave1`和`slave2`都下载了`openssh-server`，并进行了登录本机测试。**

传送公钥从`master`传送到`slave1`节点和`slave2`节点上：

```shell
ssh-copy-id -i ~./ssh/id_rsa.pub hadoop@salve1   # 要在ssh目录下执行该命令
```

![8ac6a4616705a038666d57180b54fd8](./Asset/8ac6a4616705a038666d57180b54fd8.png)

```shell
ssh-copy-id -i ~./ssh/id_rsa.pub hadoop@salve2   # 要在ssh目录下执行该命令
```

![b7d6d2f9072837fe71c2d1700b3bf87](./Asset/b7d6d2f9072837fe71c2d1700b3bf87.png)

进行免密测试，在master主机上来连接slave1节点和slave2节点：

```shell
ssh master
ssh slave1
ssh slave2
```

![e6f2c9ace88ae5cfa9fa595b9ccfba1](./Asset/e6f2c9ace88ae5cfa9fa595b9ccfba1.png)

重启SSH服务

![757e373aa85a32783109c357e165fe4](./Asset/757e373aa85a32783109c357e165fe4.png)

> **每个节点都需要进行SSH免密连接配置。**

#### 7. 传输工具的安装

##### 下载文件传输工具(Xftp)

*xftp网址*：https://www.xshell.com/zh/xftp/

进入官网后，点击下载按钮：

![663927b1f728080f333316dd852e4b1](./Asset/663927b1f728080f333316dd852e4b1.png)

点击`免费授权页面`：

![ece9acff6fdada56aaab9d69e6c6aa3](./Asset/ece9acff6fdada56aaab9d69e6c6aa3.png)

下载XFTP，也可以将XSHELL给一并安装（*XSHELL是一款非常实用的远程终端连接工具，尤其适合需要频繁远程操作服务器的开发者和运维人员使用*），我们这个项目中暂时不用XSHELL，只下载XFTP即可：

![ce71f36decdfa6fa2aaf0448e713ed6](./Asset/ce71f36decdfa6fa2aaf0448e713ed6.png)

安装Xftp，点击下一步：

![93b03d3922a035b8d55ce7a0346dc43](./Asset/93b03d3922a035b8d55ce7a0346dc43.png)

接受条款，下一步：

![600ac8e883af6e59b1ca3037c17317d](./Asset/600ac8e883af6e59b1ca3037c17317d.png)

指定安装路径，下一步：

![09ed3f895f4a6059a3c43cf519c6eaf](./Asset/09ed3f895f4a6059a3c43cf519c6eaf.png)

直接进行安装：

![0d9f865b525f7a56acc9e8adb8adcde](./Asset/0d9f865b525f7a56acc9e8adb8adcde.png)

完成：

![52c4c1c90035df53bf723ac946caab0](./Asset/52c4c1c90035df53bf723ac946caab0.png)

打开Xftp，选择新建：

![b34970fbe83784a7e05bab078e6961a](./Asset/b34970fbe83784a7e05bab078e6961a.png)

设置会话属性，进行连接：

- `名称`：这个名称是此次连接会话的名称。
- `主机`：这个是主机的IP地址，可以写为IP地址，**也可以写为IP映射后的域名**。
- `协议`：默认*SFTP*协议。
- `端口号`：默认*22*端口号。
- `方法`：选择*Password*的方式登录。
- `用户名`：要连接虚拟机的用户名称。
- `密码`：用户密码。



![4f176d6805a1bf23ea3faddc5bc80ec](./Asset/4f176d6805a1bf23ea3faddc5bc80ec.png)

接受并保存：

![14114717fdb83f0d64a4ad821178389](./Asset/14114717fdb83f0d64a4ad821178389.png)

##### 安装XSHELL（选做）

下一步：

![a22279c6fad40a5f96f3baa90b67eae](./Asset/a22279c6fad40a5f96f3baa90b67eae.png)

接受条款，下一步：

![27786ff3d0180945425ca83e58f95aa](./Asset/27786ff3d0180945425ca83e58f95aa.png)

设置存储路径，下一步：

![a1c15460ea78eee92ebe88d3226c1ba](./Asset/a1c15460ea78eee92ebe88d3226c1ba.png)

安装：

![c7f602f2822a643b7c3d5e755865e1a](./Asset/c7f602f2822a643b7c3d5e755865e1a.png)

完成：

![c5e1f2494f689b4a99473a6262dc872](./Asset/c5e1f2494f689b4a99473a6262dc872.png)

选择`后来`即可进入：

![e23a9f578b87e98d4ba007e16421022](./Asset/e23a9f578b87e98d4ba007e16421022.png)

与Xftp一致，选择新建：

![6843ab4aa9defe3e3774baf9b028337](./Asset/6843ab4aa9defe3e3774baf9b028337.png)

常规的配置：

- 名称：此次连接的名称。
- 协议：默认`SSH`协议即可。
- 主机：要连接的主机的IP地址，**也可以写为IP映射后的域名**。
- 端口号：默认`22`即可。
- 互联网协议版本：选择为自动即可。

![b92baba816aaf3164486eb681f04d3e](./Asset/b92baba816aaf3164486eb681f04d3e.png)

点击用户身份验证选项：

- `用户名`：要连接虚拟机中的用户名称。
- `密码`：对应的用户密码。
- `方法`：选择`Password`即可。

![83a65dca472f039f79b2187314f6afd](./Asset/83a65dca472f039f79b2187314f6afd.png)

#### *. 重启后掉网卡的解决办法：

```shell
sudo dhclient enp0s3   # 这里的enp0s3是掉的网卡的名称。
sudo ifconfig enp0s3   # 这里的enp0s3是掉的网卡的名称。
```

![aa5b03f9151e39ab674e1956c75e91f](./Asset/aa5b03f9151e39ab674e1956c75e91f.png)

### JDK的安装：

在`master`主机上创建`Downloads`文件夹，用于存放传输的文件。

![977f16bc9707c3eed6cd0a40fdcd6ff](./Asset/977f16bc9707c3eed6cd0a40fdcd6ff.png)

*JDK官网地址*：https://www.oracle.com/java/technologies/downloads/?er=221886#java8

选择`x64`版本的jdk下载即可：

![197f4eb53426e51f6554bbe4ab5be06](./Asset/197f4eb53426e51f6554bbe4ab5be06.png)

将下载好的JDK通过`Xftp`传输到`master`的`Downloads`文件夹中：

![9a3cd0b773703ef4c897bf7c22783bc](./Asset/9a3cd0b773703ef4c897bf7c22783bc.png)

为用户分配权限，编辑`/etc/sudoers`文件：

![71e1424ba52af988902a38b63b2a1aa](./Asset/71e1424ba52af988902a38b63b2a1aa.png)

修改的文件内容如下：

![1f8ca69ab8fceb752f87cb30e5ca77b](./Asset/1f8ca69ab8fceb752f87cb30e5ca77b.png)

为hadoop用户添加hadoop组：

```shell
sudo usermod -a -G hadoop hadoop
```

![22474cc5938035c122585c3840d0780](./Asset/22474cc5938035c122585c3840d0780.png)

解压JDK到`/usr/local`路径下：

```shell
sudo tar -zxvf jdk-8u411-linux-x64.tar.gz -C /usr/local
```

![0c78339700602cb1726258f208ff7d9](./Asset/0c78339700602cb1726258f208ff7d9.png)

修改JDK名称：

```shell
sudo mv jdk1.8.0_411/ ./jdk1.8.0
```

![01e670bd85ad1733ab1bd0948cc2a0a](./Asset/01e670bd85ad1733ab1bd0948cc2a0a.png)

添加环境变量，在`/etc/profile.d`目录下新建一个`java.sh`文件：

![249a136910a3ae720a0ab5b58434779](./Asset/249a136910a3ae720a0ab5b58434779.png)

`java.sh`文件内容如下：

![34218a598b63b0cbea3a84efc9b29c2](./Asset/34218a598b63b0cbea3a84efc9b29c2.png)

刷新一下环境变量，然后查看java版本，如果出现java版本，则表示JDK已经安装成功：

```shell
source /etc/profile
java -version
```

![26324ba4d461ea37999aeb157cccd35](./Asset/26324ba4d461ea37999aeb157cccd35.png)

> 另外两个节点也需要安装JDK，我们通过SSH传输的方式将JDK复制到其他两个节点上。

将JDK复制到slave1主机上：

```shell
ssh slave1
sudo chmod -R 777 /usr/local
exit
sudo scp -r /usr/local/jdk1.8.0/ hadoop@slave1:/usr/local/
```

![46d75daa279f3a601a120f307ed7832](./Asset/46d75daa279f3a601a120f307ed7832.png)

> **同样将JDK复制到`slave2`中去。**

将JDK的环境复制到`slave1`中：

```shell
ssh slave1
sudo chmod -R 777 /etc/profile.d
exit
sudo scp -r /etc/profile.d/java.sh hadoop@slave1:/etc/profile.d/java.sh
```

![c28009eba8e48cadc7dcc63065f1e25](./Asset/c28009eba8e48cadc7dcc63065f1e25.png)

> **同样将环境变量复制到`slave2`中去。**

连接到slave1主机上，刷新环境变量，查看java版本：

![201cdca842fadd9e48d5edc98d807fe](./Asset/201cdca842fadd9e48d5edc98d807fe.png)

> **同理，连接到slave2上，刷新环境变量，查看java版本。**

## 贰、分布式环境配置

### 一、下载安装Hadoop

Hadoop官网地址：https://archive.apache.org/dist/hadoop/common/hadoop-3.1.3/

选择Hadoop进行下载：

![6d9f5130b416599d52f527f65752c6a](./Asset/6d9f5130b416599d52f527f65752c6a.png)

下载后，将Hadoop传输到master的Downloads文件夹下：

![ee6ba99a00b453f1cdaabf286d38cbf](./Asset/ee6ba99a00b453f1cdaabf286d38cbf.png)

将Hadoop解压到`/usr/local`目录下：

```shell
tar -zxvf hadoop-3.1.3.tar.gz -C /usr/local
```

![f60e59b4ce3bda7cfc83bb3a04137d4](./Asset/f60e59b4ce3bda7cfc83bb3a04137d4.png)

查看Hadoop：

![fe446245b4966a502fd8007f49173d8](./Asset/fe446245b4966a502fd8007f49173d8.png)

重命名Hadoop，并且更改Hadoop文件的所属用户：

![9f466c8b5c184714468cf2f08479d71](./Asset/9f466c8b5c184714468cf2f08479d71.png)

配置Hadoop的环境变量，在`/etc/profile.d`目录下创建`hadoop.sh`文件：

![7f9b5189e5ef3fc1293cc569960fd02](./Asset/7f9b5189e5ef3fc1293cc569960fd02.png)

`hadoop.sh`文件内容如下：

![ea9a3020e7384f43d3289e51aaa94d1](./Asset/ea9a3020e7384f43d3289e51aaa94d1.png)

刷新环境变量，并且查看Hadoop版本，如果正常出现Hadoop版本，说明Hadoop已经配置成功：

![f0ac600c5bd64467110897880ccca8d](./Asset/f0ac600c5bd64467110897880ccca8d.png)

> 小计：每次配置完环境变量的时候都要进行刷新，并且要在刷新过后的终端窗口执行该组件的命令，如果在一个没有刷新环境变量的窗口进行执行该组件的命令，会出现错误，然后只有重启Linux才能将环境变量应用为全局的，重启过后即可在任意终端运行该组件的命令。

新建临时文件夹来存放Hadoop的临时文件：

```shell
sudo mkdir -p /usr/data/hadoop/tmp
```

![72263971c2e8d492b67de9511cb25ff](./Asset/72263971c2e8d492b67de9511cb25ff.png)

修改文件权限为hadoop用户权限：

![aed6e460dd903747ab7fcedd5fb31c8](./Asset/aed6e460dd903747ab7fcedd5fb31c8.png)

### 二、配置Hadoop

**Hadoop存放的配置文件在：`/usr/local/hadoop/etc/hadoop`目录中**

![93bd66bb21aa083e0f0f062942fed9f](./Asset/93bd66bb21aa083e0f0f062942fed9f.png)

编辑`hadoop-env.sh`文件：

![59de19dfae50fd993332d3383048f05](./Asset/59de19dfae50fd993332d3383048f05.png)

刚进入文件时，输入英文冒号，然后输入`set nu`可以显示行号：

![5c1176ac160b627d4caca7aa4a5cc74](./Asset/5c1176ac160b627d4caca7aa4a5cc74.png)

修改JAVA路径：

![27094cdc57c67735624beb53d206de6](./Asset/27094cdc57c67735624beb53d206de6.png)

编辑`core-site.xml`文件：

![7fa5ce4453cd709dcc3dc4854bae831](./Asset/7fa5ce4453cd709dcc3dc4854bae831.png)

文件内容编辑如下：

![701c1f6e5c79464f9e6f41bbd88a6fd](./Asset/701c1f6e5c79464f9e6f41bbd88a6fd.png)

编辑`hdfs-site.xml`文件：

![628aa219b37fdd7fe02c2ead2b69eba](./Asset/628aa219b37fdd7fe02c2ead2b69eba.png)

文件内容如下：

![41e6b95e5248c7209409b356743d589](./Asset/41e6b95e5248c7209409b356743d589.png)

编辑`mapred-site.xml`文件：

![271f6ac41e7a5f14bb838d000bd13a5](./Asset/271f6ac41e7a5f14bb838d000bd13a5.png)

文件内容如下：

![e6fc0720fa2490649af1fbda5f19816](./Asset/e6fc0720fa2490649af1fbda5f19816.png)

编辑`yarn-site.xml`文件：

![e51636c48305eb3ea2286947452778c](./Asset/e51636c48305eb3ea2286947452778c.png)

文件内容如下：

![c170f852537aeae43540d4ddf045880](./Asset/c170f852537aeae43540d4ddf045880.png)

指定从节点：

![49b1e5f5f5dabb00f01ea7cd59176ab](./Asset/49b1e5f5f5dabb00f01ea7cd59176ab.png)

内容如下：

![46369eb924cb98d1342ad37f5ffde4d](./Asset/46369eb924cb98d1342ad37f5ffde4d.png)

再次刷新一次Hadoop的环境变量：

![6a01f38962b4e4dfd5d2bcc2a943ce8](./Asset/6a01f38962b4e4dfd5d2bcc2a943ce8.png)

格式化HDFS：

![900a7ccb5b9e8e70eabb9bcff65d64e](./Asset/900a7ccb5b9e8e70eabb9bcff65d64e.png)

出现以下的日志则表示格式化成功：

![31ff9cd292176d48efa4c199e1cdb73](./Asset/31ff9cd292176d48efa4c199e1cdb73.png)

配置从节点的Hadoop配置文件：

1. 首先连接到`slave1`节点
2. 更改`/usr/local/`权限

![741c9faed872f2306e6e9ff740c637c](./Asset/741c9faed872f2306e6e9ff740c637c.png)

推出slave1节点：

![69d565ba85f57b303c21b31685ed995](./Asset/69d565ba85f57b303c21b31685ed995.png)

> slave2节点也需要配置`/usr/local/`目录的权限。

新建临时文件：

1. 连接到slave1节点上
2. 创建多级目录`/usr/data/hadoop/tmp`

![2f67b1791694dd13d9bd0857751fd75](./Asset/2f67b1791694dd13d9bd0857751fd75.png)

修改文件权限：

![a956107544b58ff3eec7ec1cb2fe74a](D:\Study\Data\Code\JPFile\练习题\a956107544b58ff3eec7ec1cb2fe74a.png)

查看`data`文件夹权限：

![2be769139f30dbb1567e7fb4c7a0f65](./Asset/2be769139f30dbb1567e7fb4c7a0f65.png)

> slave2权限也需要配置文件夹权限

配置从节点的环境变量，从master节点上传输`hadoop.sh`文件到slave1节点的`/etc/profile.d`路径下：

![713ba2384922341996e1e95ad01c5e0](./Asset/713ba2384922341996e1e95ad01c5e0.png)

连接到slave1节点，并且刷新一下环境变量，查看Hadoop版本，检查Hadoop是否配置成功：

![a558cf3edd0c01d3a5ca09e80484c6f](./Asset/a558cf3edd0c01d3a5ca09e80484c6f.png)

> slave2也需要进行环境变量的配置，方法与slave1一样。

在master节点上再次刷新一次环境变量：

![e06c19a26d80724b046f54f9aa278fa](./Asset/e06c19a26d80724b046f54f9aa278fa.png)

启动Hadoop，并且检查是否启动成功：

1. 启动Hadoop
   ```shell
   start-all.sh
   ```

2. 检查是否启动成功
   ```shell
   jps
   ```

![70865fdc84b6c9320e51288ed4a5565](./Asset/70865fdc84b6c9320e51288ed4a5565.png)

## 叁、HDFS

启动三个虚拟机，并打开Hadoop：

![5289762b768518cfbd57918e29296b0](./Asset/5289762b768518cfbd57918e29296b0.png)

使用浏览器打开HDFS：

- 在浏览器中输入：主节点（master）的IP地址+端口号（9870）即可进入到HDFS管理界面

```shell
ifconfig     # 查看网卡信息
192.168.56.101:9870      # inet地址+端口号
```

![414c243cca1d1e24ecdda149f2d5d2e](./Asset/414c243cca1d1e24ecdda149f2d5d2e.png)

打开的浏览器界初始界面如下：

![e2d6d1613ddd1d04248a335933bd17e](./Asset/e2d6d1613ddd1d04248a335933bd17e.png)

## 肆、MAPREDUCE

我们在编写MAPREDUCE的时候需要JAVA编程进行编写，这里我使用的是在Windows中进行写JAVA编程对虚拟机上的HDFS的分布式数据库进行操作

### 一、IDEA的安装与配置

我们使用的编译器是`IntelliJ IDEA`，具体的安装教程如下参考下面的连接：

`IDEA`安装教程：https://blog.csdn.net/weixin_61034701/article/details/132134691?spm=1001.2014.3001.5506

### 二、Maven的安装与配置

Maveb官网：https://maven.apache.org/

找到官网首页找到右边的`Download`链接：

![620123e43ad7491700f801824c5bab4](./Asset/620123e43ad7491700f801824c5bab4.png)

找到`legacy`，并且点击该超链接：

![6256d4a4a65e6467e9442be3b1ddace](./Asset/6256d4a4a65e6467e9442be3b1ddace.png)

点击`Parent Direcotory`链接：

![5bea801138d7192f1cb50bb7dbe894c](./Asset/5bea801138d7192f1cb50bb7dbe894c.png)

找到`maven-3/`，点击该链接：

![db8326a1ba9d4828d59988a74777284](./Asset/db8326a1ba9d4828d59988a74777284.png)

找到`3.6.3`版本，点击进入：

![06b4fc19fa0128a612a78450b36d0c4](./Asset/06b4fc19fa0128a612a78450b36d0c4.png)

选择`binaries`链接，进入：

![498cfdeac8450d9f3d6345200c3dbd4](./Asset/498cfdeac8450d9f3d6345200c3dbd4.png)

下载`apache-maven-3.6.3-bin.zip`：

![9a2372ab6ecfcf50822af0ef92359e6](./Asset/9a2372ab6ecfcf50822af0ef92359e6.png)

**下载好后直接解压到需要存放的位置即可**

新建一个Maven仓库，用于存放下载的文件，这个仓库的位置可以放在任何一个合适的路径下，但通常我们放在`Maven`软件内部，这样的好处是方便管理：

![7cdebcf5e0c245db5bbe5c468242e1e](./Asset/7cdebcf5e0c245db5bbe5c468242e1e.png)

打开`Maven`中的`conf/settings.xml`文件，修改以下内容：

1. 修改仓库的地址：

![79a214dbdb23223e96599cfdb35809b](./Asset/79a214dbdb23223e96599cfdb35809b.png)

2. 修改镜像地址，这样做的好处是可以更快的从远程的仓库中拉去模块：

![86b0b61184b5e4433c12bc82088ab69](./Asset/86b0b61184b5e4433c12bc82088ab69.png)

3. 修改JDK为Windows上的JDK，这里我Windows上安装的是`JDK1.8`版本的：

![f458c7f344fd9c1695fb1b02470cdf3](./Asset/f458c7f344fd9c1695fb1b02470cdf3.png)

配置环境变量，点击`win`键，搜索环境变量：

![4a49475ef5f5abacefc3ff2ca56bd6b](./Asset/4a49475ef5f5abacefc3ff2ca56bd6b.png)

进行如下操作，将`Maven`的`bin`目录添加到系统环境变量中去：

![94adec5452e3f02d917b62364920442](./Asset/94adec5452e3f02d917b62364920442.png)

在终端输入`mvn -v`，查看是否安装成功，如果正确出现版本号则说明创建成功了：

![f03a3706447cbd3d8db7d6adb33811b](./Asset/f03a3706447cbd3d8db7d6adb33811b.png)

打开IDEA的`Setting`，将IDEA的Maven换成我们自己的Maven，进行如下修改：

![c3dd0e3eedbab873468adaa70ef2165](./Asset/c3dd0e3eedbab873468adaa70ef2165.png)

在以后创建项目时，我们要求默认使用我们本地的Maven，因此需要进行如下配置：

![abc606a4b867ad5b9011d057e696587](./Asset/abc606a4b867ad5b9011d057e696587.png)

其说明与上面的一致：

![58a7ecae5ec72fbe3fcc700565930fb](./Asset/58a7ecae5ec72fbe3fcc700565930fb.png)

### 三、新建Maven项目

![64c9310c5a8eaea7daf69aabb990474](./Asset/64c9310c5a8eaea7daf69aabb990474.png)

选择Maven，勾选`Create from archetype`，选择`maven-archetype-quickstart`，NEXT：

![ccf2dc14f02143e58e89d5b255765e7](./Asset/ccf2dc14f02143e58e89d5b255765e7.png)

设置项目名称，设置项目的存储路径：

![fdc772326f597bb5329b2d5cd650c86](./Asset/fdc772326f597bb5329b2d5cd650c86.png)

检查配置，进行下一步：

![79a9fa69aeb8393addeffea3d107b5c](./Asset/79a9fa69aeb8393addeffea3d107b5c.png)

在`pom.xml`中添加一下依赖：

![e017de1a4e00ebe54e627c8d85d4162](./Asset/e017de1a4e00ebe54e627c8d85d4162.png)

点击该按钮进行构建项目：

![7e463088f5363aa77888679c6097718](./Asset/7e463088f5363aa77888679c6097718.png)

### 四、额外的配置：

> 如果需要在windows上对linux上的hadoop集群进行java代码操作，需要进行额外的下载配置：
>
> *GitHub地址： https://github.com/cdarlint/winutils*
>
> *如果打不开GitHub，就用这个链接：  https://gitcode.com/steveloughran/winutils/overview?utm_source=csdn_github_accelerator&isLogin=1*
>
> **下载之后，选择与你的Hadoop版本最接近的，但是不能大于你的Hadoop版本的文件**

克隆GitHub仓库网址：

![f7d0bb22c70a6e9d86ee314766a4ea5](./Asset/f7d0bb22c70a6e9d86ee314766a4ea5.png)

在一个合适的目录下输入`cmd`，用于下载仓库项目：

![713552bcc62bd6a81b0b15e65ba2fb9](./Asset/713552bcc62bd6a81b0b15e65ba2fb9.png)

进行克隆项目：

```powershell
git clone '项目地址'
```

![eb2a2ecaff2e423dd33fe321f54ffa0](./Asset/eb2a2ecaff2e423dd33fe321f54ffa0.png)

下载仓库后，找到`3.1.2`版本的仓库，因为我使用的Hadoop版本是`3.1.3`，`3.1.2`与我的Hadoop版本最接近：

![53f9e8aa41749a9b8513cab65b08f33](./Asset/53f9e8aa41749a9b8513cab65b08f33.png)

配置环境变量，直接在系统变量中进行新建：

![cc0c8a20157f4d1f8d9c90dfb8895c1](./Asset/cc0c8a20157f4d1f8d9c90dfb8895c1.png)

进行如下配置，重启IDEA：

![192a87a34fdc05ce27ee25d01966a4f](./Asset/192a87a34fdc05ce27ee25d01966a4f.png)

### 五、EmployeeSort

在`master`虚拟机中，输入一下命令，在HDFS上创建多级目录，`inputs`目录用于存储待处理的文件：

```shell
hdfs dfs -mkdir -p /user/hadoop/inputs
hdfs dfs -ls		# 这个命令是直接定位到/user/hadoop/目录下的文件的
```

![6cbe51e94885261393d7882468908ad](./Asset/6cbe51e94885261393d7882468908ad.png)

打开HDFS的浏览器界面，点击`Utiltiles -> Browse the file system`：

![d0cfb0268151335d71d9ed48684c5c9](./Asset/d0cfb0268151335d71d9ed48684c5c9.png)

进入创建的目录里面，进行上传文件：

![95144a10bb273bda2f1e8487cece5c6](./Asset/95144a10bb273bda2f1e8487cece5c6.png)

上传`cmp.csv`文件：

![49e5268e2137a6104859e72317e418e](./Asset/49e5268e2137a6104859e72317e418e.png)

在主节点使用命令进行创建outputs文件，outputs文件用于存储处理过后的文件：

```shell
hdfs dfs -mkdir /user/hadoop/outputs
hdfs dfs -ls     # 这个命令是直接定位到/user/hadoop/目录下的文件的
```

![463fa27b292407de649de682543f374](./Asset/463fa27b292407de649de682543f374.png)

## 伍、Hbase

### 一、下载Hbase

Hbase官网地址：https://hbase.apache.org/

找到`Downloads`选项并进入：

![79f477032b7a8895a894a49f9807e2d](./Asset/79f477032b7a8895a894a49f9807e2d.png)

找到`Apache Archive`并进入：

![692d4c7ac1437ae54f646f136c8b22e](./Asset/692d4c7ac1437ae54f646f136c8b22e.png)

找到`2.4.17/`版本，点击：

![aa783d1d4140d85bc7fcb4e092116ec](./Asset/aa783d1d4140d85bc7fcb4e092116ec.png)

找到如下链接进行下载：

![081493e47abcda141e255391a10a7be](./Asset/081493e47abcda141e255391a10a7be.png)

### 二、安装Hbase

将下载好的Hbase上传到master节点的Downloads文件中：

![287790fe54e54cd410fafdac748eb26](./Asset/287790fe54e54cd410fafdac748eb26.png)

打开`master`虚拟机，找到`hbase-2.4.17-bin.tar.gz`文件，将其解压到`/usr/local/`目录下：

![d6fbdc9bba3934c15cd165177b36470](./Asset/d6fbdc9bba3934c15cd165177b36470.png)

重命名为`habse`：

![40263f3f5b9c9f15cd5d61c5f335c09](./Asset/40263f3f5b9c9f15cd5d61c5f335c09.png)

在`hbase`目录下创建`zookeeper`目录：

![4983b22340aa7e9c5d1c9a76aad22f7](./Asset/4983b22340aa7e9c5d1c9a76aad22f7.png)

配置环境变量，创建`hbase.sh`文件：

![4557267475da752e4b6d347c6e9acb1](./Asset/4557267475da752e4b6d347c6e9acb1.png)

`hbase.sh`文件的内容如下：

![29a26673d040fbeebe3f573cfcce408](./Asset/29a26673d040fbeebe3f573cfcce408.png)

刷新环境变量，查看版本，如果出现`hbase`版本说明配置成功了：

![53b2d46444eb0aa8e750605fe920457](./Asset/53b2d46444eb0aa8e750605fe920457.png)

发现虽然成功安装配置`hbase`环境变量，但是出现了两个冲突的`jar`包：

![9ffc3a21ad69698cd0aeb4bca36a9bf](./Asset/9ffc3a21ad69698cd0aeb4bca36a9bf.png)

修改`hbase`的对应路径下的jar包名称即可，找到报错路径下的jar包：

![f497bea66b017a78353cf3715a7d3b1](./Asset/f497bea66b017a78353cf3715a7d3b1.png)

修改jar包的名称：

![5c282bbab239faf0a977857af2b6ca0](./Asset/5c282bbab239faf0a977857af2b6ca0.png)

重新查看hbase的版本，注意，如果在配置好hbase后，虚拟机没有重启，需要在hbase目录下查看hbase的版本，如果电脑重启之后，可以在任意目录下查看hbase命令：

![752fa67aa87195497b245f5941327b6](./Asset/752fa67aa87195497b245f5941327b6.png)

### 四、配置Hbase

进入到`hbase`目录下的`conf`目录里面，编辑`hbase-env.sh`文件：

![a6a6b591897947928481df6668b3349](./Asset/a6a6b591897947928481df6668b3349.png)

修改`Java`的路径：

![c777551692305aa1a1be206dea308e1](./Asset/c777551692305aa1a1be206dea308e1.png)

修改`HBASE_MANAGES_ZK`的值为`true`

![14fe3d070cf0f31ed69c1122d189974](./Asset/14fe3d070cf0f31ed69c1122d189974.png)

修改`hbase-site.xml`文件：

![1792dd5875647f14b8412218506929c](./Asset/1792dd5875647f14b8412218506929c.png)

修改的内容如下：

![8ea82fac437f6bfb97ce87190042bfb](./Asset/8ea82fac437f6bfb97ce87190042bfb.png)

编辑`regionservers`文件：

![0b8190283077d361acc9ae17a3e21e2](./Asset/0b8190283077d361acc9ae17a3e21e2.png)

内容如下：

![c7489110180afa7557aab3220154b4d](./Asset/c7489110180afa7557aab3220154b4d.png)

将主节点的`hbase`复制到从节点：

1. 复制到slave1节点中：

![860c55574c8e0f59ecdbd64407f5131](./Asset/860c55574c8e0f59ecdbd64407f5131.png)

2. 复制到slave2节点中：

![8f5081e303a6ff46cfaaf71fa33a21a](./Asset/8f5081e303a6ff46cfaaf71fa33a21a.png)

修改Hbase文件权限：

![b6789ba16885486ba654de2d791e7d3](./Asset/b6789ba16885486ba654de2d791e7d3.png)

### 五、使用Hbase

在master上启动hbase：

![055d802d217b343f8c0fe8abeb9645e](./Asset/055d802d217b343f8c0fe8abeb9645e.png)

> 一个能减少错误的方法是将`master`的`hbase/lib/client-facing-thirdparty/slf4j-reload4j-1.7.33.jar`给换名，然后`slave1`和`slave2`节点上的`jar`包的名字不用换名，这个方法能够解决`SLF4J`报错的问题

检查Hbase是否启动成功：

![8930eab87af82b2421d9752fb7a63f6](./Asset/8930eab87af82b2421d9752fb7a63f6.png)

打开hbase的shell：

![ccfd21fc27c589f6f630c1b309a267c](./Asset/ccfd21fc27c589f6f630c1b309a267c.png)

查看所有的命名空间：

![47cae4af26e2d285f9596ca7a86d65c](./Asset/47cae4af26e2d285f9596ca7a86d65c.png)

创建命名空间，并查看创建的命名空间：

![9a02338dacd52431f916e022a471a06](./Asset/9a02338dacd52431f916e022a471a06.png)

删除命名空间，并检查是否删除了命名空间：

![81031d818c33a600e90dca595b499b7](./Asset/81031d818c33a600e90dca595b499b7.png)

退出hbase的shell：

![05e2a915bcbf3b2ca69f77a028a5946](./Asset/05e2a915bcbf3b2ca69f77a028a5946.png)

## 陆、Hive

### 一、下载Hive

Hive官网地址： https://dlcdn.apache.org/hive/

找到`hive-3.1.3`版本，进入文件：

![05294b4efb4e5d1e240c0ef1edadefc](./Asset/05294b4efb4e5d1e240c0ef1edadefc.png)

下载`apache-hive-3.1.3-bin.tar.gz`即可：

![2dadd955259fe54e712b565c691e935](./Asset/2dadd955259fe54e712b565c691e935.png)

### 二、安装Hive

上传hive到master节点上：

![c0894434f82052d3b403c374a55bbff](./Asset/c0894434f82052d3b403c374a55bbff.png)

将文件解压到`/usr/local`目录下：

![e96acc34329963c7323b1fc65f6180b](./Asset/e96acc34329963c7323b1fc65f6180b.png)

重命名为`hive`：

![e43e42db3d518e9693c090169d1ce0b](./Asset/e43e42db3d518e9693c090169d1ce0b.png)

添加环境变量，创建`hive.sh`文件：

![67d614aad5643027cdbe245088f83bf](./Asset/67d614aad5643027cdbe245088f83bf.png)

`hive.sh`文件的内容如下：

![d39b67c36e655ad0a7ce12c4871a6b3](./Asset/d39b67c36e655ad0a7ce12c4871a6b3.png)

将hive的`guava-19.0.jar`包进行删除，但是更好的办法是将其重命名，使其失效即可：

![a644833b91103e2015d68c6bc50ae75](./Asset/a644833b91103e2015d68c6bc50ae75.png)

将`/usr/local/hadoop/share/hadoop/common/`目录下的`guava-27.0-jre.jar`复制到`hive/lib`目录下：

![5a124981b70363e742c7b0e8c7c7ddd](./Asset/5a124981b70363e742c7b0e8c7c7ddd.png)

为了避免再次报`SLF4J`的错误，我们直接将`hive`和`Hadoop`中较低版本的`log4j`jar包进行（重命名/删除），这里我们删除的是`hive/lib`中的`log4j-slf4j-impl-2.17.1.jar`文件：

![e30da8acdd3737201878eb92b5af391](./Asset/e30da8acdd3737201878eb92b5af391.png)

查看Hadoop中的`log4j`版本：

![66ab1a1387660eb2ff671799cf8de98](./Asset/66ab1a1387660eb2ff671799cf8de98.png)

重命名hive中的`log4j`：

![5720a1754d3f632eeaab0c5ea680e2e](./Asset/5720a1754d3f632eeaab0c5ea680e2e.png)

查看`hive`的版本：

![aaf1bb0efca63ded3b2af79e8c817d3](./Asset/aaf1bb0efca63ded3b2af79e8c817d3.png)

### 三、配置Hive

编辑`hive`中`conf`目录下的`hive-site.xml`文件：

![85460e998cbd8bf36b6bb7ca0f79a20](./Asset/85460e998cbd8bf36b6bb7ca0f79a20.png)

具体的内容如下：

![abc21b423e8cd2462c7b86678197d81](./Asset/abc21b423e8cd2462c7b86678197d81.png)

### 四、安装mysql

安装mysql：

```shell
sudo apt-get install mysql-server
```

![7f7d57cdf45b5657d732ba0e93f286d](./Asset/7f7d57cdf45b5657d732ba0e93f286d.png)

设置MySQL密码：

![7ad7be72280452d5f5cfba0e8fb7be9](./Asset/7ad7be72280452d5f5cfba0e8fb7be9.png)

启动mysql服务：

![d016268dad4d2f680e431a4349755a5](./Asset/d016268dad4d2f680e431a4349755a5.png)

输入用户密码：

![ec2dec9224d77c44e23397eda051fae](./Asset/ec2dec9224d77c44e23397eda051fae.png)

检查是否启动了MySQL服务：

![8729bd64387558416c678052e962175](./Asset/8729bd64387558416c678052e962175.png)

下载MySQL的JDBC：

![d173d1f32b88ace5290ab1fb393bc36](./Asset/d173d1f32b88ace5290ab1fb393bc36.png)

将`mysql-connecter-java-5.1.45.tar.gz`上传到`master`节点上：

![2690a3fdb6dc9e23689bca40cd8e63d](./Asset/2690a3fdb6dc9e23689bca40cd8e63d.png)

将`mysql-connecter-java-5.1.45.tar.gz`进行解压：

![e721acee0cf9d776e62aa0d9d08193c](./Asset/e721acee0cf9d776e62aa0d9d08193c.png)

进入到`mysql-connecter-java-5.1.45`中，找到`mysql-connecter-java-5.1.45-bin.jar`，将其复制到`/usr/local/hive/bin`目录下：

![0b903376cbb544114644eddd74671c8](./Asset/0b903376cbb544114644eddd74671c8.png)

进入到MySQL中：

```mysql
mysql -uroot -p
```

![5f52c0c265e94d0945a9838cc6fda23](./Asset/5f52c0c265e94d0945a9838cc6fda23.png)

在`/user/hadoop`目录下点击文件夹图标，进行创建目录：

![4f22939f12c1db40ddfff18e6e44a22](./Asset/4f22939f12c1db40ddfff18e6e44a22.png)

创建`data`目录：

![49b9e77064e0b24078f6ef8f7367535](./Asset/49b9e77064e0b24078f6ef8f7367535.png)

进行上传文件：

![9f02a8cdcf8e2abacf22b2a18b8d246](./Asset/9f02a8cdcf8e2abacf22b2a18b8d246.png)

将`mysql-connector-java-5.1.45-bin.jar`复制到`/usr/local/hive/lib`目录下：

![5f46b81def008d5d3bb61d325635564](./Asset/5f46b81def008d5d3bb61d325635564.png)

初始化数据库：

```shell
schematool -dbType mysql -initSchema
```

![6dadc407fde7033e9144f1a448ebb6b](./Asset/6dadc407fde7033e9144f1a448ebb6b.png)

### 五、使用Hive

#### 额外配置

如果启动hive的时候出现大量的警告，像下图显示的日志，我们需要进行额外的配置：

![f26ebfb23d2720936336fcd6641dfd1](./Asset/f26ebfb23d2720936336fcd6641dfd1.png)

在`/usr/local/hive/conf`目录下创建`log4j.properties`文件：

![1b94c9bf8ce3ab6f83a8e5d0c3116a2](./Asset/1b94c9bf8ce3ab6f83a8e5d0c3116a2.png)

编辑内容：

![71890b6c2a844f154f70c2c85b007e5](./Asset/71890b6c2a844f154f70c2c85b007e5.png)

启动HIVE：

![87f9d327c47e5e5ad6705d54135f3c8](./Asset/87f9d327c47e5e5ad6705d54135f3c8.png)

在`/usr/hadoop/data`中上传`dept.csv`文件和`emp.csv`文件：

![579f98499cd0fc1fb47df2afec2d5b5](./Asset/579f98499cd0fc1fb47df2afec2d5b5.png)

在HIVE中进行新建员工表和部门表：

![189cb28cb094a1d00758e78a741a66e](./Asset/189cb28cb094a1d00758e78a741a66e.png)

将`emp.csv`文件和`dept.csv`文件分别导入到员工表和部门表中：

```hive
load data inpath '/user/hadoop/data/emp.csv' into table emp001;
load data inpath '/user/hadoop/data/dept.csv' into table dept001;
```

![01eeac69b2a17296357350d77ea3520](./Asset/01eeac69b2a17296357350d77ea3520.png)

查看表中的数据：

```hive
select * from emp001;
select * from dept001;
```

![2ea00836497ebe3286d3de404135b9d](./Asset/2ea00836497ebe3286d3de404135b9d.png)

## 柒、Pig

### 一、下载Pig

Pig下载地址： https://dlcdn.apache.org/pig/pig-0.17.0/

![cc8ca44f0c33ba961d98f26b766994a](./Asset/cc8ca44f0c33ba961d98f26b766994a.png)

上传到master节点中：

![f08fcaaaf793b88f0dbbe5a0e0ad5d8](./Asset/f08fcaaaf793b88f0dbbe5a0e0ad5d8.png)

### 二、安装Pig

解压`pig`到`/usr/local`路径下：

![df1ea98a70ccd7fc7504ad4d707dc33](./Asset/df1ea98a70ccd7fc7504ad4d707dc33.png)

重命名为pig：

![26bf23565e2784902db0c7ea0be839c](./Asset/26bf23565e2784902db0c7ea0be839c.png)

配置环境变量，新建`pig.sh`文件：

![f4eac6310e4d2d249e86698a7b097d8](./Asset/f4eac6310e4d2d249e86698a7b097d8.png)

其内容如下：

![ca0d6a3fd01d9fd29383dccf25a7532](./Asset/ca0d6a3fd01d9fd29383dccf25a7532.png)

应用环境变量，查看pig版本，检查是否安装成功：

![4a4691cd481f990a72328cc49da17ba](./Asset/4a4691cd481f990a72328cc49da17ba.png)

启动Hadoop和Yarn，并检查是否启动成功：

![25727d831cc5b6a812017c37659106c](./Asset/25727d831cc5b6a812017c37659106c.png)

### 三、使用Pig

启动pig服务器模式：

![3e356b7f9d06ff95cf9606ba542adf1](./Asset/3e356b7f9d06ff95cf9606ba542adf1.png)

加载HDFS上的文件：

![ea3cfd4ddfd24abb23626f04046211a](./Asset/ea3cfd4ddfd24abb23626f04046211a.png)

> 要求`/user/hadoop/data`目录下有`emp.csv`文件：
>
> ![740eaf35d3366999de04168fdd4a49b](./Asset/740eaf35d3366999de04168fdd4a49b.png)

进行查询数据：

![2908f08406a9e5c581508a110e5743e](./Asset/2908f08406a9e5c581508a110e5743e.png)

如果报以下错误，需要进行额外的配置：

![eb2c5e3de140a39affd967135009363](./Asset/eb2c5e3de140a39affd967135009363.png)

需要进行如下配置：

![f14704f5de0f4e0b399272b34d268da](./Asset/f14704f5de0f4e0b399272b34d268da.jpg)

## 捌、Flume

### 一、下载Flume

Flume的下载地址：https://archive.apache.org/dist/flume/

下载Fluem版本是1.9.0的文件：

![2838479d6946082e0dfbaab7c2fcd34](./Asset/2838479d6946082e0dfbaab7c2fcd34.png)

进行下载：

![8f64157c392d555d3215a54de1681d4](./Asset/8f64157c392d555d3215a54de1681d4.png)

上传到master节点上：

![a4809958e3d86deac78558dec6f9cb1](./Asset/a4809958e3d86deac78558dec6f9cb1.png)

### 二、安装Flume

将Flume解压到`/usr/local/`目录下：

![3631e0cb92ad2bc6a0dc0daa68bdf48](./Asset/3631e0cb92ad2bc6a0dc0daa68bdf48.png)

重命名为flume：

![4712de30217d60d1a8f8baa69de1d9f](./Asset/4712de30217d60d1a8f8baa69de1d9f.png)

将Hadoop的`guava`的jar包替换到flume的`guava`的jar包，首先重命名`flume/lib`目录下的`guava-11.0.2.jar`：

![5bfc80c5864522222c86928f88879a2](./Asset/5bfc80c5864522222c86928f88879a2.png)

将`hadoop/share/hadoop/common/lib`目录下的`guava-27.0.jar`复制到`/usr/local/flume/lib`目录下：

![dd0828e444b06099d62c178af1db2a0](./Asset/dd0828e444b06099d62c178af1db2a0.png)

查看是否安装成功：

![20e7bf4c272208b2716136125c5984e](./Asset/20e7bf4c272208b2716136125c5984e.png)

### 三、配置Flume

配置环境变量，新建`flume.sh`文件：

![e8befcf31b766e93068c7af27ecea59](./Asset/e8befcf31b766e93068c7af27ecea59.png)

`flume.sh`的文件的内容如下：

![b65cbef886b7fe3cac80fc4ec5a96c8](./Asset/b65cbef886b7fe3cac80fc4ec5a96c8.png)

刷新环境变量，查看flume的版本信息，检查是否安装成功：

![664a860f7d9981c9b79c07b01fe359b](./Asset/664a860f7d9981c9b79c07b01fe359b.png)

进入`/usr/local/flume/conf`目录下，将`flume-env.sh.template`重命名为`flume-env.sh`：

![226034145afe50d657e85f832263fc4](./Asset/226034145afe50d657e85f832263fc4.png)

修改文件的内容如下，指定JAVA版本：

![76c71a882d44ec489dac2b606d902df](./Asset/76c71a882d44ec489dac2b606d902df.png)

### 四、使用Flume

#### 1. 监控本地目录

1. 书写配置文件，并将配置文件放在`flume`目录下的`agent`目录里（`agnet`目录需要自己创建），配置文件的名字自定义，这里我命名为`agent1.conf`，文件内容如下：

```txt
# 配置source,channel,sink名称
agent1.sources = source1   # 定义了一个名为agent1的Flume Agent,这里的agent1要和文件名称一致
agent1.channels = channel1
agent1.sinks = sink1
# 配置source
agent1.sources.source1.channels = channel1
agent1.sources.source1.type = spooldir
agent1.sources.source1.spoolDir=/usr/local/flumed   # 这里是要监控的目录

# 配置 channel
agent1.channels.channel1.type = memory


#配置source和sink绑定到channel

agent1.sinks.sink1.channel = channel1
agent1.sinks.sink1.type = logger

```

2. 创建被监控目录(`/usr/local/flumed`)，并修改权限：

![56257e9db60f061ad0a893d3eab2137](./Asset/56257e9db60f061ad0a893d3eab2137.png)

3. 启动`Flume`进行监听：

![ec3a79fff36ba4a16c04e9e9c77f7c0](./Asset/ec3a79fff36ba4a16c04e9e9c77f7c0.png)

4. 在被监听的目录下进行写入数据：

   ```shell
   echo  "Hello Flume." > test.log   # 这个命令可以创建test.log文件，并写入文本Hello Flume.
   ```

![47000a2e1f574db3f51d8ff84038cd2](./Asset/47000a2e1f574db3f51d8ff84038cd2.png)

5. 查看`Flume`监听窗口，可以看到成功监听到日志信息`Hello Flume`：

![6c4c54e4ae600628badf72186c465b4](./Asset/6c4c54e4ae600628badf72186c465b4.png)

#### 2. 传输日志到Flume监听窗口

1. 为了方便接下来的操作，将`Flume`目录的所属用户以及所属组更改为`hadoop:hadoop`：

![337b87d7ef5861b0a20438dcdcb3918](./Asset/337b87d7ef5861b0a20438dcdcb3918.png)

2. 在`/usr/local/flume/conf`目录下创建`avro.conf`文件：

![79af40b130feb31a8d28189cfd01377](./Asset/79af40b130feb31a8d28189cfd01377.png)

3. `avro.conf`文件的信息如下：

   ```txt
   a1.sources = r1
   a1.sinks = k1
   a1.channels = c1
   
   a1.sources.r1.type = avro
   a1.sources.r1.bind = 0.0.0.0
   a1.sources.r1.port = 4141
   
   a1.sinks.k1.type = logger
   
   a1.channels.c1.type = memory
   a1.channels.c1.capacity = 1000
   a1.channels.c1.transactionCapacity = 100
   
   a1.sources.r1.channels = c1
   a1.sinks.k1.channel = c1
   ```

![f84ae06140ce59b6239e0de333d146d](./Asset/f84ae06140ce59b6239e0de333d146d.png)

4. 创建`log.00`文件，并写入信息：

![c7880d857ada2bc9cec18cbc71ac4a7](./Asset/c7880d857ada2bc9cec18cbc71ac4a7.png)

![e9aff282a24f3d05118910ef7e1efa3](./Asset/e9aff282a24f3d05118910ef7e1efa3.png)

5. 将`log.00`传输到`Flume`监听端口中：

   ```shell
   flume-ng agent --conf /usr/local/flume/conf/ --conf-file /usr/local/flume/conf/avro.conf -name a1 -Dflume.root.logger=INFO,console
   ```

![518e69c18edbc8b7e1c9a6559e3b22c](./Asset/518e69c18edbc8b7e1c9a6559e3b22c.png)

6. 在`Flume`监听端口进行查看信息，可以看到正确监听到`log.00`文件中的信息：

![69528fb5ebd3287f4f288928428a9c0](./Asset/69528fb5ebd3287f4f288928428a9c0.png)

#### 3. 监听HDFS上的目录：

1. 在`/usr/local/flume/conf`目录下创建`syslogtcp.conf`文件：

![1d7c329c539c10ce91e8aa94657146c](./Asset/1d7c329c539c10ce91e8aa94657146c.png)

2. 编写`syslogtcp.conf`文件：

   ```txt
   a1.sources = r1
   a1.sinks = k1
   a1.channels = c1
   
   a1.sources.r1.type = syslogtcp
   a1.sources.r1.host = localhost
   a1.sources.r1.port = 5140  # 设置监听的端口号为5140
   
   a1.sinks.k1.type = hdfs
   # 下面一行需要根据自己的iP进行更改，以及要上传到HDFS上的那个路径下，都可以自定义更改。
   a1.sinks.k1.hdfs.path = hdfs://192.168.56.---:8020/user/hadoop/input/syslogtcp   
   a1.sinks.k1.hdfs.filePrefix = Syslog
   a1.sinks.k1.hdfs.round = ture
   a1.sinks.k1.hdfs.roundValue = 10
   a1.sinks.k1.hdfs.roundUnit = minute
   
   a1.channels.c1.type = memory
   a1.channels.c1.capacity = 1000
   a1.channels.c1.transactionCapacity = 100
   
   a1.sources.r1.channels = c1
   a1.sinks.k1.channel = c1
   ```

![cf7feb39e6a043348762ed4f3189be1](./Asset/cf7feb39e6a043348762ed4f3189be1.png)

3. 启动`Hadoop`：

![e7a5a0b6797b6c5e8ecc1590a076ed8](./Asset/e7a5a0b6797b6c5e8ecc1590a076ed8.png)

4. 启动`Flume`监听窗口，对5140端口进行监听：

   ```shell
   flume-ng agent -c /usr/local/flume/conf/ -f /usr/local/flume/conf/syslogtcp.conf -n a1 -Dflume.root.logger=INFO,console

![342744db0ed04bf0a5b47743961ceec](./Asset/342744db0ed04bf0a5b47743961ceec.png)

5. 输入文本到`HFDS`上，将字符串 'flume HDFS' 通过网络发送到本地主机的5140端口。：

![4d417fb9f19697d0f0426ba99f24681](./Asset/4d417fb9f19697d0f0426ba99f24681.png)

6. 打开`HDFS`查看`log`日志：

![ebfd286e04aa5ac3d2b163a3e39d65a](./Asset/ebfd286e04aa5ac3d2b163a3e39d65a.png)

## 玖、Sqoop

### 一、下载Sqoop

`sqoop`下载地址：https://archive.apache.org/dist/sqoop/1.4.7/

![8da6a79bac5e7f2fa6db827e3cfeb3a](./Asset/8da6a79bac5e7f2fa6db827e3cfeb3a.png)

经`sqoop`压缩包上传到虚拟机中：

![12618b3962f2487b12185d4f646f345](./Asset/12618b3962f2487b12185d4f646f345.png)

### 二、安装sqoop：

解压`sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz`到`/usr/local/`目录下：

![4a62e62ac132af71062aeaf03686d6b](./Asset/4a62e62ac132af71062aeaf03686d6b.png)

将`sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz`重命名为`sqoop`：

![e1e184ea97f558999a0497704f80217](./Asset/e1e184ea97f558999a0497704f80217.png)

### 三、配置sqoop

配置sqoop的环境变量：

![a2ffd3d376cf4275037c832d8e56bfe](./Asset/a2ffd3d376cf4275037c832d8e56bfe.png)

![fd49eebb6ef3cbe5bcd0ba29176068f](./Asset/fd49eebb6ef3cbe5bcd0ba29176068f.png)

更新环境变量：

![cb4146847b782d6b76255747c508064](./Asset/cb4146847b782d6b76255747c508064.png)

进入到`/usr/local/sqoop/conf`目录下，将`sqoop-env-template.sh`重命名为`sqoop-env.sh`：

![36b5e3d36b6ffbafe63e87a6c1568ec](./Asset/36b5e3d36b6ffbafe63e87a6c1568ec.png)

编辑`sqoop-env.sh`：

![7f622b976609d2e52ad15f4cbf038a2](./Asset/7f622b976609d2e52ad15f4cbf038a2.png)

将里面的内容都修改为对应的路径：

![7dff29744ad29e0c12be745273c5fce](./Asset/7dff29744ad29e0c12be745273c5fce.png)

配置JDBC：

> 这里为笔者记录自己的感想，与Hadoop的配置无关系，仅用于记录，可直接跳过：
>
> 在配置JDBC的时候，我出现了很多的错误，在网上进行大量的查找，耗费两天的时间并没有找到一个很好的解决方案，一个最严重的问题是，sqoop不能连接上mysql，并且我知道原因就在JDBC上，我查阅了一些资料，询问了AI，并且询问了其他同学，始终没有解决这个问题，在第三天的晚上，我尝试了一个最耗时也是最简单的思路：尝试不同版本的JDBC，我从JDBC官网上进行下载JDBC，在5.1.x的区域内进行尝试，面对将近几十个版本的JDBC，我并没有一个一个尝试，而是按照二分的思路进行尝试，先从中间的一个开始尝试，然后向上进行尝试，如果上面的版本不行的话就再向下进行尝试，有幸收到老天的照顾，我尝试了四五个，发现`5.1.49`版本的是可以将sqoop连接上mysql的，当时我真的是很激动，功夫不负有心人，我真正意义上感受到了**前人栽树后人乘凉**的重要性，但是sqoop再将MySQL上传到hive的时候还是有错误，这一点我还是没有解决，待日后进行研究……

1. 下载JDBC：

   JDBC官网：https://mvnrepository.com/artifact/mysql/mysql-connector-java

   这里选择`5.1.49`版本的JDBC：

   ![388e09dd9e5b383d257ef42aba416b8](./Asset/388e09dd9e5b383d257ef42aba416b8.png)

   ![ab18c1b2b6a2f0c14ed3b60df17bc83](./Asset/ab18c1b2b6a2f0c14ed3b60df17bc83.png)

   

2. 将JDBC上传到虚拟机中：

   ![fa2648165e6d92438d6d44827697abb](./Asset/fa2648165e6d92438d6d44827697abb.png)

3. 将JDBC复制到`/usr/local/lib`目录下：

   ![c595211903360fffa2d1181002403a0](./Asset/c595211903360fffa2d1181002403a0.png)

### 使用sqoop：

输入sqoop help如果出现了帮助文档说明sqoop安装配置成功：

![3bdfa9bb1ca147d4767daaff618ba53](./Asset/3bdfa9bb1ca147d4767daaff618ba53.png)

启动mysql，创建`sqoop`用户并赋予所有权限：

![e42b4fc8b7a877e63066ff9bf47358a](./Asset/e42b4fc8b7a877e63066ff9bf47358a.png)

创建sqoop数据库：

![9723d40dd5c5f5f426fa948424c7de1](./Asset/9723d40dd5c5f5f426fa948424c7de1.png)

在sqoop数据库中创建emp表：

```mysql
 use sqoop;
 CREATE TABLE emp (
    empno INT,
    ename VARCHAR(10),
    job VARCHAR(10),
    mgr INT,
    hiredate DATE,
    sal DECIMAL(7, 2),
    comm DECIMAL(7, 2),
    deptno INT
);
INSERT INTO emp VALUES
(7369, 'SMITH', 'CLERK', 7902, '1980-12-17', 800, NULL, 20),
(7499, 'ALLEN', 'SALESMAN', 7698, '1981-02-20', 1600, 300, 30),
(7521, 'WARD', 'SALESMAN', 7698, '1981-02-22', 1250, 500, 30),
(7566, 'JONES', 'MANAGER', 7839, '1981-04-02', 2975, NULL, 20),
(7654, 'MARTIN', 'SALESMAN', 7698, '1981-09-28', 1250, 1400, 30),
(7698, 'BLAKE', 'MANAGER', 7839, '1981-05-01', 2850, NULL, 30),
(7782, 'CLARK', 'MANAGER', 7839, '1981-06-09', 2450, NULL, 10),
(7788, 'SCOTT', 'ANALYST', 7566, '1987-04-19', 3000, NULL, 20),
(7839, 'KING', 'PRESIDENT', NULL, '1981-11-17', 5000, NULL, 10),
(7844, 'TURNER', 'SALESMAN', 7698, '1981-09-08', 1500, 0, 30),
(7876, 'ADAMS', 'CLERK', 7788, '1987-05-23', 1100, NULL, 20),
(7900, 'JAMES', 'CLERK', 7698, '1981-12-03', 950, NULL, 30),
(7902, 'FORD', 'ANALYST', 7566, '1981-12-03', 3000, NULL, 20),
(7934, 'MILLER', 'CLERK', 7782, '1982-01-23', 1300, NULL, 10);
```

![d1b7da7a7e11f829e694d4be449ff25](./Asset/d1b7da7a7e11f829e694d4be449ff25.png)

![d1b7da7a7e11f829e694d4be449ff25](./Asset/d1b7da7a7e11f829e694d4be449ff25.png)

#### 1. 使用sqoop查看MySQL中的数据库 ：

```shell
sqoop list-databases --connect jdbc:mysql://localhost:3306 --username sqoop --password sqoop
```

![46d8f47a211b9a819cee6a8a121118b](./Asset/46d8f47a211b9a819cee6a8a121118b.png)

#### 2. 查看MySQL中的`sqoop`数据库中有哪些表：

```shell
sqoop list-tables --connect jdbc:mysql://localhost:3306/sqoop --username sqoop --password sqoop
```

![ba2a2e64892ba86ba032c5fcb230353](./Asset/ba2a2e64892ba86ba032c5fcb230353.png)

可以看到sqoop数据库下只有emp表：

![8f5b4cc171015f99fda04858b924194](./Asset/8f5b4cc171015f99fda04858b924194.png)

#### 3. MySQL与HDFS互相导入

##### mysql导入hdfs中

```shell
sqoop import --connect jdbc:mysql://localhost:3306/sqoop --username sqoop --password sqoop --table emp -target-dir /input -m 1
```

![49e116d087cef11ee3c8bae3c4a90c9](./Asset/49e116d087cef11ee3c8bae3c4a90c9.png)

在Web上进行查看导入HDFS中的结果：

![f82b35bd5e192f30956c72a9238b55f](./Asset/f82b35bd5e192f30956c72a9238b55f.png)

![14dda924dc7234d78811534a0a24b8c](./Asset/14dda924dc7234d78811534a0a24b8c.png)

##### hdfs导入到mysql中：

在mysql中的sqoop数据库下创建表`emp_hdfs`用于接受`hdfs`传输过来的数据：

![b66845ac3017dfb6e7004b3b252c1dc](./Asset/b66845ac3017dfb6e7004b3b252c1dc.png)

将MySQL上传到hdfs上的`emp`表重新传回MySQL中的sqoop数据库下的`emp_hdfs`表中：

```shell
sqoop export --connect jdbc:mysql://localhost:3306/sqoop --username sqoop -P --table emp_hdfs --num-mappers 1 --export-dir /input/part-m-00000
```

![3cab38ae33d740f555dd592ea6118b6](./Asset/3cab38ae33d740f555dd592ea6118b6.png)

在MySQL中进行查表验证：

![a8c518a0cdbb4ca6671ecfe2daba6ca](./Asset/a8c518a0cdbb4ca6671ecfe2daba6ca.png)

#### 4. MySQL传输数据到Hive中

> 这一部分笔者暂时没有成功，可能是Hadoop版本不兼容的问题导致MySQL无法上传表到hive中，待日后研究成功后进行补充。

## 什、Zookeeper

### 一、下载zookeeper：

zookeeper官网下载地址：https://zookeeper.apache.org/releases.html

![e9f7c1c9bed6970edb4a7fea0378a43](./Asset/e9f7c1c9bed6970edb4a7fea0378a43.png)

![da997ada1620791364a625a78910ca0](./Asset/da997ada1620791364a625a78910ca0.png)

![c77c098da5dd1c5760f3eee0d0ed1c1](./Asset/c77c098da5dd1c5760f3eee0d0ed1c1.png)

将`zookeeper`上传到虚拟机中：

![fa00dcc98743a780318d8099cfb4519](./Asset/fa00dcc98743a780318d8099cfb4519.png)

### 二、安装zookeeper：

将`apache-zookeeper-3.6.4-bin.tar.gz`解压到`/usr/local/`目录下：

![51ec70c4cd4996daf703c9947450ab4](./Asset/51ec70c4cd4996daf703c9947450ab4.png)

将`apache-zookeeper-3.6.4-bin.tar.gz`重命名为`zookeeper`：

![88f571f5abe2bddb89bbe2de1729be6](./Asset/88f571f5abe2bddb89bbe2de1729be6.png)

### 三、配置zookeeper：

配置zookeeper的环境变量：

![dee47be24e57d31d8a82db4fdeecb2a](./Asset/dee47be24e57d31d8a82db4fdeecb2a.png)

![36df5381e4650a8269c7cf69fb075c8](./Asset/36df5381e4650a8269c7cf69fb075c8.png)

刷新环境变量：

![c999602073f70aee709a299c93d894d](./Asset/c999602073f70aee709a299c93d894d.png)

修改zookeeper的所属用户以及所属组为`hadoop:hadoop`：

![6af972162e7a728111457f2b8a9251b](./Asset/6af972162e7a728111457f2b8a9251b.png)

进入到`/usr/local/zookeeper/conf`目录下，将`zoo_sample.cfg`重命名为`zoo.cfg`：

![8edc87e8c22921c66f0a6406c37182a](./Asset/8edc87e8c22921c66f0a6406c37182a.png)

修改`zoo.cfg`文件的内容：

![6b95e481fc1109aa1ed405773b40dc0](./Asset/6b95e481fc1109aa1ed405773b40dc0.png)

在`zoo.cfg`文件的末尾添加如下内容：

```txt
server.1=master:2888:3888
server.2=slave1:2888:3888
server.3=slave2:2888:3888
```

> 其中：2888 是 Leader 端口，负责和 Follower 进行通信，3888 是 Follower 端口，负责推选 Leader

![45a2af4542f5f869f18dbdb3acbe199](./Asset/45a2af4542f5f869f18dbdb3acbe199.png)

在`/usr/local/zookeeper`目录下创建文件夹`zkdata`，并在zkdata中创建`myid`文件：

![890fde9a5a05ca14becb42d6c1a337e](./Asset/890fde9a5a05ca14becb42d6c1a337e.png)

编辑`myid`文件的内容如下：

![e85fc048b782fd287b5e5b96d882266](./Asset/e85fc048b782fd287b5e5b96d882266.png)

### 四、配置从节点的zookeeper：

将主节点的zookeeper传输到从节点：

![cc18fd153f4f6166784122eb57bd9d7](./Asset/cc18fd153f4f6166784122eb57bd9d7.png)

![30d0a2b34bbeb812ecdea8ce9cc520b](./Asset/30d0a2b34bbeb812ecdea8ce9cc520b.png)

更改从节点的`myid`文件内容：

**slave1：**

![d5c66e74be94a30903f85064a9c8b96](./Asset/d5c66e74be94a30903f85064a9c8b96.png)

![f548adc6037178ee1881e47c96f929d](./Asset/f548adc6037178ee1881e47c96f929d.png)

**slave2：**

![ba7e230654fbb984726652235300418](./Asset/ba7e230654fbb984726652235300418.png)

![dc9c844426cf22a37cc0b4ec6b017be](./Asset/dc9c844426cf22a37cc0b4ec6b017be.png)

传输环zookeeper的境变量给从节点：

![2429bd2746624ed5c1ee8a9ff3321a2](./Asset/2429bd2746624ed5c1ee8a9ff3321a2.png)

刷新主节点与从节点的环境变量：

![65b3b2b9618a0a83ac88fc50c82c91d](./Asset/65b3b2b9618a0a83ac88fc50c82c91d.png)

![30ba66ebf569077be73d07208c39b34](./Asset/30ba66ebf569077be73d07208c39b34.png)

![8f60aec611eb8e5b2e0163b7f5707a4](./Asset/8f60aec611eb8e5b2e0163b7f5707a4.png)

### 五、启动zookeeper

启动**三个**节点的zookeeper：

```shell
zkServer.sh start    # 启动zookeeper，切记三台虚拟机都要进行启动。
zkServer.sh status  # 查看zookeeper的状态
zkServer.sh stop    # 关闭zookeeper
```

![000da6694227ffd36286572989aeb86](./Asset/000da6694227ffd36286572989aeb86.png)

查看启动状态：

![9d092400aeb4063e426489ed5bfe85c](./Asset/9d092400aeb4063e426489ed5bfe85c.png)

查看zookeeper的服务：

![fc1ddbd4565a69f29de5ccd74ede13d](./Asset/fc1ddbd4565a69f29de5ccd74ede13d.png)

启动zookeeper客户端，并连接到zookeeper服务器：

```shell
zkCli.sh -server localhost:2181
```

![561cf7cbd82f9b82e9bdfbf3fdc562b](./Asset/561cf7cbd82f9b82e9bdfbf3fdc562b.png)

输入`help`，如果出现帮助文档，说明陈工配置了zookeeper：

![dda2a3c9d5388f904df4a77056adb9d](./Asset/dda2a3c9d5388f904df4a77056adb9d.png)

### 六、额外错误

如果使用zookeeper之后，无法使用pig了，在`hbase shell`写入命令的时候，出现`master`正在初始化，这是由于zookeeper中的数据没有删除导致的，报错信息和解决方案如下：

#### 1. 问题报错：

![image-20240623190518408](./Asset/image-20240623190518408.png)

#### 2. 解决方案：

退出`habse shell`，退出`habse`，将`zookeeper`下的`hbase`进行删除，然后将`hdfs`上的`/hbase`进行删除，重启`hbase`即可。

1. 启动`zookeeper`：

   ```shell
   zkCli.sh
   ```

2. 查看根目录的子节点：

   ```shell
   ls /
   ```

3. 删除`zookeeper`中根目录下的`hbase`节点：

   ```shell
   deleteall /hbase
   ```

4. 删除`hdfs`上的`hbase`：

   ```shell
   hdfs dfs -rm -r /hbase
   ```

5. 启动`hbase`，启动`hbase shell`：

   ```shell
   start-hbase.sh
   hbase shell
   ```

![image-20240623191206871](./Asset/image-20240623191206871.png)
