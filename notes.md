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
    * 因为 ```:hidden() ```是一个 ```jQuery ```延伸出来的一个选择器。 并且不是的```CSS```规范的一部分, 使用```:hidden()```查询不能充分利用原生```DOM```提供的```querySelectorAll()``` 方法来提高性能。为了在现代浏览器上获得更佳的性能，请使用```.filter(":hidden")```代替。
