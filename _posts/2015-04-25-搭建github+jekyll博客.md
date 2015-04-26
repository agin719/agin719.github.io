---
layout: post
title: "搭建github+jekyll博客"
date: 2015-04-25
---    

其实很早之前就想构建一个博客了，但就是不懂得怎么去搭，而且也没想清楚该到哪里网站搭建好，后来听别人说github可以建博客，而自己又一直想学习git，于是我就决定在github上博客，顺便借此机会学习git。
    
下面我所用的系统是centos6.5,用户名切换到root，搭建github+jekyll博客的步骤如下：

0、了解git和jekyll

你可以去[Git教程-廖雪峰的官方网站][git]学习git和[jekyll中文手册][jekyll]学习jekyll，这两个都是很好的教程。

1、安装git。

在centos上安装git很简单，用yum安装即可。
{% highlight bash %}
# yum install git
{% endhighlight %}	

2、安装jekyll。

安装jekyll之前，需要安装ruby，gem，note.js。我们可以用rvm(是什么自己查)来安装ruby和gem。

(0)以防万一先把gcc安装。
{% highlight bash %}
# yum install gcc*
{% endhighlight %}
(1)在bash上安装rvm。
{% highlight bash %}
# curl -L https://get.rvm.io | bash -s table
{% endhighlight %}
这里可能会出错，反正我是出错了，可以按照它显示的错误信息来输入命令,它先叫我先输入命令:
{% highlight bash %}
# curl -sSL https://rvm.io/mpapis.asc | gpg2 --import
{% endhighlight %}
这下应可以了，再输入：
{% highlight bash %}
# curl -L https://get.rvm.io | bash -s table
{% endhighlight %}
这下子安装成功了，把终端关闭后再打开，输入rvm -v可查看版本。

(2)输入命令rvm list known可以查看rvm能够安装ruby的版本
知道版本后安装ruby：
{% highlight bash %}
# rvm install 2.0.0
{% endhighlight %}
安装完成后可以用ruby -v来查看ruby的版本号

(3)安装gem:
{% highlight bash %}
# rvm install rubygems
{% endhighlight%}
用gem -v查看gem的版本

(4)接下来就可以用gem来安装jekyll了。
因为国外的资源被墙了，所以需要利用国内的镜像来完成下载，修改gem的源
{% highlight bash %}
# gem sources --remove https://rubygems.org/
# gem sources -a https://ruby.sdutlinux.org/
# gem sources -l
{% endhighlight %}
然后执行：
{% highlight bash %}
# gem install jekyll
{% endhighlight %}
好了，jekyll安装好了，但现在jekyll还不能用，因为需要把note.js也安装上

(5)安装note.js

安装note.js可以利用源码编译安装或者直接下载编译好的文件。
下载编译好的文件直接解压，在bin文件夹已经存在node和npm了，我们只需要做一些链接即可,这里根据自己的文件所在路径做连接文件。
{% highlight bash %}
# ln -s /home/agin/Downloads/node-v0.12.2-linux-x86/bin/node /usr/local/bin/node
# ln -s /home/agin/Downloads/node-v0.12.2-linux-x86/bin/npm /usr/local/bin/node
{% endhighlight %}
至此，jekyll安装完毕。

3、在github上面创建仓库

在 GitHub 上有一个账号，名为username(任意)，创建一个名为username.github.io(固定格式，username与账号名一致)的仓库， 项目分支名为master(固定)。

GitHub认为，一个GitHub账号对应一个用户或者一个组织，GitHub会给这个用户分配一个域名：username.github.io，当用户访问这个域名时， GitHub会去解析username用户下，username.github.io项目的master分支.

另外，GitHub还为每个项目提供了域名，例如，你有一个项目名为blog， GitHub为这个项目提供的域名为username.github.io/blog， 当你访问这个域名时，GitHub会去解析username用户下，blog项目的gh-pages 分支。

所以，要搭建自己的博客，你可以选择建立名为 username.github.io的项目， 在master分支下存放网站源代码，也可以选择建立名为 blog 的项目，在 gh-pages分支下存放网站源代码。

4、先利用jekyll建立博客

输入命令:
{% highlight bash %}
$ jekyll new myblog
$ cd myblog
$ ls
{% endhighlight%}
jekyll new myblog新建了一个myblog的文件夹。里面的_post文件夹存放我们的博客，_config.yml文件是jekyll的配置文件，index.html是博客主页，_layout文件夹是生成html页面的模板，_site文件夹存放生成后的html页面。

我们可以用jekyll build命令来将_post文件里面的博客转换为html文件(相当于编译)。
在jekyll serve启动本地服务器，在浏览器输入localhost:4000可以查看博客的内容。

5、将博客源代码托管到github上面

在myblog文件夹下：
{% highlight bash %}
$ git init
$ git add .
$ git commit -m "my blog"
{% endhighlight%}
git init是初始化git，它会在myblog里面添加文件夹.git
将username.github.io项目和我们的博客项目联系起来。
{% highlight bash %}
$ git remote origin git@github.com:username/username.github.io.git
{% endhighlight%}
推送项目到github：
{% highlight bash %}
$ git push -u origin master
{% endhighlight%}
至此，你打开username.github.io即可查看自己的博客了。github+jekyll博客搭建完成。

[git]:	   http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
[jekyll]:  http://jekyllcn.com/
