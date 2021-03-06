<https://www.runoob.com/linux/linux-command-manual.html>

## 一、tar.gz压缩格式软件安装步骤
  1）`cd`命令切换到文件目录
  2）`tar -zxvy` 文件名    --解压文件

## 二、git版本编译安装

1. 安装依赖：`yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker`
2. 下载git包：`wget https://github.com/git/git/archive/v2.8.0.tar.gz`
3. 解压：`tar -zxcf v2.8.0.tar.gz`
4. 进入git编译：`cd git-2.8.0/` 然后编译 `sudo make prefix=/usr/local all`
5. 执行安装命令：`sudo make prefix=/usr/local install`
6. 查看版本：`git --version`
7. 配置ssh秘钥：`ssh-keygen -t rsa -C "fanxing531837"`
8. 私钥添加到本地系统：`ssh-add ~/.ssh/id_rsa`（–如果系统提示：could not open a connection to your authentication agent：则需要执行一下命令：`ssh-agent bash` 然后再执行上述的 `ssh-add id_rsa` 命令）
9. 看一下：`cat ~/.ssh/id_rsa.pub`
10. git需要配置用户名和邮箱：`git config --global user.name 'fanxing'` 和 `git config --global user.email '531837586@qq.com'`

## 三、笔记本外接显示器，关闭、打开笔记本自身显示器
​    `sudo xrandr --output eDP-1 --off`
​    `sudo xrandr --output eDP-1 --auto`

## 四、递归删除指定类型文件
`find ./ -name "*~"  | xargs rm`

## 五、文件格式转换（GBK -> UTF-8）

  `enca -L zh_CN -x UTF-8 filename`
  Filename可以为：

1. 具体文件名，

2. 或当前文件夹下所有文件（./\*），

3. 以及当前文件夹下所有文件夹里面所有得文件（./\*/\*）等

如遇到 `enca: Cannot convert \./checkDetailWidget.cpp\' from unknown encoding`

可使用 `iconv -f GBK -t UTF-8 Filename -o Filename` 进行转换
注：enca 需要安装`sudo apt install enca` ，iconv 一般为Linux自带的命令


## 六、环境变量、动态库路径设置
### 1、PATH:  可执行程序的查找路径

查看当前环境变量: echo $PATH
设置方法：

1. `export PATH=PATH:/XXX` 但是退出当前终端后就失效
2. 修改 ~/.bashrc 或 ~/.bash_profile或系统级别的/etc/profile
     1. `export PATH=DIR:$PATH`
     2. `source .bashrc`  (Source命令也称为“点命令”，也就是一个点符号（.）。
         source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录)

### 2、LD_LIBRARY_PATH: 动态库的查找路径

设置：
1. `export  LD_LIBRARY_PATH=LD_LIBRARY_PATH:/XXX`  但是退出当前终端后就失效
2.  修改 ~/.bashrc 或 ~/.bash_profile 或系统级别的 /etc/profile
   1. 在其中添加例如 `export LD_LIBRARY_PATH=/opt/ActiveP/lib:$LD_LIBRARY_PATH`
   2. `source .bashrc` 
3. 这个没有修改LD_LIBRARY_PATH但是效果是一样的实现动态库的查找，
    1.  /etc/ld.so.conf  文件夹下添加对应文件 filename.conf 里面填入 /usr/local/mysql/lib
    2. 保存后执行 `ldconfig`  生效
    （ldconfig 命令的用途,主要是在默认搜寻目录(/lib和/usr/lib)以及动态库配置文件/etc/ld.so.conf内所列的目录下,搜索出可共享的动态链接库(格式如前介绍,lib*.so*),进而创建出动态装入程序(ld.so)所需的连接和缓存文件.缓存文件默认为/etc/ld.so.cache,此文件保存已排好序的动态链接库名字列表.）

