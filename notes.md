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
* ```remove()``` 移除选定元素及其内部所有元素,```remove() ```内部会自动操作事件销毁方法,所以使用起来非常方便

**remove() 与 empty()**
* 要用到移除指定元素的时候,```jQuery```提供了 ```empty()``` 与 ```remove([expr])``` 两种方法,两个元素都是删除元素,到那时两者还是有区别的
* ```empty() ```方法
    * 严格的讲,```empty() ```方法并不是删除节点,而是清空节点,他能清空元素中的所有后代节点
    * 但是,```empty() ```不能删除自己本身这个节点(就像 喝可乐,只能喝掉饼子里面的内容,但是不能吃掉瓶子)
* ```remove()```
    * 该节点与该节点所包含的所有后代节点将同时被删除(就像 吃苹果,皮 肉 都一起吃掉(假设苹果没有籽))
    * 提供传递一个筛选的表达式(```expr``` 指的是``` express ```(表达式)) ,删除指定合集中的元素

**replaceWith(newContent) 与 replaceAll(target)**
*``` replaceWith(newContent)``` : 用提供的内容替换集合中所有匹配的元素 并且 返回被删除元素的集合
* ```.replaceAll()``` 与``` .replaceWith()``` 功能类似,主要是目标和源的位置区别
* ``` .replaceWith()``` 与``` .replaceAll()```方法**会删除**与节点相关联的所有数据和事件处理程序
* ```.replaceWith()``` 方法和大部分其他``` jQuery ```方法一样,返回 ```jQuery```对象,所以可以和其他方法链接使用
* ``` .replaceWith() ```方法返回的 ```jQuery ```对象引用的是替换前的节点,而不是通过 ```replaceWith/replaceAll``` 方法替换后的节点

**小汇总**
* ```.append()  ```     --        ```appendTo()```
* ```.prepend()```      --        ```prependTo()```
* ```.before() ```      --        ```insertBefore()```
* ```.after()  ```      --       ``` insertAfter()```
* ```.detach()```
* ```.remove()```
* ```.empty()   ```
* ```.clone()  ```      --       ``` (true深拷贝;无参数 浅拷贝)```
* ```.replaceWith()```    --       ``` .replaceAll()```

**.wrapAll()**
* ```.wrapAll(wrappingElement)``` : 给集合中匹配的元素增加一个外面包裹的 ```HTML``` 结构(所有的匹配元素在一起,一共在所有元素的外面添加一个``` wrappingElement)```
* ```.wrapAll(function)``` : 一个回调函数,返回用于包裹匹配元素的``` HTML```内容 或 ```jQuery```对象(是每个匹配元素外面都添加一个 ```function ```返回的``` wrappingElement```,而不是所有元素外面总共一个 ```wrappingElement)```

**.find() 与 .children()**
* ```.find() ```与 ```.children() ```方法是相似的
* ```.children() ```只查找第一级的子元素(也就是只会查找 儿子辈 的元素,不会查找 孙子 及 孙子 后代的元素)
* ``` .find()```查找范围包括子节点的所有后代节点

**.parent() 与 .parents()**
*``` parents()```和```.parent()```方法是相似的，但后者只是进行了一个单级的DOM树查找
* ```$( "html" ).parent()```方法返回一个包含```document```的集合，而```$( "html" ).parents()```返回一个空集合。

**closest() 和 parents()**
* ``` .parents()``` 和 ```.closest() ```有点相似,都是往上遍历祖辈元素,但是两者还是有区别的,否则就没有存在的意义了
* 起始位置不同:``` .closest()``` 开始于当前元素,```.parents() ```开始于父元素
* 遍历的目标不同 : ```.closest()``` 要找到指定的目标```.parents() ``` 遍历到文档根元素```.closest() ``` 向上查找,直到找到一个匹配的就停止查找,``` .parents() ``` 一直找到根元素,并将匹配的元素加入集合
* 结果不同: ```.closest(``` 返回的是包含零个或者一个元素``` jQuery``` 对象,```.parents()  ```返回的是 包含零个或者一个或者多个元素的 ```jQue``` 对象

**.mouseenter()**
* ```.mouseenter() JavaScript``` 事件是``` IE``` 专有的.由于该事件在平时很有用,```jQuery``` 的模拟这一事件,以便他可用于所有浏览器.该事件在鼠标移入到元素上时被触发.任何 ```HTML``` 元素都可以接受此事件
* ``` .mouseenter() ```与 ```.mouseover() ```的区别
    * 冒泡的方式处理问题


## 表单事件
**focus focusin blur focusout**
* ``` focus``` : 当 ```focusable``` 元素获得焦点时,不支持冒泡
* ``` focusin``` 和  ```focus ```一样,只是 ```focusin ```支持冒泡
* ```blur ```: 当 ```focusable``` 元素失去焦点时,不支持冒泡
* ``` focusout``` 和``` blur``` 一样,只是``` focusout ```支持冒泡
* 事件触发顺序
    * 对于同时支持这四个事件的浏览器,事件执行顺序为``` focusin``` > ```focus ```> ```focusout``` > ```blur```

**focusable**
* 什么是 ```focusable``` 元素
    * 默认情况下,只有部分``` HTML``` 元素能够获得鼠标焦点,如 ```input``` ,很大一部分 ```HTML``` 元素是不能获得鼠标焦点的 如 ```div ```,这些能够获得鼠标焦点的元素就是 ```focusable ```元素.
* 要想一个元素获得焦点,可以通过三种方式
    * 鼠标点击
    * ```tab``` 键
    * 调用 ```focus() ```方法
* 默认情况下,哪些元素是 ```focusable``` 元素
    * ``` window ```: 当页面窗口从隐藏变为前置可见时 ,``` focus ```事件就会触发
    * 表单元素(```form controllers```) : ```input``` /``` option``` / ```textarea ```/``` button```
    * 链接元素(```links```) : ```a``` 标签 /``` area``` 标签 (必须要带 ```href``` 属性,包括 ```href``` 属性为空)
    * 设置了 ``` tabindex``` 属性(```tabindex ```值非 ```-1```) 的元素
    * 设置了``` contenteditable = "true"``` 属性的元素

**form submit**
* ```form ```元素有默认提交表单的行为,如果通过``` submit``` 处理的话,需要禁止浏览器的默认行为.
* 传统的方式是调用事件对象``` e.preventDefault()``` 来处理
* ```jQuery ```中,可以直接在函数中最后结尾``` return false``` 即可
```
$("#target").submit(function(data) { 
   return false; //阻止默认行为，提交表单
});
```


## 键盘事件
**keydown**
* ```keydown``` 事件会少一个字符是因为事件触发在前,获取输入在后,所以获取的是前面已经输入的字符,而不是```keydown``` 时间发生时正在输入的字符
* ```keyup ```事件没有 ```keydown ```的问题存在,是因为 ```keyup``` 事件发生的时候,内容已经输入了,已经获得了输入 相应的值,所以可以直接获取此次 ```keyup``` 事件输入时的文本内容

**keypress**
* ```keypress``` 与 ```keydown``` ```keyup ```的主要区别
* 只能获取单个字符,不能捕获组合键
* 无法响应系统功能键(如: ```delete```  ```backspace```)
* 不区分小键盘和主键盘的数字字符
* ```keypress ```主要用来接收字母 数字等``` ANSI ```字符,而 ```keydown``` 和 ```keyup``` 是事件过程可以处理任何不被 ```keypress ```识别的击键.比如: 功能键(```F1``` ~ ```F12```) , 编辑键 定位键 以及 任何这些键和键盘换档键的组合等
* 补充: 什么是 ```ANSI```
    * 在``` ASCII ```之后,由于各国语言的加入 ,```ASCII``` 已经不能满足信息交流的需要,因此,为了能够表示其他国家的文字,各国在``` ASCII``` 的基础上制定了自己的字符集,这些从 ```ANSI ```标准派生的字符集被习惯的统称为``` ANSI ```字符集,他们正式的名称应该是 ```MBCS```(```Multi-Byte Chactacter System``` 即 多字节字符系统)

* ``` keydown``` ```keypress```  ```keyup ```事件的区别
    * [参考资料](http://www.jianshu.com/p/8f839f558319)


## 事件的绑定和解绑

**on()**
* 在表单事件和键盘事件中,都可以直接给元素绑定一个处理函数,所有这类事件都是属于快捷处理,素有的快捷事件在底层的处理都是通过一个 ```on``` 方法来实现的
* ```jQuery``` ```on()``` 方法是官方推荐的绑定事件的一个方法
* 基本用法 : ```.on(evens,[selector],[data])```
* 快捷键 与 ```on()``` 事件的不同
    * ```on ```可以自定义事件名称
    ```
    $("#elem").click(function(){})  //快捷方式
    $("#elem").on('click',function(){}) //on方式
    ```
    * 多个事件绑定同一个函数
    ```
    $("#elem").on("mouseover mouseout",function(){ });
    ```
    > 通过空格分离,传递不同的事件名称,,可以同时绑定多个事件

    * 多个事件绑定不同函数
    ```
    $("#elem").on({
    mouseover:function(){},  
    mouseout:function(){}
    });
    ```

    > 通过空格分离,传递不同的事件名,可以同时绑定多个事件,每一个事件执行自己的回调方法

    * 将数据传递到处理程序 

    ```
    function greet( event ) {
        alert( "Hello " + event.data.name ); //Hello 慕课网
    }
    $( "button" ).on( "click", {
        name: "慕课网"
    }, greet );
    ```

    > 可以通过第二参数(对象),当一个事件被触发时,要传递给事件处理函数

    * ```on() ```的事件委托机制 **on的高级用法**
    ```
    <div class="left">
    <p class="aaron">
        <a>目标节点</a> //点击在这个元素上
    </p>
    </div>
    ```
    操作如下: ```$("div").on("click","p",fn)```
    *   事件绑定在最上层的``` div ```元素上,当用户触发在``` a 元```素上的事件时,事件会向上冒泡,一直会冒泡到``` div ```元素上.如果提供了第二个参数,那么事件在网上冒泡的过程中遇到了选择器匹配的元素,将会触发事件回调函数

## 事件对象
**事件对象的作用**
* 事件对象是用来记录一些事件发生时的相关信息的对象.事件对象只有事件发生时才会产生,并且只能是事件处理函数内部访问,在所有事件处理函数运行结束后,事件对象就被销毁
* ```event.target``` 
    *``` target ```属性可以是注册事件时的元素,或者它的子元素,通常用于比较 ```event.target``` 和 ```this ```来确定事件是不是由于冒泡而触发的.经常用于事件冒泡时处理事件委托
    * 简单来说,```event.target ```代表当前触发事件的元素,可以通过当前元素对象的一系列属性来判断是不是我们想要的元素

**jQuery事件对象的常用属性和方法**
* ```event.type``` : 获取事件的类型
```
$("a").click(function(event) {
  alert(event.type); // "click"事件
});
```
* ```event.pageX ``` 和 ```event.pageY``` : 获取鼠标当前相当于页面的坐标
    * 通过这两个属性,可以确定元素在当前页面的坐标值,鼠标相对于文档的左边缘的位置(左边)与(顶边)的距离,简单来说是从页面左上角开始,既是以页面为参考点,**不随滑动条移动而变化**
* ```event.preventDefault()``` 方法 : 阻止默认行为
    * 这个用的特别多,在执行这个方法后,如果点击一个链接(比如:```a ```标签) ,浏览器不会跳转到新的``` URL``` 去了.我们可以用 ```event.isDefaultPrevented() ```来确定这个方法是否(在那个事件对象上)被调用过了
    * eg 
    ```
    $(document).ready(function(){
        $("a").click(function(event){
            event.preventDefault();
            alert("Default prevented: " + event.isDefaultPrevented());
        });
    });
    // 返回值为:Default prevented : true
    ```

* ```event.stopPropagation() ```方法 : 阻止事件冒泡
    * 事件是可以冒泡的,为防止事件冒泡到``` DOM``` 树上,也就是不触发任何前辈元素上的事件处理函数
    * 该方法将停止事件的传播,阻止它被分派到其他 Document 节点.在时间传播的任何阶段都可以调用它.注意,虽然该方法不能阻止同一个 ```Document``` 节点上的其他事件句柄被调用,但是他可以阻止把事件分派到其他节点

* ```event.which```  : 获取在鼠标单击时,单击的是鼠标的哪个按键
    * ```event.which ```将``` event.keyCode ```和 ```event.charCode``` 标准化了
    * ```event.which```也将正常化的按钮按下(```mousedown``` 和 ```mouseup``` ```events```)，左键报告```1```，中间键报告```2```，右键报告```3```
    
*  ```event.currentTarget``` : 在事件冒泡过程中的当前DOM元素
    * 冒泡前的当前触发事件的```DOM```对象, 等同于```this.```

* ```this```和 ```event.target ```的区别：
    * ```js```中事件是会冒泡的，所以```this```是可以变化的，但```event.target```不会变化，它永远是直接接受事件的目标```DOM```元素；

* ```.this```和```event.target```都是```dom```对象
    * 如果要使用```jquey```中的方法可以将他们转换为```jquery```对象。比如```this```和```$(this)```的使用、```event.target```和```$(event.target)```的使用；

## 动画基础隐藏与显示
**show() 与 hide()**
* show 与 hide 方法非常常用,但是一般很少会基于这两个属性执行动画,大多数情况下还是直接操作元素的显示与隐藏为主
* 注意事项
    * show 与 hide 方法是修改的 display 属性,通过 visibility 属性布局的 css 的方法来单独设置
    * 如果使用 !important 在样式中,比如: display: none !important ,如果希望使用 .show() 方法正常工作,必须使用 .css('display','block !important') 重写样式
    * 如果让 show 与 hide 成为一个动画,那么默认执行动画会改变元素的高度,宽度,透明度

## 上卷下拉效果
**.slideDown() .slideUp()**
* .slideDown( [ duration] [,complete] )
* 持续时间(duration) 是以毫秒为单位的.字符串 fase slow 分别表示 200ms  600ms
* 如果提供其他任何字符串,或者这个 duration 参数被省略,那么默认使用 400ms

**toggle  slideToggle  fadeToggle**
* toggle : 对整个元素的可见样式属性进行动画过渡处理(宽度width 高度height 透明度opacity) -- 既是 切换 显示与隐藏 效果
* slideToggle : 对元素做 高 与 透明度 的过渡处理 -- 切换 上下拉卷滚 的效果
* fadeToggle : 对元素仅做透明度过渡处理 -- 切换淡入淡出效果
* 测试用例代码
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JQ</title>
    <style>
        div { width: 100px; height: 100px; background: yellow; border: 1px red solid; }
    </style>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
    <input type="button" value="yes,im ok">
<!-- JS -->
 
<script src="js/jquery-3.2.1.min.js"></script>
<script>
 
$('input').click(function(){
    $('div:eq(0)').toggle(3000)
    $('div:eq(1)').slideToggle(3000)
    $('div:eq(2)').fadeToggle(3000)
})
     
</script>
</body>
</html>
```

**toggle 与 slideToggle 细节区别**
* toggle : 动态效果为 从右至左.横向动作,toggle 通过 display 来判断切换所有匹配元素的可见性
* slideToggle : 动态效果从下至上.竖向动作,slideToggle 通过高度变化来切换所有匹配元素的可见性

**fadeToggle**
* fadeToggle() 方法在 fadeIn()  和 fadeOut() 方法之间切换
* 元素是淡出显示的,fadeToggle() 会使用淡入效果显示匹配的元素
* 元素是淡入显示的,fadeToggle() 会使用淡出效果显示匹配的元素
* **注释** : 隐藏的元素不会被完全显示(不再影响页面的布局)

## 淡入淡出效果 fadeIn() fadeOut() 方法
* 常见的淡入淡出动画的原理 : 透明度的方法,设置元素透明度为 0 ,可以让元素不可见,透明度的参数是 0 ~ 1 之间的值,通过改变这个值可以让元素有一个透明度的效果

**fadeOut()**
* fadeOut() 函数用于隐藏所有匹配的元素,并且带有 淡出 的过渡动画效果
* 所谓"淡出" ,表示如果元素已经是隐藏状态了,那就不做任何改变;如果元素是可见的,则将其隐藏
* .fadeOut( [ duration ],[ complete ] )
* 通过不透明度的变化来实现所有元素的淡出效果,并在动画完成后可选地触发一个回调函数
* 这个动画只调整元素的不透明度,也就是说 所有匹配的元素的 width 和 height 都不会发生改变


## 动画效果
**animate()**
* 该方法通过 CSS 样式将元素从一个状态改变为 另一个状态.CSS属性值是逐渐改变的,这样就可以创建动画效果
* 只有数字值可以创建动画(比如: margin: 30px),字符串值无法创建动画(比如: backgroun-color:red)
* 数字型的样式属性值会产生渐变效果,非数字型的样式属性值会产生突变效果
* 可以使用 "+=" "-=" 来创建相对动画(relative animations)
* 语法 : 
    * .animate( properties , [ duration ] , [ easing ] , [ callback ] )
        * properties : CSS 样式使用 DOM 名称(比如: fontSize) 来设置,而非 CSS 名称(比如: font-size)
    * .animate( properties , options )
        * options 参数(可选,规定动画的额外选项)
        * 可能的值为 : 
            * duration  --      设置动画执行的时间
            * easing    --      规定要使用的 easing 函数,过渡使用哪种缓动函数
            * step      --      规定每个动画的每一步完成之后要执行的函数
            * progress  --      每一次动画调用的时候会执行这个回调,就是一个进度的概念
            * callback  --      动画完成之后会调用的回调函数
            * queue     --      布尔值.指示是否在效果队列中放置动画.如果为false ,则动画立即开始
            * specialEasing -- 来自 properties 参数的一个或多个 CSS 属性的映射,以及他们的对应的 easing 函数
* **注意** : 如果多个元素执行动画,回调将在每个匹配的元素执行一次,不是作为整个动画执行一次
    * [相关链接](http://www.w3school.com.cn/tiy/t.asp?f=jquery_eff_ani_font)
    * 可以尝试改变动画变化需要的时间,效果会明显一些
* width : "toggle"        --      设置为 左右隐藏
* height : "toggle"     --      设置为 上下滑动隐藏
* opacity : "toggle"    --      设置为 淡出淡入隐藏 
* 常用的方式
```
$('#elem').animate({
    width: 'toggle',  
    height: 'toggle'
  }, {
    duration: 5000,
    specialEasing: {
      width: 'linear',
      height: 'easeOutBounce'
    },
    complete: function() {
      $(this).after('<div>Animation complete.</div>');
    }
  });
  ```
