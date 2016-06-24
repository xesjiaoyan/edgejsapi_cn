#元件
##Edge Animate 元件

Edge Animate 运行时是围绕元件这个概念来组织的。
一个元件设置自己的行为,时间轴和图形。
舞台也是一个元件,在Edge Animate作品中,它总是唯一的根。

舞台和其他元件隶属于DOM元素。
元件的子元素被称为Actor的元件拥有。

元件可扩展,你能够定义行为,绑定时间给行为,还可以在运行时改变元件

##元件闭包
project-name_edgeActions.js文件是一个设置了嵌套的Javascript闭包。
打开Edge Animate,创建一个新的项目,保存,打开project-name_edgeActions.js。
你应该能够看到类似这样的代码:

```
(function($, Edge, compId){
 var Symbol = Edge.Symbol;
  // alias for commonly used Edge class
  //Edge symbol: 'stage'
      (function(symbolName) {

      })("stage");
          //Edge symbol end:'stage'
      })(jQuery, AdobeEdge, "EDGE-110465113");

````

每个元件的行为都包含在一个JavaScript闭包中。
这提供了元件级别的包装。
你可以添加一个元件到舞台然后保存,看看project-name_edgeActions.js代码。

注意:当使用元件实例并访问时间轴,你处理的元素名字不是元件自己的名字,这点比较重要。
比如,如果元件库有一个元件叫"kitten_sym"并且在元素面板中有一个实例叫"kitten_1",
当你访问该实例的时候使用"kitten_1"。

##通过舞台访问时间轴上的元件
使用以下代码访问舞台时间轴上的元件

```
// Play the symbol timeline
sym.getSymbol("symbolName").play();

````

你还能从舞台控制元件中的元素,例如:

```
// Hide the element "kitten_paw" within the symbol "kitten_1"
sym.getSymbol("kitten_1").$("kitten_paw").hide();

````

###从某个元件里面访问另外一个元件的时间轴

从一个元件里访问另外一个元件,使用sym.getComposition().getStage().getSymbol()。如下例:

```
// Get the stage from the composition level, get the symbol,
// and play the timeline
sym.getComposition().getStage().getSymbol("symbolName").play();

````

从元件中访问嵌套元件时间轴,嵌套调用getSymbol,如下例:

```
// Get the stage from the composition level, get the parent symbol,
// then get the nested symbol timeline
sym.getComposition().getStage().getSymbol("symbolName1").getSymbol("symbolName2").play(0);


````

你能从另一个元件的某个元件时间轴访问元素,如下例:

```
//Get the symbol element "kitten_1" and hide the element "kitten_paw"
sym.getComposition().getStage().getSymbol("kitten_1").$("kitten_paw").hide();

````

###从stage访问嵌套元件时间轴

访问嵌套元件的时间轴,在你的事件中,这样写:

```
sym.getSymbol("symbolName").getSymbol("nestedElementName").play();

```

你也可以从舞台的嵌套元件里访问元素。


```
// Hide the element "paw" from within a nested symbol
sym.getSymbol("kitten_1").getSymbol("kitten_paw").$("paw").hide();
```
###从另外的元件访问嵌套的元件时间轴
```
sym.getComposition().getStage().getSymbol("symbolName").getSymbol("nestedElementName").play();


````
你能够从舞台访问嵌套时间轴里面的元素。

```
// Hide the element "paw" from within a nested symbol
sym.getComposition().getStage().sym.getSymbol("kitten_1").getSymbol("kitten_paw").$("paw").hide();

````

##使用元件元素

访问元件的相关元素:
```
sym.getSymbolElement();
```

返回元素的AdobeEdge.$处理函数。如果jQuery被添加到作品的扩展脚本中,或者在Edge Animate运行时之前加载,将返回jQuery处理函数。
你可以使用任何在AdobeEdge.$中可用的API文档,而不使用jQuery。例如:

```
sym.getSymbolElement().hide();

````

注意:如果你要将jQuery作为扩展依赖添加到Edge作品中,sym.getSymbolElement()将返回一个jQuery包装,
这种情况下AdobeEdge.$重新定义为jQuery。
在返回结果中你可以使用jQuery的API。

另外的例子:
```
// Create a new symbol "kitten_paw" on the Stage
var kitten_paw = sym.createChildSymbol("kitten_paw", "Stage");
// Reference the symbol
var kitten_sym = kitten_paw.getSymbolElement();
// Hide the element
kitten_sym.hide();



````

##获取元件子对象

使用一下方法获取parent的所有子元件:

```
sym.getChildSymbols();

````

例如,如果你在舞台级别设置了以下事件,所有舞台的子元件将被影响,但孙子节点保持不变:

```
//设置子元件变量
var childSymbols=sym.getChildSymbols();
 for(var i=0;i<childSymbols.length;i++){
    childSymbols[i].stop();//停止所有子元件
 }

````

##获取元件父

操作父元件,使用以下代码:

```
sym.getParentSymbol();

````

他讲获取子元件的父,例如:
我们拥有以下层级结构:stage>kitten_sym>kitten_paw。
以下代码设置了一个click事件在"kitten_paw"里面。

```
//停止父元件时间轴
sym.getParentSymbol().stop();

```

##动态创建元件

创建子元件:

```
sym.createChildSymbol();


````

以下通过父元素名称返回一个独立的元件对象:

```
// Create a child symbol instance of "kittenpaw_sym" inside the
// element "kitten".
// Note: "kitten_sym" is the name as it appears in the symbol library,
// not the elements panel.
sym.createChildSymbol("kittenpaw_sym", "kitten")


````

另一种:

```
// Create an instance of symbol kitten_paw under every div element with a class name 'container'.
sym.getComposition().createSymbolChild("kitten_paw", "div.container");

````

