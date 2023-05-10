## javaScript
    alert() 警告框
    confirm();  确认框
    prompt();  提示框

    "use strict";  严格模式
    debugger;  断点、调试代码

    # 数据类型
        typeof xxx  检测类型
        基本类型
            u  undefined
            s  string symbol
            o  object
            n  null number
            b  boolean

        引用类型
            Object
            Array
            Function
            RegExp   正则
            Date     日期
    # 数组
        .unshift()  向数组开头添加元素，并返回新的数组长度
        .shift()  删除数组的第一个元素,并返回被删除的元素
        .push()  向数组末尾添加一个元素，并返回新的数组长度
        .pop()  删除最后一个元素,并返回被删除的元素
        .reverse()  反转数组顺序
        .sort((item) => {})  数组排序
        .slice(start, end)  选取数组的一部分，并返回新数组
        .splice(1, 1, '')  添加或删除元素,并返回被删除的元素

        .concat(arr2);  连接两个数组
        .fill('', 0, 2)  填充数组
        .join()  把数组每个元素放入一个字符串

        .forEach((item) => {})  //遍历数组里的每个元素并执行一遍回调  //修改原数组
        .map((item) => {})  通过指定函数处理每个元素，并返回处理后的数组  //不修改原数组，返回新数组
        .every((item) => {})  遍历每一个数组是否符合条件，全符合为true,否则false
        .filter((item) => { arr2.has(item)})  //过滤器   .has//筛选所匹配的值
        .some((item) => {})  检测数组元素中是否含有符合指定条件，只要有一项满足条件，就会返回true

        .find((item) => {})  //返回第一个所匹配的值
        .findIndex(item => )  //返回所匹配元素的下标
        
        .isArray()   判断是否为数组
        
        .entries();  返回数组可迭代对象
        .from()  通过给定对象中创建一个数组(数组为对象中属性值集合)
        .flat(2)  将多维数组转换成低维数组，参数为深度

        Number()           将字符串转换为数字
        Number.EPSILON     js表示的最小精度
        Number.isFinite()  判断是否为有限数
        Number.isNaN()     判断是否为非数
        Number.isInteger() 判断是否为整数
        Number.parseInt()  字符串转整数
        
        # Math
            .abs()  返回绝对值
            .ceil()  对数进行上舍入
            .floor()  对数进行下舍入
            .round()  四舍五入
            .max()  返回最高值
            .min()  返回最低值
            .pow(x, y)  返回x的y次幂
            .random()  1~0之间的随机数
            .trunc()       去掉小数部分
            .sign()        判断为正数 负数 还是零
    
    # 字符串
        属性
            constructor  返回创建字符串属性的构造函数
            .prototype  向对象添加属性方法

        方法
            .trim()  去除首尾空白
            .toString()  返回字符串对象值

            .indexOf()  返回指定的字符串值首次出现的位置。如果没有找到匹配的字符串则返回 -1。
            .charAt(index)  返回指定索引位置的字符
            .concat(string)  连接字符串并返回
            .includes('')  判断字符串是否包含某个值
            .lastlndexOf('')  返回指定字符最后一次出现的索引值

            .toLowerCase()   转小写
            .toUpperCase()   转大写

            valueOf()       返回某个字符串对象的原始值
            
            trimStart()     去除左侧
            trimEnd()       去除右侧
            split()         字符串转化  p.split(':')[2] 以：分割，取索引为2的值

            matchAll()      数据批量提取

    # 对象扩展
        Object.is(a, b)    判断两个值是否相等
        Object.assign(obj1, obj2)  覆盖对象
        Object.setPrototypeOf(obj1, obj2)  给对象添加原型对象
        Object.getPrototypeOf(obj1)   读取对象
        
        Object.entries(obj)  返回对象可遍历属性[key, value]的数组
        Object.getOwnPropertyDescriptors(obj)  获取对象属性的描述对象

        Object.fromEntries()  将二维数组转换成对象
        Object.entries()      将对象转换成二维数组

    # 日期
        milliseconde  时间戳
        https://www.runoob.com/jsref/jsref-obj-date.html  日期文档

    # 正则表达式
        https://www.runoob.com/jsref/jsref-obj-regexp.html

    # 函数
        # this指向
            myFun.call(obj, 'xx', 'xx')
            myFun.apply(obj, ['xx', 'xx'])
            myFun.bind(obj, 'xx', 'xx')()  //有返回值且是个函数

    # 全局
        eval()  计算字符串，并作为脚本代码执行
        parseInt()  解析字符串并返回整数
        parseFloat()  解析字符串并返回浮点数

    #判断
        值类型可以用typeof，引用类型用instanceof。

        不同的结果执行不同的代码
            switch(){
                case 1: xxx;
                case 2: sss;
                default: ccc;
            }
        instanceof  //判断一个属性是否存在一个对象身上
            value instanceof Promise

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

    # Cookie
        document.cookie  返回所有cookie
        document.cookie="username=John Doe";  创建
        document.cookie="username=";  删除
        expires=Thu, 18 Dec 2043 12:00:00 GMT;  添加过期时间

## 事件
    event.target  触发事件的元素

    # 鼠标事件
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
        search     搜索框输入文本时
        select     选取文本时
        submit     提交表单时

    #事件传播
        event.stopPropagation();  //阻止事件传播
        event.preventDefault()  取消默认行为

    # 鼠标位置
        event.offsetX/offsetY
        event.clientX  跟screenX相比就是将参照点改成了浏览器内容区域的左上角，该参照点不会随之滚动条的移动而移动。
              clientY
              screenX  鼠标位置相对于用户屏幕水平偏移量，而screenY就是垂直方向的，此时的参照点也就是原点是屏幕的左上角。
              screenY
              pageX： 参照点也是浏览器内容区域的左上角，但它会随着滚动条而变动

    # 绑定事件
        box.addEventListener('mouseout',function(){
            console.log("haha")
        }, true/false捕获or冒泡)

        removeEventListener()  移除事件

## Dom Document对象
    # 获取元素
        document.getElementsByClassName();  //获取所有指定类名的元素（[0]获取第一个元素）
        document.getElementById();  //返回指定 ID 的元素
        document.getElementsByName();  //返回带有指定名称的对象的集合（name：xxx）
        document.getElementsByTagName();  //返回带有指定标签名的对象的集合（[0]获取第一个元素）

        document.querySelector();  //返回文档中匹配指定CSS选择器的一个元素
        document.querySelectorAll()；  //返回所有的元素

        .parentNode();  某元素的父节点
        .childNodes();  某元素的子节点
        .attributes();  元素的属性节点
        .lastChild	    返回最后一个子节点

        .innerHTML();  //向标签放入文本或标签

        .insertBefore();  指定子节点前面插入新的子节点
        .insertAdjacentHTML(position,text)  //beforbegin插入自身元素前面、afterbegin插入到元素第一个子节点之前、beforeend元素最后一个子节点之后、afterend元素自身的后面

        .appendChild();  //创建新的子节点到尾部
        .removeChild();  删除子节点
        .replaceChild();  替换子节点
        .createAttribute();  创建属性节点
        .createElement();  创建元素节点
        .createTextNode();  创建文本节点

        .setAttribute('name', 'value');  //给标签设置属性
        .getAttribute();  返回指定的属性值
        .className='value';  //给标签设置class属性
        .children	返回元素的子元素的集合

        element.firstElementChild	返回元素的第一个子元素
        element.focus()	获取焦点
        element.hasAttribute()	如果元素中存在指定的属性返回 true，否则返回false。
        element.previousSibling	返回某个元素紧接之前元素
        element.nextSibling	返回指定元素之后的下一个兄弟元素
        element.tagName	作为一个字符串返回某个元素的标记名（大写）
        element.textContent	设置或返回一个节点和它的文本内容
        element.title	设置或返回元素的title属性

    # 获取滚动条高度
        const height = document.documentElement.scrollTop || document.body.scrollTop

        onscroll  滚动条事件
        window.scrollTo({
            behavior: 'smooth'  //滚动方式,平滑、
        })  //滚动到哪

        element.scrollHeight	返回整个元素的高度（包括带滚动条的隐蔽的地方）
        element.scrollLeft	元素的左边缘和左边缘之间的距离
        element.scrollTop	实际元素的顶部边缘和顶部边缘之间的距离
        element.scrollWidth	返回元素的整个宽度（包括带滚动条的隐蔽的地方）

##  BOM
    # Window
        window.location.href = ''  //页面跳转
        window.location.reload()  //刷新页面

        <!-- 本地存储/会话存储 -->
            本地存储： 持久化
                window.localStorage.setItem('key', 'value');  //添加本地存储
                window.localStorage.getItem(key);  //读取数据：
                window.localStorage.removeItem('id')  //删除本地储存
                window.localStorage.clear();  //删除所有数据
            会话存储： 并非持久化
                sessionStorage

        window.innerHeight - 浏览器窗口的内部高度(包括滚动条)document.body.clientHeight
        window.innerWidth - 浏览器窗口的内部宽度(包括滚动条)document.body.clientWidth

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

    # 迭代器
        for of 循环原理

    # 生成器函数
        function* gen(){
            yield xxx;  //函数分割线
        }
        gen.next();

## 模块化
    # CommonJS
        暴露模块
            module.exports = {value}
            exports.xxx = value
        
        引入模块
            require(xxx)
                第三方模块(模块名字)
                自定义模块(文件路径)

        打包
            npm i browserify
            browserify url -o url

    # AMD
        暴露模块
            define(function(){
                return 模块
            })
            define(['module1', 'module2'], function(){
                return 模块
            })
        引入模块
            require(['module1', 'module2'], function(){
                使用m1/m2
            })

    # ES6
        暴露模块
            分别暴露
                export function(){}
            统一暴露
                export {}
            默认暴露
                export defaylt name = {}

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