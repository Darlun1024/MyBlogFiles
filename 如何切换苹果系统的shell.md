---
title: 如何切换 mac OS系统中的shell
date: 2017-05-25 16:43:32
tags: 笔记
---

### 列出系统已经安装的shell
`cat /etc/shells`
输出结果：
```
	/bin/bash
	/bin/csh
	/bin/ksh
	/bin/sh
	/bin/tcsh
	/bin/zsh
```
至于网上提到的另一种方法“ chsh -l ” ，在Mac 系统中亲测不能使用。

### 切换shell
`chsh -s /bin/zsh`

*chsh--> "change shell"* 

