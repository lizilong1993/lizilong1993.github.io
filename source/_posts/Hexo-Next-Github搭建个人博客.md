---
title: Hexo+Next+Github搭建个人博客(新手向)
date: 2021-01-09 04:45:20
tags:
- Hexo
- Next
- Github 
- 个人博客
categories: 
- 教程
comments: true
---


# 前言
- 所有的软件都基于Windows10环境，其它平台应该差不多。
- 本文只是列出了大概过程，可能有部分细节缺失。
- 这也是我第一次搭建个人博客，欢迎交流。


# 配置环境
> 以下是我当时使用的环境。
- Nodejs 
- Git 
- Hexo 个人博客软件
- Github Pages静态网页服务
- Next主题
- PicGo 图床软件
- Markdown编辑器(Visual Studio Code)


# nodejs 安装

首先下载nodejs，我这里推荐长期支持版。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111224907.png)
安装一路选默认选项，完成后打开**CMD**输入<font color=red>node -v</font>和<font color=red>npm -v</font>，如果出现版本号就代表安装成功。
<center>
    <img src="https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111225325.png" width="100%" height="">
</center>

# 添加国内镜像源
因为众所周知的原因，需要国内镜像进行加速。
~~~ bash
npm config set registry https://registry.npm.taobao.org
~~~
设置完成后打开**CMD**输入<font color=red>cnpm -v</font>，如果显示版本号则安装成功。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111230053.png)

# Git 安装
因为需要用到Github，所以要下载[Git](https://git-scm.com/download/win)。我的电脑是win10 64位，所以这里我下载选中的版本。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111223225.png)
安装选项还是全部默认，只不过最后一步添加路径时选择 **Use Git from the Windows Command Prompt**，这样我们就可以直接在命令提示符里打开git了。

安装完成后在命令提示符中输入 <font color=red>git --version</font> 验证是否安装成功。
<center>
    <img src="https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111224035.png" width="100%">
</center>



# Github设置
## 创建Github账号
去[github](https://github.com/)注册一个github账号。
## 新建博客仓库
有了账号，我们还需要创建一个仓库来存放我们的个人博客文件，点击 + 号，选择**New repository**。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111230528.png)
记住这里的仓库名一定要跟你的用户名一致，如果**不一致则发布后的个人博客网站会出现二级域名**。

![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111230744.png)
选择**Public**开放仓库访问权限，然后点击**Create repository**完成个人博客仓库创建。

## 开启Pages服务

项目仓库创建完成后，需要开启Github Pages服务来发布个人博客的静态网站。
点击**Settings**，然后一直往下拉。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111232316.png)
直到Github Pages设置区域，可以选默认的**main**分支，也可以再自己创建一个专门的分支来发布Pages服务。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111232417.png)
发布成功后会出现一个链接，点击进去就是你将来的个人博客静态网页。当然这里点进去肯定啥都没有2333，下图是我已经弄了一半的效果，注意我这里的网址就只有一级域名。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111233037.png)
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210111233159.png)
> 注：如果不嫌麻烦，建议单独建一个新分支用来发布Github Pages服务，main分支（也就是master分支）专门用来存个人博客源代码。


# Hexo
建好了仓库，接下来我们需要安装个人博客开源软件。
> 注：想要了解其它博客框架可以去看这篇博客[个人博客搭建——介绍几种博客搭建框架](https://blog.csdn.net/weixin_45784655/article/details/104780438)。据说hugo速度比较快，想尝试的话可以去看这篇文章[如何用hugo 搭建博客](https://zhuanlan.zhihu.com/p/126298572)。

## Hexo安装

在合适的地方新建一个文件夹，用来存放自己的博客文件，比如我的博客文件都存放在**D:\Data\Blog**目录下。

在该目录下右键点击**Git Bash Here**，打开git的控制台窗口，以后我们所有的操作都在git控制台进行，就不要用Windows自带的控制台了。

定位到该目录下，输入以下命令安装Hexo。可能会有几个报错，无视它就行。
~~~ bash
cnpm install hexo-cli -g
~~~


安装完后输入<font color=red>hexo -v</font>验证是否安装成功。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112000645.png)
然后就要初始化我们的网站，输入<font color=red>hexo init</font>初始化文件夹，接着输入npm install安装必备的组件。

这样本地的网站配置也弄好啦，输入<font color=red>hexo g</font>生成静态网页，然后输入<font color=red>hexo s --debug</font>以调试模式打开本地服务器，然后浏览器打开<http://localhost:4000/>，就可以看到我们的博客啦，效果如下：
![](https://godweiyang.com/2018/04/13/hexo-blog/5.jpg)

按**ctrl+c**关闭本地服务器。

## 生成密钥SSH Key
> 这一步主要是为了简化步骤，避免每次部署博客到github都需要输入一遍自己的账户名和密码。

首先右键打开git bash，然后输入下面命令：
~~~ bash
git config --global user.name "你的Github名字"
git config --global user.email "你的Github邮箱"
~~~

用户名和邮箱根据你注册github的信息自行修改。

然后生成密钥SSH key：
~~~ bash
ssh-keygen -t rsa -C "你的Github邮箱"
~~~
打开github，在头像下面点击**settings**，再点击**SSH and GPG keys**，新建一个SSH，名字随便，内容先空着等一下。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112001425.png)
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112001546.png)
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112001642.png)
git bash中输入
~~~ bash
cat ~/.ssh/id_rsa.pub
~~~
将输出的内容复制到上图空着的框中，点击**Add SSH Key**保存。

输入ssh -T git@github.com，如果如下图所示，出现你的用户名，那就成功了。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112001925.png)



## 部署博客到Github
打开博客根目录下的*config.yml*文件，这是**博客**的配置文件，在这里你可以修改与博客相关的各种信息。

修改最后一行的配置：
~~~ yml
deploy:
  type: git
  repository: https://github.com/lizilong1993/lizilong1993.github.io.git
  branch: master
~~~
repository修改为你自己的github项目地址。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112002545.png)

## 写文章&发布文章

首先在博客根目录下右键打开**git bash**，安装一个扩展<font color=red> cnpm i hexo-deployer-git</font>。

然后输入<font color=red>hexo new post "你新建的文章名"</font>，新建一篇文章。

然后打开*D:\Data\Blog\source\_posts*的目录，可以发现下面多了一个.md文件，就是你的文章文件啦。

编写完markdown文件后，根目录下输入<font color=red> hexo g</font>生成静态网页，然后输入<font color=red> hexo s --debug</font>可以本地预览效果，最后输入<font color=red> hexo d</font>上传到github上。这时打开你的github.io主页就能看到发布的文章啦。

## 绑定域名
这里我就不介绍怎么绑定域名了，因为我自己也没钱买域名。不过如果你有这个需求的话，可以参考[超详细Hexo+Github博客搭建小白教程](https://godweiyang.com/2018/04/13/hexo-blog/)里的这部分。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112004125.png)

# 备份与下载博客源文件
这里可以继续参考[超详细Hexo+Github博客搭建小白教程](https://godweiyang.com/2018/04/13/hexo-blog/)里的这部分，我太懒了，没有弄这一部分2333。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112004417.png)

# 美化博客
原生的Hexo默认主题是**landscape**,我个人不太喜欢。

## Hexo主题推荐
可以参考这几篇文章里介绍的主题：
- [好康的Hexo主题推荐](https://yukinouta.github.io/2020/hexo-theme-recommend/)
- [有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335?sort=created&page=3)
- [官方网站](https://github.com/hexojs/hexo/wiki/Themes)里面主题很多，只不过没有预览罢了。

我这里只介绍比较火的极简风格主题Next。
## Next主题
### 安装
切换到D:\Data\Blog路径下，右键选择**Git Bash Here**打开命令行工具，输入
~~~ Bash
git clone https://github.com/theme-next/hexo-theme-next themes/next
~~~
安装成功后输入<font color=red> hexo s --debug</font>可以本地预览效果。
> 注：如果安装完后出现一堆奇怪的东西或错误，那么八成是安装的next版本不对，建议直接git clone我上文推荐的这个仓库。我之前就是安装成了另一个虽然高星但停止维护的低版本去了，导致一直应用不了主题，还是后来发现并安装了这个版本才成功。

## 评论功能
Next v8.0.0版本只支持*disqus | disqusjs | changyan | livere | gitalk | utterances*几种评论系统。我鼓捣了很久的*Valine*评论框架一直没有成功，最后还是选择了*changyan*（畅言）。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112013607.png)
这里首先打开Next主题文件夹下面的<b>_config.yml</b>，选择激活**active：*changyan***。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112013923.png)


### 畅言配置
先去[畅言云评](https://changyan.kuaizhan.com/)官网注册个账号。
然后按照这个顺序填写自己的信息。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112014522.png)
然后点这里获取appid和appkey。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112014917.png)
最后将上面获取的appid和appkey填入到这里。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112014003.png)
最终效果如下：
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112015411.png)
删除评论需要去畅言官网。

## 其它Next插件

[next官网](https://github.com/next-theme/awesome-next)还介绍了好几款不错的插件，例如**hexo-generator-searchdb**插件可以搜索博客内容， **hexo-filter-emoji**可以让hexo支持emoji等等。
Hexo还有很多插件，例如音乐插件Aplyer，动漫插件live2d等等，需要的可以自行百度。

# markdown编辑器推荐
没什么好推荐的，我这边比较喜欢Visual Studio Code，因为我觉得VSC安上这两个插件就很好用了。
<center>
<img src="https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112015608.png">
</center>

这篇文章[主流 Markdown 编辑器推荐](https://zhuanlan.zhihu.com/p/69210764)里介绍了很多markdown编辑器,有需要的可以看看这篇文章。

# 图床推荐
图床这里投推荐用GitHub仓库作为图床，用PicGo软件来快速上传图片并获取图片 URL 链接。这样就避免了因为路径问题，在本地储存的图片部署到Github上后失效。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112021225.png)
## PicGo配置Github图床
首先，需要在GitHub上新建一个图床仓库。过程同6.2。

然后创建一个token。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112022027.png)
最后把相关信息填到PicGo的图床设置——>GitHub图床配置里，并且选择**设为默认图床**。
![](https://raw.githubusercontent.com/lizilong1993/FigureBed/master/20210112022225.png)
到这里就配置完图床了。
## 使用PicGo
使用截图工具（例如QQ）截图后，按快捷键<kbd>Shift</kbd>+<kbd>Ctrl</kbd>+<kbd>P</kbd>就可以快速将粘贴板里的截图上传到GitHub图床仓库，按快捷键<kbd>Ctrl</kbd>+<kbd>V</kbd>就可以将图片的URL粘贴到指定位置。

# 参考文献
> - [Markdown教程|菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)
> - [个人博客搭建——介绍几种博客搭建框架](https://blog.csdn.net/weixin_45784655/article/details/104780438)
> - [Hexo+Github+Coding搭建博客](https://zhuanlan.zhihu.com/p/142545818)
> - [Hexo中文文档](https://hexo.io/zh-cn/docs/configuration.html)
> - [超详细Hexo+Github博客搭建小白教程](https://godweiyang.com/2018/04/13/hexo-blog/)