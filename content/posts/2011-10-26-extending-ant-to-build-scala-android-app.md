---
date: 2011-10-26 12:43:44
title: 暂时还是用ANT打包SCALA写的ANDROID应用吧
categories: 
- Android-dev
slug: extending ant to build scala android app
---

android sdk tool r14发布之后sbt和gradle的android plugin都还没做相应更新，maven的android plugin只有3.0 alpha可以用，而且需要用maven3，这样和公司的maven环境冲突，于是只能退回来继续扩展sdk tool的ant脚本了。

最早开始用scala写android的时候就是通过这里 [Exploring Android](http://lamp.epfl.ch/~michelou/android/) 的ant脚本编译打包应用的，后来想方便的集成[Robospecs](https://github.com/jbrechtel/robospecs) ([Robolectric](http://pivotal.github.com/robolectric/) with [Specs2](http://specs2.org)) 做单元测试，才把目光转向了sbt和gradle，可惜这俩对library project的支持不好，虽然sdk tool r14对这块做了不少优化，还是不能简单的把library project做成一个jar library(现在仅包含class文件，资源文件还是单独处理的)，roadmap里说r15会争取实现这个功能。

好吧，总不能因噎废食，还是扩展sdk tool的ant脚本最满足当前的需求，于是在 [Exploring Android](http://lamp.epfl.ch/~michelou/android/) 的基础上改出了这个 [ant-android-scala](https://github.com/imsizon/ant-android-scala)
