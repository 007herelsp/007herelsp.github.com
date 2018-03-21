---
layout: post
title: MinGW编译boost库
key: 20180321
tags: MinGW BOOST
lang: zh
share: true <-- here
---

# MinGW编译boost库

## 介绍
在windows下编译boost可以选择msvc和mingw两种方式，这里介绍使用mingw方式编译,msvc也是类似的操作

## 源码下载
例如1.48.0
http://www.boost.org/users/history/version_1_48_0.html
使用不同的版本时将version_1_48_0替换即可

## 编译
### 编译 b2.exe
进入boost的目录，运行bootstrap.bat,成功后会生成b2.exe
```
D:\opensrc\boost_1_59_0\boost_1_59_0>bootstrap.bat
Building Boost.Build engine

Bootstrapping is done. To build, run:

    .\b2

To adjust configuration, edit 'project-config.jam'.
Further information:

    - Command line help:
    .\b2 --help

    - Getting started guide:
    http://boost.org/more/getting_started/windows.html

    - Boost.Build documentation:
    http://www.boost.org/build/doc/html/index.html

```

### 编译Boost
进入boost的目录
.\b2.exe install toolset=gcc --prefix=c:\Boost # --prefix 为类库生成地址, 不指定路径则安装在c:\boost. 可以指定参数 --with-XXX 编译指定模块, 否则全部编译
等待完成. 速度快的话大概半个小时.
```
b2 -q	-j4	toolset=gcc    link=shared	threading=multi	--layout=versioned	--without-python	--prefix="c://Boost" 
```

## CMakeLists.txt
```
cmake_minimum_required(VERSION 3.3)
project(demo)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(SOURCE_FILES main.cpp)
set(Boost_USE_STATIC_LIBS OFF)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)
find_package(Boost 1.59.0 COMPONENTS system filesystem regex REQUIRED)
if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    link_directories(${Boost_LIBRARY_DIR})
    add_executable(demo ${SOURCE_FILES})
    target_link_libraries(demo ${Boost_LIBRARIES})
endif()
# windows 下增加这一段
if(WIN32)
    target_link_libraries(demo wsock32 ws2_32)
endif()

```