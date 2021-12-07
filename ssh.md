# SSH

[参考](https://zhuanlan.zhihu.com/p/355748937)

**以下命令默认为root用户**

## 1. ssh配置

### 1.1 ssh服务安装

Ubuntu20.04子系统自带的ssh服务无法连接，需卸载后重新安装。

- 卸载ssh服务

```
apt remove openssh-server
```

- 重装ssh服务

```
apt install openssh-server
```

### 1.2 修改配置信息

编辑`/etc/ssh/sshd_config`文件。

（1）修改ssh服务监听端口和监听地址

``` sh
Port 2222 # 修改这里
#AddressFamily any
ListenAddress 0.0.0.0 # 修改这里
```

（2）修改ssh服务允许使用用户名密码方式登入

``` sh
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes # 修改这里
#PermitEmptyPasswords no
```

（4）修改ssh服务允许远程root用户登入

``` sh
#PermitRootLogin prohibit-password
PermitRootLogin yes # 修改这里
#StrictModes yes
```

（5）重启ssh服务。

```
service ssh restart
```

### 1.3 设置开机自启

在前篇提到的`/etc/init.wsl`文件中添加`service ssh start`设置ssh服务开机自启。

## 2. ssh连接

### 2.1 本机连接

在Power Shell中通过ssh命令连接wsl子系统。

```
ssh root@localhost -p 2222
```

其中`2222`为上面设置ssh服务监听端口。

### 2.2 远程连接

此时通过PC的**IP地址**是无法访问wsl的，需设置端口转发和防火墙。

（1）查看wsl的地址

- 安装`ifconfig`工具

```
apt install net-tools
```

- 查看IP地址，eth0后ip地址为wsl的ip地址

```
ifconfig
```

（2）将端口转发到wsl，在Power Shell下执行命令，将[IP]和[PORT]替换为wsl的IP和端口。

```
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=2222 connectaddress=[IP] connectport=[PORT]
```

（3）开启防火墙入站规则（也可以在**控制面板-Windows Defender 防火墙-高级设置-入站规则**中设置）

```
netsh advfirewall firewall add rule name=WSL2 dir=in action=allow protocol=TCP localport=2222
```

设置完成后，即可通过IP地址远程访问wsl。