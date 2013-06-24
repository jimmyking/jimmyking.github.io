---
layout: post
title: "使用Octopress搭建Github博客"
date: 2013-06-24 15:41
comments: true
categories: 随记
---

###Step1. 建立自己的[Github page:](https://github.com/new)

首先创建一个github repository，在Repository name的地方填入username.github.io

###Step2. [Setup Octopress](http://octopress.org/docs/setup/)

首先你需要安装Git and Ruby(1.9.3)

然后：
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
gem install bundler
bundle install
rake install
```

如果执行```rake install```命令报bundle的版本异常的话，可以使用```bundle exec rake install```

###Step3. [部署octopress到Github Pages](http://octopress.org/docs/deploying/github/)

执行名称如下：
```
bundle exec rake setup_github_pages
bundle exec rake generate
bundle exec deploy
```

注意在执行```rake setup_github_pages```时一定要输入正确的github的repository地址。

我第一次部署老是报没有找到对应的repository地址的错误。执行这个命令时会有一个提示，这个提示的地址中最后缺少了```.git```。当然如果地址填写错误我们还是有办法补救的。我们可以修改```.git/config```文件找到对应的地方修改之就可以了。

除了部署你的Github pages,我们还需要将代码也保存到repository中
```
git add .
git commit -m 'first deploy'
git push origin source
```

这样我们的代码将push到source分支中，而pages的代码则在master分支中。

###Setp4. [设置博客参数](http://octopress.org/docs/configuring/)

这里可以修改标题、子标题、作者等信息

###Setp5. [写博客](http://octopress.org/docs/blogging/)

执行```bundle exec rake 'new_post[title]'```将会在生成对应post的MD文档,它就是你写博客的地方了。

写完post之后执行

```
bundle exec rake generate
bundle exec rake watch
bundle exec rake preview
```

打开[浏览器](http://localhost:4000)查看预览

最后部署

```
git add .
git commit -m "add a post"
git push
bundle exec rake deploy
```

###Tips. [更新octopress](http://octopress.org/docs/updating/)

octopress在不断更新有时我们需要更新octopress到最新的版本，执行如下命令更新octopress

```
git pull origin master
bundle install
bundle exec rake update_source
bundle exec update_style
```




