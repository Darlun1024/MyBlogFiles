---
title: Java 内存模型简述
tags: Java
date: 2017-06-10 09:00:00
categories: Java
---

最新公司招聘Android开发人员，在面试的时候，技术人员总喜欢问一些JMM相关的问题，发现一部分App开发者对JMM的了解都还在小白阶段。
在下面的类里面，str和mStr中的“abc”分别存储在什么位置？
```
    public class Test(){
        private static  String str = "abc";
        private String  mStr = new String("abc");
    }
```
这个问题就难倒了好多人。

这个问题我倒是能回答，但是我发现其实自己对JMM的了解也不成系统，甚是惭愧。本周，我又翻出了之前看过的书，然后从别人Blog里面扒拉点东西，拼凑一篇关于Java内存模型的介绍文章。主要目的是梳理一下自己的知识体系，同时希望给看到此文的有缘人提供帮助和借鉴。
刚开始想系统的介绍一下JMM，发现真是高估了自己，这些知识估计能写本书了。后来，在标题上加了简述二字。无知者无畏啊。




