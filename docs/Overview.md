#Overview
##Edge Animate 运行时

`Edge Animate`动画制作依赖'Edge时间轴'和'元件JavaScript库'。该文档对应Adobe Edge Animate CC JavaScript API 5.0版本。

你可以从[这里](http://animate.adobe.com/runtime/5.0.1/EdgeAnimateRuntime5.0.1.zip)下载一个未压缩的动画运行时和预加载器。
它提供在BSD许可下允许的调试,优化,修改以及其他任何使用方式。使用和修改这些文件不会得到任何层面的Adobe支持,请慎重使用,自行评估风险。
该运行时在此[许可](http://animate.adobe.com/runtime/5.0.1/License.txt)之下。

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

最后的两个参数分别表示预加载器和下层stage DOM。

重要:为了能够使用Edge Animate中的文件,你必须原封不动的保留代码里面的注释。


##JavaScript文件

*project-name_edge.js*

*project-name_edge.js*文件使用JSON格式定义元件(图形和时间轴)。
在你每次保存作品的时候Edge Animate会覆写该文件。
推荐你使用语义明确的Javascript来编辑该文件,任何Edge Animate不明白的地方将被丢失。



*project-name_edgeActions.js*

Edge Animate使用匿名方法来包装和限制变量作用域。整个*project-name_edgeActions.js*文件被包含在一个单独的匿名方法域(anonymous function scope)中。
你可以在该匿名方法域(anonymous function scope)中定义作品的变量或方法。一定要使用`var`来定义变量以及使用局部范围的语法来定义方法。


##Edge Animate运行时&jQuery

早期版本的Edge Animate运行时依赖jQuery。该依赖在5.0.1版中被移除。
不过,Edge Animate运行时提供了$的基础实现,通过使用AdobeEdge.$,
支持一些基础的jQuery选择器以及一些普通jQuery AIP,具体可参考以下:

以下列表中的项对应jQuery的API,可以直接在Edge Animate运行时中使用。

- `addClass`
- `append`
- `attr`
- `bind`
- `css`
- `each`
- `empty`
- `eq`
- `get`
- `hasClass`
- `height`
- `hide`
- `html`
- `is`
- `offset(Only getter,no setter)`
- `parent`
- `parents`
- `remove`
- `removeClass`
- `show`
- `text`
- `trigger`
- `unbind`
- `width`

如果在你作品的扩展脚本中添加了jQuery,此时Edge Animate运行时重新定义**AdobeEdge.$**为**jQuery**并且可以以同样的方式使用。
此时,任何返回一个包装的Edge Animate API都将返回一个AdobeEdge.$类型的包装。
无论jQuery被包含在作品的扩展脚本中,还是在'edge运行时'之前被加载,
API都将返回一个jQuery包装。

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

通常我们不需要访问底层HTML Elements。
当处理`click`事件时尤其有用。比如,代码访问一个名字叫'TextOne'的底层元素使用`sym.$("TextOne");`。

访问导入的HTML内容可以通过该元素的`ID`或者`class`,如`sym.$("#myid");`。
你也可以使用该方法访问Edge Animate作品外面的DOM,比如,`sym.$("footer")`;



