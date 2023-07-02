## JavaScript 原理
    运行原理：编译一行，执行一行。
        编译    声明变量
        执行   赋值
        赋值变量LHS查询
        引用变量RHS查询

    作用域：能够储存变量中的值，并且能对其进行访问或修改的区域。

    异常处理：
        ReferenceReeor: 作用域相关
        TypeError: 操作非法或不合理

    with()/eval()：
        把字符串当作js代码执行（非"use strict"；模式下）
        注意️：影响性能，引擎无法在编译时对其作用域查找进行优化。

## javaScript API
    "use strict";  严格模式
    debugger;  断点、调试代码

    # 数据类型
    值类型可以用typeof，引用类型用instanceof。
        typeof xxx  检测类型
        instanceof  //判断一个属性是否存在一个对象身上
            value instanceof Promise

    # Array数组
        array.unshift()	向数组的开头添加一个或更多元素，并返回新的长度。
        array.shift()	删除并返回数组的第一个元素。
        array.push()	向数组的末尾添加一个或更多元素，并返回新的长度。
        array.pop()	删除数组的最后一个元素并返回删除的元素。
        array.reverse()	反转数组的元素顺序。
        array.fill('', start, end)  使用一个值来替换数组
        array.slice(start, end)	选取数组的一部分，并返回一个新数组
        array.splice(index, num, newItem)	删除并返回删除元素后添加新元素
        array.join()	把数组的所有元素中间放入一个字符串。生成新数组
        array.indexOf()	搜索数组中的元素，并返回它所在的位置。
        array.includes()	判断一个数组是否包含一个指定的值。
        Array.isArray()   判断是否为数组
        array.concat(newArr)  连接两个数组/字符串，并返回结果。

        array.forEach((item) => {})  遍历数组(改变原数组)
        array.map((item) => {})  遍历数组(不改变原数组)
        array.filter((item) => {})  过滤器,返回所匹配的值，生成新的数组
        array.every((item) => {})  遍历数组是否符合条件，全符合为true,否则false
        array.some((item) => {})  遍历数组是否含有符合条件，只要有一项满足条件，就会返回true
        array.find((item) => {})  //返回第一个所匹配的值
        array.findIndex(item => {})  //返回所匹配元素的下标
        array.sort(item => {})	对数组的元素进行排序。默认升序
    
        Array.from(arr, callback)	通过给定的对象中创建一个数组(必须要有length属性)
        array.flat(2)  将多维数组转换成低维数组，参数为深度
        array.flatMap(item => {})	将多维数组降维并遍历数组

        array.lastIndexOf()	从后面搜索数组中的元素，并返回它第一次出现的位置。
        array.reduce((total, value, index, arr)=>{}, v)	累加器（从左到右）
        array.copyWithin(index, start, end)  拷贝到指定位置，开始拷贝元素的位置	
        array.of('item')	将一组值转换为数组。
        array.at(index)	返回索引值的值(可以是负数)
        array.keys()	返回数组的可迭代对象，包含原始数组的键(key)。
        array.entries()	返回数组的可遍历对象num.next().value

    # Number
        Number()  将字符串转换为数字
        Number.EPSILON  js表示的最小精度
        Number.isFinite()  判断是否为有限数
        Number.isNaN()  判断是否为非数
        Number.isInteger()  判断是否为整数
        Number.isSafeInteger  检测指定参数是否为安全整数。
        Number.parseInt()  字符串转整数
        Number.toFixed(num)  保留几位小数
        
    # Math
        Math.abs(num)  返回绝对值
        Math.ceil()  对数进行上舍入
        Math.floor()  对数进行下舍入
        Math.round()  四舍五入
        Math.max(arr)  返回最高值
        Math.min(arr)  返回最低值
        Math.pow(x, y)  返回x的y次幂
        Math.random()  1~0之间的随机数
        Math.trunc()  去掉小数部分
        Math.sign()  判断为正数 负数 还是零
        Math.sqrt(num)	返回数的平方根。
    
    # String 对象
        属性
        length  字符串的长度
        constructor	 返回创建字符串属性的构造函数
        prototype  允许您向对象添加属性和方法

        方法
        valueOf()	返回字符串原始值
        toString()	返回一个字符串
        trim()	去除首尾空白,trimStart()|trimEnd()
        charAt(index)	返回在指定索引的字符
        toLowerCase()	把字符串转换为小写
        toUpperCase()	把字符串转换为大写
        search('')  查找相匹配的值,如果没有找到匹配的字符串则返回 -1。

        match(reg)	正则表达式的匹配,返回匹配值
        matchAll(reg)  批量匹配
        substr(index, num)	从索引提取字符串中指定数目的字符
        substring(index, index)	提取字符串中两个指定的索引号之间的字符。
        repeat(num)  复制字符串指定次数，并将它们连接在一起返回
        replace('newStr', 'oldStr')  匹配字符串并替换(单个)
        replaceAll('newStr', 'oldStr')	匹配字符串并替换(所有)
        
        startsWith()  查看字符串是否以指定的字符串开头。
        endsWith('')  判断当前字符串是否是以指定的子字符串结尾的

        charCodeAt()	返回在指定的位置的字符的 Unicode 编码。
        fromCharCode()	将 Unicode 编码转为字符。

    # Date对象
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

    # 对象扩展
        Object.is(a, b)    判断两个值是否相等
        Object.assign(obj1, obj2)  覆盖对象
        Object.setPrototypeOf(obj1, obj2)  给对象添加原型对象
        Object.getPrototypeOf(obj1)   读取对象
        
        Object.entries(obj)  返回对象可遍历属性[key, value]的数组
        Object.getOwnPropertyDescriptors(obj)  获取对象属性的描述对象

        Object.fromEntries()  将二维数组转换成对象
        Object.entries()      将对象转换成二维数组

    # 函数
        # this指向
            myFun.call(obj, 'xx', 'xx')
            myFun.apply(obj, ['xx', 'xx'])
            myFun.bind(obj, 'xx', 'xx')()  //有返回值且是个函数

    # 全局
        eval()  计算字符串，并作为脚本代码执行
        parseInt()  解析字符串并返回整数
        parseFloat()  解析字符串并返回浮点数

    # 条件语句
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

    #定时器
        执行一次
            const in = setTimeout(() => {}，1000)

        循环执行
            setInterval(() => {}, 1000)

        关闭定时器/重启
            clearInterval(xxx);
            clearTimeout(xxx);

            in = setTimeout(() => {}，1000)

## 事件
    event.target  触发事件的元素
    data-xx='xx' 自定义属性
    event.target.dataset  读取自定义属性

    event.offsetX  鼠标相对于事件源元素（srcElement）的X,Y坐标
    event.offsetY

    # 鼠标事件
        <!-- 
            nouse  鼠标
            enter  进入
            leave  离开
         -->

        click  鼠标单击
        dblclick  双击
        contextmenu  点击鼠标右键
        mousedown  鼠标按钮被按下
        mouseup  鼠标按键被松开

        mouseenter  当鼠标指针移动到元素上时触发。  不支持冒泡
        mouseleave  当鼠标指针移出元素时触发

        mouseover  鼠标移到某元素之上。  冒泡
        mouseout  鼠标从某元素移开。

        mousemove  鼠标被移动。
        
    # 键盘事件
        onkeydown  按下键盘按键
        onkeyup    松开按键
        onkeypress 按下并松开

    # 表单事件
        blur       失去焦点时
        change     内容发生改变时
        focus      获取焦点时
        focusin    即将获取焦点时
        focusout   即将失去焦点时
        input      获取用户输入时
        reset      表单重置时
        select     选取文本时
        submit     提交表单时

    #事件传播
        event.stopPropagation();  //阻止事件传播
        event.preventDefault()  取消默认行为

## Dom Document对象
     <!-- 
        document  文档
        element  元素
        attribute  属性
        text  文本
        comment  注释
        node  节点
        child  子

        create  创建
        insert  插入
        replace  替换
        remove  删除

        before  在...之前
     -->

    # 获取元素
    document对象
        document.getElementById();  //返回指定 ID 的元素
        document.getElementsByClassName()	返回文档中所有指定类名的元素集合
        document.getElementsByName();  //返回带有指定名称的对象的集合（name：xxx）
        document.getElementsByTagName()	返回指定标签名的所有子元素集合。
        document.querySelector()	返回匹配指定 CSS 选择器元素的第一个子元素
        document.querySelectorAll()	返回匹配指定 CSS 选择器元素的所有子元素节点列表

        document.open()	打开一个流，以收集来自任何.write() 或.writeln() 方法的输出。
        document.write()	向文档写 HTML 表达式 或 JavaScript 代码。
        document.writeln()	等同于 write() 方法，不同的是在每个表达式之后写一个换行符。

        基本属性/方法
        document.documentElement	返回文档的根节点
        document.body	返回文档的body元素
        document.title	返回当前文档的标题。
        document.cookie	设置或返回与当前文档有关的所有 cookie。
        document.URL	返回文档完整的URL
        document.baseURI	返回文档的绝对基础 URI
        document.domain	返回当前文档的域名。
        document.readyState	返回文档状态 (载入中……)
        document.referrer	返回载入当前文档的文档URL
        document.activeElement	返回当前获取焦点元素
        document.documentMode	返回用于通过浏览器渲染文档的模式
        document.documentURI	设置或返回文档的位置
        document.inputEncoding	返回用于文档的编码方式（在解析时）
        document.lastModified	返回文档被最后修改的日期和时间。
        document.forms	返回对文档中所有 Form 对象引用
        document.images	返回对文档中所有 Image 对象引用
        document.scripts	返回页面中所有脚本的集合。
        document.strictErrorChecking	设置或返回是否强制进行错误检查。

        创建
        document.createElement()	创建元素节点。
        document.createAttribute()	创建一个属性节点
        document.createTextNode()	创建文本节点。
        document.createComment()	方法可创建注释节点。
        document.createDocumentFragment()	创建空的文档片段对象，并返回此对象。
        document.normalize()	删除空文本节点，并连接相邻节点
    
    element属性/方法
        添加/移除事件
        element.addEventListener('', ()=>{}, true/false捕获or冒泡)	向指定元素添加事件句柄
        element.removeEventListener()	移除由 addEventListener() 方法添加的事件句柄

        元素操作
        element.firstElementChild	返回元素的第一个子元素
        element.lastElementChild	返回元素的最后一个子元素
        element.previousElementSibling	元素的前一个兄弟元素
        element.nextElementSibling	返回元素下一个兄弟元素
        element.children	返回元素的子元素的集合

        element.appendChild(node)	为元素添加一个新的子元素0
        element.insertBefore(newNode, oldnode)	元素的子元素之前插入一个新的子元素
        element.removeChild(node)	删除一个子元素
        element.replaceChild(newNode, oldnode)	替换一个子元素

        .insertAdjacentHTML('position', html)
        .insertAdjacentElement('position', node)
        .insertAdjacentText('position',text)
            afterbegin插入到元素第一个子节点之前
            beforeend元素最后一个子节点之后
            beforbegin插入自身元素前面
            afterend元素自身的后面

        节点操作
        element.parentNode	返回元素的父节点
        element.firstChild	返回元素的第一个子节点
        element.lastChild	返回元素的最后一个子节点
        element.previousSibling	返回元素上一个节点
        element.nextSibling	返回该元素的下一个节点
        element.childNodes	返回元素的所有子节点

        element.getAttributeNode(attribute)	返回指定属性节点
        element.setAttributeNode(attributeNode)	设置或者改变指定属性节点。
        element.removeAttributeNode(attributeNode)	删除指定属性节点并返回移除后的节点。
        
        属性操作
        element.getAttribute(attr)	返回指定元素的属性值
        element.setAttribute('name', 'value')	设置或者改变指定属性并指定值。
        element.removeAttribute(attr)	从元素中删除指定的属性
        element.attributes	返回一个元素的属性数组
    
        判断boolean
        element.hasAttribute('attr')	如果元素中存在指定的属性返回 true，否则返回false
        element.hasAttributes()	 如果元素有任何属性返回true，否则返回false
        element.hasChildNodes()	返回一个元素是否具有任何子元素
        element.hasFocus()	返回布尔值，检测文档或元素是否获取焦点

        element.isContentEditable	如果元素内容可编辑返回 true，否则返回false
        element.isEqualNode(element)	检查两个元素是否相等
        element.isSameNode(element)	检查两个元素所有有相同节点。

        基本属性/方法
        element.id	设置或者返回元素的 id。
        element.style	设置或返回元素的样式属性
        element.className	设置或返回元素的class属性
        element.classList	返回元素的类名，作为 DOMTokenList 对象。
        element.title	设置或返回元素的title属性
        element.innerHTML	设置或者返回元素的内容。
        element.toString()	一个元素转换成字符串
        element.focus()	设置文档或元素获取焦点
        element.tagName	作为一个字符串返回某个元素的标记名（大写）
        element.textContent	设置或返回一个节点和它的文本内容
        element.tabIndex	设置或返回元素的标签顺序。
        element.lang	设置或者返回一个元素的语言。
        element.nodeName	返回元素的标记名（大写）
        element.nodeType	返回元素的节点类型
        element.nodeValue	返回元素的节点值
        element.cloneNode()	克隆某个元素

    # 获取滚动条高度
        <!-- 
            scroll  滚动
         -->
        const height = document.documentElement.scrollTop || document.body.scrollTop

        
        element.offsetWidth	 返回元素的宽度，包括边框border
        element.offsetHeight  返回任何元素的高度包括边框border
        element.offsetParent	返回元素的偏移父元素
        element.offsetLeft	返回当前元素的相对水平偏移位置的偏移容器
        element.offsetTop	返回当前元素的相对垂直偏移位置的偏移容器
        element.clientWidth	在页面上返回内容的可视宽度
        element.clientHeight	在页面上返回内容的可视高度
        element.clientLeft	表示一个元素的左border的宽度，以像素表示。
        element.clientTop	表示一个元素的顶部border的宽度，以像素表示。
        element.scrollWidth	返回元素的整个宽度（包括带滚动条的隐蔽的地方
        element.scrollHeight	返回整个元素的高度（包括带滚动条的隐蔽的地方）
        element.scrollLeft	返回元素的左边缘和视图左边缘之间的距离
        element.scrollTop	返回元素的顶部边缘和视图顶部边缘之间的距离
        
            offset  包含边框
            client  不含边框(不含滚动条)
            scroll  不含边框(包含滚动条)

## 属性对象
    attr.isId	如果属性是 ID 类型，则 isId 属性返回 true，否则返回 false。
    attr.name	返回属性名称
    attr.value	设置或者返回属性值
    attr.specified	如果属性被指定返回 true ，否则返回 false
        
    nodemap.getNamedItem()	从节点列表中返回的指定属性节点。
    nodemap.item()	返回节点列表中处于指定索引号的节点。
    nodemap.length	返回节点列表的节点数目。
    nodemap.removeNamedItem()	删除指定属性节点
    nodemap.setNamedItem()	设置指定属性节点(通过名称)

## BOM
    # window
        window.alert()	显示带有一段消息和一个确认按钮的警告框。
        window.confirm()	显示带有一段消息以及确认按钮和取消按钮的对话框。
        window.prompt()	显示可提示用户输入的对话框。

        window.getSelection()	返回一个 Selection 对象，表示用户选择的文本范围或光标的当前位置
        window.getComputedStyle()	获取指定元素的 CSS 样式。

        window.innerHeight  返回窗口的文档显示区的高度。
        window.innerWidth	 返回窗口的文档显示区的宽度。
        window.scrollTo(x, y)	把内容滚动到指定的坐标(绝对位置)
        window.scrollBy(x, y)	按照指定的像素来滚动内容。(相对位置)

            登录/注册流程            服务器                  数据库
                用户申请----    向数据库发请求----     生成唯一id标识并返回

        本地存储/会话存储
            本地存储： 持久化
                window.localStorage.setItem('key', 'value');  //添加本地存储
                window.localStorage.getItem(key);  //读取数据：
                window.localStorage.removeItem('id')  //删除本地储存
                window.localStorage.clear();  //删除所有数据
            会话存储： 并非持久化
                sessionStorage
            会话控制
                session
                token
                Cookie
                    document.cookie  返回所有cookie
                    document.cookie="username=John Doe";  创建
                    document.cookie="username=";  删除
                    expires=Thu, 18 Dec 2043 12:00:00 GMT;  添加过期时间

    # location
        window.location.hash	返回一个URL的锚部分
        window.location.host	返回一个URL的主机名和端口
        window.location.hostname	返回URL的主机名
        window.location.href	返回完整的URL/页面跳转
        window.location.pathname	返回的URL路径名。
        window.location.port	返回一个URL服务器使用的端口号
        window.location.protocol	返回一个URL协议
        window.location.search	返回一个URL的查询部分
        window.location.reload()  //刷新页面

    # history历史记录
        window.history.back()  回退
        window.history.forward()  前进
        window.history.go()  指定步数

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
. 
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
            统一暴露
                export {}
            默认暴露
                export default name = {}

        引入模块
            常规暴露
                import {name} from 'url'
            
            默认暴露
                import name from 'url'

            统一引入
                import * as API from 'url';

## Promise
    const p = new Promise((resolve, reject) => {xxx? resolve() : reject();})
        p.then((value) => {},(reason) => {})

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

## RegExp
    https://www.runoob.com/jsref/jsref-obj-regexp.html
    const phone = /^1\d{10}$/


    let iphone = /^1[0-9]{10}$/
    let password = /^[a-z][a-z0-9]{5}$/
    ^ 开始标记
    $ 结束标记

## jQuery
    JS函数库，封装简化DOM操作
    https://www.runoob.com/jquery/jquery-tutorial.html
    npm i jquery

    $('选择器').操作()
        选择器
            p
            #id
            .class

    事件
        $('p'),click(function(){})

    显示隐藏
        $('').hide(1000, callback);
        $('').show(1000, callback);
        $('').toggle(1000, callback);  //切换显示与隐藏

    淡入淡出
        $('').fadeIn(1000, callback);  //淡入
        $('').fadeOut(1000, callback);  //淡出
        $('').fadeToggle(1000, callback);  //切换淡入淡出
        $('').fadeTo(1000, opacity, callback);  //渐变至透明度(slow、fast、10000, 0.5, callback)

    滑动
        $('').slideDown(1000, callback);  //向下滑动
        $('').slideUp(1000, callback);  //向上滑动
        $('').slideToggle(1000, callback);  //切换

    动画
        $('').animate({}, 1000, callback);  {变换的css属性}
        $('').stop();  //停止动画

    jquery链式调用
        $('p').slideDown().slideUp

    捕获元素
        $('').html(callback(a, b));  //设置或返回元素的内容及标签 a:当前元素下标，b:旧的元素文本内容
        $('').text(callback(a, b));  //设置或返回元素的文本内容
        $('').val(callback(a, b));  //设置或返回元素的表单值

    修改属性值
        $('').attr('属性名', newValue/callback(a, b));

    添加元素
        $('').append('text');  //在元素结尾追加内容
        $('').prepend('text');  //在元素开头追加内容
        $('').after()  //在元素之后插入内容
        $('').before()  //在元素之前插入内容

    删除元素
        $('').remove();  //删除被选元素
        $('').empty();  //删除被选元素的子元素

    操作CSS
        $('.off').addClass('active')  //添加类名
        $('.on').removeClass('active')  //删除类名
        $('.on').toggleClass('active')  //切换添加删除类名
        $('').css()  //设置或返回css属性

    尺寸
        https://www.runoob.com/jquery/jquery-dimensions.html

    遍历
        $('').parent()  返回元素的父元素
        $('').children()  返回元素的所有直接子元素
        $('').find('span')  返回元素的所有后代子元素
        $('').siblings()  返回元素的所有兄弟元素
        $('').next()  返回元素的下一个兄弟元素
        $('').nextAll()  元素的后的所有兄弟元素
        $('').first()  选中元素的第一个元素
        $('').last()  选中元素的最后一个元素
        $('').eq(0)  选中元素的指定索引号元素
        $('').fiter('xxx')  过滤不匹配的元素
        $('').not  与fiter互逆

    $(this).prop('src', '../xxx');  //调用该对象的内置属性
    $(this).trim();  //用于去除字符串两端的空白字符

    const data = $('form').serialize()   // 采集用户信息
    const data = $('form').serializeArray();  //获取表单所有键值对

    #ajax
        $.get( url [, data ] [, callback ] [, dataType ] )
        $.post(url [, data ] [, callback ] [, dataType ] )

## Angular JS
    JS结构化框架

    Angular state inspector 扩展程序

    引入
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>

    const app = angular.module('myApp', []);  //创建angularjs模块

    指令
        ng-app  //绑定容器($rootScope)

        ng-controller="myCtrl"  //添加控制器,并在控制器中定义属性和方法
            app.controller('myCtrl', ['$scope', function($scope){
                $scope.carname = "";
                $scope.seyHello = function(){
                    console.log('hello-angularJS');
                }
            }])

        ng-model=""  //双向绑定数据

        ng-init="name='' "  //初始化当前作用域变量

        ng-repeat="i in arr";  {{i}}  //循环遍历数组生成元素节点(类似v-for)
            $index  //索引
            {{$first}}  //开头为true，后面为false
            {{$last}}  //结尾为true，其余为false
            {{$middle}}  //中间为true,头尾为false
            {{$odd}}  //奇数true，偶数false
            {{$even}}  //偶数true，奇数false

        ng-bind="xxx"  //解决使用{{}}显示数据闪屏问题

        ng-show=""  //显示与隐藏
        ng-hide=""

        事件
            ng-click
            ng-mouseenter  //鼠标移入
            ng-mouseleave  //鼠标移出

        ng-class  //动态引用定义样式{.class: true}
        ng-style  //动态引入通过js指定的样式对象{color: 'red'}

    {{}}  //插值语法
    {{username | uppercase}}  //过滤器currency格式化数字为货币格式。filter	从数组项中选择一个子集。lowercase	格式化字符串为小写。orderBy	根据某个表达式排列数组。uppercase	格式化字符串为大写。

    自定义指令
        const app = angular.module('myApp', []);
        app.directive('myBind', function(){
            return {
                template: "<div>自定义指令myBind</div>";
            }
        })
        <my-bind></my-bind>
        <div my-bind></div>

    发送请求
        传入$http
        $http({
            method: 'get',
            url: ''
        }).then()
        $http.get('url').then(()=>{})

    定时器
        $timeout
        $timeout(()=>{}, 1000)
        $interval  //循环定时器
        $interval(()=>{}, 1000)

    

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