#Edge Animate 触发器,事件以及行为

## 触发器

在*Adobe Edge Animate*,你可以在时间轴上指定的位置创建触发器。
当Edge Animate播放时间轴并到达出发点,将会执行对应的Javascript代码。
你还可以绑定代码到文档,时间轴以及指定元素。
当处理元素行为的时候,你的代码会元件的上下文中执行。
当前元件被存储在一个叫做`sym`的变量中。
你能够执行元件的API,像这样`this.play() 或者 sym.play()`。
当你使用`setTimeout`的时候`sym`变量更耐用。

##事件

当执行代码的时候,Edge Animate 传递一个事件对象,`e`它能够让你在被调用的地方知道更多的上下文。
比如,`sym.$(e.target).hide();`将在不必知道元素名字的情况下隐藏该元素。

###页面级别的DOM事件

Edge Animate支持以下页面级别事件:

- `scroll`
- `keydown`
- `keyup`
- `resize`
- `orientationChange`

###作品级别的DOM事件

Edge Animate支持以下作品级别的DOM事件:

- `compositionReady`在作品准备播放之后触发,但是在`autoPlay`发生之前。
- `onError`当Javascript error的时候触发,该事件可在页面中的所有作品上触发,因此如果一个页面中有多个作品,
所有的作品处理函数都会被执行。
为了区分是哪个作品出了问题,在参数`e`中设置了`compId`属性来表示作品的ID。
你可以通过比较`compId`来值处理。
另外,`e.originalEvent`值表示导致该错误的事件。

###Element级别DOM事件

Edge Animate提供原生的桌面浏览器element事件。
仅`click`在触屏设备中生成。
如果click事件被绑定,其他鼠标事件将被模拟。
在触屏设备,除了mouse事件之外你还能侦听touch事件。

- `click`
- `dblclick`
- `mouseover`
- `mousedown`
- `mousemove`
- `mouseup`
- `mouseout`



###元素的touch事件

Edge Animate支持设备原生的touch事件。
touch事件能够快速的响应移动设备并且还能支持多点触碰,相反click事件就不能。

- `touchstart`
- `touchmove`
- `touchend`

Edge Animate支持方便的触击事件。
避免parent和child同时侦听触击事件,如果在child中没有处理好触击事件将导致该事件在parent中触发两次。


- `swipeleft`
- `swiperight`

###jQuery事件

Edge支持以下jQuery事件

- `mouseenter`
- `mouseleave`
- `focus`

你能够使用`mouseenter`和`mouseleave`替代`mouseover`和`mouseout`来避免和其他元素冲突。
比如,当在一个元件上使用`mouseover`,元件的子元素可能会打断该鼠标事件。使用`mouseenter`能够避免该冲突

在element事件上阻止默认行为

一些浏览器,尤其是Android版本的WebKit,如果你侦听了鼠标事件将会在touch元素周围显示高亮。
如果你不想要该行为,在你的处理函数中执行`preventDefault`,像这样:

`e.preventDefault();`

###时间轴事件

- `update`
- `play`
- `complete`
- `stop`

###元件事件

- `creationComplete` 当元件被创建和初始化之后`autoPlay`发生之前立即执行。
- `beforeDeletion` 元件被删除之后执行。




##行为

行为是用来响应各种各样事件的JavaScript方法。
为一个给定元素绑定行为到一个事件,我们可以在Edge Animate编辑器和project-name_edgeAction.js中处理。
绑定Edge Animate中的行为会在project-name_EdgeActions.js中生成代码。

尽可能保存生成的代码和注释结构,这些代码能在Edge Animate中手动编辑也可以稍后编辑。
有件事需要注意,手动编写代码的时候不要调用有阻断功能的代码,比如`alert("Hello")`,因为这样会阻断剩下的动画。

**较之前版本的变化**

element 选择器格式修改。
早期版本,我们使用`_`加在element名字前面,新版本中这不是必须的。
老选择器格式:`${_RoundRect}`
新选择器格式:`${RoundRect}`


