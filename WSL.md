# WSL

windiws�ļ�λ��

``` sh
C:\Users\Administrator\AppData\Local\Packages\com..
```

## windows����

``` cmd 
wsl
# ����
wsl -d id
# �鿴��������
wsl -l --running
# ֹͣ
wsl -t id
# ����
wsl --export id path\filename.tar
# ɾ��
wsl --unregister id
# ��ԭ
wsl --import id targetpath\filename.tar
```

## ͼ�λ�����

[XLaunch](https://sourceforge.net/projects/vcxsrv/)

#### ��װ����

``` linux
#!/bin/bash
sudo apt-get update #����Դ
sudo apt-get install xfce4 xfce4-terminal #��װxfce4����
echo -e "\n##DISPLAY Configuration" >> ~/.bashrc #��������
echo "export DISPLAY=127.0.0.1:0.0" >> ~/.bashrc #�������
source ~/.bashrc #������Ч
#run xfce4
startxfce4 #�������xfce4
```



## �������

- XLaunch
- ssh

