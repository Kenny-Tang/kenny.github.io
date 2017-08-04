title: maven
date: 2017-08-04 11:34:59
tags:
---
### 简介
[Maven](https://maven.apache.org) 是一个优秀的开源代码管理工具， [Apache](http://www.apache.org/) 基金会下众多的顶级项目之一，在Java的世界里Maven的重要性是不言而喻的，已经成为了Java项目构建事实上的标准，她所使用的思想影响了很多人，让大家对项目如何构建有了一个崭新的认知。

从 [Apache](http://www.apache.org/) 首页的项目列表中我们可以找到她
![](/images/lALPACOG82b-633NAgTNBZs_1435_516.png_620x10000q90g.jpg)
### 安装与配置
[Maven](https://maven.apache.org) 的安装十分的简单，解压即安装
笔者安装目录为 
I:\example\


![](/images/pasted-0.png)

接下来就是要配置Maven
首先设置环境变量
计算机 --> 右键属性 --> 高级系统设置 --> 高级选项页 -->  环境变量 --> 新建环境变量



变量名称 MAVEN_HOME
变量值 I:\example\apache-maven-3.3.3

在DOS 窗口中测试如下


通常其他的配置可以再settings.xml 文件中进行相应的配置，settings.xml 文件存在于两个位置，
一个用于Maven的全局配置，
该文件位于${MAVEN_HOME}/conf/settings.xml， 
另外一个为用户自定义配置项位于用户目录下
${user.home}/.m2/settings.xml
通常不会更改全局配置文件。
一般需要更改仓库目录到自定义的位置，如果不进行配置则默认在${user.home}/.m2/respository下
配置示例如下 ： &lt;localRepository>/path/to/local/repo&lt;/localRepository>

![](/images/pasted-1.png)