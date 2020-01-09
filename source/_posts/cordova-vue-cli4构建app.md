---
title: cordova+vue-cli4构建app
date: 2020-01-09 14:15:52
tags:
---

本文会详细的介绍如何使用cordova来打包vue项目，生成app（android）
<!--more-->
* 欢迎加入前端交流群来获取视频资料以及前端学习资料：[749539640](//shang.qq.com/wpa/qunwpa?idkey=f528775f242a7c39fe8512383febb8990e621bf97354c2fb82f6832097b7c501) 


你将学会：
* 基于cordova构建vue项目app
* 自定义app名字/图标/启动页图片
* 自动构建脚本

> Cordova[(中文官网详细介绍)](https://cordova.axuer.com/docs/zh-cn/latest/guide/overview/)是一个开源的移动开发框架。允许你用标准的web技术-HTML5,CSS3和JavaScript做跨平台开发,应用的实现是通过web页面，默认的本地文件名称是index.html
大体思路就是把打包好的vue项目放在cordova的Web App中来启动；我们开始吧

#### 1.环境准备
* Java SDK 8(cordova最高支持到8)[下载地址](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
   * [window环境配置](https://www.runoob.com/java/java-environment-setup.html)
   * [linux环境配置](https://www.runoob.com/w3cnote/win7-linux-java-setup.html)
   * [mac Os环境配置](https://java.com/en/download/help/mac_install.xml)
* [Gradle](https://gradle.org/install/)
* [Cordova 8.0](https://cordova.axuer.com/)
* [Node](http://nodejs.cn/)
* [vue-cli](https://cli.vuejs.org/zh/)
* [Android Studio /Android SDK](https://cordova.axuer.com/docs/zh-cn/latest/guide/platforms/android/index.html)
  * [Android Studio](https://developer.android.com/studio?pkg=tools)
  * [Android SDK](https://developer.android.com/studio?pkg=tools)

#### 2.验证环境
![](https://user-gold-cdn.xitu.io/2020/1/6/16f79016fdc46f83?w=1072&h=950&f=png&s=129274)

* 项目目录
```
cordova
│   cordova-project
│   my-app   
```
这里把cordova项目和vue项目平级存放，也可以嵌套（自行看情况）

#### 3.新建cordova项目
* ###### 3.1新建cordova目录
* ###### 3.2在cordova文件夹下新建cordova项目
```
mkdir cordova
cd cordova
cordova create cordova-project
```
* ###### 3.3添加Android平台
```
cd cordova-project
cordova platform add android --save
```
> 要构建和运行App，你需要安装每个你需要平台的SDK。另外，当你使用浏览器开发你可以添加 browser平台，它不需要任何平台SDK。

* ###### 3.4 检测你是否满足构建平台的要求:
```
cordova requirements
```
![](https://user-gold-cdn.xitu.io/2020/1/6/16f79016fd4c88cb?w=838&h=135&f=png&s=21675)

* ###### 3.5打包app安装到手机上（前提是手机连上电脑并开启USB调试模式）
```
cordova run android
```
* 或者只是打包apk
```
cordova build android
```
apk生成目录：cordova-project/platforms/android/app/build/outputs/apk/debug/app-debug.apk

默认生成的cordova app 图标：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901700ca43ad?w=105&h=104&f=png&s=13778)
运行界面：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901700db02da?w=800&h=1280&f=png&s=83037)

进行到这里的时候，cordova部分先告一段落，下面开始第二部分
#### 4.新建vue项目（[vue-cli](https://cli.vuejs.org/zh/)）
```
cd cordova
vue create my-app
//配置里我们选择默认项就行default (babel, eslint)
cd my-app
npm install 
npm run serve
```

* ###### 4.1浏览器运行vue项目界面：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901701f43c63?w=700&h=1302&f=png&s=103383=100px*100px)
* ###### 4.2打包vue项目
* 配置[vue.config.js](https://cli.vuejs.org/zh/config/)
* my-app目录下新建vue.config.js（这里只做路径配置，其他配置项可详情[vue.config.js](https://cli.vuejs.org/zh/config/)）
> 默认情况下，cordova create命令生成基于web的应用程序的骨骼，项目的主页是 www/index.html 文件。

```
'use strict'

module.exports = {
  publicPath: './',
//这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径，也可以用在类似 Cordova hybrid 应用的文件系统中。
  outputDir: '../cordova-project/www',
//将打包目录指向/cordova-projec下的www
  productionSourceMap: false,
//如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。

}

```
* 配置好之后我们进行打包
```
npm run build 
```
*  ###### 4.3打包apk安装到手机上
```
cd cordova-project
cordova run android 
```
或者是打包apk
```
cd cordova-project 
cordova build android 
```
运行至手机界面：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901703463555?w=1080&h=1920&f=png&s=199676)

#### 5.浏览器调试app
运行```cordova run android ```后，app会装到手机上
谷歌浏览器输入：chrome://inspect/#devices
看到如下界面：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f790171c9ef400?w=396&h=438&f=png&s=39837)
找到自己的设备（手机中也需要运行app），点击inspect，接下来就可以调试样式了
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901724d53642?w=1210&h=744&f=png&s=237101)

#### 6.更换app图标以及app名字以及app启动页
先随便准备2张图片（图标以及启动页图片）
*  ###### 6.1更改图标：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901724d519f5?w=212&h=216&f=png&s=128131)
进入文件夹：```cordova/cordova-project/res/icon/android ```
将图片进行替换即可（名字/图片格式推荐png）
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901726e3b0b1?w=458&h=118&f=png&s=22844)
替换为：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f790172995d8b1?w=476&h=108&f=png&s=16175)

*  ###### 6.2更改启动页图片：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901727c089d7?w=318&h=578&f=png&s=94922)
安装splashscreen插件：
```
cd cordova-project
cordova plugin add cordova-plugin-splashscreen
```
进入文件夹：```/cordova/cordova-project/res/screen/android ```
将图片进行替换即可,这里只替换了竖屏的（名字/图片格式推荐png）
![](https://user-gold-cdn.xitu.io/2020/1/6/16f7901741bd0a56?w=659&h=271&f=png&s=28137)
替换为
![](https://user-gold-cdn.xitu.io/2020/1/6/16f790174a5fad86?w=663&h=236&f=png&s=26149)

* 打开```config.xml```
*  ###### 6.3更改名字(name标签内的内容进行更改即可)
```
 <name>vueApp</name>
```
*  ###### 6.4更改配置项
添加图标以及启动页，在``` <platform name="android"> </platform>```添加如下代码

```
   <platform name="android">
        <allow-intent href="market:*" />
        <icon density="ldpi" src="res/icon/android/icon-36-ldpi.jpg" />
        <icon density="mdpi" src="res/icon/android/icon-48-mdpi.jpg" />
        <icon density="hdpi" src="res/icon/android/icon-72-hdpi.jpg" />
        <icon density="xhdpi" src="res/icon/android/icon-96-xhdpi.jpg" />
        <splash density="port-ldpi" src="res/screen/android/screen-ldpi-portrait.png" />
        <splash density="port-mdpi" src="res/screen/android/screen-mdpi-portrait.png" />
        <splash density="port-hdpi" src="res/screen/android/screen-hdpi-portrait.png" />
        <splash density="port-xhdpi" src="res/screen/android/screen-xhdpi-portrait.png" />
        <preference name="ShowSplashScreenSpinner" value="false" /><!-- 启动页面淡入淡出的效果 -->
    </platform>
```
* 打包查看
图标以及名字：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f790174a6d407a?w=90&h=115&f=png&s=20233)
启动页：
![](https://user-gold-cdn.xitu.io/2020/1/6/16f790174d621f02?w=800&h=1280&f=png&s=267397)

#### 7.自动构建脚本（shell）
每次打包需要执行如下命令，很麻烦
```
cd cordova/my-app
npm install
npm run build
cd ../cordova-project
cordova build android /cordova run android
```
我们可以在cordova目录下新建build.sh文件
```
#!/usr/bin/env bash



PLATFORM=android
#!1(not clean)   0(clean)
TYPE=build
#!(-d)debug   build
TYPE=$1

 
function echo_action() {
    INFO_START='\033[1;36m'
    INFO_END='\033[0m'
    echo -e "\xF0\x9F\x90\xB6 ${INFO_START}$1${INFO_END}"
}

function echo_info() {
    INFO_START='\033[1;32m'
    INFO_END='\033[0m'
    echo -e "\xF0\x9F\x92\x9A ${INFO_START}$1${INFO_END}"
}

function echo_warn() {
    INFO_START='\033[1;33m'
    INFO_END='\033[0m'
    echo -e "\xF0\x9F\x92\x9B ${INFO_START}$1${INFO_END}"
}

function echo_err() {
    INFO_START='\033[1;31m'
    INFO_END='\033[0m'
    echo -e "\xF0\x9F\x92\x94 ${INFO_START}$1${INFO_END}"
}


function addAndroidPlatform() {
    echo_action "Start add android platform ..."
     cordova platform add android
    if [ "$?" != "0" ]; then
        return 1
    fi
    return 0
}



function installDependencesCordova() {
    echo_action "Installing Cordova dependences ..."
    npm install
    echo_info " Cordova Dependences installed"
}


function installDependences() {
    echo_action "Installing dependences ..."
    echo_action "cd ./my-app"
    cd ./my-app
    npm install
    echo_info "Dependences installed"
}


function buildWebapp() {
    echo_action "Start building my-app..."
    npm run build
    echo_info "Build Command:  npm run build"

}

function installPlugins() {
    addAndroidPlatform
    echo_info "Install App Updater plugin finished"
}

function buildApk() {
    echo_action "Start building ..."
    if [ "${TYPE}" == "debug" ]; then
          cordova run android
          echo_info "Build Command:  cordova run android"
    else
        cordova build android
         echo_info "Build Command:  cordova build android"
    fi
}


echo_info "Build for ${PLATFORM}"
if [ "${TYPE}" == "debug" ]; then
        echo_info "Build Command:  cordova run android"
else
        echo_info "Build Command:  cordova build android"
fi


installDependences
if [ "$?" == "0" ]; then
    echo_info "All dependences have been installed successfully."
else
    echo_err "Failed to install dependences."
fi

buildWebapp
if [ "$?" == "0" ]; then
    echo_info "All things done successfully."
else
    echo_err "Build failed."
fi

echo_action "cd ../cordova-project"
cd ../cordova-project

installPlugins
if [ "$?" == "0" ]; then
    echo_info "All plugins have been installed successfully."
else
    echo_err "Failed to install plugins."
fi

installDependencesCordova
if [ "$?" == "0" ]; then
    echo_info "All dependences have been installed successfully.."
else
    echo_err "Failed to install dependences."
fi


buildApk
if [ "$?" == "0" ]; then
    echo_info "All things done successfully."
else
    echo_err "Build failed."
fi

```
这样我们下次就可以
```
cd cordova
./build.sh build //打包apk
./build.sh debug //调试至手机
```

#### 8.vue中使用cordova,详情[vue-cordova](https://github.com/kartsims/vue-cordova)
