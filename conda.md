# conda使用笔记

## Miniconda

1、添加conda的镜像服务器

```sh
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```

2、使用

```sh
# 创建虚拟环境
conda create –n py37 python=3.7
-n : 虚拟环境的名称
python= : 下载的版本号

# 进入虚拟环境：
conda activate py37

# 退出虚拟环境：
conda deactivate

# 查看所有虚拟环境
conda env list

# 删除环境
conda remove -n env-name all

# 查看环境中的包
conda list

在虚拟环境中安装、卸载、更新包：
conda install python=3.6  激活虚拟环境后安装包 (可以指定版本)
conda remove packname 激活虚拟环境后移除包
conda update packname 激活虚拟环境后更新包
也可以pip安装，建议conda
```

## Archiconda

> jetson nano是aarch64架构， Anaonda的仓库中并不存在aarch64的相关编译版本 ，适合使用Archiconda和miniforge等，Archiconda最新更新2019年0.2.3版本，建议使用miniforge

[github](https://github.com/Archiconda/build-tools/releases) 

```docs
# 赋权并安装
sudo chmod 755 Archiconda3-0.2.3-Linux-aarch64.sh
./Archiconda3-0.2.3-Linux-aarch64.sh
# 使用和Anaconda一致
```

**Note**:需要的包需要有aarch64的版本才行，否则只能使用whl包离线安装，要是whl包也没有那就只能放弃了 

##  miniforge 

[github](https://github.com/conda-forge/miniforge)

```docs
# 下载aarch64版本并安装，并初始化conda ,初始化后需重新打开终端
bash Miniforge3-4.12.0-2-Linux-aarch64.sh -b
~/miniforge3/bin/conda init
# 使用和Anaconda一致
```

## 环境迁移

1、将要迁移的环境打包

```docs
conda pack -n 虚拟环境名称 -o output.tar.gz
#如果报错：No command ‘conda pack’：尝试使用：conda install -c conda-forge conda-pack
#如果CondaPackError: Cannot pack an environment with editable packages，
#忽略这些库：conda pack -n pcdet -o pcdet.tar.gz --ignore-editable-packages
```

2、目标机器或位置解压

```docs
#进到conda的安装目录：/anaconda(或者miniconda)/envs/,并在该名目录下创建文件夹
解压conda环境：tar -xzvf output.tar.gz -C /anaconda(或者miniconda)/envs/创建的文件夹/
使用conda env list查看虚拟环境
source /anaconda(或者miniconda)/envs/创建的文件夹/bin/activate #激活环境
#或conda create -n 环境2 --clone 复制的环境1的路径
```

3、若存在editable packages，打包对应库

```docs
# 列出所有库并手动查看所有editable packages
pip list
# 在对应库位置对其打包zip或tar
# 解压到pip list中库所在指定位置
```

