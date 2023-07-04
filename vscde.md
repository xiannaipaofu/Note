运行脚本文件
        以管理员权限打开windows powershell，输入set-ExecutionPolicy RemoteSigned，选择y或者a即可。

## Auto Rename Tab
    自动闭合标签

## Chinese
    中文

## Live Server
    保存自动刷新浏览器

## Open in browser
    打开默认/指定浏览器

## Vetur
    vue格式化工具

## Vue 3 Snippets
    快速生成vue模板

## Vue language Features
    代码高亮

## ESLint
    js语法检测

## Prettier - Code formatter
    代码格式化

## Easy LESS
    less文件转css

## vue-helper
    ElementUI组件属性提示

## Vscode-element-helper
    ElementUI组件标签提示

## Codelf(变量命名神器)

## css-auto-prefix

## px to rem & rpx & vw (cssrem)
    屏幕适配

## 书写规范
    编写规范
        不要出现拼音命名
        开发过程中随时添加注释
        尽量按照 ESLint 格式要求编写代码

    普通变量命名规范
        命名方法 ：驼峰命名法且与内容相关
            let mySchool = "我的学校"
        class 类名
            命名方法 : 全部小写
            命名规范 : 使用小写字母和中划线来组合命名，中划线用以分割单词。 例如：
        ID
            命名方法 : 全部大写
            命名规范 : 使用大写字母和下划线来组合命名，下划线用以分割单词。 例如：
            <view id="MENU_ITEM"></view>
    组件命名
        文件夹的命名统一首字母大写 及驼峰命名规则
        文件名统一使用index.vue
        组件名应该始终是多个单词的
        有意义的名词、简短、具有可读性
        例: OrgSelectDialog
            UserMenu

    method 方法命名命名规范
        驼峰式命名，统一使用动词或者动词+名词形式
        请求数据方法，以 data 结尾
        methods: {
            jumpPage(){},
            openCarInfoDialog(){},
            getListData(){},
            postFormData(){}
        }
        尽量使用常用单词开头（set、get、go、can、has、is） 可以参考如下的动作：
        has: 判断是否含有某个值
        is: 判断是否为某个值
        get: 获取某个值
        set: 设置某个值
        update: 更新某个值
        fetch: ajax 请求（一般用在 vuex 里的 actions）
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

## 单词
    HTML
        标签
            textarea  文本域
            select  下拉框
            audio  音频
            video  视频

        属性
            placeholder  占位符
            autofoucus  焦点
            disabled  禁止
    
    CSS
        opacity  透明度
        cursor  光标
        vertical-align  垂直的对齐方式
        heddien  隐形的
        before  在...之前
        after  在...之后
        position  定位
        relative  相对
        absolute  绝对
        fiexd  固定
        sticky  粘性
        outline  轮廓
        repeat  重复
        transparent  透明的
        cover  覆盖
        indent  缩进
        decoration  装饰
        transform  使变形
        white  白色
        space  空地
        visited  拜访
        
        last  上一个
        first  下一个

