# WSL

windiws文件位置

``` sh
C:\Users\Administrator\AppData\Local\Packages\com..
```

## windows命令

``` cmd 
wsl
# 运行
wsl -d id
# 查看正在运行
wsl -l --running
# 停止
wsl -t id
# 备份
wsl --export id path\filename.tar
# 删除
wsl --unregister id
# 还原
wsl --import id targetpath\filename.tar
```

## 图形化界面

[XLaunch](https://sourceforge.net/projects/vcxsrv/)

#### 安装命令

``` linux
#!/bin/bash
sudo apt-get update #更新源
sudo apt-get install xfce4 xfce4-terminal #安装xfce4桌面
echo -e "\n##DISPLAY Configuration" >> ~/.bashrc #配置声明
echo "export DISPLAY=127.0.0.1:0.0" >> ~/.bashrc #添加配置
source ~/.bashrc #配置生效
#run xfce4
startxfce4 #如何运行xfce4
```



## 配套软件

- XLaunch
- ssh

