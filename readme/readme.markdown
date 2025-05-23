### 项目名称：Violet(紫罗兰)

### 项目介绍：
本项目是一个网站爬虫集合，目前计划做某音，某书，某站的爬虫，后续可能会考虑做其他网站（比如某些se se的网站嘿嘿）。
本项目长期维护，绝不烂尾。
作者本人还在读研，所以可能网站更新了，恰好又在忙，不一定及时会更新，但是有空一定会处理的。

### 项目环境：
编辑器：vscode
py环境：3.12.3 （无特殊要求，新手直接使用最新的py环境就行）

所需要的包：
- pip安装：
``` python
pip install requests
pip install pprint  
pip install aiohttp
pip install asyncio  
pip install typing-extensions  
pip install loguru
pip install urllib3  
```

- conda安装（需要有conda虚拟环境）：
``` python
conda install -c conda-forge requests
conda install -c conda-forge pprint
conda install -c conda-forge aiohttp
conda install -c conda-forge typing-extensions  
conda install -c conda-forge loguru
conda install -c conda-forge urllib3
```

新手的话，直接使用pip命令就好了，虚拟环境我估计新手不太会用。

### 一些需要手动获取的参数：
![alt text](image-1.png)
如上图所示，这三个p参数和三个w参数就是我们要获取的，一旦获取，长期使用，参数只要搞一次可以用很长时间。

那我们如何获取这三个参数呢？

1.首先，打开兄弟们的电脑（电脑应该都有吧，我这个是网页端哦），打开edge浏览器或者google浏览器。

2.搜索某音，并扫码登录你的账号（注意，你一定要登录！！！
重要的事说三遍，一定要登录才能获取参数
重要的事说三遍，一定要登录才能获取参数
重要的事说三遍，一定要登录才能获取参数）

3.找一个你自己喜欢的博主，打开他/她/它的个人主页，如下图所示，这里我用edge浏览器为例子：
![alt text](image-2.png)

这里我随便找了一个博主，可以看到我现在是在该博主的个人主页中。

4.关键的一点来了，找到 p的三个参数（批量数据包参数）所在的数据包!
![alt text](image-3.png)(!!!)
鼠标右键点击，我们的屏幕上会出现一个鼠标页，如上图所示，最下面的是检查，我们要点击检查，从而打开浏览器开发者工具。
或者兄弟们按键盘的f12键也可以直接打开浏览器开发者工具

打开后是这个样子![alt text](image-4.png)
在这里我们要点击网络这个选项卡

点击后会出现如下图所示的界面![alt text](image-5.png)
左边有一个很明显的搜索栏，我就不特地标了。
在这个搜索栏中，我们搜索post字段，搜：post， 也就是输入post这四个字母进行搜索

搜索完之后会出现很多匹配项![alt text](image-8.png)

这个时候别急，我们按键盘的ctrl + r重新刷新一下， 然后再次回车搜索

![alt text](image-7.png)

在这里的话我们可以很明显的看到搜索出来两个post字段的数据包，这个数据包就是我们想要的东西。
其实这个就是我们常说的“抓包”

上面这种情况是顺利抓包抓到post，那也有可能我刷新了一下，重新搜索post没有抓到包，这该怎么办呢？
别急，我们可以用这个套路：重新ctrl + r刷新页面，同时鼠标滚轮向下滚动加载新作品（鼠标是放在抖音那个你打开的博主的个人页面往下滚动哦，抖音是流式加载，需要你滚动才能加载新作品。    不要放在抓包的开发者工具里往下滚动呀！！！！！！！！）
这个时候，你再去开发者工具里的搜索栏搜索post，回车确定，大概率百分之99都能找到post这个字段的数据包，如果还没找到，你就重复这个操作多遍，一定能找到。


其实在这里聪明的兄弟们已经明白了，哪怕不是计算机专业的。在上面的图中，我并没有往下滑动页面，搜索出来两个post数据包（这个post其实就是一个流式加载数据包，每一个post里都含有20或者30多个视频的信息）
如果你一直往下滑动的话，你会发现post会越来越多。因为某音是流式加载的（某书也是）。

5.获取p（批量数据包）三个参数

![alt text](image-9.png)

随便点击一个post，你要用鼠标点击哦


右边会出现这个包具体对应的部分：

![alt text](image-10.png)

右边那个post开头的，整体灰色的那个第一行很明显吧？
鼠标放到上面，右键点击复制，点击复制为bash

![alt text](image-11.png)

打开网站：https://www.lddgo.net/convert/curl-to-code。这个网站是一个在线curl转python代码的一个工具

![alt text](image-12.png)

选择语言为py，把输入框里的baidu那个东西删了，把你复制的bash粘贴进去，点击转换

![alt text](image-13.png)

复制右边的输出
你可以看到右边的整体输出是：

import request

cookies = {}

headers = {}

params = {}

response = request.get()

这里我们只需要把cookies headers params大括号里面的参数 复制粘贴到 我代码中对应的那三个 p_cookies, p_headers, p_params就可以了。

6.最后一步啦，获取w的三个参数（单独作品属性数据包获取）
兄弟们可能觉得已经烦了，卧槽你这什么垃圾教程，这么多，老子看得都费劲，彩笔。

兄弟们稍安勿躁，其实已经完成百分之90了，第6步跟第5步一个套路。

还剩三个参数w_headers w_params w_cookies。

这里我们随便选择这个博主个人主页的一个视频，点击进去

![alt text](image-14.png)

老样子，打开开发者工具，点击网络选项卡，找到左边的搜索栏

我们要怎么获得w的三个参数呢？

我们可以观察这个页面：

![alt text](image-15.png)

不知道兄弟们有没有注意到平时浏览器上面的搜索栏:https://,这个其实是url，也就是我们常说的地址。
细心的兄弟们已经可以看出来了，这个地址由多个字段组成：

https://www.douyin.com/user/MS4wLjABAAAAiEdTJStt_v5pqfD1SmXNy__FzyM9fYwUARoeouw9zII?from_tab_name=main&modal_id=7497211019389390116&vid=7497211019389390116

www.douyin.com   user   MS4wLjABAAAAiEdTJStt_v5pqfD1SmXNy__FzyM9fYwUARoeouw9zII  modal_id vid

其中我们只需要关注MS4wLjABAAAAiEdTJStt_v5pqfD1SmXNy__FzyM9fYwUARoeouw9zII和modal_id对应的值

如果兄弟们多找几个博主的视频就可以发现：每一个博主的MS4wLjABAAAAiEdTJStt_v5pqfD1SmXNy__FzyM9fYwUARoeouw9zII这个字段都是不一样的

这个字段的名字叫做：sec_user_id 有兴趣的兄弟们可以自己去抓包玩玩，就可以发现这个很长的MS4w开头的其实就是博主的个人id号码（和抖音主页那个id不是一回事），每一个人都不一样

还有一个modal_id，同样的多找几个视频观察一下，就会发现，每一个视频的modal_id都是不一样的，这个modal_id其实就是每一个视频对应的id

那很明显了，我们要获取单独作品的属性数据包。一个作品由哪些属性构成呢？ modal_id啊，相当于作品的身份证，那么肯定还有姓名喽，这不就是每一个作品的文案嘛？

我们想要抓到w三个参数所在的数据包，就可以在开发者工具栏中搜索modal_id 或者 作品文案啊

立马搜索，结果果然找到了（找不到按照第五步的重试步骤多试几次）

![alt text](image-16.png)

细心的兄弟们肯定已经发现了，这个数据包不就是这个博主，叫若什么的 的sec_user_id嘛，就是地址栏里的那一串Ms4w开头的。
后面就是跟第五步一样啦。点击这个数据包，右边会有对应的灰色的一行出现，我们把光标移动到灰色的那一个行，右键点击，选择复制，选择复制为bash

再去刚才那个网站：https://www.lddgo.net/convert/curl-to-code     重复一遍操作，这里我就不说了，第五步说了

最后把把cookies headers params大括号里面的参数 复制粘贴到 我代码中对应的那三个 w_cookies, w_headers, w_params就可以了。

7.终于做完了前置工作，接下来就是跑通代码啦！

见证奇迹的时刻，我们只需要把你想要爬取的博主的sec_user_id放进main函数里，右键点击运行，就可以啦！
![alt text](image-17.png)

666,真的跑起来啦
![alt text](image-19.png)

vscode里不支持播放声音只能看视频，但是我们可以打开文件管理器看，mp4是可以正常播放的，有画面有声音

并且我设置下载是默认按最高画质无水印下载。

纯正技术贴，兄弟们这不给我点一波赞？
代码会发在论坛里，同时github也会上传代码。
不会编程的兄弟我后续会制作exe脚本上传，不知道论坛给不给上传，开箱即用
会py的兄弟们可以自己试一下，如果觉得可以的话，能麻烦兄弟们去github给我点个星星嘛。非常感谢兄弟们

后续我会完善代码

现在代码还有一些问题：

1.目前这个代码只能下载视频，假如作品是图片的话就会报错，所以兄弟们下载的话尽可能去找作品全是视频的博主下载

2.没有设置爬取速率，我打算加一个函数由兄弟们自己设置爬取速率，不过我估计意义不大，应该不会触发反爬

3.对于验证码的处理，有时候可能爬着爬着会跳出来验证码，程序就被迫停止（兄弟们放心，你爬好几天都不一定能遇见），不过这个确实很坑爹就是了
目前没啥好办法，如果遇到只能手动重新跑

未来的计划:
1.完善某音代码

2.出某音爬虫作品教程贴（如果有兄弟们感兴趣我就详细的说下我的思路是怎么样子的。给兄弟们详细分析思路是怎么样子的，怎么写的，因为某音的视频图片获取不需要加a_bogus参数，所以很容易就写出来了，基本demo也就吃个饭的工夫就出来了）
评论直播那些暂时不出，因为那些有参数加密，需要js逆向，录视频说都特别麻烦更何况图文教程了，可能后续会直接扔进github项目里，有兴趣的兄弟们自己去下载搭环境跑代码就行了


3.更新某书、某站的爬虫，或许兴致来了也会找些sese网站练练手
代码全部开源，有兴趣的兄弟们可以自己研究下
有能力的兄弟们希望可以帮忙去GitHub下点下星星，谢谢兄弟们
我会一直维护爬虫项目的。


