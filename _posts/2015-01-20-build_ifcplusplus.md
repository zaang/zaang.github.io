---
layout: post
category: Linux
title: Build IfcPLusPlus
tagline: 2015-01-20
tags: [linux, osg]
---

在 Ubuntu14.04 版本中编译 IfcPLusPlus

<!--more-->

更新源

    sudo apt-get update

安装依赖库

    apt-get install build-essential
    
    apt-get install cmake git
    
    apt-get install libboost-dev
    
    apt-get install libopenscenegraph-dev
    
    apt-get install libqt4-dev

下载并编译

    git clone git://github.com/berndhahnebach/IfcPlusPlus/ ifcplusplus
    
    cd ifcplusplus
    
    mkdir build
    
    cd build
    
    cmake ../
    
    make
    
    cd Debug
    
    ./IfcPlusPlusViewer