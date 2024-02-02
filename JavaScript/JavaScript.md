## 各浏览器兼容性
    # 窗口尺寸
        有三种方法能够确定浏览器窗口的尺寸:
            对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：
                window.innerHeight - 浏览器窗口的内部高度(包括滚动条)
                window.innerWidth - 浏览器窗口的内部宽度(包括滚动条)
            对于 Internet Explorer 8、7、6、5：
                document.documentElement.clientHeight
                document.documentElement.clientWidth
            或者
                document.body.clientHeight
                document.body.clientWidth

            例: 实用的 JavaScript 方案（涵盖所有浏览器，包含 IE8 及以下版本的浏览器）：
                var w=window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;
                var h=window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight;

## JavaScript 原理
    运行原理：编译一行，执行一行。
        编译    声明变量
        执行   赋值
        赋值变量LHS查询
        引用变量RHS查询

    堆与栈: 

    作用域：能够储存变量中的值，并且能对其进行访问或修改的区域。

    闭包: 形成一个不销毁的栈环境。

    with()/eval()：
        把字符串当作js代码执行（非"use strict"；模式下）
        注意️：影响性能，引擎无法在编译时对其作用域查找进行优化

    this指向:


    <!-- 模态窗口 -->
        https://www.runoob.com/try/try.php?filename=trycss_image_modal_js

## 书写规范
    const定义常量、let定义变量
        let mySchool = "我的学校"

    class,使用小写字母和中划线
        class="my-school"

    ID,大写字母和下划线
        <view id="MY_SCHOOL"></view>

    组件命名
        首字母大写,及驼峰命名规则
        文件名统一使用index.vue
        例: MyPay

    method 方法命名命名规范
        驼峰式命名，统一使用动词或者动词+名词形式
        请求数据方法，以data结尾
        methods: {
            jumpPage(){},
            openCarInfoDialog(){},
            getListData(){},
            postFormData(){}
        }
        has: 判断是否含有某个值
        is: 判断是否为某个值
        get: 获取某个值
        set: 设置某个值
        update: 更新某个值
        on: 触发事件（click/change 等 dom 事件或者emit派发事件）
        render: 渲染页面
        handle: 执行某一个事件（如果不清楚用什么动词前缀，可以使用 handle）
        还有很多类似的动作，例如：add/delete/put/select/change/move/remove/to等

    例外情况
        作用域不大临时变量可以简写，比如：str，num，bol，obj，fun，arr。
        循环变量可以简写，比如：i，j，k 等，例：
        for (let i = 0; i < arr.length; i ++){
        let obj = arr[i]
        } 

    多个特性的元素应该分多行撰写，每个特性一行。(增强更易读) 例：
        <img
        src="https://"
        alt=""
        >
        <my-component
        a="a"
        d="b"
        c="c"
        >
        </my-component>

    源码风格
        使用 ES6 风格编码
        定义变量使用 let ,定义常量使用 const
        静态字符串一律使用单引号，动态字符串使用反引号
        数组成员对变量赋值时，优先使用解构赋值
        const [num1, num2] = arr
        函数的参数如果是对象的成员，优先使用解构赋值    
        function getUserData({ age, name }) {}
        箭头函数 需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了 this
        ()=> {};

    指令规范
        指令有缩写一律采用缩写形式
        :value=""
        @click=""
        v-for 循环必须加上 key 属性，在整个 for 循环中 key 需要唯一
        避免 v-if 和 v-for 同时用在一个元素上（性能问题）, 可将数据替换为一个计算属性，让其返回过滤后的列表(先把你要循环的数据通过计算属性进行处理)

    挂载全局 :
        Vue.prototype.$api = api
        Vue.prototype.$axios = axios
        Vue.prototype.$echarts = echarts
        Vue.prototype.$dayjs = dayjs
        Vue.prototype.$hotkeys = hotkeys

## javaScript API
    使用 document.write() 方法将内容写到 HTML 文档中

    转义字符\
        \'	单引号
        \"	双引号
        \\	反斜杠
        \n	换行
        \r	回车
        \t	tab(制表符)
        \b	退格符
        \f	换页符

    # 数据验证
        数据验证用于确保用户输入的数据是有效的。

        典型的数据验证有：

        必需字段是否有输入?
        用户是否输入了合法的数据?
        在数字字段是否输入了文本?
        大多数情况下，数据验证用于确保用户正确输入数据。

        数据验证可以使用不同方法来定义，并通过多种方式来调用。

        服务端数据验证是在数据提交到服务器上后再验证。

        客户端数据验证是在数据发送到服务器前，在浏览器上完成验证。

    JavaScript 验证 API
        https://www.runoob.com/js/js-validation-api.html

    HTMLCollection 与 NodeList 的区别

    "use strict";  严格模式
    debugger;  断点、调试代码

    # Error错误处理
        try(){

        }catch(err){

        }

        异常处理：
            ReferencError  非法引用
            TypeError  类型错误
            SyntaxError  语法错误
            URIError  encodeURI() 函数产生的错误
            RangeError  数值超出规定的范围
            SyntaxError  eval()函数产生的错误

            err.name  错误类型
            err.message  错误信息

    # 数据类型
        值类型: String、Number、Boolean、Null、Undefined、Symbol。
        引用类型: Object、Array、Function，RegExp、Date。

        值类型可以用typeof，引用类型用instanceof。
            typeof xxx  检测类型
            instanceof  //判断一个属性是否存在一个对象身上
                value instanceof Promise

        new Boolean():
            值为0、-0、null、""、false、undefined、NaN时为false

    # 运算符
        位运算符: 位运算符工作于32位的数字上。任何数字操作都将转换为32位。结果会转换为JavaScript数字
            运算符	描述	例子	    类似于	        结果	十进制
                &	AND	    x = 5 & 1   0101 & 0001	    0001    1
                |	OR	    x = 5 | 1	0101 | 0001	    0101    5
                ~	取反	x = ~ 5	    ~0101	        1010    -6
                ^	异或	x = 5 ^ 1	0101 ^ 0001	    0100    4
                <<	左移	x = 5 << 1	0101 << 1	    1010    10
                >>	右移	x = 5 >> 1	0101 >> 1	    0010    2

    # 全局属性
        属性:
            Infinity  代表正的无穷大的数值
            NaN  指示某个值是不是数字值
            undefined  指示未定义的值

        方法:
            encodeURI()  把字符串编码为 URI
            decodeURI()  解码某个编码的 URI
            encodeURIComponent()  把字符串编码为 URI 组件
            decodeURIComponent()  解码一个编码的 URI 组件

            eval()  计算 JavaScript 字符串，并把它作为脚本代码来执行
            
    # Array数组
        array.unshift()  向数组的开头添加一个或更多元素，并返回新的长度
        array.shift()  删除并返回数组的第一个元素
        array.push()  向数组的末尾添加一个或更多元素，并返回新的长度(改变原数组)
        array.pop()  删除数组的最后一个元素并返回删除的元素(改变原数组)
        array.reverse()  反转数组的元素顺序(改变原数组)
        array.fill('', start, end)  使用一个值来替换数组
        array.slice(start, end)  选取数组的一部分，并返回一个新数组(不改变原数组)
        array.splice(index, number, newItem)  删除并返回删除元素后添加新元素
        array.join()  使用字符串拼接数组，并返回字符串
        array.indexOf()  搜索数组中的元素，并返回它的索引值,没找到则返回-1
        array.includes()  判断一个数组是否包含一个指定的值
        array.concat(arr)  连接两个或更多的数组/字符串，并返回结果

        array.forEach((item) => {})  遍历数组(改变原数组)
        array.map((item) => {})  遍历数组(不改变原数组)
        array.filter((item) => {})  过滤器,返回所匹配的值，生成新的数组
        array.every((item) => {})  遍历数组是否符合条件，全符合为true,否则false
        array.some((item) => {})  遍历数组是否含有符合条件，只要有一项满足条件，就会返回true
        array.find((item) => {})  //返回第一个所匹配的值
        array.findIndex(item => {})  //返回第一个所匹配的值的索引
        array.sort((a, b) => {return a-b;})	对数组的元素进行排序。默认升序(unicode编码)
    
        Array.isArray()  判断是否为数组
        Array.from(arr, callback)  通过给定的对象中(伪数组)创建一个数组(必须要有length属性)
        array.flat(2)  将多维数组转换成低维数组，参数为深度(使用 Infinity，可展开任意深度的嵌套数组)
        array.flatMap(item => {})  将多维数组降维并遍历数组

        array.reduce((total, item, index, arr)=>{}, value)  累加器（从左到右）
            total  必需。初始值, 或者计算结束后的返回值。
            item  必需。当前元素
            currentIndex  可选。当前元素的索引
            arr  可选。当前元素所属的数组对象
            value  可选。传递给函数的初始值
        reduceRight()  将数组元素计算为一个值（从右到左）

        array.lastIndexOf()  从后面搜索数组中的元素，并返回它第一次出现的位置
        array.copyWithin(index, start, end)  拷贝到指定位置，拷贝元素的开始/结束位置
        array.of(item, item2)  将一组值转换为数组
        array.at(index)  返回索引值的值(负数倒数)
        
        array.entries()  返回数组的可遍历对象num.next().value
        array.keys()  返回数组的可迭代对象，包含原始数组的键(key)

    # Number
        属性:
            Number.NaN  非数字
            Number.EPSILON  js表示的最小精度
            Number.MAX_VALUE  可表示的最大的数
            Number.MIN_VALUE  可表示的最小的数
            Number.POSITIVE_INFINITY  正无穷，在溢出时返回,Infinity
            Number.NEGATIVE_INFINITY  负无穷，在溢出时返回,-Infinity
            Number.MAX_SAFE_INTEGER  最大安全整数
            Number.MIN_SAFE_INTEGER  最小安全整数
            
        方法:
            Number()  将字符串转换为数字
            
            Number.parseFloat()  将字符串转换成浮点数，和全局方法 parseFloat() 作用一致
            Number.parseInt()  将字符串转换成整型数字，和全局方法 parseInt() 作用一致

            Number.isFinite()  判断传递的参数是否为有限数字
            Number.isInteger()  判断传递的参数是否为整数
            Number.isNaN()  判断传递的参数是否为NaN
            Number.isSafeInteger()  判断传递的参数是否为安全整数

        pototype:
            toFixed(x)  保留几位小数
            toPrecision(x)  返回一个指定位数的数字
            toExponential()  返回一个数字的指数形式的字符串，如：1.23e+2
        
    # Math
        Math.random()  1~0之间的随机数
        Math.abs(x)  返回 x 的绝对值
        Math.ceil()  对数进行上舍入(5.12=6)
        Math.floor()  对数进行下舍入(1.59=1)
        Math.round()  四舍五入
        Math.max(...arr)  返回最高值
        Math.min(...arr)  返回最低值
        Math.pow(x, y)  返回x的y次幂
        Math.trunc()  去掉小数部分
        Math.sign()  判断为正数1 负数-1 还是零0
        Math.sqrt(x)	返回数的平方根

        Math.PI  圆周率3.14159

        Math.E  算术常量e,约等于2.718
        Math.SQRT2  返回2的平方根,约等于 1.414
        Math.SQRT1_2  返回2的平方根的倒数,约等于 0.707
        Math.LN2  2的自然对数,约等于0.693
        Math.LN10  10的自然对数,约等于2.302
        Math.LOG2E  以2为底的e的对数,约等于 1.4426950408889634
        Math.LOG10E  以10为底的e的对数,约等于0.434

        Math.exp(x)	返回e的指数(e的x次方)
        Math.log(x)  返回数的自然对数（底为e）

        Math.sin(x)  返回数的正弦
        Math.cos(x)  返回数的余弦
        Math.tan(x)  返回角的正切
        Math.tanh(x)  返回一个数的双曲正切函数值
        Math.asin(x)  返回 x 的反正弦值
        Math.acos(x)  返回 x 的反余弦值
        Math.atan(x)  以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值
        Math.atan2(y,x)  返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）

    # String 对象
        属性:
            length  字符串的长度
            constructor	 返回创建字符串属性的构造函数
            prototype  允许您向对象添加属性和方法

        方法:
            String()  把对象的值转换为字符串
            toString()	返回一个字符串(转换16、8、2进制)
            trim()  去除首尾空白
            trimStart()  去除开头空白
            trimEnd()  去除结尾空白
            charAt(index)  返回在指定索引的字符
            toUpperCase()  把字符串转换为大写
            toLowerCase()  把字符串转换为小写
            search('')  查找相匹配的值,并返回索引值,没找到则返回-1(or正则)

            match(reg)  正则表达式的匹配,返回匹配值
            matchAll(reg)  批量匹配
            substr(index, num)	从索引开始提取指定数量字符串
            substring(index, index)  提取字符串中两个指定的索引号之间的字符
            repeat(num)  复制字符串指定次数，并将它们连接在一起返回
            replace('newStr', 'oldStr')  匹配字符串并替换(单个)
            replaceAll('newStr', 'oldStr')	匹配字符串并替换(所有)
            startsWith(str)  查看字符串是否以指定的字符串开头
            endsWith(str)  判断当前字符串是否是以指定的子字符串结尾的
            charCodeAt(index)  返回在指定索引值的字符的 Unicode 编码
            String.fromCharCode()  将 Unicode 编码转为字符

            valueOf()  返回字符串原始值(通常由 JavaScript 在后台自动进行调用，而不是显式地处于代码中)
            localeCompare()  用本地特定的顺序来比较两个字符串,完全匹配0 匹配1 不匹配-1
            toLocaleLowerCase()  根据本地主机的语言环境把字符串转换为小写
            toLocaleUpperCase()  根据本地主机的语言环境把字符串转换为大写
        
        Arrtr:
            includes()  查找字符串中是否包含指定的子字符串
            indexOf()  返回字符串中检索指定字符第一次出现的位置
            lastIndexOf()  返回字符串中检索指定字符最后一次出现的位置
            slice()  提取字符串的片断，并在新的字符串中返回被提取的部分
            split()  把字符串分割为字符串数组
            concat()  连接两个或多个字符串，返回连接后的字符串
        
    
        String HTML 包装方法:
            str.anchor(attr)  创建a标签,str为文本,attr为name值

            big()  用大号字体显示字符串<big>hello world</big>
            small()  使用小字号来显示字符串
            bold()  使用粗体显示字符串
            italics()  使用斜体显示字符串
            strike()  用于显示加删除线的字符串
            link('')	将字符串显示为链接

            fontcolor('color')	使用指定的颜色来显示字符串
            fontsize(num)	使用指定的尺寸来显示字符串。
            fixed()  以打字机文本显示字符串
            sub()  把字符串显示为下标(基线)
            sup()  把字符串显示为上标(基线)

    # 对象扩展
        Object.is(a, b)    判断两个值是否相等
        Object.assign(obj1, obj2)  覆盖对象
        Object.setPrototypeOf(obj1, obj2)  给对象添加原型对象
        Object.getPrototypeOf(obj1)   读取对象
        
        Object.entries(obj)  返回对象可遍历属性[key, value]的数组
        Object.getOwnPropertyDescriptors(obj)  获取对象属性的描述对象

        Object.fromEntries()  将二维数组转换成对象
        Object.entries()      将对象转换成二维数组

     # this指向
        myFun.call(obj, 'xx', 'xx')
        myFun.apply(obj, ['xx', 'xx'])
        myFun.bind(obj, 'xx', 'xx')()  //有返回值且是个函数

    # 条件语句
        if(){}else{}

        不同的结果执行不同的代码
            switch(item){
                case 1: xxx;
                break;
                case 2: sss;
                default: ccc;
            }

    # 循环
        for(let i=0; i<number; i++){}

        for(item in obj){}

        while(){}

        do{}while()

        break 跳出循环

        continue 跳过本次循环

    # JSON
        JSON.parse(data)  将JSON转换成字符串
        JSON.stringify()  将字符串转换成JSON

    # 定时器
        执行一次
            const in = setTimeout(() => {}，1000)

        循环执行
            setInterval(() => {}, 1000)

        关闭定时器/重启
            clearInterval(xxx);
            clearTimeout(xxx);

            in = setTimeout(() => {}，1000)

## Dom
    # DOM 节点
        文档节点、元素节点、属性节点、文本节点、注释节点

### Document 对象
        是 Window 对象的一部分，可通过 window.document 属性对其进行访问

        属性:
            document.activeElement  返回当前获取焦点的元素
            document.cookie  设置或返回与当前文档有关的所有cookie
            document.title  返回当前文档的标题  // Document
            document.body  返回文档的body元素
            document.inputEncoding  返回用于文档的编码方式（在解析时）  // UTF-8
            document.domain  返回当前文档的域名  // 127.0.0.1
            document.doctype  返回与文档相关的文档类型声明 (DTD)  // <!DOCTYPE html>
            document.documentElement  返回文档的根节点  // <html lang="en"></html>
            document.readyState  返回文档状态 (载入中……)  // loading
            document.lastModified  返回文档被最后修改的日期和时间  // 09/04/2023 21:11:58

            document.URL  返回文档完整的URL  // http://127.0.0.1:5501/html-demo/HTML/index.html
            document.baseURI  返回文档的绝对基础URI  // http://127.0.0.1:5501/html-demo/HTML/index.html
            document.documentURI  获取文档本地URI(IE不支持)  // http://127.0.0.1:5501/html-demo/HTML/index.html
            document.referrer  返回载入当前文档的文档URL  // http://127.0.0.1:5501/html-demo/HTML/index.html

            document.forms  返回当前页面所有表单的数组集合  // <form name="Form1"></form>
            document.images  集合返回当前文档中所有图片的数组  // <img src="klematis.jpg">
            document.links	集合返回当前文档所有链接的数组  // <a href=""> 标签和 <area> 标签
            document.scripts  返回文档中所有 <script> 元素的集合  // <script></script>
            document.anchors  集合返回了当前页面的所有超级链接数组  // <a name='#'></a>
            document.embeds  返回文档中所有 <embeds> 元素的集合  // <embed src="helloworld.swf">

            document.implementation  返回处理该文档的 DOMImplementation 对象???

        方法:
            document.addEventListener('click', ()=>{}, true/false)  向文档添加事件句柄
            document.removeEventListener()  移除文档句柄
            document.hasFocus()  方法来查看当前文档是否获取焦点

            创建:
            document.createElement('button')  创建元素节点
            document.createAttribute('class')  创建属性节点  // attr.value='demo'
            document.createTextNode('按钮')  创建文本节点
            document.createComment('注释')  创建注释节点
            document.createDocumentFragment()  创建空的文档片段对象，并返回此对象
            document.normalize()  删除空文本节点，并连接相邻节点???

            获取元素:
            document.getElementById('ID')  返回指定 ID 的元素
            document.getElementsByName('name')  返回带有指定名称的对象的集合
            document.getElementsByTagName('div')  返回指定标签名的所有子元素集合
            document.getElementsByClassName('class')  返回文档中所有指定类名的元素集合，作为 NodeList 对象
            document.querySelector('div'|'#ID'|'.class'|'attr'|'value')  返回指定CSS选择器元素的第一个子元素
            document.querySelectorAll()  返回匹配指定 CSS 选择器元素的所有子元素节点列表

            流:
            document.open()  打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出
            document.write()  向文档写 HTML 表达式 或 JavaScript 代码
            document.writeln()  等同于 write() 方法，不同的是在每个表达式之后写一个换行符
            document.close()  关闭用 document.open() 方法打开的输出流，并显示选定的数据
            
            document.adoptNode(node)  从另外一个文档返回 adapded 节点到当前文档???
            document.importNode()  把一个节点从另一个文档复制到该文档以便应用???

### element 对象
        注: 
            元素可以有属性,属性属于属性节点
            元素对象的子节点可以是元素节点，文本节点，注释节点
            NodeList对象代表了节点列表，类似于HTML元素的子节点集合

        属性:
            element.ownerDocument  返回元素的根元素（文档对象）
            element.tagName  作为一个字符串返回某个元素的标记名（大写）
            element.id  设置或者返回元素的 id
            element.title  设置或返回元素的title属性
            element.attributes  返回一个元素的属性数组
            element.style  设置或返回元素的样式属性,返回一个 CSSStyleDeclaration 对象。
            element.className  设置或返回元素的class属性
            element.classList  返回元素的类名集合,作为 DOMTokenList 对象  // .add()添加类、.remove()移除、.toggle()切换类
            element.innerHTML  设置或者返回元素的内容
            element.textContent  设置或返回一个节点和它的文本内容  // 注: 文本内容包括所有子节点的文本
            element.accessKey='w'  设置Alt+'快捷键'

            element.nodeName  返回节点的节点名（大写）
            element.nodeType  返回元素的节点类型  // 元素1、属性2、文本3、注释8、文档9
            element.(attr、text、comment).nodeValue  返回元素节点的节点值  // 'heelo world'

            element.lang  设置或者返回一个元素的语言
            element.dir  设置或返回一个元素中的文本方向  // ltl左、rtl右
            element.tabIndex  可设置或返回单选按钮的 tab 键控制次序
            element.contentEditable  设置或返回元素的内容是否可编辑  // inherit继承、true可编辑、false不可编辑
            element.isContentEditable  如果元素内容可编辑返回 true，否则返回false
            element.namespaceURI  返回元素命名空间的 URI  // http://www.w3.org/1999/xhtml
            
            父:
            element.parentNode  返回元素的父节点
            兄弟:
            element.previousSibling  返回某个元素紧接之前元素(包含文本节点或注释节点)  // #text  注: 空格文本是文本节点
            element.nextSibling  返回该元素紧跟的下一个节点(包含文本节点或注释节点)  // #text  注: 空格文本是文本节点
            element.previousElementSibling  返回指定元素的前一个兄弟元素(忽略文本和注释节点)
            element.nextElementSibling  返回指定元素之后的下一个兄弟元素(忽略文本和注释节点)
            子:
            element.children  返回元素的子元素的集合
            element.childNodes	返回元素的一个子节点的数组(元素、文本、注释)
            element.firstChild	返回元素的第一个子节点(包含文本节点或注释节点)  // #text  注: 空格文本是文本节点
            element.lastChild  返回最后一个子节点(包含文本节点或注释节点)  // #text  注: 空格文本是文本节点
            element.firstElementChild  返回元素的第一个子元素(忽略文本和注释节点)  // .tagName获取标签名、.text获取文本
            element.lastElementChild  返回指定元素的最后一个子元素(忽略文本和注释节点)  // .tagName获取标签名、.text获取文本

        方法:
            element.addEventListener('', ()=>{}, true/false捕获or冒泡)	向指定元素添加事件句柄
            element.removeEventListener()  移除由 addEventListener() 方法添加的事件句柄
            element.getElementsByTagName('div')  返回指定标签名的所有子元素集合
            element.getElementsByClassName('class')  返回文档中所有指定类名的元素集合，作为 NodeList 对象。
            element.querySelector()  返回匹配指定 CSS 选择器元素的第一个子元素
            element.focus()  为元素设置焦点
            element.blur()  移除元素焦点
            元素: 增、删、改、克隆
            element.appendChild(element)  为元素添加一个新的子元素or移除元素到另外一个元素
            element.insertBefore(newArrt, attr)  在指定子元素之前添加新元素
                注: 如果文档树中已经存在了newchild，它将从文档树中删除，然后重新插入它的新位置
            element.removeChild(node)  删除一个子节点
            element.replaceChild(newNode, oldNode)  替换一个子节点
            element.cloneNode(true/false)  克隆某个元素  // true克隆子节点/false克隆当前节点(默认)

            element.insertAdjacentHTML('position', html)
            element.insertAdjacentElement('position', node)
            element.insertAdjacentText('position',text)
                position:
                    afterbegin插入到元素第一个子节点之前
                    beforeend元素最后一个子节点之后
                    beforbegin插入自身元素前面
                    afterend元素自身的后面

            属性: 读取、修改、删除
            element.setAttribute('attrName', 'attrValue')  设置或者改变指定属性并指定值
            element.setAttributeNode(attrNode)  设置或者改变指定属性节点
            element.getAttribute('name')  返回指定元素的属性值
            element.getAttributeNode()  返回指定属性节点  // .value获取值
            element.removeAttribute('attr')  从元素中删除指定的属性
            element.removeAttributeNode(attrNode)  删除指定属性节点并返回移除后的节点(ie不支持)  // 需先获取属性节点后再删除，不建议使用
            检索元素:
            element.hasAttribute('attrName')  检测元素是否存在指定属性
            element.hasAttributes()  检测元素是否存在任何属性
            element.hasChildNodes()  检测元素是否具有任何子节点(包含元素、文本、注释)
            element.hasFocus()  返回布尔值，检测文档或元素是否获取焦点  // ?如何检测元素获取焦点
            element.matches('.class')  如果元素匹配指定的 CSS 选择器  // 返回 true，或者 false

            element.toString()  一个元素转换成字符串  // [object HTMLDivElement]
            element.isEqualNode()  检查两个元素是否相等  // ???
            element.isSameNode()  检查两个元素所有有相同节点(火狐不支持)  // ===来比较
            element.normalize()  合并相邻的文本节点并删除空的文本节点???
            element.isDefaultNamespace()  查看定义的命名空间是否为默认的命名空间,是true，否则返回 false。  // ???
            element.isSupported('feature功能','version版本')  如果在元素中支持指定特征返回 true
            element.getFeature()  返回指定特征的执行APIs对象。???
            element.setUserData()  在元素中为指定键值关联对象。???
            element.getUserData()  返回一个元素中关联键值的对象。???
            element.compareDocumentPosition(element)  比较两个元素的文档位置
                值可能是：
                    1：没有关系，这两个节点不属于同一个文档。
                    2： 第一节点（P1）位于第二个节点后（P2）。
                    4：第一节点（P1）定位在第二节点（P2）前。
                    8： 第一节点（P1）位于第二节点内（P2）。
                    16： 第二节点（P2）位于第一节点内（P1）。
                    32:没有关系的，或是两个节点在同一元素的两个属性。
                    注意： 回值可以是值的组合。例如，返回 20 意味着在 p2 在 p1 内部（16），并且 p1 在 p2 之前（4）

    # 获取元素宽高:
        const height = document.documentElement.scrollTop || document.body.scrollTop  // 获取文档滚动条滚动后的高度

        element.offsetWidth	 返回元素的宽度(包括边框border)
        element.offsetHeight  返回任何元素的高度(包括边框border)
        element.offsetLeft  返回当前元素的相对水平偏移文档左上角的距离  // (0, 0)
        element.offsetTop  返回当前元素的相对垂直偏移文档左上角的距离  // (0, 0)
        element.offsetParent  返回元素的偏移父元素  // <body></body>

        element.clientWidth  在页面上返回内容的可视宽度  // 元素width
        element.clientHeight  在页面上返回内容的可视高度  // 元素height
        element.clientLeft  表示一个元素的左border的宽度，以像素表示
        element.clientTop  表示一个元素的顶部border的宽度，以像素表示

        element.scrollWidth  返回元素的整个宽度（包括带滚动条的隐蔽的地方）
        element.scrollHeight  返回元素的整个高度（包括带滚动条的隐蔽的地方）
        element.scrollLeft  返回元素滚动后的左边缘和视图左边缘之间的距离  // 滚动后
        element.scrollTop  返回元素滚动后的顶部边缘和视图顶部边缘之间的距离  // 滚动后
        
            offset  包含边框
            client  不含边框(不含滚动条)
            scroll  不含边框(包含滚动条)

### 属性对象
    attr.name  返回属性名称
    attr.value  设置或者返回属性值
    attr.specified  如果属性被指定返回 true ，否则返回 false

    attr.isId  如果属性是 ID 类型，则 isId 属性返回 true，否则返回 false。  // ie and opera不支持
        
    nodemap.getNamedItem()  从节点列表中返回的指定属性节点  // element.attributes.getNamedItem("onclick")
    nodemap.removeNamedItem()  从节点列表中删除指定属性节点  // element.attributes.removeNamedItem('attrName')
    nodemap.setNamedItem()  从节点列表中设置指定属性节点(通过名称)  // element.attributes.setNamedItem(attr)

    nodemap.item()  返回节点列表中处于指定索引号的节点  // 等同于[0]
    nodemap.length  返回节点列表的节点数目

### 事件对象
    

    # 鼠标事件
        onclick  当用户点击某个对象时调用的事件句柄
        ondblclick  当用户双击某个对象时调用的事件句柄
        oncontextmenu  在用户点击鼠标右键打开上下文菜单时触发

        onmousedown  鼠标按钮被按下
        onmouseup  鼠标按键被松开  注: 按键松开后才触发click/contextmenu

        mouseover  当鼠标指针移至元素之上时运行脚本(冒泡)
        mouseout  当鼠标指针移出元素时运行脚本(冒泡)

        mouseenter  当鼠标指针移动到元素上时触发(非冒泡)
        mouseleave  当鼠标指针移出元素时触发(非冒泡)

        mousemove  当鼠标指针移动时运行脚本
        mousewheel  当转动鼠标滚轮时运行脚本

    # 键盘事件on
        keydown  当按下按键时运行脚本
        keypress  当按下并松开按键时运行脚本
        keyup  当松开按键时运行脚本

    # 框架/对象事件
        onscroll  当文档/元素被滚动时发生的事件
        onerror  在加载外部文件（文档或图像）发生错误时触发  // img

        onload  在页面或图像加载完成后立即发生  // 从浏览器缓存中读取时不触发  <body></body>
        onpageshow  该事件在用户访问页面时触发  // 在每次加载页面时触发  <body></body>

        onbeforeunload  该事件在即将离开页面（刷新或关闭）时触发  // 离开前  <body></body>
        onpagehide	在用户离开网页时触发  <body></body>
        onunload  用户退出页面  <body></body>

        onresize  在窗口或框架被调整大小时发生  <body></body>
        onhashchange  该事件在当前 URL 的锚部分发生修改时触发  <body></body>

    # 表单事件
        onblur  元素失去焦点时触发
        onfocus  元素获取焦点时触发
        oninput  元素获取用户输入时触发  // 立即触发
        onchange  该事件在表单元素的内容改变时触发  // 失焦后触发

        onselect  用户选取文本时触发  // <input>
        onsubmit  表单提交时触发  // <form></form>
        onreset  表单重置时触发  // <input type="reset">  HTML5不支持
        
        onfocusin  元素即将获取焦点时触发  // 兼容性不好
        onfocusout  元素即将失去焦点时触发  // 兼容性不好
        onsearch  用户向搜索域输入文本时触发  // ie、火狐不支持 <input type="search">

        表单事件on:
            invalid  当元素无效时运行脚本
            contextmenu  当触发上下文菜单时运行脚本
            formchange  当表单改变时运行脚本
            forminput  当表单获得用户输入时运行脚本

    # 剪贴板事件
        oncopy  该事件在用户拷贝元素内容时触发
        oncut  该事件在用户剪切元素内容时触发
        onpaste  该事件在用户粘贴元素内容时触发

    # 打印事件
        onafterprint  该事件在页面已经开始打印，或者打印窗口已经关闭时触发  // safari、opera不支持  <body></body>
        onbeforeprint  该事件在页面即将开始打印时触发  // chrome、safari、opera不支持  <body></body>

    # 拖动事件
        ondrag  该事件在元素正在拖动时触发
        ondragend  该事件在用户完成元素的拖动时触发
        ondragenter  该事件在拖动的元素进入放置目标时触发
        ondragleave  该事件在拖动元素离开放置目标时触发
        ondragover  该事件在拖动元素在放置目标上时触发
        ondragstart  该事件在用户开始拖动元素时触发
        ondrop  该事件在拖动元素放置在目标区域时触发

    # 动画事件
        animationend  该事件在 CSS 动画结束播放时触发  // webkitAnimationEnd兼容性 Chrome, Safari 和 Opera
        animationiteration  该事件在 CSS 动画重复播放时触发  // webkitAnimationIteration
        animationstart  该事件在 CSS 动画开始播放时触发  // webkitAnimationEnd

    # 过渡事件
        transitionend	该事件在 CSS 完成过渡后触发  // webkitTransitionEnd  // Safari 3.1 到 6.0 代码

    # 其他事件
        onmessage  该事件通过或者从对象(WebSocket, Web Worker, Event Source 或者子 frame 或父窗口)接收到消息时触发 
        onpopstate  该事件在窗口的浏览历史（history 对象）发生改变时触发。	 
        onstorage  该事件在 Web Storage(HTML 5 Web 存储)更新时触发	 
        onwheel  该事件在鼠标滚轮在元素上下滚动时触发
    
        visibilitychange  该事件用于检测当前页面的可见性状态是否发生变化

    # 鼠标/键盘事件对象
        鼠标:
        event.button  返回当事件被触发时，哪个鼠标按钮被点击  // 0左键|1中间|2右键

        event.clientX  鼠标指针的水平坐标  // 相对于浏览器页面(0, 0)
        event.clientY  鼠标指针的垂直坐标  // 相对于浏览器页面(0, 0)
        event.screenX  鼠标指针相对于屏幕的水平坐标
        event.screenY  鼠标指针相对于屏幕的垂直坐标

        event.relatedTarget  返回与事件的目标节点相关的节点
            对于 mouseover 事件来说，该属性是鼠标指针移到目标节点上时所离开的那个节点
            对于 mouseout 事件来说，该属性是离开目标时，鼠标指针进入的节点

        键盘:
        event.ctrlKey	返回当事件被触发时，"CTRL" 键是否被按下并保持住  // true|false|1|0
        event.altKey  返回当事件被触发时，Alt 键是否被按下并保持住  // true|false|1|0
        event.shiftKey	返回当事件被触发时，"SHIFT" 键是否被按下并保持住  // true|false|1|0
        event.metaKey  返回当事件被触发时，"meta" 键是否被按下并保持住  // true|false|1|0

        获取按下的键盘按键Unicode值:
        event.charCode  返回onkeypress事件触发键值的字母代码,该属性用于 onkeydown 或 onkeyup 事件，返回值总为 "0"。
        event.keyCode  返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码  // event.which || event.keyCode  兼容火狐
        event.which  返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码  // event.which || event.keyCode  兼容IE
        event.key  按下按键时获取键盘按钮

        event.Location  返回按键在设备上的位置  // safari不支持
            由4个常数表示：
                0该值几乎包含了所有的按键
                1左侧按键 (如左侧的 "CTRL" 键或左侧的 "ALT" 键)
                2右侧按键 (如右侧的 "CTRL" 键或左侧的 "ALT" 键)
                3数字按键（在标准键盘的右侧）

        方法:
            event.initMouseEvent()  初始化鼠标事件对象的值
            event.initKeyboardEvent()  初始化键盘事件对象的值

## BOM
    属性:
        window.scrollX  获取滚动条滚动后的左边缘和视图左边缘之间的距离  // 滚动后
        window.scrollY  获取滚动条滚动后的顶部边缘和视图顶部边缘之间的距离  // 滚动后

        window.innerWidth  返回当前窗口显示的宽度(文档区域)
        window.innerHeight  返回当前窗口显示的高度(文档区域)
        window.outerWidth  返回当前窗口宽度，包含工具条与滚动条(整个浏览器窗口)
        window.outerHeight  返回当前窗口高度，包含工具条与滚动条(整个浏览器窗口)

        window.screenLeft  返回窗口相对于屏幕的x坐标(不兼容火狐)
        window.screenTop  返回窗口相对于屏幕的y坐标(不兼容火狐)
        window.screenX	返回窗口相对于屏幕的x坐标(不兼容IE)
        window.screenY	返回窗口相对于屏幕的y坐标(不兼容IE)


        window.self  返回对当前窗口的引用。等价于Window属性
        window.top  返回最顶层的父窗口
        window.parent  返回父窗口
        window.closed  返回窗口是否已被关闭
        window.name  设置或返回窗口的名称
        window.opener  返回对创建此窗口的窗口的引用

        window.frames  返回窗口中所有命名的框架。该集合是 Window 对象的数组，每个 Window 对象在窗口中含有一个框架
        window.length  设置或返回窗口中的frames框架数量

    方法:
        scrollBy(x, y)	按照指定的像素值来滚动内容
        scrollTo(x, y)	把内容滚动到指定的坐标

        JavaScript 弹窗:
            alert()  显示带有一段消息和一个确认按钮的警告框
            confirm()  显示带有一段消息以及确认按钮和取消按钮的对话框
            prompt()  显示可提示用户输入的对话框

        计时器:
            setTimeout(()=>{}, 1000)  延时器
            setInterval(()=>{}, 1000)  循环器
            
            clearTimeout()  取消延时器
            clearInterval()  取消循环器
        
        窗口:
            window.open(url[,opution(宽高)])  打开一个新的浏览器窗口
            window.close()  关闭浏览器窗口
            window.blur()  把键盘焦点从顶层窗口移开(保证新的窗口没有获得焦点)
            window.focus()  把键盘焦点给予一个窗口
            window.getSelection()	获取用户选择的文本范围或光标的当前位置
            window.moveBy(x, y)  可相对窗口的当前坐标把它移动指定的像素
            window.moveTo(x, y)  把窗口的左上角移动到一个指定的坐标
            window.resizeTo(x, y)	把窗口的大小调整到指定的宽度和高度
            window.resizeBy(x, y)	按照指定的像素调整窗口的大小
            
        btoa()	创建一个 base-64 编码的字符串
        atob()	解码一个 base-64 编码的字符串
        print()  打印当前窗口的内容
        stop()  停止页面载入
        getComputedStyle(event).width  获取指定元素的 CSS 样式
        matchMedia("(min-width: 700px)").matches  该方法用来检查media query语句
        postMessage()	安全地实现跨源通信??

    # 本地存储
        length  返回存储对象中包含多少条数据
        key(index)  返回存储对象中第 n 个键的名称

        localStorage:
            localStorage.setItem("key", "value");  添加键和值，如果对应的值存在，则更新该键对应的值
            localStorage.getItem("key");  返回指定键的值
            localStorage.removeItem("key");  移除键
            localStorage.clear()  清除存储对象中所有的键

        sessinStorage:
            sessinStorage.setItem("key", "value");  添加键和值，如果对应的值存在，则更新该键对应的值
            sessinStorage.getItem("key");  返回指定键的值
            sessinStorage.removeItem("key");  移除键
            sessinStorage.clear()  清除存储对象中所有的键

    ## 会话控制
        session(用户身份、用户信息)  // 以cookie形式发送给浏览器
        token(识别用户身份): 主要用于移动端app  npm i jwt  // 便于生成token
        # Cookie(标记用户、用户主题)
            按照域名(不同网页)划分保存
            默认情况下，cookie 在浏览器关闭时删除

            创建:
                document.cookie = "username = puff";
                您还可以为 cookie 添加一个过期时间（以 UTC 或 GMT 时间）
                document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT";
                您可以使用 path 参数告诉浏览器 cookie 的路径。默认情况下，cookie 属于当前页面。
                document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";

            读取:
                const myCookie = document.cookie

            修改:
                document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";  重新赋值

            删除:
                删除 cookie 非常简单。您只需要设置 expires 参数为以前的时间即可，如下所示，设置为 Thu, 01 Jan 1970 00:00:00 GMT:
                document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
                注意，当您删除时不必指定 cookie 的值。

            JavaScript Cookie 实例
                设置 cookie 值的函数
                获取 cookie 值的函数
                检测 cookie 值的函数

    ## 注册账号密码 → 数据库保存 → 用户登录 → 登录成功返回session/token → 验证session/token

    # window.location 对象包含有关当前 URL 的信息
        location.href  返回完整的URL/页面跳转  // http://127.0.0.1:5501/html-demo/HTML/index.html
        location.protocol  返回一个URL协议  // http:
        location.host  返回一个URL的主机名和端口  // 127.0.0.1:5501
        location.hostname  返回URL的主机名  // 127.0.0.1
        location.port  返回一个URL服务器使用的端口号  // 5501
        location.pathname  返回的URL路径名  // /html-demo/HTML/index.html
        location.search  返回一个URL的查询部分  // ?
        location.hash  返回一个URL的锚部分  // #
        location.origin  起源  // http://127.0.0.1:5501

        location.reload()  刷新当前页面
        location.assign(URL)  载入新文档
        location.replace(newURL)  用新文档取代当前文档

    # history 对象包含用户（在浏览器窗口中）访问过的URL
        length  返回历史列表中的网址数

        history.back()  回退
        history.forward()  前进
        history.go(number|URL)  指定步数

    # window.screen 对象包含有关客户端显示屏幕的信息
        screen.width  返回屏幕的总宽度
        screen.height  返回屏幕的总高度
        screen.availWidth  返回屏幕的宽度（不包括Windows任务栏）
        screen.availHeight  返回屏幕的高度（不包括Windows任务栏）

        screen.colorDepth  返回目标设备或缓冲器上的调色板的比特深度
        screen.pixelDepth  返回屏幕的颜色分辨率（每象素的位数）

    # window.navigator 对象包含有关访问者浏览器的信息
        <script>
            txt = "<p>浏览器代号: " + navigator.appCodeName + "</p>";
            txt+= "<p>浏览器名称: " + navigator.appName + "</p>";
            txt+= "<p>浏览器版本: " + navigator.appVersion + "</p>";
            txt+= "<p>启用Cookies: " + navigator.cookieEnabled + "</p>";
            txt+= "<p>硬件平台: " + navigator.platform + "</p>";
            txt+= "<p>用户代理: " + navigator.userAgent + "</p>";
            txt+= "<p>用户代理语言: " + navigator.language + "</p>";
            document.getElementById("example").innerHTML=txt;
        </script>
        警告:
            来自 navigator 对象的信息具有误导性，不应该被用于检测浏览器版本，这是因为：
                navigator 数据可被浏览器使用者更改
                一些浏览器对测试站点会识别错误
                浏览器无法报告晚于浏览器发布的新操作系统

## ES6
    # rest参数
        用来获取函数的实参
            let data = function(...rest){
                console.log(rest)([1, 2, 3])
            }
            data(1, 2, 3)

    # 类型
        Symblo类型
            let sym = Symblo();  //函数
            let sym = Symblo.for();  //函数对象
            独一无二
            不能运算
            不能for...in循环,但是可以使用reflect.ownKeys来获取对象的所有键名
            防止创建方法和对象本身的方法冲突
                const game = {}
                let sym = Symblo();
                game[sym] = functiom(){}
                game[sym]();
            
            Symbol.prototype.description  获取symblo字符串描述

    # set集合
        数组去重
        let s = new Set();

    # Map集合
        键的范围不限于字符串
        let m = new Map();
        let school = {name: '学校'}
        m.set(school, 'xxx')

    # import按需加载:
        import("./js/count")
        .then((res)=>{
            console.log('模块加载成功', res)
        })
        .catch((err)=>{
            console.log('模块加载失败', err)
        })

    #calss 类
        calss Promise{
            name;  //公有属性
            #age  //私有属性，只能出现在类的内部
            static resolve(){}  //<!-- 静态属性 -->  //属于类，不属于构造对象
            
            <!-- 构造函数 -->
            constructor(){
                this.xxx = xxx;
            };
            
            get name(){}  //属性被读取时触发、访问私有属性
            set name(){}  //属性被调用时触发
        }

        extends继承一个类
            class Pro extends Promise{
                constructor(xxx){
                    super(xxx)  调用父类的构造方法
                }
            }

## 模块化
    # CommonJS
        暴露模块
            module.exports = {value}
            exports.name = value
        
        引入模块
            require(xxx)
                第三方模块(模块名字)
                自定义模块(文件路径)

        打包
            npm i browserify
            browserify url -o url

    # ES6
        暴露模块
            分别暴露
                export function(){}
            
            默认暴露
                export default name = {}
                
            统一暴露
                export {}

        引入模块
            常规暴露
                import {name} from 'url'
            
            默认暴露
                import name from 'url'

            统一引入
                import * as API from 'url';

## Promise
    const p = new Promise((resolve, reject) => {xxx? resolve() : reject();})
        p.then((value) => {}, (reason) => {})

        // 只能做失败回调
        p.catch(() => {})

        异常穿透
            promise链式最后调用.catch()

        中断promise链
            返回一个peding状态的promise

    promise方法
        Promise.resolve()
            传入非promise对象，返回一个成功的promise对象
            传入promise对象，由参数结果决定resolve结果

        Promise.reject()
            返回一个失败的promise对象

        Promise.all()
            传入promise数组
            返回一个新的promise，只有所有的promise都成功才成功，只要有一个失败就直接失败

        Promise.allSettled()
            传入promise数组
            返回一个promise数组，值为每一个promise的状态和值

        Promise.race()
            传入promise数组
            返回一个新的promise，最先完成promise状态改变的结果

## RegExp正则
    https://www.runoob.com/jsref/jsref-obj-regexp.html
    const phone = /^1\d{10}$/

    let iphone = /^1[0-9]{10}$/
    let password = /^[a-z][a-z0-9]{5}$/
        ^ 开始标记
        $ 结束标记

## Date日期
    get/set/getUTC/setUTC
    getTime()	返回 1970 年 1 月 1 日至今的毫秒数。
    getFullYear()   返回年份
    getMonth()      返回月份(0-11)
    getDate()       返回当日
    getHours()      返回小时
    getMinutes()    返回分钟
    getSeconds()	返回秒数
    getMilliseconds()   返回毫秒

    parse()	返回1970年1月1日午夜到指定日期（字符串）的毫秒数。
    getDay()        一周中的某一天
    UTC()	根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。
    getUTCDay()	根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。

    toJSON()	以 JSON 数据格式返回日期字符串。
    toISOString()	使用 ISO 标准返回字符串的日期格式。
    toDateString()	把 Date 对象的日期部分转换为字符串。
    toLocaleString()	根据本地时间格式，把 Date 对象转换为字符串。2023/5/31 14:11:53
    toLocaleDateString()	根据本地时间格式，把 Date 对象的日期部分转换为字符串。2023/5/31
    toLocaleTimeString()	根据本地时间格式，把 Date 对象的时间部分转换为字符串。14:12:12
    
    toString()	转换为字符串。Wed May 31 2023 14:12:31 GMT+0800 (中国标准时间)
    toTimeString()	把 Date 对象的时间部分转换为字符串。14:12:57 GMT+0800 (中国标准时间)
    toUTCString()	根据世界时，把 Date 对象转换为字符串。

## TypeScript
    npm i -g typescript

    类型断言
        变量 as 类型
        <类型>变量

    类型
        number
        string
        boolean
        boject  //{}、let b :{name: string, [name: string]: any}
        function  //(形参：类型, ...) => 返回值类型
        array  //数值类型[]、Array<类型>
        any  //任意类型
        unknown  //安全的任意类型
        void  //函数空值
        never  //函数没有值
        tuple  //[类型, 类型],固定长度数组
        enum  //枚举  enum 属性{属性名, 属性名}
        类型别名  type 属性名 = 类型;

    编译 tsc -w
        tsconfig.json
            {
                <!-- 编译指定文件 -->
                "include": [
                    "./src/**任意目录/*任意文件"
                ],
                <!-- 指定不编译文件 -->
                "exclude": [
                    "./src/**任意目录/*任意文件"
                ],
                <!-- 继承指定配置文件 -->
                "extends": "url",
                <!-- 指定编译文件列表 -->
                "files": [
                    "文件名",
                    "文件名"
                ],
                <!-- 编译器选项 -->
                complierOptions: {
                    "target": "ES3",  //指定编译版本
                    "mudule": "es6",  //指定模块化规范，conmmonjs
                    "lib": [],  //指定项目中要使用的库 
                    "outDir": "url",  //指定编译后的文件路径目录
                    "outFile": "url",  //将代码合成为一个文件
                    "allowJs": false,  //是否编译js文件
                    "checkJs": false,  //是否检查js代码
                    "removeComments": false,  //是否移除注释
                    "noEmit": false,  //是否不生成编译文件
                    "noEmitOnError": false,  //产生错误时是否编译文件
                    "alwaysStrict": false,  //是否开启严格模式
                    "noImplicitAny": false,  //是否不允许隐式的any
                    "noImplicitThis": flase,  //是否不允许不明确类型的this
                    "strictNullChecks": false,  //是否严格的检查空值
                    "strict": false,  //所有严格检查总开关
                }
            }
            
    面向对象
        类
            public  //公用属性（默认）
            private  //私有属性
            protected  //包含属性，当前类和子类中访问
            readonly name;  //只读属性

        抽象类
            abstract class Promise  //抽象类，不能用来被创建实例
            abstract demo();  //抽象方法，没有方法体，子类必须重写

        接口
            interface myInter{}  // 定义类的结构(相当抽象类)

            class myClass implements myInter{} //实现接口

    泛型
        定义泛型
            function fn<T>(a: T): T{

            }
            fn<number>(10);  //指定泛型类型