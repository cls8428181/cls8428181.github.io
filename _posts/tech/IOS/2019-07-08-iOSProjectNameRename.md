---
layout: post
title: 在iOS项目中，如何完美的修改项目名称
category: iOS
tags:
keywords:
description:
---

### 前言：

在iOS开发中，有时候想改一下项目的名字，这会遇到很多麻烦。

*   直接改项目名的话，Xcode不会帮你改所有的名字
*   项目中的很多文件、文件夹或者是项目设置的项，都是不能随便改的，有时候改着改着，就会编译不了。

所以各位重命名项目时，记得先备份好一份噢。本文我会介绍一种“完美”的修改方法。

**注意：重命名项目时，记得先备份好一份**

**注意：重命名项目时，记得先备份好一份**

**注意：重命名项目时，记得先备份好一份**

**重要的事情说三遍**

本文会把一个项目名叫 `OldDemo123` 改成 `NewDemo`。

### 正文：

修改前的项目结构：

 ![](https://upload-images.jianshu.io/upload_images/329784-a6c5e150a4b8bbb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/512/format/webp)

 修改前的项目结构

##### 1、打开项目，对项目名进行 **`Rename`**

1.1、选中项目名并按下回车，进入可编辑状态：

 ![](https://upload-images.jianshu.io/upload_images/329784-fa558ab1342570c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/570/format/webp)

 选中项目名字，进行编辑

1.2、输入新的项目名字，然后按回车，弹出改名前和改名后的文件对名，这时点击 `Rename`：

 ![](https://upload-images.jianshu.io/upload_images/329784-8a1cf4874bf9ddd4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 点击 **Rename**

##### 2、修改文件夹名字和显示包内容

2.1、打开应用所在文件夹，修改文件夹名字

注意：

*   文件夹`NewDemoTests`和`NewDemoUITests`里面也要修改
*   这里的`NewDemoTests`，原先为`OldDemo123Tests`。
    我们改名字时需要注意，只需要把旧名字（`OldDemo123`）替换成新名字（`NewDemo`）即可，不要把其它字符（`Tests`）删除！

 ![](https://upload-images.jianshu.io/upload_images/329784-15b4a71e159e09a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 修成后的文件夹名字

2.2、选中 `NewDemo.xcodeproj` 右键打开 --> 显示包内容 --> 双击打开 `project.pbxproj`。

 ![](https://upload-images.jianshu.io/upload_images/329784-c4227fc432a4ed20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/782/format/webp)

 显示包内容，双击打开 project.pbxproj

2.3、打开 `project.pbxproj` 文件之后，用搜索快捷键 `command + f` 全局搜索旧的项目名 `OldDemo123` ，并用新的项目名 `NewDemo` 进行替换。替换完成后进行保存 `command + s`，然后关闭。

注意：要把所有的 `OldDemo123` 更换成 `NewDemo`。

 ![](https://upload-images.jianshu.io/upload_images/329784-17b868c4b814bb4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 搜索 OldDemo123 ，并替换成 NewDemo

##### 3、打开 `NewDemo.xcodeproj` 文件

注意：打开的是 `NewDemo.xcodeproj` 文件，而不是 `NewDemo.xcworkspace`文件。

3.1、此时会弹出提示框，点击 `OK` 就行。

 ![](https://upload-images.jianshu.io/upload_images/329784-9b7901662ad6609b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/906/format/webp)

 弹出提示框

3.2、显示此时项目结构和修改更新`Podfile`文件

 ![](https://upload-images.jianshu.io/upload_images/329784-65a4d17f717f2a52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/506/format/webp)

 修改好项目结构

如果你的项目里面没有使用CocoaPods的话，项目应该可以运行成功了。

使用CocoaPods的话，项目虽然表面看起来已经修改成功了，但是运行之后发现提示错误：

 ![](https://upload-images.jianshu.io/upload_images/329784-1ad843df8f7d8e34.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 使用CocoaPods的话，会提示的错误

此时打开项目文件夹，找到 `Podfile` 文件，双击打开，修改 `target` 后的项目名为最新的项目名 `NewDemo`。

<code class="ruby">target 'NewDemo' do
pod 'AFNetworking', '~> 3.0'
end</code> 

然后在终端，用 `cd` 到项目目录下，运行 `$ pod install`，进行更新。

3.3、打开 `NewDemo.xcworkspace` 文件
此时文件显示错误：因为文件路径的原因

 ![](https://upload-images.jianshu.io/upload_images/329784-431876ffa52d9a54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/764/format/webp)

 错误显示

选中显示红色的 `OldDemo123` 文件，点击右侧文件夹小图标，更改路径。

 ![](https://upload-images.jianshu.io/upload_images/329784-d4d1415c11a34bf5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 修改文件路径

路径更改成功之后，项目基本就可以运行成功了。

##### 4、修改 `Scheme` 名

选中 `OldDemo123` --> 下拉中选中 `Manage Schemes` --> 弹出一个显示框。

 ![](https://upload-images.jianshu.io/upload_images/329784-089c8f378d70371d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/832/format/webp)

 修改Scheme名

选中要修改的 `OldDemo123` 那一行，并按下回车，进行修改新的名称 `NewDemo`，然后点击 `Close`。

 ![](https://upload-images.jianshu.io/upload_images/329784-0ec6c2834a67baa5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 修改新的 Scheme 名

##### 5、项目内全局修改、替换

其实到上面，项目已经基本修改完成了，但是对于一些处女座、强迫症患者来说，还有一些问题，如下：

 ![](https://upload-images.jianshu.io/upload_images/329784-3e495148014f7c0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

 生成类时的顶部介绍

5.1、全局搜索旧的项目名

 ![](https://upload-images.jianshu.io/upload_images/329784-e985cd32211e3036.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/584/format/webp)

 全局搜索

5.2、把 `Find` 修改为 `Replace`，输入新的项目名，点击 `Replace All` 全局替换。

 ![](https://upload-images.jianshu.io/upload_images/329784-df17899bc5e1b894.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/592/format/webp)

 全局替换

### 最后：

到此，项目名已经完全修改完成了，小伙伴们可以尝试修改了。

下面是修改后的项目结构：

 ![](https://upload-images.jianshu.io/upload_images/329784-a145959de5ce3f72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/644/format/webp)

 修改后的项目结构

**注意：重命名项目时，记得先备份好一份**

感谢收看，如果对大家有帮助，请[github上follow和star](https://github.com/cls8428181)，本文发布在[常立山的技术博客](https://cls8428181.github.io/)，转载请注明出处
