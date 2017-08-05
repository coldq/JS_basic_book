## 响应式设计-概念&应用

### 响应网页设计是究竟什么？
网上有关于响应式web设计的定义非常多，但大多数都是非常抽象，哲理或者是不可信的。如果你想学习与理解真正响应式web设计的定义，它可以归为如下的三种技术：

- 流体图像；
- 流体网格；
- 媒体查询。

让我们进一步学习响应式web设计的每一个关键组件。

### 流体图像与流体网格

什么是最好的方法来设计一个网站应用在成千上百不同的屏幕尺寸,哪些可能甚至不存在了？最好的方法不是适应某些特定的设备，而是使得布局扩展性强，灵活性高，并且可以适应屏幕所有尺寸，包括一些现在还不流行的屏幕尺寸。

前些年，灵活的布局还不是这么流行，唯一的灵活布局元素就是网格列和文本。图像却没有以灵活性的思想去设计，因此在很多情况下，图形容易坏掉了或者显示不正常。幸运的是，现在，图像已被包含在响应式web设计思路里面，可以自动地适应屏幕尺寸，这做法促进了对更大概念设计和项目原本想法的保护。图像总是那么引人注目，感谢的是，你的响应布局可以而且应该保持这种响应界面强大的方面。无图像的移动网站是最初移动设计遗留的方法。

从技术的角度来说，当你在创建一个响应式设计时，为图像创建灵活性是一大要解决的问题。现已有多种技术来按照比例缩放图片；有些是很容易实现的，最著名的是，Ethan Marcotte写关于流体图像的文章里面有两个简单的CSS规则：`max-width`和`height:auto`,就如：

```
img{ 
max-width: 100%; 
height: auto; 
}
```

第一条规则确保图像保持在父容器，而并不会溢出；忽略元素的高度与宽度；你让浏览器根据设备来设置图像的大小。把图像的宽度设置为最大值就是浏览器的宽度或者设备的宽度，所有当宽度减少时，图像会按照比例缩小（这是值得推荐的，但IE不兼容）。如果图片的尺寸有限制和要适应老版本的浏览器，那这并不是最优的方案，但可以使用JavaScript来解决这个问题，如何实现？有兴趣的同学可以进入上面的链接学习。

总体来说，使用这规则是可以完美的运行的，然而，如果你在维护旧版页面，那些宽度高度等属性都被直接写在html里面，那响应的图像可能会被妥协了。现在为了防止这些，你并不需要去改变HTML的代码，只需要添加CSS规则height:auto，这样你的图像就可以被争取的渲染和缩放了。

Filament组提出了另外一种技术不仅是正确地设置图像的尺寸，在较小的设备中为了节约空间，还降低图像的分辨率，加载时间和移动宽带（流量）。

这种技术需要一些文件，这些文件都在Github:一个JavaScript文件（rwd-images.js），Htaccess文件，和一张图片（rew.gif），然后，在HTML代码中，我们引用两种图片:一个小的“R”前缀，必须适应(“响应”)和大的data-fullsrc(HTML5启用的一个属性,更多详情可以访问这个页面)。

实现这种技术，看起来如下：

```
img <img src="smallRes.jpg" data-fullsrc="largeRes.jpg">
```

当屏幕尺寸大于480px，页面就去加载大图片（largeRes.jpg）。JavaScript插入元素是可以允许页面分离适应的图片。当页面加载完成，除了大或者小图片会根据预先的设置来加载之外，所有文件都会正常的加载下来。如果这技术不起作用，所有的（大的和小的）图片都被加载下来，这样就会浪费宽带，反过来说，这技术防止了不必要的图片加载下来，另外它是兼容现代浏览器（包括IE8）和移动设备的。著作权归作者所有。

### 媒体查询

对于那些web开发者必须创建响应式网站来说，媒体查询可能是最好的工具了。这技术使得能够创建流体设计来适应用户设备。值得建议的是,这组指导原则(或规则)应该保存在一个单独的CSS样式表中，但这不是必需的,所以你可以根据自己需求去做。就我个人而言,我更喜欢我自己的分离组织,所以我创建一个新的CSS表(不要忘记在HTML代码链接这样式表)。

```
<link href="media-queries.css" rel="stylesheet" type="text/css" />
```

你可以写尽可能多的媒体查询。其主要目的是应用不同的CSS规则为了获得不同的布局,根据显示窗口的宽度赋予你的内容。媒体查询中的值被表示为百分数,而不是像素。这个特性,使得各种页面元素流体和灵活。与不同的屏幕尺寸比例扩张和收缩;固定像素值会反应迟钝,会导致不可伸缩。

如下代码示例:

```
@media screen and (max-width: 980px){
   #pagewrap{
      width: 95%;
   }

   #content{
      width: 60%;
      padding: 3% 4%;
   }

   #sidebar{
      width: 30%;
   }
}
```

通过设置一系列的CSS规则,设备的屏幕最大宽度为980像素,容器content将占据60%的宽度(padding填占3%,4%,3%,4%),而侧栏sildebar将占总宽度的30%。

媒体查询有助于考虑多个显示尺寸的可能性,因此,组织样式规则可以快速而方便地修改。使用相同的过程,我们可以设置不同的规则应用于屏幕宽度小于650像素,小于480像素等。

也可以针对不同的媒体,使用不同 stylesheets :

```
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

#### 媒体查询优点

- 面对不同分辨率设备灵活性强 
- 能够快捷解决多设备显示适应问题

#### 媒体查询缺点

- 兼容各种设备工作量大，效率低下 
- 代码累赘，会出现隐藏无用的元素，加载时间加长 
- 其实这是一种折中性质的设计解决方案，多方面因素影响而达不到最佳效果 
- 一定程度上改变了网站原有的布局结构，会出现用户混淆的情况