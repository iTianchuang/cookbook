gitolite安装和配置
==============
普通用户操作
--------------
#####1. 生成用户的密钥对(请注意将[username]更换为用户名)：#####

    $ ssh-keygen -f ~/.ssh/[username]

此命令将生成密钥对: ~/.ssh/[username] 和 ~/.ssh/[username].pub
#####2. 将公钥文件username.pub发送给管理员#####

#####3. 在.ssh目录下创建文件 config, 并输入如下内容#####

    host gitserv                 # gitolite所在机器的别名
    user git                     # 用来访问gitolite库的用户名
    hostname 192.168.2.100       # gitolite所在机器的IP地址
    port 22                      # sshd的端口
    identityfile ~/.ssh/username # 用来访问gitolite库的用户的私钥文件
                                 # username为上一步的username
    
#####4. clone项目库至本地:#####

    $ git clone gitserv:testing.git  #testing.git为库名


管理员操作(安装与配置)
--------------
#####1: 安装git#####

    $ yum -y install git
#####2: 新建git用户#####

    $ useradd --system --shell /bin/bash --create-home git
#####3:安装#####

    $ su - git
    $ mkdir bin
    $ git clone git://github.com/sitaramc/gitolite.git
    $ ~/gitolite/install -to ~/bin
    $ ssh-keygen –f ~/.ssh/git  //（管理员在客户端操作）客户端生产key并上传到服务端
    $ ~/bin/gitolite setup -pk ~/git.pub
    
#####4: 管理（管理员在客户端操作）#####
在客户端的.ssh目录新建config文件，输入以下内容保存

    host gitserv
    user git
    hostname 192.168.2.100
    port 22
    identityfile ~/.ssh/git
将gitolite-admin clone下来可对gitolite进行管理

    $ git clone gitserv:gitolite-admin  
其中conf/gitolite文件是对repo的配置管理
keydir目录是对用户的配置
#####5: 新增用户（管理员在客户端操作）#####
将用户发送的pub文件放到gitolite-admin项目的keydir目录并上传至服务器

附: [git使用教程](http://git-scm.com/book/zh/%E8%B5%B7%E6%AD%A5)


