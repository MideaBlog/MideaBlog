---
title: AppleDoc Guide
date: 2016-02-24 11:20:39
tags:
---

## AppleDoc简介
手工写文档是一件苦差事，appledoc 是一个能从源码中抽取注释生成文档的专用工具，简单方便，适于生成 apple 官网帮助风格的 html 文档，也可以直接集成到 Xcode 帮助（Docset 格式），这样后续只需要按照规定的格式在代码里写好注释就行了，无需单独再编写帮助文档（这个工具仅限于输出 apple 文档格式，如果是要图文并茂的文档，另行他法）。
appledoc官网 [http://gentlebytes.com/appledoc/](http://gentlebytes.com/appledoc/)

github网址 [https://github.com/tomaz/appledoc](https://github.com/tomaz/appledoc)
## AppleDoc安装
正常安装，在终端下操作只需三步，该工具是一个二进制可执行文件，缺省会安装到 `/usr/local/bin/` 目录下，安装步骤：
`git clone git://github.com/tomaz/appledoc.git`<p>
`cd ./appledoc`<p>`sudo sh install-appledoc.sh`
另外，也可以去 [github网站](https://github.com/tomaz/appledoc) 上直接下载源码编译安装。## AppleDoc使用
在终端下进入工程文件所在目录，运行下面的命令（注意命令最后有个小点），缺省会编译出 Docset 并安装进 Xcode。
`appledoc --output ./doc --project-name MideaSDK --project-company MideaSDK --company-id cn.com.Midea . `>参数注明——<p>
--output ./doc：设置输出目录为当前目录下的 doc 文件夹下，可以自己设置<p>
--project-name MideaSDK：设置项目名为 “MideaSDK”，可自己设置<p>--project-name MideaSDK：设置项目名为 “MideaSDK”，可自己设置<p>--project-company MideaSDK：设置公司名为 “MideaSDK”，可自己设置<p>--company-id cn.com. MideaSDK：设置公司id为 “cn.com.MideaSDK”，可自己设置<p>
.：当前目录命令执行期间，会对整个工程目录进行扫描，并生成文档，期间可能在终端上会产生一些告警，说明哪些文件注释写得有问题或者无法生成文档，告警很直观，可以根据告警来修改注释的格式。
>目前知道 enum 枚举和 block 无法生成文档
缺省会编译出的 Docset 是放在下面的路径：`/Users/XXX/Library/Developer/Shared/Documentation/DocSets`
Docset格式，实际上是一个bundle，里面包含了一些 xml 和 html。显示包内容后就可以查看和修改了。如果需要放到网站上，或者拿出来给别人阅读，可以单独将 html 部分取出来就行。
当该命令完成后，重启 Xcode 打开 Xcode 帮助文档，会发现其中新增了 MideaSDK 相关文档。如果不想编译成 Docset 格式，只需要 html 文档时，可以加上参数 `--no-create-docset`，如果不想扫描整个工程目录，需要忽略其中一些目录的时候，还可以加上 `--ignore`参数（注意命令行最后有个小点）：`appledoc --output ./doc --no-create-docset --ignore ./MSmartSDK/MSmartSDK/Internal/Vendors --project-name MideaSDK --project-company MideaSDK --company-id cn.com.Midea . `当该命令完成后，在当前目录会生成一个 html 文件夹，使用浏览器打开`./doc/html/index.html`即可查看帮助文档。

可以通过命令`appledoc --help`来查看 appledoc 所有参数用法。## AppleDoc注释语法
* 首先，文档中的注释只有符合规范，才能被 appledoc 认可。
* 凡是以 "///"、"/**" 或 "/*!" 开头的注释块，都算所 appledoc 注释。下面是示例:
	> `///` 这是单行注释。<p>	> `/**` 这也是单行注释 `*/`<p>	> `/*!` 同样是单行注释 `*/`<p>	> `/**` 这也是单行注释，<p>	> `*` 第二行会接上第一行。<p>	> `*/`
* 注释块中，每一行开头的空格和 "*" 字符多数情况都会被 appledoc 忽略。连续的两行(即没有间隔空行)的注释，将被合并成一个段落，并忽略换行，就像 html。### 下面是一个完整的语法例子以及最终显示效果:

`/**` 类的简介 `【整个注释的示例 从“ /** ”开始,到 " */ "结束 】`
* 无序列表: (每行以 '*'、'-'、'+' 开头):
 	> * this is the first line<p>	> * this is the second line<p>	> * this is the third line<p> * 有序列表: (每行以 1.2.3、a.b.c 开头):
 	> a. this is the first line<p>	> b. this is the secode line<p> * 多级列表:
 	> * this is the first line<p>    	a. this is line a<p>    	b. this is line b<p>
    		> * this is the second line<p>    	1. this in line 1<p>    	2. this is line 2 * 标题:
	> `# This is an H1` 
	> `## This is an H2` 
	> `### This is an H3`
	> `#### This is an h4`	> `##### This is an h5` 
	> `###### This is an H6`	 * 链接:
	> 普通URL直接写上`http://www.midea.com/cn/`，appledoc 会自动翻译成链接: http://www.midea.com/cn/ 	> `[隐藏URL](http://www.midea.com/cn/)` 链接会隐藏实际URL: [隐藏URL](http://www.midea.com/cn/). * 表格:
	> | header1 | header2 | header3 | 	> |---------|:-------:|--------:| 	> | normal  |  center |  right  | 	> | cell    | cell    | cell    |
 	* 引用:
	> 这里会引用到方法 `someMethod:`，
	> 这里会引用到类 `YYColor` 	> 这里会引用到一个代码块     `void CMYK2RGB(float c, float m, float y, float k,float *r, float *g, float *b) {          *r = (1 - c) * (1 - k);         *g = (1 - m) * (1 - k);         *b = (1 - y) * (1 - k);     }`
     	
 @since iOS5.0 
 `*/`
`@interface AppledocExample : NSObject` 
/** 这里是属性说明: 名字 */
`@property (nonatomic, strong) NSString *name;` 
 /** 
  @brief 这里是方法的简介。该Tag不能放到类注释里。
  @exception UIColorException 这里是方法抛出异常的说明
  @see YYColor
  @see someMethod:
  @warning 这里是警告，会显示成蓝色的框框
  @bug 这里是bug，会显示成黄色的框框
  @param red   这里是参数说明1
  @param green 这里是参数说明2
  @param blue   这里是参数说明3
  @return  这里是返回值说明
  */
 `- (UIColor *)initWithRed:(int)red green:(int)green blue:(int)blue;` `- (void)someMethod:(NSString *)str;`
`@end`

编译出的效果是这样：
![Alt text](http://i12.tietuku.com/7642139687e0eb7e.png)

![Alt text](http://i13.tietuku.com/9f2ec1bb4e778b36.png)


![Alt text](http://i12.tietuku.com/d52c1219753b2f18.png)

