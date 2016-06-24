#JavaScript API

##扩展元件和作品
这些被所有元件实例继承的API通过添加行为扩展了元件的定义。

注意:project-name_edgeActions.js定义了Edge.Symbol的别名"Symbol"。
该别名被短暂的用在该章节中。

重要:当事件发生时"this"将设置到元件实例中,该行为方法调用。
DOM,时间轴和触发的事件,该处理函数的参数"sym"表示元件实例"e"表示一个jQuery事件。
该jQuery事件对象将它的属性附加到真是的事件类型之上。


###bindElementAction
```
Symbol.bindElementAction(compId,symbolName,elementSelector,eventName,actionFunction)


````

- compId -作品ID,通过项目级别的闭包传递。如"EDGE-519469"。
- symbolName -元件ID,通过元件闭包传递。
- elementSelector -元素选择器,例如:"${Rectangle}"
- eventName -事件,例如:click
- actionFunction -事件触发时执行的JavaScript方法

描述:将一个方法和一个动作关联。

例如:

```
AdobeEdge.Symbol.bindElementAction(compId, "stage", "document", "click", function(sym, e) {
    window.open("http://www.mysite.com", "_self");
});

````

###bindTriggerAction

```
Symbol.bindTriggerAction(compId,symbolName,timelineName,delay,actionFunction)

````

- compId -作品ID,通过项目级别的闭包传递。如"EDGE-519469"。
- symbolName -元件ID,通过元件闭包传递。
- timelineName -时间轴名字
- delay -延迟
- actionFunction -事件触发时执行的JavaScript方法

描述:动态创建一个指定元件的触发器。

例如:
```
var time = sym.getLabelPosition("myLabel");
Symbol.bindTriggerAction(compId, symbolName, "Default Timeline", time, function(sym, e) {
    sym.stop();
});

````

###bindTimelineAction

