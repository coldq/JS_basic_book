## 响应式设计：跨浏览器兼容性

在整个网页开发过程中，尤其你想创造一个响应式的结构——一个web开发人员必须去面对一个最重要及最频繁的问题就是兼容各种浏览器。

“兼容性”意味着什么？网页开发人员必须确保他们的设计可以良好地运行起来，然后网页内容保持完整性并且原有的功能性保持不变。毫无疑问，这是一个最复杂及令人沮丧的的问题之一，你必须意识到，当你在设计一个新项目时，不能给兼容性留下任何机会，要在整个设计中保持跨浏览器兼容性的思想。

在最新的CSS3版本中有了很多新的CSS功能，但还没在所有主流浏览器中得到支持。事实上，有些功能是不推荐使用的，因此会在浏览器中全部被忽略掉，如果你使用了一些不支持的CSS功能，结果会导致重大的问题发生。这不仅仅是发生在不同类型浏览器之间，即使在同类型不同版本的浏览器之间也能够支持（或者不支持）各种设计技术，这些问题都会增加跨浏览器兼容性的难度。

回到图像管理，这可能是RWD方案的弱点所在，特别是对于浏览器兼容性问题。照片和媒体需要具有灵活性和适应不同的设备，与此同时，很重要的一点是不会减慢对页面加载过程。因此，依然没有明确、理想的解决方案，如不同的屏幕尺寸，有限制的带宽(移动终端浏览)，在高分辨率(“视网膜”)上显示，等等。

明显地，在所有设备上都使用一张大图片（尽可能是最大的版本）是不推荐的。想想一个使用着慢吞吞的2G网络的智能手机用户需要花多长时间来加载你的设计吖。经过漫长时间加载图片之后，这些高分辨率的图片也可能只显示原来的四分之一。

最大的问题就是媒体查询（media queries）在老版本浏览器中是不被支持的。因此，一个依赖很多CSS3功能的响应式网页只有在一个不断支持CSS3、更新的浏览器中才能完好地显示出来。幸运的是，有3种JavaScript解决方案可以使得在老版本浏览器中运行响应式网站，而不会受限于对CSS3的支持。Respond.js、Modernizr和adaptive.960.js，接下来学习一下。

### Respond.js

第一种方案也是最简单的一种——我现在谈到的是一个脚本叫respond.js，是可以增强老版本浏览器理解和执行CSS3的媒体查询。添加如下代码就可以使用它。

```
<script type="text/javascript" src="js/respond.min.js"></script>
```

这样子，浏览器就可以支持媒体查询、最小宽度、最大宽度和所有媒体类型（例如，屏幕（screen））。这个脚本有助于CSS3指令正确地执行，甚至在更加老的浏览器上也行。

看起来Respond.js很容易成为一种理想的解决方案，但对许多项目，这是一个伟大的解决方案，因为代码是从最新的CSS3桌面浏览器和为智能手机设计的所有浏览器读取的。脚本的唯一目的是让老版本浏览器能够理解并执行媒体查询的CSS3指令，没有多余的功能。

### Modernizr

第二种解决方案就是使用Modernizr工具。正如在其官方文档上所解释那样，“Modernizr是一个智能的JavaScript库，能够检测出本机实现新web技术的可用性，例如，基于HTML5和CSS3标准的新特性。”

这些特性的大部分至少在一种主流浏览器中实现，Modernizr所做的——非常简单——告诉你目前的浏览器是否实现这些特性。这是一个不可缺少的工具，可以通过javascript驱动功能检测给你更好的控制体验。

除此之外，Modernizr创建一个JavaScript对象并且在HTML元素中增加类来锁定你的CSS代码。这是一种极好的解决方案，因此这样有助于你很简单地编写条件式的JavaScript和CSS代码来处理每种方案，不管浏览器是否支持某种特性与否。

Modernizr支持这些浏览器：IE6+, 火狐3.5+, Opera 9.6+, Safari 2+, Chrome, Mobile Safari, Android基于WebKit内核的浏览器，Opera手机和火狐手机（浏览器）。

你可以下载该库的完整版本和根据自己的定制去实现它。然而，如果你只是需要测试浏览器对CSS3的兼容性，你可以设置库提供的各种选项并创建自己的压缩代码。在一个外部的js文件中粘贴这些代码，用标签包含在HTML文档里。Modernizr团队建议在导入CSS之后才加入该库。

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Your title</title>
        <script type="text/javascript" src="modernizr-latest.js""></script>
    </head>
    <body>Your content</body>
</html>
```

现在你有一个JavaScript库，表明你使用CSS3和HTML5功能得到支持。让页面在浏览器上运行，然后使用Chrome开发工具或Firebug审查代码。

你可能看到代码如下：

```
<html class="js flexbox canvas canvastext webgl no-touch geolocation postmessage websqldatabase no-indexeddb hashchange history draganddrop websockets rgba hsla multiplebgs backgroundsize borderimage no-borderradius boxshadow textshadow opacity cssanimations csscolumns cssgradients cssreflections csstransforms csstransforms3d csstransitions fontface generatedcontent video audio no-localstorage no-sessionstorage webworkers applicationcache svg inlinesvg smil svgclippaths">
    ....
</html> 
```

### adapt.960.js

对于第三种解决方案，我们认为是非常不同于前两种的，尤其是因为它并不利用CSS3和相应的媒体查询。然而，其概念非常类似于CSS3的媒体查询。

如果我们单独文件中使用CSS3，这个库要求我们去用多个CSS文件分开这些代码，其中一份为每种设备类型而准备的。该库会解析设备的分辨率并为特定的屏幕分辨率调用对应的CSS设计。

我们可以下载该库，然后在页面代码中添加如下代码行：

```
<script type="text/javascript" src="js/adapt.min.js"></script>
```

接着，复制下面代码：

```
<script type="text/javascript">
var ADAPT_CONFIG = {
  // Where is your CSS?   
  path: 'assets/css/',     
  dynamic: true,     
  callback: myCallback,    
   range: [     
   '0px    to 760px  = mobile.css',     
   '760px  to 980px  = 720.css',     
   '980px  to 1280px = 960.css',     
   '1280px to 1600px = 1200.css',     
   '1600px to 1920px = 1560.css',     
   '1940px to 2540px = 1920.css',     
   '2540px           = 2520.css'   
   ] 
  };
 ```

我们可以看到在“range”包含了一系列CSS文件，每个CSS文件就是对应了一组分辨率，文件内包含相对应的CSS属性，就好比，代码是编写在CSS媒体查询中。

公共CSS——就是应该应用在所有的屏幕尺寸中——会被包含在不同的CSS文件汇总，为了方便，我们可以叫此CSS文件为master.css，像平常的CSS文件那样引入它：

```
<link href="assets/master.css" rel="stylesheet" type="text/css" media="screen" />
```

### 总结

在这三种方案中，我们应该采用哪一种？它们都是有效的、合理的方案。如果你选择应用第一个解决方案(respond.js)，你必须编写和管理一个单独的CSS文件，这点不像adapt.960.js，则需要多个CSS文件。最后，如果你选择去尝试Modernizr，将利用浏览器支持新的CSS3功能，并且很容易和可靠的手段来控制或者浏览器无法控制的局势。

如果你相信在未来几年内，老版本浏览器会变得无关紧要了，移动浏览器将取代桌面浏览器，我相信最好使用媒体查询和支持老版本浏览器可用的javascript扩展插件。

记住目前也有基于web的服务来测试响应式网站和模拟浏览器窗口的大小。其中有两个方案，一是responsive.is，这个是非常容易上手的；而是studiopress.com，输入网址后，从不同的角度并排地展示你的网站。

除了基于web的解决方案之外，还有应用程序，可以直接安装在你的个人电脑。其中，发现Opera移动模拟器 Opera Mobile Emulator，可在Mac、Linux和Windows上安装使用。安装后打开应用程序，将发现有一个列设备类型选择来模拟的(不幸的是，苹果设备除外)。

总结这篇文章，我想分享一个非常有用的在线工具来测试你的网站的兼容性:crossbrowsertesting.com。你必须选择一个操作系统和一个web浏览器。通过在一系列浏览器截图，使得对你的网站有了较为完整视图，通过这种方式，将更容易地理解你应该修改哪些元素使得你的项目完全兼容任何平台。

著作权归作者所有。
商业转载请联系作者获得授权,非商业转载请注明出处。
原文: http://www.w3cplus.com/responsive/understanding-responsive-web-design-cross-browser-compatibility.html