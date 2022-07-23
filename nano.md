# Nano

- 2022.7 nano暂不支持cuda11，支持cuda10，架构为aarch64

## nano swap扩容

原装官方系统内存Mem 4G，Swap2G，总共6G。可通过**free**或**jtop**命令查看。

```docs
# 运行进程时内存不足会显示“pid号 已杀死”，可通过如下命令显示log
dmesg | egrep -i -B100 'killed process'
# 若显示“Out of memory”，可通过“Killed process pid号”后“total-vm”计算所需mem，从而进行Swap扩容
```

扩容操作如下：

```docs
# 生成swapfile文件
#1）新增swapfile文件大小自定义，6G换为所需mem
sudo fallocate -l 6G /var/swapfile
#2）配置该文件的权限
sudo chmod 600 /var/swapfile
#3）建立交换分区
sudo mkswap /var/swapfile
#4）启用交换分区
sudo swapon /var/swapfile
#5）设置为自动启用swapfile
sudo bash -c 'echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab'
```

**参考**

- [程序进程莫名被杀死](https://blog.csdn.net/ispringmw/article/details/112719262)
- [查看CPU\GPU\内存使用率](https://blog.csdn.net/biubiubiu617/article/details/107984931)
- [Jetson nano增加Swap分区大小操作指南](https://blog.csdn.net/qq_33475105/article/details/108372878)