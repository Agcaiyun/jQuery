> 在这里会记录一些 jQuery 基础学习过程中的一些笔记，如果笔记能帮到您，那是再好不过的了，如果您发现有错误或者不当的地方，欢迎您随时指正 ^ _ ^

# jQuery 基础笔记

* ```jQuery```是一个```JavaScript```脚本库，不需要特别的安装，只需要我们在页面 ```<head>``` 标签内中，通过 ```script``` 标签引入 ```jQuery``` 库即可
    * 比如： 

    ```
    <script type="text/javascript" src="http://libs.baidu.com/jquery/1.9.1/jquery.js"></script>

    ```
**$(":visible") $(":hidden")**
* 这两个选择器都是 ```jQuery``` 延伸出来的
* ```:hidden ```选择器,不仅仅包含样式是 ```display:"none" ```的元素,还包括隐藏表单``` visibility ```等等
* 我们有几种方式可以隐藏一个元素
    * ```CSS display ```的值是 ```none```
    * ```type="hidden" ```的表单元素
    * 宽度 和 高度 都显式设置为``` 0 ```
    * 一个祖先元素是隐藏的,该元素不会在页面上显示
* 元素的``` visibility: hidden ```或``` opacity: 0 ```被认为是可见的,因为他们仍然占用空间布局.在动画,隐藏一个元素,该元素被人误是可见的,直到动画结束.
* 不在文档中的元素是被认为是不可见的;如果当他们被插入到文档中,```jQuery```没有办法知道他们是否是可见的,因为元素可见性依赖于使用的样式
* 在动画显示的元素期间,动画一旦开始,该元素就被认为是可见的
* 在```jQuery 1.3.2```中，```:hidden```判断方式做了修改。如果他或者其任何父级元素不占据布局空间，这个元素就被认为是隐藏的。CSS的能见度属性```（visibility）```不影响这个选择器的判断（因此```$(elem).css('visibility','hidden').is(':hidden') == false ）```
* [hidden 修改的相关资料](http://docs.jquery.com/Release:jQuery_1.3.2#:visible.2F:hidden_Overhauled)
* **其他注意事项**
    * 因为 ```:hidden() ```是一个 ```jQuery ```延伸出来的一个选择器。 并且不是的```CSS```规范的一部分, 使用```:hidden()```查询不能充分利用原生```DOM```提供的```querySelectorAll()``` 方法来提高性能。为了在现代浏览器上获得更佳的性能，请使用```.filter(":hidden")```代替

**时间绑定中,绑定了多少事件,不用的时候一定要记得销毁(为了防止"内存泄露")**
* remove() 移除选定元素及其内部所有元素,remove() 内部会自动操作事件销毁方法,所以使用起来非常方便

**remove() 与 empty()**
* 要用到移除指定元素的时候,jQuery提供了 empty() 与 remove([expr]) 两种方法,两个元素都是删除元素,到那时两者还是有区别的
* empty() 方法
    * 严格的讲,empty() 方法并不是删除节点,而是清空节点,他能清空元素中的所有后代节点
    * 但是,empty() 不能删除自己本身这个节点(就像 喝可乐,只能喝掉饼子里面的内容,但是不能吃掉瓶子)
* remove()
    * 该节点与该节点所包含的所有后代节点将同时被删除(就像 吃苹果,皮 肉 都一起吃掉(假设苹果没有籽))
    * 提供传递一个筛选的表达式(expr 指的是 express (表达式)) ,删除指定合集中的元素

**replaceWith(newContent) 与 replaceAll(target)**
* replaceWith(newContent) : 用提供的内容替换集合中所有匹配的元素 并且 返回被删除元素的集合
* .replaceAll() 与 .replaceWith() 功能类似,主要是目标和源的位置区别
* .replaceWith() 与 .replaceAll() 方法**会删除**与节点相关联的所有数据和事件处理程序
* .replaceWith() 方法和大部分其他 jQuery 方法一样,返回 jQuery对象,所以可以和其他方法链接使用
* .replaceWith() 方法返回的 jQuery 对象引用的是替换前的节点,而不是通过 replaceWith/replaceAll 方法替换后的节点

**小汇总**
* .append()       --        appendTo()
* .prepend()      --        prependTo()
* .before()       --        insertBefore()
* .after()        --        insertAfter()
* .detach()
* .remove()
* .empty()   
* .clone()        --        (true深拷贝;无参数 浅拷贝)
* .replaceWith()    --        .replaceAll()

**.wrapAll()**
* .wrapAll(wrappingElement) : 给集合中匹配的元素增加一个外面包裹的 HTML 结构(所有的匹配元素在一起,一共在所有元素的外面添加一个 wrappingElement)
* .wrapAll(function) : 一个回调函数,返回用于包裹匹配元素的 HTML内容 或 jQuery对象(是每个匹配元素外面都添加一个 function 返回的 wrappingElement,而不是所有元素外面总共一个 wrappingElement)

**.find() 与 .children()**
* .find() 与 .children() 方法是相似的
* .children() 只查找第一级的子元素(也就是只会查找 儿子辈 的元素,不会查找 孙子 及 孙子 后代的元素)
* .find() 查找范围包括子节点的所有后代节点

**.parent() 与 .parents()**
* parents()和.parent()方法是相似的，但后者只是进行了一个单级的DOM树查找
* $( "html" ).parent()方法返回一个包含document的集合，而$( "html" ).parents()返回一个空集合。

**closest() 和 parents()**
* .parents() 和 .closest() 有点相似,都是往上遍历祖辈元素,但是两者还是有区别的,否则就没有存在的意义了
* 起始位置不同: .closest() 开始于当前元素,.parents() 开始于父元素
* 遍历的目标不同 : .closest() 要找到指定的目标,.parents() 遍历到文档根元素,.closest() 向上查找,直到找到一个匹配的就停止查找, .parents() 一直找到根元素,并将匹配的元素加入集合
* 结果不同: .closest() 返回的是包含零个或者一个元素的 jQuery 对象,.parents() 返回的是 包含零个或者一个或者多个元素的 jQuery 对象

