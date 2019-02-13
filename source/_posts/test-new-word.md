---
title: xll测试测试测试
date: 2017-7-7
author: alanJiang
tags:
    - HEXO
    - HEXO_GitHub个博
categories:
    - 个博搭建
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: 测试发布文章
---

<div class="tmd-content">
<p style="text-indent:2em;">
上一篇我们学习了<a href="http://www.xiazaiba.com/jiaocheng/5557.html" rel="nofollow" style="color:rgb(20,162,24);text-decoration:none;" target="_blank">谷歌Chrome浏览器开发者工具的基础功能</a>，下面介绍的是Chrome开发工具中最有用的面板Sources。&nbsp;Sources面板几乎是最常用到的Chrome功能面板,也是解决一般问题的主要功能面板。通常只要是开发遇到了js报错或者其他代码问题,在审视一遍代码而一无所获之后打开Sources进行js断点调试,几乎能解决8成的代码问题。</p>
<p style="text-indent:2em;">
js断点功能让人兴奋不已,以前只能在IE中靠alert弹出窗口调试js代码,那样的开发环境对于前端程序员来说简直是一场噩梦。本篇介绍Sources的具体用法,帮助各位在开发过程中够愉快地调试js代码,而不是因它而发疯。</p>
<p style="text-indent:2em;">
首先打开F12开发工具切换到Sources面板中</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505296188716922624.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
Sources功能面板是资源面板,他主要分为四个部分,四个部分并不是独立的,他们互相关联,互动共同实现一个重要的功能:监控js在执行期的活动。简单来说就是断点啦。</p>
<p style="text-indent:2em;">
首先我们来看区域1,它的功能有些类似于Resources面板,主要是显示网页加载的脚本文件:例如css, js等资源文件(它不包含cookie,img等静态资源文件)。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297182076113664.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
区域1的导航条上有三个tab切换选项,他们都存有不同域名和环境下的js和css文件,我们首先来说明Sources(资源)选项的作用:</p>
<p style="text-indent:2em;">
Sources: 包含该项目的静态资源文件。双击选中文件,该文件内容会在区域2中显示,如果你选中的是js文件,那么你可以在区域2种单击行号进行断点调试,只要js执行到了你所标记的这一行,它会停止向下执行并且等待你的命令:</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_144350529745828799232.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
从上图可以看到js执行到断点处时各个区域的变化,首先是区域3中的Breakpoints记录信息会变高亮,然后是区域4中Scope&nbsp;选项中列出了断点处私有和公有的变量信息,这样,我可以很直观地知道,此时此刻js的执行状态。同样的,你可以把鼠标放到区域2种的某个变量上,浏览器会弹出一个小框框,框框里面则是你悬浮其上的变量所有信息:</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297284107332352.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
然后,你可以按F10跟着js执行的路径一步一步地走下去,如果你遇到了一个函数包含着另外一个函数,那么你可以按F11进入到个函数中去观察它的代码执行活动。你也可以通过点击区域1底部的各个图标对js代码进行跟踪。不过我建议你使用快捷键,故名思义,因为它比较快捷方便。不过怎么用完全按照个人习惯来吧。下图是各个按钮的作用功能。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_144350529767609476352.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
在上图蓝色圆圈中数字,它们分别代表:</p>
<p style="text-indent:2em;">
1、停止断点调试</p>
<p style="text-indent:2em;">
2、不跳入函数中去,继续执行下一行代码(F10)</p>
<p style="text-indent:2em;">
3、跳入函数中去(F11)</p>
<p style="text-indent:2em;">
4、从执行的函数中跳出</p>
<p style="text-indent:2em;">
5、禁用所有的断点,不做任何调试</p>
<p style="text-indent:2em;">
6、程序运行时遇到异常时是否中断的开关</p>
<p style="text-indent:2em;">
接下来在区域4种切换到Watch Expressions&nbsp;选项,它的作用是为目前断点添加表达式,使得每次断点往下走一步都会执行你写下的js代码。需要注意的是这个功能必须谨慎使用,因为这可能会导致你写下的监控代码段会不断地被执行。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297128935059968.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
为了避免你的调试代码重复执行,我们可以在调试时直接在console控制台上一次性地输出当前断点处的信息(推荐这样做)。为了验证我们在console面板中拥有的是当前断点环境,我门可以对比断点执行前后的this值变化。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297442640154112.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297150922971392.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
如果你觉得在断点的时候为了看一个变量必须借用console面板输出的方式来查看会比较麻烦,那么你可以更新最新版的Chrome,它已经为我们解决了这个烦恼。为了方便开发者调试,在这一点上谷歌已经做到了极致,就在前几天更新过Chrome以后,卤煮意外地发现了断点时监控环境变量的另外一种方式,这种方式极为清晰,在断点调试的时候,区域2中会自动显示每个变量的值,每次代码往下走的时候这个值都回时时更新。这让开发者对当前环境变量几乎可以说是<a href="https://www.baidu.com/s?wd=%E4%B8%80%E7%9B%AE%E4%BA%86%E7%84%B6&amp;tn=24004469_oem_dg&amp;rsv_dl=gh_pl_sl_csd" target="_blank">一目了然</a>。(此功能有一个小缺陷,那就是无法查看数组或者对象的具体索引和值,不过我相信google会改进它的。)</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_144350529761068672768.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
当你的项目已经线上,出现了一个bug,你修复了之后无法看到它真正在线上的效果,那么你可以在打开线上的项目,直接在浏览器中修改代码然后看到效果。这样的效果往往是最直接的,这种方法也能帮你省去频繁验证发布的麻烦,毕竟身为前端码农的你也一定会听到过后台(通常情况下是后台发布)大哥的抱怨:“XXX,测试通过了没,不要出现了哈,发布一次很麻烦的!”。而在Chrome里面,只需要在区域2种直接修改,你就可以验证你的代码在线上是否可行。卤煮在此处只是指出该功能的用法之一。其他的就凭诸位的<a href="https://www.baidu.com/s?wd=%E8%81%AA%E6%98%8E%E6%89%8D%E6%99%BA&amp;tn=24004469_oem_dg&amp;rsv_dl=gh_pl_sl_csd" target="_blank">聪明才智</a>去想了。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505297338450508032.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505298403449654784.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
即使在断点时,你也可以编辑代码,按ctrl+S保存之后,你会看到区域2的背景由白色变为浅色,而断点会重新开始执行。</p>
<p style="text-indent:2em;">
回到区域1,Content script&nbsp;选项开里面包含着一些第三方插件或者浏览器自身的js代码,经常它是被忽略的,实际上它的作用很少。我们可以更多关注一下Snippets选项。还记得基础篇里面介绍的style吗?在里面我们可以编辑界面的css代码并且即时看到它们的映射效果,同样地,在Sinppets中,我们也 可以编辑(重写)js代码片段。这些片段实际上就相当于你的js文件一样,不同的是本地的js文件在编辑器里面编辑的,而此处,你是在浏览器中编写的。这些代码片段在浏览器刷新的时候既不会消失,也不会执行,除非是你手动执行它。它可以存在你的本地浏览器中,即使关闭浏览器,再次打开时它依然还在那里。它的主要作用可以使得我们编写一些项目的测试代码时提供便捷,你知道,如果你在编辑器上编写这些代码,在发布时你必须为它们添加注释符号或者手动删除它们,而在浏览器上编写就不需要这样繁琐了。</p>
<p style="text-indent:2em;">
在Snippets选项的空白处右键后选择弹出的new选项,建立一个你自己的新的文件,然后在区域2种编辑它。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505298471418083328.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
Snippets&nbsp;的非常功能强大,它的许多隐藏功能还有待发掘。目前卤煮使用它是在记住调试片段、单元测试、少量的功能代码编写功能上。</p>
<p style="text-indent:2em;">
最后我们看看js中时间丰富的监控功能,同上篇文章介绍的一样,Sources面板和Elements面板一样有监控事件的功能,而且Sources中功能更加丰富,也更加强大。它的这部分功能集中在区域3中。我以下图为例,观察其作用。</p>
<p style="text-align:center;">
<img alt="Chrome开发者工具不完全指南（二、进阶篇）" src="http://www.xiazaiba.com/uploadfiles/content/2015/0929/water_1443505298233745898240.jpg" style="border:0px;vertical-align:middle;display:block;"></p>
<p style="text-indent:2em;">
从上到下,紫色圈内的数字的意义:</p>
<p style="text-indent:2em;">
1、断点处的债堆栈,就是从该函数起,逐级追寻调用到他的函数名。例如:</p>
<p style="text-indent:2em;">
<a href="http://www.open-open.com/lib/view/open1435630175716.html#" rel="nofollow" style="color:rgb(20,162,24);text-decoration:none;" target="_blank">?</a></p>
<div class="table-box"><table cellpadding="0" cellspacing="0" width="760" style="border-collapse:collapse;border-spacing:0px;border:1px solid rgb(204,204,204);font-size:14px;"><tbody><tr class="firstRow"><td style="border:1px solid rgb(204,204,204);font-size:14px;">
<p>
1</p>
<p>
2</p>
<p>
3</p>
<p>
4</p>
<p>
5</p>
<p>
6</p>
<p>
7</p>
<p>
8</p>
<p>
9</p>
<p>
10</p>
<p>
11</p>
<p>
12</p>
<p>
13</p>
<p>
14</p>
<p>
15</p>
<p>
16</p>
<p>
17</p>
</td>
<td style="border:1px solid rgb(204,204,204);font-size:14px;">
<p>
function a () {</p>
<p>
&nbsp;&nbsp;&nbsp;b();</p>
<p>
}</p>
<p>
function b() {</p>
<p>
&nbsp;&nbsp;&nbsp;c();&nbsp;</p>
<p>
}</p>
<p>
function c() {</p>
<p>
&nbsp;&nbsp;//在该处断点,查看call stack&nbsp;</p>
<p>
}</p>
<p>
a-&gt;b-&gt;c.</p>
<p>
call stack 从上到下的顺序就是</p>
<p>
c</p>
<p>
b</p>
<p>
a</p>
</td>
</tr></tbody></table></div><p style="text-indent:2em;">
2、在区域2中你的断点调试信息。当某个断点在执行的时候对应的信息会高亮,双击该处信息可以在区域2中快速定位。</p>
<p style="text-indent:2em;">
3、添加的Dom监控信息。</p>
<p style="text-indent:2em;">
4、击+ 并输入 URL 包含的字符串即可监听该 URL 的 Ajax 请求,输入内容就相当于 URL 的过滤器。如果什么都不填,那么就监听所有 XHR 请求。一旦 XHR 调用触发时就会在 request.send() 的地方中断。</p>
<p style="text-indent:2em;">
5、为网页添加各种类型的断点信息。如选中了Mouse中的某一项(click),当你在网页上出发这个动作(单击网页任意地方),你浏览器就是立刻断点监控该事件。</p>
<p style="text-indent:2em;">
值得再次重复一遍,Sources是一般的功能开发中最常用到也是最有用的功能面板,它里面的许多功能对于我们开发前端工程来说是非常有帮助的。在web2.0时代的今天,我不推荐依然在自己的代码里面写调试信息的行为,因为这会然你的开发变得繁琐。Chrome开发工具给我们提供的强大功能,我们应该好好利用之。这篇文章就到此结束,虽然有点繁琐,但总算基本表述了卤煮使用经验和想法,希望对你有帮助。如果你觉得不错,请推荐一下本文并继续关注卤煮在的博客。在下一篇中我将向大家介绍Chrome开发工具中的性能方面的调试。</p>
<div><br></div>
</div>