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