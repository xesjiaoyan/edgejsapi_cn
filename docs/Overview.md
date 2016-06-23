#Overview
##Edge Animate 运行时

`Edge Animate`动画制作依赖Edge的'时间轴'和'元件JavaScript库'。该文档对应库的5.0版本。

你可以从[这里](http://animate.adobe.com/runtime/5.0.1/EdgeAnimateRuntime5.0.1.zip)下载一个未压缩的动画运行时和预加载器。
它提供在BSD许可下允许的调试,优化,修改,其他任何使用方式。使用和修改这些文件不会得到任何层面的Adobe支持,即一切后果自负。请慎重使用。
该运行时也在[此许](http://animate.adobe.com/runtime/5.0.1/License.txt)可之下。

[下载未压缩的Edge Animate运行时](http://animate.adobe.com/runtime/5.0.1/EdgeAnimateRuntime5.0.1.zip)

##CND托管

使用Adobe Content Distribution Network(CND)能够快速提升动画制作速度。Edge使用Adobe CND共享了一个jQuery的URL和Edge运行时。
浏览器会主动缓存它,因此,用户仅需要下载一个库文件创作者都能够使用,甚至在不同的网站,不同的作者也都能够使用。

如果你的创作必须运行在一个没有internet网络的地方,或者你想使用自己的托管,那么就可以不用CDN。


动画运行时CND使用一下URL

```
<script type="text/javascript" charset="utf-8" src="http://animate.adobe.com/runtime/5.0.1/edge.5.0.1.min.js"></script>

````

##HTML页面
Edge Animate插入一个独立的Javascript标签到Html页面中,允许创作者来逐步下载。

注意:为了能够看到你的作品使用了哪些文件,你可能需要刷新你的浏览器。(特别是Chrome和Safari浏览器)

```
<!--Adobe Edge Runtime-->
   <script type="text/javascript" charset="utf-8"
        src="edge_includes/edge.5.0.1.min.js"></script>
           <style>
                .edgeLoad-EDGE-1689000495 { visibility:hidden; }
           </style>
  <script>
     AdobeEdge.loadComposition('project-name', 'EDGE-1689000495',
      {
        scaleToFit: "none",
        centerStage: "none",
        minW: "0",
        maxW: "undefined",
        width: "550px",
        height: "400px"
        },
        {dom: [ ]},
        {dom: [ ]
       });
  </script> <!--Adobe Edge Runtime End-->

````

最后的两个参数分别表示预加载器和stage DOM的级别。

重要:为了能够使用Edge Animate中的文件,你必须完整的保留里面的注释。


##JavaScript文件

project-name_edge.js

project-name_edge.js文件包含JSON格式对元件(图形和时间轴)的定义。
Edge Animate在你每次保存的时候覆写该文件。推荐您使用语义明确的Javascript来编辑该文件,任何Edge Animate不明白的地方将被丢失。

project-name_edgeActions.js

Edge Animate 使用匿名方法老包装和限制变量作用域。project-name_edgeActions.js文件被包含在一个独立的匿名域中。
这将为你提供一个位置,让你能定义作品的局部变量和函数。一定要使用var和function使用局部范围的语法来定义变量。


##Edge Animate 运行时 & jQuery

早起的Edge Animate 运行时依赖jQuery。该依赖在5.0.1版中被移除。不过,Edge Animate运行时提供了$的基础实现,通过AdobeEdge.$使用,
支持一些基础的jQuery选择器以及一些普通使用方法,具体可参考以下列出的API:

和jQuery相对应的API,可以直接在Edge Animate运行时中使用。

- addClass
- append
- attr
- bind
- css
- each
- empty
- eq
- get
- hasClass
- height
- hide
- html
- is
- offset(Only getter,no setter)
- parent
- parents
- remove
- removeClass
- show
- text
- trigger
- unbind
- width

如果在你的作品的扩展脚本中包含jQuery,此时Edge Animate运行时重新定义**AdobeEdge.$**为**jQuery**就可以同样使用了。
于是,任何Edge Animate API返回一个AdobeEdge.$类型的包装。如果jQuery被包含在作品的扩展脚本中,或者html页面中的edge运行时被加载之前,
API将返回一个jQuery包装。

这样做
```
var myVar = "局部作用域,不会和其他代码冲突";

````

避免
```
myVar = "这是全局的,有可能和页面中的其他代码冲突";

````

这样做
```
function handleClick() {   alert('This is scoped properly and should not conflict with other code.');


````

避免
```
window.handleClick=function() {   alert('This might conflict with other code in the page.');

````

##Work with elements directly

通常不必访问底层HTML Elements。当处理`click`事件时尤其有用。比如,代码访问一个底层元素通过名字'TextOne'`sym.$("TextOne")`。

通过代码访问导入的HTML内容可以通过该元素的`ID`或者`class`,如`sym.$("#myid");`。你也可以指向Edge Animate作品外面的目标DOM,比如,`sym.$("footer")`;



