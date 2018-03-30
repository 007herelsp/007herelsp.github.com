---
layout: post
title: "windows+CMake+mingw 搭建c c++开发环境"
date: 2018-03-30 22:23:06
tags: windows CMake mingw c/c++
key: 201803302223
description: 本文教你如何在windows环境下使用CMake和mingw搭建同linux开发一样体验的c/c++开发环境
---

## CMake 安装
### CMake 下载
官方下载地址: https://cmake.org/download/
![cmake下载页面](https://upload-images.jianshu.io/upload_images/4938916-1f66b219b69a68c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择自己系统(**Platform**)对应的版本并下载
这里我们选择**Windows win64-x64 Installer: Installer tool has changed. Uninstall CMake 3.4 or lower first!**

![CMake 下载完成](https://upload-images.jianshu.io/upload_images/4938916-6c0b1b8cc84e2665.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### CMake 安装
安装时根据自己系统的安全设置，可能会出现如下对话框，不用担心，直接点击 **"运行(R)"**
![安装时安全警告](https://upload-images.jianshu.io/upload_images/4938916-4e1403fa98b8f0dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![CMake Steup](https://upload-images.jianshu.io/upload_images/4938916-7fe8c54b142d87b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![License](https://upload-images.jianshu.io/upload_images/4938916-6f36f8cdf38badc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
*必须选择同意，否则不能进入下一步*

![安装选项](https://upload-images.jianshu.io/upload_images/4938916-242076ca9dd5c541.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 是否添加环境变量，这里我们选择 **"Add CMake to the system PATH for all users"**
* 是否创建桌面快捷图标，根据自身情况而定，这个只是创建桌面图标使用方便，并不会对以后的使用造成实质上的影响

### 安装路径
这里选择自己习惯存放程序的路径，我们这里采取默认值
![安装路径](https://upload-images.jianshu.io/upload_images/4938916-55fcc11c9e84a4aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 安装最后确认
经过前面的操作终于把需要配置的都配置了，下面该程序自己干活了
![安装最后确认](https://upload-images.jianshu.io/upload_images/4938916-ea54db960ee87f5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 进入安装
真正开始安装的阶段，这一阶段比较耗时，完全取决于电脑自身的配置高低，系统主要是解压文件和写磁盘
![安装中](https://upload-images.jianshu.io/upload_images/4938916-4b14d25d350f6d99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 安装完成
共享你，终于将CMake安装完成了
![安装完成页面](https://upload-images.jianshu.io/upload_images/4938916-c9485943428202dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 确认CMake安装
验证CMake是否成功安装，可以调出CMD窗口，输入`cmake`，瞧瞧系统会给你说什么，如果出现如下窗口，那么恭喜你没有任何问题。
![CMake安装好 ](https://upload-images.jianshu.io/upload_images/4938916-63fc0b883d5d7970.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

那么万一出现的是如下内容呢

![CMake没安装好](https://upload-images.jianshu.io/upload_images/4938916-61e292f409a36952.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们一般有如下处理步骤和处理方法：
* 1. 确认是新调出CMD窗口再进行的操作
* 2. 我们可以手动修改系统的环境变量指定CMake的bin目录位置

![系统环境变量 Path](https://upload-images.jianshu.io/upload_images/4938916-cd4618df2662ed20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
确认如图所示内容在Path中配置，如果没有可以手动输入并确定

* 3. 待2操作完成后可以再验证，如果解决那么恭喜，如果问题仍存在，那么需要重启系统（一般都能解决了，除非比较低的系统版本可能需要重启）


## mingw
### mingw 下载
这里给出64系统使用的mingw, https://sourceforge.net/projects/mingw-w64/

![mingw下载完成](https://upload-images.jianshu.io/upload_images/4938916-e1b2e4fb22c7b05b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里其实是下载的一个安装器，具体的安装是通过运行这个安装器来引导安装的

### mingw 安装
![开始运行安装器](https://upload-images.jianshu.io/upload_images/4938916-c74924e17d0399fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### mingw 安装选项
![安装选项](https://upload-images.jianshu.io/upload_images/4938916-7eabb5f28f9f3b06.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里需要做出对应的选择，当然完全默认没有任何问题，我们这里采用默认，继续安装
### mingw 安装位置
![安装位置选择](https://upload-images.jianshu.io/upload_images/4938916-81c3b5084fc69ae9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**这里有坑，我们先入坑**, 继续安装

### mingw 安装中
![安装中](https://upload-images.jianshu.io/upload_images/4938916-cd59d5495342b2e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
安装器需要从网上下载所需要的文件，这一步耗时较长

### mingw 安装完成
![安装完成](https://upload-images.jianshu.io/upload_images/4938916-0f09070d12a4069f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 环境变量设置
同CMake的一样，mingw安装完后自动了设置环境变量，你也可以通过运行其安装目录下的`mingw-w64.bat`来进入运行环境
![mingw-w64.bat](https://upload-images.jianshu.io/upload_images/4938916-278142c689b098f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
验证mingw环境是否设置好，同样新调出CMD窗口，输入`gcc`命令，出入如下信息则表示安装没有问题，否则请参照CMake配置环境变量的方式来解决。
![gcc 命令](https://upload-images.jianshu.io/upload_images/4938916-a3fa27ce782fa639.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## CMake+mingw 实例
我们安装完环境后来个实例运行下吧
* 编写源码文件
来个宇宙最著名的程序吧
```
#include <stdio.h>

int main()
{
	printf("hello\n");
	
	return 0;
}
```
* 编写CMake文件
```
cmake_minimum_required(VERSION 3.0)
project(Hello)
set(SOURCE main.cpp)
add_executable(${PROJECT_NAME} ${SOURCE})

```
* 生成Make file

```
mkdir build
cd build
cmake -G"Unix Makefiles" ../
```
很不幸，这一步会出问题
```
CMake Error: CMake was unable to find a build program corresponding to "Unix Makefiles".  CMAKE_MAKE_PROGRAM is not set.  You probably need to select a different build tool.
CMake Error: CMAKE_C_COMPILER not set, after EnableLanguage
CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage
-- Configuring incomplete, errors occurred!
See also "D:/tmp/build/CMakeFiles/CMakeOutput.log".

```
意思就是不能生成Unix Makefiles，这是缺少make程序造成的，
解决方法就是找到mingw安装目录下mingw32-make.exe拷贝一份并重命名为make.exe
![make](https://upload-images.jianshu.io/upload_images/4938916-65e8b10f721b725f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
再运行`cmake -G"Unix Makefiles" ../`
```
$ cmake -G"Unix Makefiles" ../
-- The C compiler identification is GNU 7.2.0
-- The CXX compiler identification is GNU 7.2.0
-- Check for working C compiler: C:/Program Files (x86)/mingw-w64/i686-7.2.0-posix-dwarf-rt_v5-rev1/mingw32/bin/gcc.exe
-- Check for working C compiler: C:/Program Files (x86)/mingw-w64/i686-7.2.0-posix-dwarf-rt_v5-rev1/mingw32/bin/gcc.exe -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: C:/Program Files (x86)/mingw-w64/i686-7.2.0-posix-dwarf-rt_v5-rev1/mingw32/bin/c++.exe
-- Check for working CXX compiler: C:/Program Files (x86)/mingw-w64/i686-7.2.0-posix-dwarf-rt_v5-rev1/mingw32/bin/c++.exe -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: D:/tmp/build

```
这样就对了
* 编译
```
make
```

什么，又有问题
```
$ make
/usr/bin/sh: -c: line 0: syntax error near unexpected token `('
/usr/bin/sh: -c: line 0: `C:/Program Files (x86)/mingw-w64/i686-7.2.0-posix-dwarf-rt_v5-rev1/mingw32/bin/make -f CMakeFiles/Makefile2 all'
make: *** [Makefile:84: all] Error 1

```
还记得前面我们安装mingw时说的坑吗，现在我们需要填坑了，文件就是万恶的`C:/Program Files (x86)`，这也好办，将`mingw-w64`文件夹复制到一个正常的目录吧，比如直接`C:/mingw-w64`，然后需要修改环境变量
![修改mingw环境变量](https://upload-images.jianshu.io/upload_images/4938916-f694a58c71443330.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
$ make
Scanning dependencies of target Hello
[ 50%] Building CXX object CMakeFiles/Hello.dir/main.cpp.obj
[100%] Linking CXX executable Hello.exe
[100%] Built target Hello

```
* 运行
```
$ ./Hello.exe
hello
```
好了，终于成功了

