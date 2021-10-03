# linux


## WSL图形化界面

[xcsrv](https://sourceforge.net/projects/vcxsrv/)

``` linux
#!/bin/bash
# this is bash command
sudo apt-get update #更新源
sudo apt-get install xfce4 xfce4-terminal #安装xfce4桌面
echo -e "\n##DISPLAY Configuration" >> ~/.bashrc #配置声明
echo "export DISPLAY=127.0.0.1:0.0" >> ~/.bashrc #添加配置
source ~/.bashrc #配置生效
#run xfce4
startxfce4 #如何运行xfce4
```

## Source

### Ubuntu

| Ubuntu version                            | codename |
| ----------------------------------------- | -------- |
| Ubuntu 16.04                              | xenial   |
| Ubuntu 17.04                              | zesty    |
| [Ubuntu 18.04](./ubuntu-18.04-source.txt) | bionic   |
| Ubuntu 19.04                              | disco    |
| Ubuntu 20.04                              | focal    |

[Tsinghua](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)