# DOM DOM事件模型或DOM 事件机制与事件委托
事件是用户或者浏览器自己执行的某种动作，是文档或者浏览器发生的一些交互瞬间，比如点击（click）按钮等，这里的click就是事件的名称。JS与html之间的交互是通过事件实现的，DOM支持大量的事件。
示例代码：
<div class="爷爷">
<div class="爸爸">
<div class="儿子">文字</div>
        </div>
</div>
即.爷爷>.爸爸>.儿子, 给3个div分别添加事件监听fnYe/fnBa/fnEr
即点击父元素也算点击子元素，相反也一样。
但再调用顺序上网景与IE就有了不同，再W3C 2002年发布标准后规定浏览器同时支持两种调用顺序.首先按爷爷->爸爸->儿子顺序看有没有函数监听, 然后按儿子->爸爸->爷爷顺序看有没有函数监听。按照专业术语来说就是先捕获然后冒泡。
因此, 用专业术语来说这2种顺序分别就是DOM事件模型的事件捕获和事件冒泡.一个事件发生后，会在子元素和父元素之间传播（propagation）。

由外向内找监听函数, 叫事件监听.
由内向外找监听函数, 叫事件冒泡.

## 事件绑定API addEventListener

IE5: baba.attachEvent(‘onclick’, fn)//事件冒泡
网景: baba.addEventListener(‘click’, fn)//事件捕获
W3C: baba.addEventListener(‘click’, fn, bool)//如果bool不传或为falsy, 则fn使用事件冒泡, 反之则fn使用事件捕获.
target 与 currentTarget 区别
e.target 用户操作的元素 e.currentTarget 程序员监听的元素
取消冒泡
捕获不能取消，冒泡可以 e.stopPropagation 中断冒泡

## 简述事件委托

js里的事件委托：当事件触发时，把想要做的事情委托给父元素处理。

事件委托的优点有两点
1. 可以省内存
2. 可以监听动态元素

## 怎么阻止默认动作？

使用event.preventDefault()可以取消默认事件。
## 怎么阻止事件冒泡？

使用e.stopPropagation()来阻止事件冒泡
注：有些事件不可取消冒泡
MDN搜索scroll event，看到Bubbles和Cancelable
Bubbles的意思是该事件是否冒泡
Cancelable的意思是开发者是否可以取消冒泡
推荐看MDN英文版，中文版内容不全