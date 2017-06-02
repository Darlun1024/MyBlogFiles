---
title: Kotlin 第一行代码
date: 2017-05-23 10:10:08
tags: Kotlin
categories: Kotlin

---
### 使用 kotlin 打印一行文本
***
`package com.wsj.kotlin`

`class Main {}`
`fun main(args:Array<String>){`
	`	println("hello world!")`
`}`

就这么几行代码和Java的区别就有好几处
1.代码后面可以没有分号；
2.方法定义在class的{}外面；
3.main函数不需要用static关键字限定；
4.方法的定义和Java也有较大的区别 fun 方法名(参数:参数类型){方法体}