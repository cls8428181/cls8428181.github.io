---
layout: post
title: 如何优雅的在 Xcode8以上版本使用插件.
category: iOS
tags:
keywords:

description:
---

升级Xcode8之后会发现，在Xcode8中所有第三方插件都失效了，xcode8增加了安全相关的检查，并且连之前菜单栏的插件选项也不存在了。在之前很多的iOS开发者，都是通过恶魔来管理插件的，现在恶魔也是不可用的。但是Xcode8自身也对编译器进行了升级，将一些比较好的插件功能加入到的Xcode中，例如单行高亮显示等。

在Xcode8中支持了开发插件工程，并且为我们提供了一个插件模板，开发的插件可以上传到App Store下载苹果这么做有一个原因在于，之前Xcode和插件是运行在同一个进程的，所以插件的崩溃也会导致Xcode的崩溃。苹果现在将插件作为一个单独的应用程序，分开进程运行，不会对Xcode中带来其他影响。

![]({{site.url}}/assets/postImages/ios/buildxcode_01.png)
----

###但是，如果我就是想继续使用恶魔，怎么办？（别急，方法肯定是有的）

* 在 Docker 上右键关闭你的 Xcode

* 准备一个代码证书, 打开钥匙串，KeyChain Access - >证书助理 - >创建证书
![]({{site.url}}/assets/postImages/ios/buildxcode_02.png)
* 为证书类型选择“代码签名”, 在这里我自定义 Name 为 XcodeSigner, 你可以自定义自己喜欢的 Name, 但是一定要记住,因为一会要用到。
![]({{site.url}}/assets/postImages/ios/buildxcode_03.png)
* 在终端重新签署Xcode, 注意⚠️你的命名是不是XcodeSigner，如果不是,就替换掉。(这个过程可能需要一会,请耐心等待)

````
$ sudo codesign -f -s XcodeSigner /Applications/Xcode.app 
````
* 使用 git Clone XVim

````
$ git clone https://github.com/XVimProject/XVim.git
````
* 切换目录到刚才下载的 XVim 根目录,然后使用下面的确认xcode-select是否是你的的Xcode路径, 正确的路径应该是 /Applications/Xcode.app/Contents/Developer, 请检查是否一样

````
$ xcode-select -p
````
* 用命令行 build XVim

````
$ make
````

* 如果出现下列提示, 请输入 y 继续

````
XVim hasn't confirmed the compatibility with your Xcode, Version X.X
Do you want to compile XVim with support Xcode Version X.X at your own risk? 
````
* make 完成之后了,输入如下命令切换回根目录

````
$ cd ~
````
* 下载并安装 Alcatraz,关于 Alcatraz 的使用请看这里[ Alcatraz 的使用](http://www.jianshu.com/p/7a2484123bf6)

````
$ curl -fsSL https://raw.github.com/supermarin/Alcatraz/master/Scripts/install.sh | sh
````

* 好了,最后一步,确认你的 Xcode 是关闭着的,并在终端输入下列命令

````
$ find ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins -name Info.plist -maxdepth 3 | xargs -I{} defaults write {} DVTPlugInCompatibilityUUIDs -array-add `defaults read /Applications/Xcode.app/Contents/Info.plist DVTPlugInCompatibilityUUID`
````
* 重新打开Xcode，加载插件, 安装成功.

感谢收看，如果对大家有帮助，请[github上follow和star](https://github.com/cls8428181)，本文发布在[常立山的技术博客](https://cls8428181.github.io/)，转载请注明出处