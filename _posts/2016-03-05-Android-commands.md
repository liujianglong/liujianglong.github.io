---
layout: post
title: Android开发中常用到的小工具及其命令
category: blog-cn
tags: Android 命令 Commands adb sqlite3
keywords: 
description:
---


正所谓工欲善其事必先利其器，提高效率的最主要的途径之一就是学会利用工具。在Android开发中我们会用到很多工具，其中adb，sqlite3在其中的两个非常有用的工具。这里稍微总结一下adb和sqlite3的用法，方便以后查用。

### adb

* 查看当前运行的模拟器：adb devices

* 从电脑复制文件到手机：adb push pathInPC pathInPhone  
 例如：adb push d:\abc.txt /sdcard/

* 从手机复制文件到电脑：adb pull pathInPhone pathInPC  
 例如：adb pull /sdcard/abc.txt d:\

* 启动模拟器的shell窗口： adb shell

* 安装程序： adb [-r] install abc.apk  
 [-r]表示重新安装

* 卸载程序: adb uninstall packageName

* 查看帮助信息: adb help

* 启动Activity：adb shell am start -n packageName/ClassName

* 查看Log信息：adb logcat -s 签名


### sqlite3

* .databases 查看当前的数据库
* .tables 查看当前数据库的数据表
* .help 查看sqlite3支持的命令



