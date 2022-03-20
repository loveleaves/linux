# 基于Ubuntu+Python+Tensorflow+Jupyter notebook搭建深度学习环境

[TOC]



## 前言

如今，人工智能、深度学习等高深知识逐渐融入大家的视野，小大验证码的识别，大到无人驾驶技术等都离不开深度学习。迎合时代的脚步，跟上技术的潮流，开始学习深度学习首先需要搭建深度学习环境。搭建环境的方式也有不少，本文主要是介绍，基于**Ubuntu+Python+Tensorflow+Jupyter ntebook**来搭建环境，以便开始深度学习之旅。该文主要从以下几个部分的内容来进行介绍：

- 环境准备
- Xshell远程连接Ubuntu
- Jupyter notebook服务器的配置及远程访问
- 深度学习远程环境的测试

OK，话不多说，开始进入正轨吧。(#`O′)

------

## 一、环境准备

### 环境介绍

- 准备两台计算机，一个作为服务端，一个作为客户端，通过客户端远程连接服务端的深度学习环境。
- 服务端：Linux系统（[Ubuntu](https://www.ubuntu.com/download/desktop)），也可根据自身需求使用其他Linux系统。
  [Ubuntu介绍](https://baike.baidu.com/item/ubuntu/155795?fr=aladdin)：Ubuntu（友帮拓、优般图、乌班图）是一个以桌面应用为主的开源GNU/Linux操作系统，Ubuntu 是基于Debian GNU/Linux，支持x86、amd64（即x64）和ppc架构，由全球化的专业开发团队（Canonical Ltd）打造的。
  Linux系统区别于windows系统最大的区别是其主要是利用终端 Shell 命令来进行一系列的操作，所以在实际使用过程中常常用来搭建服务器，该系统搭建在VMware虚拟机中。
- 客户端：Windows10系统
  这个大家再熟悉不过了，就不介绍了。
- [Anaconda](https://www.anaconda.com/download/)
  [Anaconda介绍](https://baike.baidu.com/item/anaconda/20407441?fr=aladdin)：Anaconda指的是一个开源的Python发行版本，其包含了conda、Python等180多个科学包及其依赖项。所以说，当我们下载了Anaconda之后就不必要再下载Python其他包了，其内部集成了大量大Python工具，其中就包括我们这篇文章的主角Jupyter notebook。
- [Xshell](https://xshell.en.softonic.com/?ex=BB-682.0)
  这个就没什么好说的了，它主要是一种远程连接的工具，使用它之后我们就可以通过ssh协议来远程连接Ubuntu系统了，而且它常常与远程文件传输工具Xftp配套使用。

### 软件下载

官网：

1. Anaconda：https://www.anaconda.com/download/，于服务端下载
2. Xshell：https://xshell.en.softonic.com/?ex=BB-682.0，于客户端下载
3. Ubuntu：https://www.ubuntu.com/download/desktop，于服务端下载
4. VMware：https://www.vmware.com/，于服务端下载

### VMware下安装Ubuntu

注意：以下内容都是在服务端计算机中进行配置

在VMware虚拟机下安装Ubuntu系统虽然有点步骤，也需要点时间，但是并不复杂。在综合考虑到时间成本与其给大家带来的价值的关系下，博主就用文字描述了，暂时不贴图了。但是你不必担心，关键步骤还是会贴图说明的，大家根据下方的流程搭建安装即可 ( ﹁ ﹁ ) ~→。

- 在服务端下载好VMware及Ubuntu之后。首先打开VMware你会发现他会让你输入VMware秘钥，以下将给出几个目前有效的秘钥，当你使用的时候也许已经失效了，你可以自行查找可用的秘钥即可：

```
FF31K-AHZD1-H8ETZ-8WWEZ-WUUVA
CV7T2-6WY5Q-48EWP-ZXY7X-QGUWD
ZY5H0-D3Y8K-M89EZ-AYPEG-MYUA8
ZC5XK-A6E0M-080XQ-04ZZG-YF08D
ZY5H0-D3Y8K-M89EZ-AYPEG-MYUA8
```

- 输入秘钥之后 ，进入到了VMware的页面了，这个时候我们需要用到在之前下载好的Ubuntu镜像文件了，在VMware中新建一个虚拟机，流程如下：

![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLzl2bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vYzk5NWQxNDNhZDRiZDExMzUyNzkzZDc1NTdhZmE0MGY0YWZiMDVjNC5qcGc=.jpg)

### Ubuntu下Anaconda的安装

在VMware下安装好Ubuntu后，虽然Ubuntu内自带了Python，但是其版本一般是2.7的，而且许多常用的工具包并没用集成，所以我们还需要安装Anaconda（一招解千愁），如果熟悉Java的话，Anaconda就类似Maven一样的存在。我们根据以上介绍的Anaconda的下载方式在Ubuntu下载好Anaconda之后，进入到其目录之下（或者cd操作），然后打开终端，执行如下命令来进行安装：

```
bash Anaconda3-5.3.1-Linux-x86_64.sh    # 不要盲目的复制粘贴，根据自己所下载的Anaconda版本执行
```

执行之后会有一些列诸如同意协议之类的问题，我们直接默认默认选项即可（直接Enter，或者yes），直到出现Anaconda环境变量配置的显示（不要无脑yes过头了），我们需要选择将其加入到环境变量中去。一系列操作之后，我们关闭终端然后在重新打开终端，然后在终端分别执行**conda list、python**命令，如果你的终端界面出现类似以下输出，则恭喜你说明你已经完成了anaconda的安装。

![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLzk0bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vMzdkM2Q1MzliNjAwM2FmM2FhMTg1NjI3MzgyYWM2NWMxMTM4YjZkMy5qcGc=.jpg)

这里再说明一点：而如果你的终端输错报错（未找到**conda**命令之类的）或者Python版本为2.7，那就说明你以上操作中未将Anaconda加入到环境变量(yes过头)，所以你需要手动配置Anaconda的环境变量，操作如下：

打开环境变量的配置文件，从这里我们就可以看出Linux和Windows下的操作的区别了（windows一般是通过界面的形式进行设置，而Linux下则大多数通过终端并使用vim进行配置）

```
# 打开环境变量的配置文件，从这里我们就可以看出Linux和Windows下的操作的区别了# windows一般是通过界面的形式进行设置，而Linux下则大多数通过终端并使用vim进行配置sudo vim gedit /root/.bashrc    
```

打开文件之后我们需要在文件末尾添加如下内容（需要熟悉vim操作），其中XXX为你的Anaconda的bin目录，例如我的是**/home/lxj/anaconda3/bin**

```
export PATH="XXX:$PATH"   # XXX为你的Anaconda的bin目录，例如我的是/home/lxj/anaconda3/bin
```

然后保存（Esc -> shift+: -> wq -> 回车），在终端输入source ~/.bashrc进行更新即可完成Anaconda环境变量的配置，不出意外的话再次分别执行**Python、conda list**命令之后你会看见conda包的列表以及Python3.7的输出了。

补充：这里额外说明一下，以上的操作是使用Vim进行文件编辑的，他不同于windows下的记事本等，而是通过特定的操作来对文件进行编辑。对于熟悉Vim操作的应该会理解以上Anaconda环境变量的配置，然而如果是对Vim比较陌生的朋友可能会卡壳，所以在这里简单介绍一些vim的操作：



在终端使用vim命令之后将会进入到vim的界面，此时的界面是不允许modify任何内容的，只允许read only。此时我们输入i将会进入到vim的编辑模式，现在就能对该文件进行修改了。文件内容修改完成之后，我们需要退出该vim编辑模式，vim 的退出常用的有以下几种（首先输入Esc键）：

- q! -> 不保存文件修改并退出
- wq -> 保存文件的修改并退出
- wq! -> 有时候我们需要root权限才能编辑文件，使用该命令之后就能够强制修改并退出。

对于以上Anaconda环境变量的配置，vim的熟悉至此就足够了，顺便介绍一下其他常用的命令供大家参考

- read模式下双击d -> 删除当行内容
- Ctrl+b -> 内容向前移动一页
- ctrl+f -> 内容向后移动爷爷
- shift+g -> 鼠标指针定位到最后
  常用的就是以上一些了，其他的操作有需要的自行学习

注意：以上内容都是在服务端计算机中进行配置

至此，我们已经完成了环境的搭建，接下来我们介绍一下如何使用Xshell远程连接Ubuntu操作

------

## 二、Xshell远程连接Ubuntu系统

注意：以下内容都是在客户端计算机中进行配置

安装好Anaconda之后，我们需要通过Xshell使用Xshell来远程连接我们的Ubuntu系统，此时我们的目标需要转移至客户端了。

首先在以上软件下载中根据链接下载Xshell，之后Windows傻瓜式安装好Xshell（顺便把Xftp安装下，与Xshell配套使用的，虽然在本文中使用不到）。之后的操作会有几个坑，但是不必担心，下面会详细带你一个一个的填掉 o(*≧▽≦)ツ┏━┓。

坑一：连接失败
我们双击打开Xshell，并点击**文件**并新建，然后根据如下图进行操作：
![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLzk0bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vN2RkOThkMTAwMWU5MzkwMTkxYTAwNzc5NzZlYzU0ZTczN2QxOTZkMy5qcGc=.jpg)

> 补充，上方中的主机属性是填Ubuntu的ip地址，该地址可在Ubuntu的终端执行ifconfig（windows是ipconfig）命令得到。

以上信息填写完之后在出现的界面输入自己Ubuntu下的用户登录密码即可。
执行之后你会发现连接失败，此时我们需要检查一下Ubuntu是否与客户端处于同一网段下，可以将Ubuntu设置成桥接模式（右键Ubuntu虚拟机然后进行设置，一般用于有线连接情况）或者使用Nat模式（用于无线），之后再次检查一下客户端（Windows10）是否能够ping通服务端（Ubuntu），在客户端的cmd中执行如下：

```
ping XXX.XXX.XXX.XXX    # XXX.XXX.XXX.XXX为服务端的ip
```

在以上操作之后，一般就能ping通了，如果失败了则在Ubuntu终端下执行**sudo wfw disable**命令关闭防火墙。

坑二：连接失败 (ノへ￣、)

在如上操作之后，我们再次尝试重新连接。我们可以发现依然连接失败，显示拒绝连接之类的信息。这是因为Xshell是通过ssh协议来连接Ubuntu的，但是Ubuntu默认是没有开启ssh服务的，所以我们需要在其终端执行如下命令来开启ssh服务：

```
sudo service ssh restart
```

之后我们再次尝试连接。

坑三：连接失败 (ノへ￣、) (ノへ￣、)

一般来讲，这个时候依然是连接失败，因为在默认情况下Ubuntu未安装ssh服务，此时我们需要在Ubuntu下安装ssh服务，执行以下命令进行安装：

```
sudo apt-get install openssh-server
```

待其安装好后，我们再再再次连接Ubunut。如果无法安装，则需要执行**apt-get update**进行更新，更新之前如果出现无法获得锁相关的报错信息，则执行如下命令断开apt进程后再次更新：

```
# 查看apt相关进程ps aux |grep apt# 然后把apt进程杀掉kill -9 进程号# 重新更新apt-getapt-get update
```

以上坑踩过之后也该连接成功了吧。的确此时你将成功连接到Ubuntu了，之后Xshell将打开一个终端，这个终端就是Ubuntu下的终端了，也就是说我们可以使用该终端控制Ubuntu了，并对其进行Shell操作。ヽ(✿ﾟ▽ﾟ)ノ

------

## 三、Jupyter notebook服务器的配置及远程访问

由于我们在之前已经安装过了Anaconda，所以此时的Ubuntu就已经集成了**ipython** 以及**jupyter-notebook**（Anaconda就是这么的强大）。对此，我们将通过Xshell远程连接Ubuntu来搭建Jupyter notebook的服务器，并对其进行远程访问。

- 在终端中启动ipython或者python，然后执行以下命令

```
from IPython.lib import passwdpasswd()
```

上述命令执行之后将会在终端显示**设置密码**，方便起见，在这我们将密码设置成：123，之后enter并确认即可完成密码的设置。

注意：这里的密码是暗文的形式，输入之后不会显示的，还有此时你输入的密码需要记住，因为我们待会远程访问Jupyter notebook服务器的时候需要用到该密码进行登录

密码输入之后，我们将会看到有一个较长字符串，该字符串是上述密码的一个加密形式，我们需要将其复制下来，在之后的ipython_notebook_config.py文件的设置中需要使用，操作结果如下图所示：

![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLzk0bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vOTgyNWJjMzE1YzYwMzRhODhlNDAzMmM2YzYxMzQ5NTQwODIzNzZkMy5qcGc=.jpg)

- 随后为了方便上述加密密码字符串的记录，我们在此开启另一个终端（这也是Xshell的方便所在），然后使用如下命令创建一个服务器名，比如，在此我们将该名字设置为：XXX

```
ipython profile create XXX
```

在上述服务器名创建完成之后，将在终端输出两个py文件（**ipython_config.py、ipython_kernel_config.py**）路径，之后使用如下cd命令我们进入到**.ipython**路径**cd ./.ipython**。具体操作图示如下：

![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLy12bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vZDc4OGQ0M2Y4Nzk0YTRjMjc4NmQ2ZDZjMDNmNDFiZDVhZDZlMzkyZS5qcGc=.jpg)

- 进入**.ipython**目录之后使用**ls**命令将会列出上述创建的两个py文件所在，但是我们需要再额外创建一个py配置文件并对其进行设置，在这里我们使用vim来进行操作，关于vim的使用，上述的Anaconda环境配置过程中已经介绍了，遗忘的朋友可以返回看一看再熟悉一下。熟悉之后我们完成如下步骤：

```
cd .ipython/profile_txj     vim ipython_notebook_config.py
```

进入到vim环境之后我们在ipython_notebook_config.py文件中编辑如下内容，主要是配置notebook的登录密码（加密后的形式）以及服务的开放端口：

```
c = get_config()c.IPKernelApp.pyalb = "inline"c.NotebookApp.ip = "*"c.NotebookApp.open_browser = Falsec.NotebookApp.allow_root = Truec.NotebookApp.password = u"加密后的密码"    # 这里我们需要使用上述加密后的密码，在另一个终端可见c.NotebookApp.port = 8888   # 在这里，我们需要设置一个jupyter-notebook的端口，尽量设置的少见点，以免造成端口冲突
```

编辑好后，**wq**命令保存并退出。

- 在上述一切操作完成之后，我们现在来开启该服务器，新建一个终端并执行如下命令

```
jupyter notebook --config=【你的ipython_notebook_config.py文件路径】    # 例如/home/lxj/.ipython/profile_XXX/ipython_notebook_config.py
```

在上述命令执行之后，如果出现如下图片所示内容，则说明我们的服务端已经正常启动
![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLy1mbzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vMmNmNWUwZmU5OTI1YmMzMTkyZTk4YmRmNTNkZjhkYjFjYTEzNzBjNS5qcGc=.jpg)

![img](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHBzL2dzczAuYmFpZHUuY29tLy00bzNkU2FnX3hJNGtoR2tvOVdUQW5GNmhoeS96aGlkYW8vcGljL2l0ZW0vMzc3YWRhYjQ0YWVkMmU3M2NmNzQwYzZiOGEwMWExOGI4NmQ2ZmFkYy5qcGc=.jpg)

- 在服务端启动完成之后，我们在客户端打开浏览器，访问**XXX.XXX.XXX.XXX:8888**（ubuntu的ip加开放的端口）试试，看看能否正常请求。如果随后出现一个如上所示的Jupyter notebook的登录页面，那么恭喜你，至此Jupyter notebook服务器配置完成，并能够远程访问了。在表单中输入你所设置的密码（上面第一步设置的密码，123）即可开始你的深度学习之旅了。

以上就是Jupyter notebook服务器的配置及远程访问的内容了，但是能否正常使用呢，我们下面将通过几个简单的例子来对其进行测试。

------

## 四、远程环境的测试

### Tensorflow软件库的安装

> TensorFlow™ 是一个采用数据流图（data flow graphs），用于数值计算的开源软件库。节点（Nodes）在图中表示数学操作，图中的线（edges）则表示在节点间相互联系的多维数据数组，即张量（tensor）。它灵活的架构让你可以在多种平台上展开计算，例如台式计算机中的一个或多个CPU（或GPU），服务器，移动设备等等。TensorFlow 最初由Google大脑小组（隶属于Google机器智能研究机构）的研究员和工程师们开发出来，用于机器学习和深度神经网络方面的研究，但这个系统的通用性使其也可广泛用于其他计算领域。

上述操作完成之后，我们需要在Anaconda下安装Tensorflow包，这里我们可以采用Anaconda虚拟环境中安装：

1. Anaconda下通过**create**命令并指令Python版本创建一个虚拟环境
2. **conda env list**可以看见当前所拥有的环境
3. **activate**命令激活所需要的虚拟环境
4. 成功进入后后我们即可直接通过pip进行安装**tensorflow2**（本文直接安装CPU版本，如需安装GPU版本可看注释）

```
# Anaconda下通过`create`命令并指令Python版本创建一个虚拟环境，命名tensorflow2conda create --name tensorflow2 python=3.6、# `conda env list`可以看见当前所拥有的环境conda env list# `activate`命令激活所需要的虚拟环境conda activate tensorflow2# 成功进入后后我们即可直接通过pip进行安装`tensorflow2`pip install -U tensorflow -i https://pypi.tuna.tsinghua.edu.cn/simple --default-timeout=1000# GPU版本安装：conda create -n tf2 tensorflow-gpu，执行之后会自动安装 CUDA,cuDNN,TensorFlow GPU 等
```

在虚拟环境安装好Tensorflow2之后，要想在Jupyter notebook下使用该虚拟环境，我们还需要在该环境下安装ipkernel：

```
conda install ipykernelpython -m ipykernel install --name tensorflow2 --display-name tensorflow2
```

成功安装之后，在tensorflow2虚拟环境下使用**jupyter notebook**命令即可启动，登录之后在服务页面中即可指定**tensorflow2 kernel**环境来编写代码。通过上述的操作，我们已经完成了所有的工作。下面我们对其进行验证，看看Anaconda下的第三方包能否正常使用。为此，我们通过以下几个小的案例来进行验证：

- 百度及其子链接的简单爬虫（**requests， BeautifulSoup**）
- 数据可视化操作（**numpy，matplotlib，skimage**）
- 基于神经网络实现fashion_mnist图片的识别（**Tensorflow、Keras**）

### 简单爬虫

```
import requestsfrom bs4 import BeautifulSoupdef get_page(url, headers=None):    return requests.get(url).textif __name__ == "__main__":    baidu_url = "https://www.baidu.com"    baidu_soup = BeautifulSoup(get_page(baidu_url), "html.parser")    son_links = [biaoqian_a.attrs["href"] for biaoqian_a in baidu_soup.find_all("a")]    for index, son_link in enumerate(son_links):        print("正在请求第{}个页面".format(str(index)))        print(get_page(son_link))
```

### 数据可视化

```
import numpy as npimport pandas as pdimport matplotlib.pyplot as pltimport matplotlib as mpl% matplotlib inlinefor module in np, pd, mpl:    print(module.__name__, module.__version__)if __name__ == "__main__":    ax =pd.DataFrame(np.random.randn(1000, 6), columns=list('ABCDEF')).cumsum().plot(secondary_y=["D", "E", "F"])    ax.set_ylabel('ABC plot')    ax.right_ax.set_ylabel('DEF scale')    ax.legend(loc='upper left')    ax.right_ax.legend(loc='upper right')    plt.show()
```

### 基于神经网络实现fashion_mnist图片的识别

```
import tensorflow as tfimport numpy as npfrom matplotlib import pyplot as pltimport matplotlib as mpl%matplotlib inlinefor module in tf, np, mpl:    print(module.__name__, module.__version__)if __name__ == "__main":    (x_train_all, y_train_all), (x_test, y_test) = tf.keras.datasets.fashion_mnist.load_data()    x_valid, x_train = x_train_all[:50000], x_train_all[50000:]    y_valid, y_train = y_train_all[:50000], y_train_all[50000:]    model = tf.keras.models.Sequential()    model.add(tf.keras.layers.Flatten(input_shape = [28, 28]))  # 定义输入层    model.add(tf.keras.layers.Dense(300, activation="relu")) # 定义全连接层（最普通的神经网络），中间定义两个隐藏层    model.add(tf.keras.layers.Dense(100, activation="relu")) # 再定义一个全连接层    model.add(tf.keras.layers.Dense(10, activation="softmax")) # 定义输出层    model.compile(loss = "sparse_categorical_crossentropy",                 optimizer = "adam",                 metrics = ["accuracy"])    history = model.fit(x_train, y_train, epochs=10,             validation_data=(x_valid, y_valid))    pd.DataFrame(history.history).plot(figsize=(8, 5))    plt.grid(True)    plt.gca().set_ylim(0, 1)    plt.show()
```

## 总结

通过上述的演示，已经完成了windows10下使用xshell远程连接linux系统以及远程访问jupyter-notebook服务，并通过几个小例子来对其进行验证说明可以正常使用linux下的anaconda。这样的话即可实现两台PC级之间的协调工作，一台用作服务端提供环境，另外一台作为客户端来远程进行访问并编写代码，而且其中的优势也是显而易见的，既能在一定程度上减小计算机的压力，又能方便管理且易于操作。另外，以上的环境搭建只作为一个案例，并不唯一，比如你可以使用Linux Centos、aliyun云服务器等。如果以上内容帮助到了你，请点个赞吧.ﾟヽ(｡◕‿◕｡)ﾉﾟ.:｡+ﾟ