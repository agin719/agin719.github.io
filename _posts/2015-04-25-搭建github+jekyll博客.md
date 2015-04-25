---
layout: post
title: "搭建github+jekyll博客"
date: 2015-04-25
---    

其实很早之前就想构建一个博客了，但就是不懂得怎么去搭，就一直听别人说很简单很简单的，而且也没想清楚该到哪里网站搭建好，后来听别人说github可以建博客，而自己又一直想学习git，于是我就决定在github上博客，顺便借此机会学习git。
    下面我所用的系统是centos6.5,用户名切换到root，搭建github+jekyll博客的步骤如下：

1、安装git。
	在centos上安装git很简单，用yum安装即可。
{% highlight bash %}
yum install git
{% endhighlight %}	

2、安装jekyll。
	安装jekyll之前，需要安装ruby，gem，note.js。
我们可以用rvm(是什么自己查)来安装ruby和gem。

(0)以防万一先把gcc安装。
{% highlight bash %}
yum install gcc*
{% endhighlight %}
(1)在bash上安装rvm。
{% highlight bash %}
curl -L https://get.rvm.io | bash -s table
{% endhighlight %}
这里可能会出错，反正我是出错了，可以按照它显示的错误信息来输入命令,它先叫我先输入命令:
{% highlight bash %}
curl -sSL https://rvm.io/mpapis.asc | gpg2 --import
{% endhighlight %}
这下应可以了，再输入：
{% highlight bash %}
curl -L https://get.rvm.io | bash -s table
{% endhighlight %}
这下子安装成功了，把终端关闭后再打开，输入rvm -v可查看版本。

(2)输入命令：rvm list known可以查看rvm能够安装ruby的版本
知道版本后安装ruby：
{% highlight bash %}
rvm install 2.0.0
{% endhighlight %}
安装完成后可以用ruby -v来查看ruby的版本号

(3)安装gem:
{% highlight bash %}
rvm install rubygems
{% endhighlight%}
用gem -v查看gem的版本

(4)接下来就可以用gem来安装jekyll了。
因为国外的资源被墙了，所以需要利用国内的镜像来完成下载，修改gem的源
{% highlight bash %}
gem sources --remove https://rubygems.org/
gem sources -a https://ruby.sdutlinux.org/
gem sources -l
{% endhighlight %}
然后执行：
{% highlight bash %}
 gem install jekyll
{% endhighlight %}
好了，jekyll安装好了，但现在jekyll还不能用，因为需要把note.js也安装上

(5)安装note.js
安装note.js可以利用源码编译安装或者直接下载编译好的文件。
下载编译好的文件直接解压，在bin文件夹已经存在node和npm了，我们只需要做一些链接即可,这里根据自己的文件所在路径做连接文件。
{% highlight bash %}
ln -s /home/agin/Downloads/node-v0.12.2-linux-x86/bin/node /usr/local/bin/node
ln -s /home/agin/Downloads/node-v0.12.2-linux-x86/bin/npm /usr/local/bin/node
{% endhighlight %}
至此，jekyll安装完毕。

3、先利用jekyll建立博客

输入命令:
{% highlight bash %}
jekyll new myblog
cd myblog
ls
{% endhighlight%}
jekyll new myblog新建了一个myblog的文件夹。里面的_post文件夹存放我们的博客。
我们可以用jekyll build命令来将_post文件里面的博客转换为html文件(相当于编译)。
在jekyll serve启动本地服务器，在浏览器输入localhost:4000可以查看博客的内容。

