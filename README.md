gitolite安装和配置
==============
安装
--------------
#####1：安装git#####

    $yum -y install git
#####2: 新建git用户#####

    $useradd --system --shell /bin/bash --create-home git
#####3:安装#####

    $su - git
    $mkdir bin
    $git clone git://github.com/sitaramc/gitolite.git
    $~/gitolite/install -to ~/bin
    $ssh-keygen –f ~/.ssh/git  //客户端生产key并上传到服务端
    $~/bin/gitolite setup -pk ~/git.pub
#####4:管理#####
在客户端的.ssh目录新建config文件，输入以下内容保存

    host git
    user git
    hostname 192.168.2.100    //gitolite服务器ip
    port 22
    identityfile ~/.ssh/git
将gitolite-admin clone下来可对gitolite进行管理

    $git clone git:gitolite-admin  
其中conf/gitolite文件是对repo的配置管理
keydir目录是对用户的配置
#####5:新增用户#####
打开git命令行
Windows用户使用git bush
输入命令：

    $ssh-keygen ~/.ssh/username   //username为邮箱的@前面部分
将.ssh目录下的username.pub文件复制一份发送给我
在.ssh目录下创建文件 config     //无文件后缀名
在config文件中输入如下内容保存(username为上一步的username)：

    host username
    user git
    hostname 192.168.2.100
    port 22
    identityfile ~/.ssh/username


