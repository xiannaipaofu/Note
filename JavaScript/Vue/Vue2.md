## 基本流程
    vue2/3:
        npm install @vue/cli -g  // 全局安装Vue脚手架
        vue create name  // 初始化项目
        npm run serve  // 运行
        npm run build  // 项目打包
            vue.config.js:
                productionSourceMap: false  // 项目打包处理MAP文件

    Vue.config.productionTip = false  // 关闭警告(vue3不需配置)
    vue.config.js:
        module.exports = defineConfig({lintOnSave:false})  // 关闭eslint语法校验功能

    Vue.js devtools 6.2.1  // Chrome安装扩展程序

## 数据代理原理
    原生js:
        Object.defineProperty(obj, 'name'){
            value: '杨超越',  // 设置初始值,默认值undefine
            enumerable: true,  // 控制属性是否可以枚举，默认值false
            writable: true,  // 控制属性是否可以修改，默认值false
            configurable: true,  // 控制属性是否可以被删除，默认值false
            get(){},  // 读取时触发
            set(value){}  // 修改时触发
        }

    给后添加的属性做响应式：
        import Vue from 'vue'
        Vue.set(this.student, 'key', 'value')

        this.$set(this.student, 'key', 'value')  // 添加一个响应式数据
        this.$delete(this.student, 'key', 'value')  // 删除一个响应式数据

    修改数组中的元素要用以下方法：
        1.使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
        2.Vue.set() 或 vm.$set()

        特别注意：Vue.set 和vm.$set()不能给vm或vm的根数据对象添加属性！！！

## 生命周期
    beforeCreate(){}  // 数据代理初始化前
    created(){}  // 数据代理初始化后(虚拟DOM未开始)
    beforeMount(){}  // 真实DOM挂载之前（虚拟DOM完成）
    mounted(){}  // 挂载完毕(虚拟DOM替换成真实DOM)
    beforeUpdate(){}  // 更新数据：更新之前（页面尚未和数据保持同步）  
    updated(){}  // 更新数据：更新之后（页面和数据保持同步）
    beforeDestroy(){}  // 实例销毁之前                                  
    destroyed(){}  // 销毁之后

    this.$nextTick(()=>{})  // 模板下一次更新后

## Vue组件间通信方式

### props(父←→子)
    <Home :name="name"></Home>
    props(['myCar'])
    props({myCar: String, data: String})
    props({
        myCar: {
            type: String, 
            required: true, 
            default: '奥迪'
        }
    })

    路由中的props
        方式：对象、布尔值、函数

### 自定义事件(子→父)
    <Father @msg="callback"/>  or  this.$on('msg', ()=>{})
    beforeDestroy(){
        this.$off('msg')
    }

    <Child>
        this.$emit('msg', data)
    </Child>

    *组件绑定原生DOM事件时，需要使用@click.native=""修饰符。
            
### $bus(全能)
    main.js:
        Vue.prototype.$bus = this;

    Child1.vue:
        this.$bus.$on('msg', ()=>{})
        beforeDestroy(){
            this.$bus.$off('msg')
        }

    Child2.vue:
        this.$bus.$emit('msg', data)

### pubsub-js
    场景：全能
        npm i pubsub-js
        import PubSub form 'pubsub-js';
        Vue.use(PubSub)

        PubSub.subscribe('msg', callback(msg, data))
        PubSub.publish('msg', data)

        PubSub.unsubscribe(pid)

### vuex(全能)

### 插槽(父子结构通信)
    默认插槽:
        父组件：
            <Child>
                <div>html结构、数据、样式</div>
            </Child>
        子组件：
            <slot>插槽默认内容</slot>  // 插槽展示位置

    具名插槽:
        父组件：
            <Child>
                <template v-slot:center>
                    <div>html结构</div>
                </template>
            </Child>

        子组件：
            <slot name="center">插槽默认内容</slot>

    作用域插槽:
        父组件：
            <Child>
                <template slot-scope="{game}">
                    {{game}}
                </template>
            </Child>

        子组件：
            <slot :game="games"></slot>  //回传数据

### v-model(场景:封装UI组件)
    <标签>:
        <input type="text" v-model="data">
        <input type="text" :value='date' @input='data=$event.target.value'>

    <组件>:
        <Father v-model='data'></Father>
        <Father :value='data' @input='data=$event'></Father>
    
        <Child>
            <input type='text' :value=value @input="@emit('input', $event.target.value)">
            props: ['value']
        </Child>

### .sync修饰符(与v-model相似)
    <Home :money='money' @update:money='money = $event'></Home>
    <Home :money.sync='money'></Home>

    <button @click="@emit('update', money - 100)">
    props: ['money']

    :money.sync="money"
        传递props: ['money']
        绑定自定义事件：@update:money='money = $event'

### this.$attrs(祖←→孙)/$listeners
    this.$attrs:
        <Father/>  <Child/>  <Son/>
        
        <Child v-bind="$attrs"/>  // 获取祖组件传递的props数据并传递给孙组件
    
    $listeners:
        获取父组件传递的自定义事件
        v-on="$listeners"

### $children/$parent
    $children
        获取当前组件中全部子组件  //当组件过多时[0]索引值并非按顺序排列

    $parent
        获取当前组件的父组件

### 混入mixin
        export default {}

        import myMixin from ''
        mixins: [myMixin]

## API
    Vue2:
        export default {
            name: 'app',
            components: {},
            props: ['data'],
            data(){return{}},
            methods:{},
            computed:{},
            watch:{}
        }

    ### this.$options
        vue的实例属性，是一个对象，获取vue组件的方法和数据。
        this.$options.data()这个是vue原始的数据，就是你页面刚加载时的data
        this.$data这个是现在阶段的vue数据，就是你改变data的数据

### ref(标签)
    

### props
    props:

### computed
    computed:{
        fnName(){}  // 函数,简写（只读）
        fnName:{  // 对象,(读写)
            get(){},
            set(value){}
            }
        }

### watch
    watch:{
        name(newValue, oldValue){}  // 简写
        name:{  // 完整写法
            deep:true,  // 深度监视
            immediate:false,  // 初始化时先调用一下
            handler(newValue, oldValue){}
        }
    }
    
### mixin(代码复用)


### composition API
    Vue.component()  // 注册全局组件
        import Home from ''
        Vue.component('Home', Home)

    Vue.

### 样式

    深度选择器
        原生CSS  >>> .class
        less  /deep/ .class
        scss  ::v-deep .class

    封装的过渡与动画
        元素进入的样式
        .v-enter：进入的起点  // Vue3: .v-enter-from
        .v-enter-active：进入过程
        .v-enter-to：进入的终点

        元素离开的样式
        .v-leave：离开的起点  // Vue3: .v-leave-from
        .v-leave-active：离开过程
        .v-leave-to：离开的终点

        2.使用<transition>包裹要过渡的元素，并配置name属性：
            <transition-group name="hello" appear>
                <h1 v-show="!isShow" key="1">你好啊！<h1>
                <h1 v-show="!isShow" key="2">你好啊！<h1>
            </transition-group>

        备注：若有多个元素需要过渡，则需要使用：<transition-group>,且每个元素都要指定key值

### Vue语令
    v-bind(单向):  
        v-bind:name="data"
            <input type='text' :name="data">  // 简写
            <Father v-bind='{name:'杨超越',age:18}'/>  // 对象形式
        
    v-model(文本框、单选、复选)
        文本框: 收集value
        单选: 收集value值，且要给标签配置value值
            <input type="radio" v-model="radio" value='足球'>
            <input type="radio" v-model="radio" value='篮球'>
        复选: 
            1.没有配置input的value属性，收集的是布尔值
            2.配置input的value属性：
                1.v-model的初始值是非数组，那么收集的是布尔值
                2.v-model的初始值是数组，那么收集的就是value组成的数组

        v-model的三个修饰符：
            .lazy  // 失去焦点再收集数据
            .number  // 输入字符串转为有效的数字
            .trim  // 输入首尾空格过滤

### 事件语令
    <Home @click.native></Home>  // 组件绑定原生事件，不加修饰符相当于自定义事件

    v-onclick="function()"  // 简写@click="",

    v-on 修饰符：
        @click.prevent=""  // 取消默认行为
        @click.noce=""  // 只触发一次
        .stop  // 阻止事件冒泡
        .capture  // 使用事件的捕获模式
        .self  // 只有event.target是当前操作的元素时才触发事件
        .passive  //事件的默认行为立即执行，无需等待事件回调执行完毕
        .native  // 自定义事件变成原生事件(组件使用时)  // vue3移除

### 键盘事件语令
    注意: vue3移除keyCode作为v-on的修饰符

    1.Vue中常用的按键别名：
        回车 => enter
        删除 => delete
        退出 => esc (捕获'删除'和'退格'键)
        空格 => space
        换行 => tab (特殊，需配合keydown使用)
        上 => up
        下 => dows
        左 => lefy
        右 => right
    2.Vue未提供别名按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）
    3.系统修饰键（用法特殊）：ctrl、alt、shift、meta（win键）
        （1）.配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
        （2）.配合keydown：正常触发事件
    Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名  // vue3不再支持

## vue.config.js
    配置代理服务器：
        devServer:{
            proxy:{
                '/api':{
                    target:'http://127.0.0.1:8080',
                    pathRewrite:{'^/api':''},  // 正则匹配重写路径
                    ws:true,  // 用于支持websocket
                    changeOrigin:true  // 用于控制请求头中的host值
                }
            }
        }

## Vue-Vuex
    ## 基本使用
        npm i vuex@3

        src/store/index.js
            import Vue from 'vue'
            import Vuex from 'vuex'
            Vue.use(Vuex)

            import Home from './Home'

            export default new Vuex.Store({
                modules: {
                    Home
                }
            })

        src/store/Home/index.js
            const actions = {}
            const mutations = {}
            const state = {}
            const getters = {}

            export default {
                namespaced: true,
                actions,
                mutations,
                state,
                getters
            }

        main.js:
            import store from './store'

            new Vue({
                el:'#app',
                render: h => h(App),
                store
            })

    ## API
        读取vuex中的数据：$store.state.sum
        修改vuex中的数据：$store.dispatch('函数',数据)或$store.commit('函数',数据)

        function(context){}:小仓库

        map方法的使用
            import {mapState,mapGetters,mapActions,mapMutations} from 'vuex'

            1.mapState方法：
                computed:{
                    ...mapState({he:'sum',xuexiao:'school',xueke:'subject'})
                    ...mapState(['sum','school','subject'])
                }

            2.mapGetters方法：
                computed:{
                    ...mapGetters({bigSum:'bigSum'})
                    ...mapGetters(['bigSum'])
                }

            3.mapActions方法：用于帮助我们生成与actions对话的方法，即包含：$store.dispatch(xxx)的函数
                methods:{
                    ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'}),
                    ...mapActions(['jiaOdd','jiaWait']),
                }

            4.mapMutations方法：用于帮助我们生成与mutations对话的方法，即包含：$store.commit(xxx)的函数
                methods:{
                    ...mapMutations({increment:'JIA',decrement:'JIAN'})
                    ...mapMutations(['JIA','JIAN'])
                }

    ##  开启命名空间后，组件中读取state数据：
            1.方法一：this.$store.state.Count.sum
            2.方法二：...mapState('Count',['sum','school','subject'])

        开启命名空间后，组件中读取getters数据：
            1.方法一：this.$store.getters['Person/fistPersonName']
            2.方法二：...mapGetters('Count',['bigSum'])

        开启命名空间后，组件中读取dipatch数据：
            1.方法一：this.$store.dispatch('Home/function', data)
            2.方法二： ...mapActions('Count',['jiaOdd','jiaWait']),

        开启命名空间后，组件中读取commit数据：
            1.方法一：this.$store.commit('Person/ADD_PERSON',personObj)
            2.方法二：...mapMutations('Count',['JIA','JIAN']),

## Vue-router

### 基本使用
    vue2:
        npm i vue-router@3  //安装
        src/router/index.js
            import Vue from 'vue';
            import VueRouter from 'vue-router';
            Vue.use(VueRouter)  // 应用
            import Home from '@/views/Home'
            const router = new VueRouter({mode: 'history/hash',routes:[{}]})
            export default router

        main.js
            import route from '@/router'
            new Vue({el:'#app',render: h => h(App),router})

### 展示/切换
    vue2:
        <router-link to=""></router-link>  // 字符串
        <router-link :to="{}"></router-link>  // 对象
        <router-view></router-view>  // 展示位置

    编程式路由导航:
        this.$router.push()
        this.$router.replace()
        
        this.$router.back()  // 后退
        this.$router.forward()  // 前进
        this.$router.go(-1/2/3)  // 前进/后退

### query/params传参/路由props
    query传参
        <router-link :to="`/about?id=${m.id}&title=${m.title}`"></router-link>  // 字符串写法
        <router-link :to="{path:'/about',query:{id:m.id,title:m.title}}"></router-link>  // 对象写法

    params参数
        路由占位：
            routes: [{path:'detail/:id/:title?'}]  //占位符声明接受params参数
        传递参数
            <router-link :to="`/about/${m.id}/${m.title}`"></router-link>  // 字符串写法

            // 对象写法
            <router-link :to="{
                name:'hello',  //params对象写法，必须使用name配置，不能使用path
                params:{id:m.id,title: '' || undefined}  //当参数是空串的时候，用undefined解决
            }">
            </router-link>

    接收参数
        this.$route.query.id
        this.$route.params.id

    路由props
        {
            path:'/detail',
            component:Detail,
            props:{a:1,b:'hello'},  //值为对象，该对象中的所有key-value都会以props的形式传给组件
            props:true,   //值为布尔值，若布尔值为真，就会把该路由组件收到的所有params参数，以props的形式传给组件
            //值为函数，该函数返回的对象中每一组key-value都会通过props传给组件
            props($route){
                return{
                    id:$route.query.id,
                    title:$route.params.title
                }
            }
        }

### 缓存路由组件，让不展示的路由组件保持挂载，不被销毁。
    1.具体编码：
        <keep-alive include="News">
            <router-view></router-view>
        </keep-alive>
            
    ## 两个新的生命周期钩子（路由组件独有）
        activated(){}  //路由组件激活时触发
        deactivated(){}  //路由组件失活时触发

    ## 组件内守卫: 进入之前，离开之前  // 不能获取当前组件实例this，因为组件实例还没创建
        beforeRouteEnter(to, from, next){}
        beforeRouteLeave(to, from, next){}

### 重写push|replace
    let originPush = VueRouter.prototype.push;
    let originReplace = VueRouter.prototype.replace;

    VueRouter.prototype.push = function(location, resolve, reject){
        if(resolve && reject){
            // call,改变this指向
            originPush.call(this, location, resolve, reject);
        }else{
            originPush.call(this, location, () => {}, () => {});
        }
    }
    VueRouter.prototype.replace = function(location, resolve, reject){
        if(resolve && reject){
            originReplace.call(this, location, resolve, reject);
        }else{
            originReplace.call(this, location, () => {}, () => {});
        }
    }

## 项目应用
    菜单联动、轮播图、分页器、放大镜、面包屑、登录、注册、日历

## 后台项目
    https://github.com/PanJiaChen/vue-admin-template  简洁版模板
    https://github.com/PanJiaChen/vue-admin-template.git  git克隆链接

    "dev": "set NODE_OPTIONS=--openssl-legacy-provider & vue-cli-service serve",
    修改package.json，在相关构建命令之前加入set NODE_OPTIONS=–openssl-legacy-provider
    npm run dev报错

    http://39.98.123.211:8170/swagger-ui.html
    http://39.98.123.211:8510/swagger-ui.html

## 基本知识(了解即可)
    v-text指令：
        1.作用：向其所在的节点中渲染文本内容。
        2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。

    v-html指令：
        1.作用：向指定节点中渲染包含html结构的内容。
        2.与插值语法的区别：
            1.v-html会替换掉节点中所有的内容。{{xx}}则不会。
            2.v-html可以识别html结构。
        3.严重注意：v-html有安全性问题！！！
            1.在网站上动态渲染任意html是非常危险的，容易导致xss攻击
            2.一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！

    v-cloak指令（没有值）
        1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
        2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。

    v-once指令：
        1.v-once所在节点在初次动态渲染后，就视为静态内容了。
        2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

    v-pre指令：
        1.跳过其所在节点的编译过程。
        2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。

### 自定义指令
        <input type="text" v-hello:value="n">

        配置对象中常用的3个回调（钩子）：
        1.bind：指令与元素成功绑定时调用。
        2.inserted：指令所在元素被插入页面时调用。
        3.update：指令所在模板结构被重新解析时调用。

        Vue.directive('hello',{
            bind(element,binding){
                element.value = binding.value
            },
            inserted(element,binding){
                element.focus()
            },
            update(element,binding){
                element.value = binding.value
            }
        })



