---
date: 2018-6
tag: 
  - git知识点整理
author: hzSilence
location: ShangHai  
---
# git同一个电脑生成多个ssh-key
## 安装git之后，配置全局变量

```
git config --global user.name "hzSilence"
git config --global user.email "sher.hui@55haitao.com"

```
## 1.生成gitlab对应的私钥公钥
执行命令 `ssh-keygen -t rsa -C email`创建对应的sshkey,命名为id_rsa_gitlab,密码为空 `ssh-keygen -t rsa -C sher.hui@55haitao.com`

```
ssh-keygen -t rsa -C sher.hui@55haitao.com
```
## 2.同样的方式生产shinelon的私钥公钥（邮箱地址可以相同也可以不同）
执行命令`ssh-keygen -t rsa -C email`创建gitlab对应的sshkey,命名为id_rsa_shinelon,密码为""
```
ssh-keygen -t rsa -C 15289381762@163.com
```
![An image](../.vuepress/assets/git/git1.png)

## 3.在当前用户目录创建.ssh目录，并把id_rsa文件放入其中

当前用户目录一般是在C盘用户目录下面的Administrator目录或者其他的用户目录（如果为Windows系统创建过其他用户）。 这里我的是`C:\Users\shinelon` 目录，进入`C:\Users\shinelon`目录，如果没有 `.ssh`目录，在当前目录下进入cmd执行命令 `mkdir .ssh` 即可创建。

## 4.把上面得到的文件拷贝到git默认访问的.ssh目录(C:\Users\shinelon\.ssh)

除了秘钥文件之外，config文件是后面的步骤中手动生产的，known_hosts文件是后续自动生产的

## 5.在.ssh目录创建config文本文件并完成相关配置(最核心的地方)  [touch config]
每个账号单独配置一个Host，每个Host要取一个别名，每个Host主要配置HostName和IdentityFile两个属性即可

IdentityFile两个属性即可;Host的名字可以取为自己喜欢的名字，不过这个会影响git相关命令，例如：
Host gitlab.55haitao.com 这样定义的话，命令如下，即git@后面紧跟的名字改为gitlab.55haitao.com
git clone git@gitlab.55haitao.com:GoCashBack/gocashback-web.git
 
HostName 　　　　　　　      这个是真实的域名地址
IdentityFile 　　　　　　　  这里是id_rsa的地址
PreferredAuthentications    配置登录时用什么权限认证--可设为publickey,password publickey,keyboard-interactive等
User 　　　　　　　　　　　   配置使用用户名

```
#配置gitlab
Host gitlab.55haitao.com
HostName gitlab.55haitao.com
IdentityFile C:\\Users\\shinelon\\.ssh\\id_rsa_gitlab
PreferredAuthentications publickey
User "sher.hui@55haitao.com"

#配置shinleon
Host github.com
HostName github.com
IdentityFile C:\\Users\\shinelon\\.ssh\\id_rsa_shinelon
PreferredAuthentications publickey
User "15289381762@163.com"
```

## 6.远程仓库添加 id_rsa_gitlab.pub

## 7.打开Git Bash客户端（管理员身份运行）执行测试命令测试是否配置成功（会自动在.ssh目录生成known_hosts文件把私钥配置进去）

![An image](../.vuepress/assets/git/git2.png)

## 8.进入不同的仓库设置用户名和邮箱

```
git config user.name "shinleon"
git config user.email "15289381762@163.com"
```