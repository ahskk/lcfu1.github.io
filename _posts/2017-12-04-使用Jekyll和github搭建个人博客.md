---
layout: post
title: 使用Jekyll和github搭建个人博客
author: lcfu1
original: 原创
---
## 一、下载[Git for windows](https://git-for-windows.github.io/)和[Ruby](http://www.ruby-lang.org/zh_cn/)并安装

## 二、Jekyll环境配置
- Jekyll的中文官网：http://jekyllcn.com
- 在一个空文件夹中右键选择打开Git Bash Here，然后**依次**按以下命令执行,可能会比较慢，因为要下载安装，所以要耐心等待：
```
$ gem install jekyll bundler
$ jekyll new blog
$ cd blog
$ bundle install
$ bundle exec jekyll serve
```
- 执行`$ bundle exec jekyll serve`后，打开浏览器输入http://127.0.0.1:4000/，就可以看到如下图：
![image.png](http://upload-images.jianshu.io/upload_images/6025530-abd5e3a061db60ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 默认使用的是[minima主题](https://github.com/jekyll/minima)

## 三、使用Github Pages服务
- 创建仓库，Repository name填写username.github.io，username是你的github用户名，其它的默认。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-e59cec66eef353b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 进入username.github.io仓库，点击Settings进入选择一个模板主题。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-6ea6879e62aac381.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](http://upload-images.jianshu.io/upload_images/6025530-54b723e1a7846603.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 在浏览器中输入https://username.github.io/ ，可以看到如下图。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-2a6b523036ca8328.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 四、部署我们电脑上的blog
- 在前面那个空文件夹中再次右键选择打开Git Bash Here，git clone我们github上的仓库。如git clone我的`$ git clone https://github.com/lcfu1/lcfu1.github.io.git`
- 打开刚刚下载的username.github.io文件夹，把我们电脑上的blog复制粘贴到这个文件夹上，相同的就选择替换，执行`$ jekyll serve`，打开浏览器输入http://127.0.0.1:4000/，同样可以看到如下图：
![image.png](http://upload-images.jianshu.io/upload_images/6025530-fdb65b727bdefb5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **依次**执行以下命令，如果不懂Git，可以找一下相关文章看一下，我也写了一篇关于git的，可以去找来看一下。
```
$ git status       //检查本地项目的状态
$ git add .        //添加全部文件到追踪列表
$ git commit -m "first commit"       //提交到本地仓库
$ git push         //推送到github
```
- 在浏览器中输入https://username.github.io/，就可以看到如下图，以前的模板改变了，变的跟我们在电脑上配置的一样。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-6521adb0dd8840e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 五、修改我们的博客信息和写博客
- _config.yml 按自己实际情况修改。
- 我都是用[Markdown](http://daringfireball.net/projects/markdown/)写博客的，你也可以用[Textile](http://redcloth.org/textile/)和HTML。以YEAR-MONTH-DAY-title.MARKUP格式命名并放到_posts中。
- 然后依次执行
```
$ git status       //检查本地项目的状态
$ git add .        //添加全部文件到追踪列表
$ git commit -m "first commit"       //提交到本地仓库
$ git push         //推送到github
```
- 过一会儿在浏览器中输入https://username.github.io/就可以看到你的修改信息和博客了。

## 六、绑定域名
- 到github上打开我们的username.github.io仓库，点击Settings进入，在下图圈圈中输入你的域名并保存，但是前提需要你的域名已经解析并添加了你的博客github域名。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-fdd91cab3a3af1fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 购买域名，然后到控制台按下图做类似修改进行域名解析。
![image.png](http://upload-images.jianshu.io/upload_images/6025530-8157c552e38ed9cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 七、修改主题
- [主题](http://jekyllthemes.org/)
- 选择一个你喜欢的主题，这里我选的一个Jasper2主题，git clone 到一个空文件夹下，依次执行以下命令，
```
$ git clone https://github.com/myJekyll/jasper2.git
$ cd jasper2
$ gem install jekyll bundler
$ bundle install
$ bundle exec jekyll serve
```
- 执行完$ bundle exec jekyll serve，打开浏览器输入http://127.0.0.1:4000/，可以看到如下图：
![image.png](http://upload-images.jianshu.io/upload_images/6025530-0f7add3a1c782880.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 可以把Jasper2文件夹下的文件复制到你的blog文件夹下，相同的就选择替换，右键选择打开Git Bash Here，`$ bundle exec jekyll serve`，然后再打开浏览器输入http://127.0.0.1:4000/，可以看到主题变为Jasper2主题了。`$ bundle exec jekyll serve`后可能会提示一些error，这就需要你后面的修改了。
- 修改和写博客后可以再次推送到github上。
```
$ git status       //检查本地项目的状态
$ git add .        //添加全部文件到追踪列表
$ git commit -m "first commit"       //提交到本地仓库
$ git push         //推送到github
```

## 八、结束
- 到这里你的博客就完成差不多了，后面看个人需要可以添加一些功能。
- 如果遇到问题，可以自己摸索或谷歌一下，也可以找相关博客文章文档查看。
- 当然也可以在简书上评论私信我，我知道的尽量帮你解决难题。
