---
title: AppleDoc Guide
date: 2016-02-24 11:20:39
tags:
---

## AppleDoc简介



github网址 [https://github.com/tomaz/appledoc](https://github.com/tomaz/appledoc)



`cd ./appledoc`<p>



--output ./doc：设置输出目录为当前目录下的 doc 文件夹下，可以自己设置<p>
--project-name MideaSDK：设置项目名为 “MideaSDK”，可自己设置<p>
.：当前目录
>目前知道 enum 枚举和 block 无法生成文档




可以通过命令`appledoc --help`来查看 appledoc 所有参数用法。





`/**` 类的简介 `【整个注释的示例 从“ /** ”开始,到 " */ "结束 】`

 
 
 
    	

	> `## This is an H2` 
	> `### This is an H3`
	> `#### This is an h4`
	> `###### This is an H6`


 	

	> 这里会引用到类 `YYColor`
     	
 @since iOS5.0
 `*/`

/** 这里是属性说明: 名字 */

 /** 
 
 
 
 
 
 
 
 
 
 
 
 








![Alt text](http://i12.tietuku.com/d52c1219753b2f18.png)
