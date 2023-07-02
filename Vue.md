## 单文件组件
    const school = Vue.extend({
        template: `
            <div></div>
        `,
        data(){
            return{}
        }
    })

    new Vue({
        el: '#root',
        components: {
            school
        }
    })

## Vue-API
    eslint语法校验功能关闭
        ---配置vue.config.js
            module.exports = defineConfig({
                lintOnSave:false  // 关闭语法检查
            })

    ## 基本配置
        Vue.config.productionTip = false  //关闭警告 and Vue.js devtools 6.2.1
        methods: {},  //事件处理（事件修饰符、键盘事件）
        computed:{},  //计算属性
        watch:{},  //监视属性

        beforeCreate() {},  //数据代理初始化前                                   
        created() {},  //初始化后(虚拟DOM未开始)
        
        beforeMount() {},  //真实DOM挂载之前（虚拟DOM完成）                      
        mounted() {},  //挂载完毕(虚拟DOM替换成真实DOM)
        
        beforeUpdate() {},  //更新数据：更新之前（页面尚未和数据保持同步）  
        updated() {},  //更新数据：更新之后（页面和数据保持同步）
        
        beforeDestroy() {},  //实例销毁之前                                  
        destroyed() {},  //销毁之后
        
        *计算属性
            computed:{
              简写（只读不取）
              fullName(){}，

              完整写法
              fullName:{
                get(){},
                set(value){}
                }
            }

        *监视属性
            watch:{
              简写(不需要配置的时候)
              isHot(){}

              完整写法
              isHot:{
                deep:true,  //深度监视
                immediate:false,  //初始化时先调用一下
                handler(newValue, oldValue){}
              }
            }
       
    ## 基本语令
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

        自定义指令
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

    ## nextTick（钩子）
        this.$nextTick(()=>{})

    ## 基本原理
        Key的原理
            key是虚拟DOM对象的标识，状态中的数据发生变化时，Vue会根据[新数据]生成[新的虚拟DOM]，[新虚拟DOM]与[旧虚拟DOM]进行差异比较。

            index作为key，当进行破坏数组顺序的操作时，会产生没有必要的真实DOM更新，效率低。
            如果结构中还包含输入类的DOM：
                        会产生错误DOM更新 ==> 界面有问题

        数据代理原理
            Object.definePropety(obj, 属性名){
                // value:20,
                // enumerable:true,//控制属性是否可以枚举，默认值为false
                // writable:true,//控制属性是否可以修改，默认值为false
                // configurable:true,//控制属性是否可以被删除，默认值为false
                get(){},
                set(){}
            }
            Vue监视数据的原理：
                1. vue会监视data中所有层次的数据。

                2.如何监测对象中的数据？
                    通过srtter实现监测，且要在new Vue时就传入要监测的数据。
                        1.对象中后追加的属性，Vue默认不做响应式处理
                        2.如需给后添加的属性做响应式，请使用如下API：
                            Vue.set(this.student, 'key', 'value')
                            this.$set(this.student, 'key', 'value')

                3.如何监测数组中的数据？
                    通过包裹数组更新元素的方法实现，本质就是做了两件事：
                        1.调用原生对应的方法对数组进行更新。
                        2.重新解析模板，进而更新页面。

                4.在Vue修改数组中的某一个元素一定要用以下方法：
                    1.使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
                    2.Vue.set() 或 vm.$set()

                特别注意：Vue.set 和vm.$set() 不能给vm 或 vm的根数据对象添加属性！！！

        生命周期原理
            基本原理：
                Vue在关键时刻帮我们调用的一些特殊名称的函数。
      
            常用的生命周期钩子：
                1.mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等[初始化操作]
                2.beforeDestroy：消除定时器、解绑字典已事件、取消订阅消息等[收尾工作]

    ## v-model(文本框、单选、复选)
        文本框: 收集value
        单选: 收集value值，且要给标签配置value值。
            <input type="radio" v-model="radio" value='足球'>
            <input type="radio" v-model="radio" value='篮球'>
        复选: 
            1.没有配置input的value属性，收集的是布尔值
            2.配置input的value属性：
                1.v-model的初始值是非数组，那么收集的是布尔值
                2.v-model的初始值是数组，那么收集的就是value组成的数组

        *备注：v-model的三个修饰符：
            lazy：失去焦点再收集数据
            number：输入字符串转为有效的数字
            trim：输入首尾空格过滤

## 事件
    组件绑定原生事件
        <Home @click.native></Home>  //不加修饰符相当于自定义事件

    ## 基本语法
        v-on 修饰符： 
            @click.prevent="" 取消默认行为
            @click.noce="" 只触发一次
            .stop: 阻止事件冒泡；
            .capture：使用事件的捕获模式；
            .self：只有event.target是当前操作的元素时才触发事件；
            .passive：事件的默认行为立即执行，无需等待事件回调执行完毕；
            .native  //自定义事件变成原生事件

    <!-- 
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
            （2）.配合keydown：正常触发事件。

        4.也可以使用keyCode去指定具体的按键（不推荐）

        5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名。
    -->

## 插槽 
    场景: 父子通信
        1.默认插槽
            父组件：
                <Category>
                    <div>html结构</div>
                </Category>
            子组件：
                <template>
                    <div>
                        <!-- 定义插槽展示位置 -->
                        <slot>插槽默认内容</slot>
                    </div>
                </template>

        2.具名插槽
            父组件：
                <Category>
                    <template v-slot:center>
                    <div>html结构</div>
                    </template>

                    <template v-slot:footer>
                    <div>html结构</div>
                    </template>
                </Category>

            子组件：
                <template>
                    <div>
                        <!-- 定义插槽 -->
                        <slot name="center">插槽默认内容</slot>
                        <slot name="footer">插槽默认内容</slot>
                    </div>
                </template>

        3.作用域插槽
            父组件：
                <Category>
                    <template slot-scope="{game}">
                        <ul>
                            <li v-for="(g,index) in games" :key="index"></li>
                        </ul>
                    </template>
                </Category>

            子组件：
                <template>
                    <slot :game="games"></slot>  //回传数据
                </template>

            **ElementUI插槽

## 封装的过渡与动画
    1.作用：在插入、更新或移除DOM元素时，在合适的时候给元素添加样式类名。

    2.写法：
        1.准备好样式：
            元素进入的样式
            .v-enter：进入的起点

            .v-enter-active：进入过程

            .v-enter-to：进入的终点

            元素离开的样式
            .v-leave：离开的起点

            .v-leave-active：离开过程

            .v-leave-to：离开的终点

        2.使用<transition>包裹要过渡的元素，并配置name属性：
            <transition-group name="hello" appear>
                <h1 v-show="!isShow" key="1">你好啊！<h1>
                <h1 v-show="!isShow" key="2">你好啊！<h1>
            </transition-group>

        3.备注：若有多个元素需要过渡，则需要使用：<transition-group>,且每个元素都要指定key值。

        animate.css 动画库
            npm i anitate.css
            import 'anitate.css'

## 配置代理服务器
    编写vue.config.js配置具体代理规则：
        devServer:{
            proxy:{
                '/api':{
                    target:'http://127.0.0.1:8080',
                    pathRewrite:{'^/api':''},  //正则匹配重写路径
                    ws:true,  //用于支持websocket
                    changeOrigin:true //用于控制请求头中的host值
                },
                '/foo':{
                target:'other_url'
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
    ## 基本使用
        npm i vue-router@3  //安装

        src/router/index.js
            import Vue from 'vue';
            import VueRouter from 'vue-router';
            Vue.use(VueRouter)  //应用

            import Home from '@/views/Home'

            // 重写push|replace
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

            const router new VueRouter({
                routes:[
                    {
                        name: 'hello',
                        path: '/about',
                        component: About|()=>import('@/views/about'),
                        meta: {show: true},  // 路由元信息 v-show="$route.meta.show"
                        children: [{path:'news',component:News}],
                        beforeEnter: (to, from, next) => {}  // 独享守卫: 进入之前
                    }
                ]
            })

            router.beforeEach((to, from, next) => {})  //全局前置路由守卫--初始化的时候被调用、每次路由切换之前被调用

            router.afterEach((to, from) => {})  //全局后置路由守卫--每次路由切换之后被调用

            export default router

        main.js
            import route from '@/router'
            new Vue({
                el:'#app',
                render: h => h(App),
                router
            })

    ## 展示
        实现切换（active-calss可配置高亮样式）
            <router-link active-calss="active" to="/About">About</router-link>

        指定展示位置
            <router-view></router-view>

    ## 注意
        1.每个组件都有自己的$route（路由）属性，一般获取路由信息【path、query、params等等】

        2.整个应用只有一个$router（路由器），一般进行编程式导航进行路由跳转【push|replace】

    ## 路由跳转
        1.<router-link to="/about/news">News</router-link>

        2.编程式路由导航
                具体编码：
                    this.$router.push({path:'/about/message/detail'})
                    this.$router.replace({path:'/about/message/detail'})
                    
                    this.$router.back()  // 后退
                    this.$router.forward()  // 前进
                    this.$router.go(-1/2/3)  // 前进/后退

    ## query传参
        1.传递参数
            字符串写法
            <router-link :to="`/about?id=${m.id}&title=${m.title}`"></router-link>

            对象写法
            <router-link :to="{
                path:'/about',
                query:{
                    id:m.id,
                    title:m.title
                }
            }">
            </router-link>

        2.接收参数
            $route.query.id
                        
    ## params参数
        路由占位：
            routes: [
                {
                    path:'detail/:id/:title?',  //占位符声明接受params参数,加上？号代表参数可传可不传
                }
            ]

        传递参数
            字符串写法
            <router-link :to="`/about/message/detail/${m.id}/${m.title}`"></router-link>

            对象写法
            <router-link :to="{
                name:'hello',  //params对象写法，必须使用name配置，不能使用path
                params:{
                    id:m.id,
                    title: '' || undefined  //当参数是空串的时候，用undefined解决
                }
            }">
            </router-link>

        3.接收参数
            $route.params.id

    ## 路由的props配置
        作用：让路由组件更方便的收到参数
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

    ## 缓存路由组件，让不展示的路由组件保持挂载，不被销毁。
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

## Vue组件间通信方式
    props
        场景：父子组件通信
            函数：子组件给父组件传递数据（通过子组件调用父组件传递的函数传递数据）
            非函数：父组件给子组件传递函数
        传递: <:name="name">
        书写方式：
            props: ['props'] | {name: number} | {name: {type: number, required:true, default: ''}}
        路由中的props
            方式：对象、布尔值、函数

    自定义事件
        场景：子组件给父组件传递数据
            $on('msg', callback)  or <Home @msg="callback"/>
            $emit('msg', data)

        *组件上也可以绑定原生DOM事件，需要使用@click.native=""修饰符。
            
    全局事件总线$bus
        场景：全能
        Vue.prototype.$bus = this;
        this.$bus.$on('msg', callback)
        this.$bus.$emit('msg', data)

    pubsub-js
        场景：全能
            npm i pubsub-js
            import PubSub form 'pubsub-js';
            Vue.use(PubSub)

            PubSub.subscribe('msg', callback(msg, data))
            PubSub.publish('msg', data)

            PubSub.unsubscribe(pid)

    vuex
        场景：全能

    插槽
        场景：父子组件通信（结构）
            默认插槽、具名插槽、作用域插槽

    父子组件数据同步
        v-model
            <Home :value='msg' @input='msg = $event'></Home>
            <Home v-model='msg'></Home>

            <input type=text :value=value @input="@emit('input', $event.target.value)">
            props: ['value']

            v-model='msg'
                传递props: ['value']
                绑定自定义事件@input='msg = $event'

        .sync修饰符(与v-model相似)
            <Home :money='money' @update:money='money = $event'></Home>
            <Home :money.sync='money'></Home>

            <button @click="@emit('update', money - 100)">
            props: ['money']

            :money.sync="money"
                传递props: ['money']
                绑定自定义事件：@update:money='money = $event'

    $attrs/$listeners
        this.$attrs
            获取父组件传递的props数据
            v-bind="$attrs"

        $listeners
            获取父组件传递的自定义事件
            v-on="$listeners"

    $children/$parent
        $children
            获取当前组件中全部子组件  //当组件过多时[0]索引值并非按顺序排列

        $parent
            获取当前组件的父组件

    混入mixin
        export default {}

        import myMixin from ''
        mixins: [myMixin]

    作用域插槽
        父组件
            <Home>
                <template slot-scope='todo'>
                    <span>{{todo.text}}</span>
                </template>
            </Home>

        子组件
            <slot :todo="item"></slot>  //数据回传

## 插件
    ##nprogress 进度条
        npm i nprogress

        import nprogress from 'nprogress';  // 引入进度条
        import 'nprogress/nprogress.css';  // 引入进度条样式
        
        nprogress.start();  // 进度条开始
        nprogress.done();  // 进度条结束

    ##lodash防抖与节流
        npm i lodash

        import _ from 'lodash'  //引入lodash
        import throttle from 'lodash/throttle'  // 引入节流
        import debounce from 'lodash/debounce'  // 引入防抖
        import cloneDeep from 'lodash/cloneDeep'  // 引用lodash的深拷贝

        throttle(()=>{}, 50),  // 防抖

        data1 = cloneDeep(data)  // 深度克隆

        节流： 在规定的时间范围内不会重复触发回调，只有大于这个时间间隔才会触发。(设置cd)
            _.throttle(function(){}, 1000)

        防抖： 前面的所有的触发都被取消，最后一次执行在规定的时间之后才会触发。（回城）
            _.debounce(function(){}, 1000)

    ##swiper 轮播图
        npm i swiper@5

        main.js
            import 'swiper/css/swiper.min.css'

        <template>
            <div class="swiper-container">
                <div class="swiper-wrapper">
                    <div class="swiper-slide"></div>
                    <div class="swiper-slide"></div>
                    <div class="swiper-slide"></div>
                </div>

                <!-- 如果需要分页器 -->
                <div class="swiper-pagination"></div>

                <!-- 如果需要导航按钮 -->
                <div class="swiper-button-prev"></div>
                <div class="swiper-button-next"></div>
            </div>
        </template>

        <script>
            import Swiper from 'swiper/js/swiper.min'

            export default {
                mounted() {
                    const swiper = new Swiper('.swiper-container', {
                        loop: true, // 循环模式选项

                        autoplay:true,//等同于以下设置

                        // 如果需要分页器
                        pagination: {
                            el: '.swiper-pagination',
                            clickable: true
                        },

                        // 如果需要前进后退按钮
                        navigation: {
                            nextEl: '.swiper-button-next',
                            prevEl: '.swiper-button-prev',
                        }
                    })
                }
            };
        </script>

        <style scoped>
            .swiper-container{
                width: 600px;
                height: 400px;
            }
        </style>

    ##vue-lazyload 图片懒加载(vue2使用 1.3.4版本)


    ##vee-validate 表单验证


    ##moment.js  生成日期对象


    ##qrcode 二维码

    
    ElementUL

## 前台项目：
    菜单联动 轮播图 分页器 放大镜 面包屑 登录 注册 日历

## 后台项目：
    https://github.com/PanJiaChen/vue-admin-template  简洁版模板
    https://github.com/PanJiaChen/vue-admin-template.git  git克隆链接

    "dev": "set NODE_OPTIONS=--openssl-legacy-provider & vue-cli-service serve",
    修改package.json，在相关构建命令之前加入set NODE_OPTIONS=–openssl-legacy-provider  npm run dev报错

    http://39.98.123.211:8170/swagger-ui.html
    http://39.98.123.211:8510/swagger-ui.html

    proxy: {
        '/dev-api': {
            target: 'http://39.98.123.211',
            pathRewrite: {'^/dev-api' : ''}
        }
    }

    npm run lint --fix  //格式化代码规范

    ElementUL
        button  //type类型、icon图标、disabled是否禁用
        input  //type: text/textarea、placeholder输入框占位文本

        table  //data绑定的数据、border纵向边框、
        table-column  //type:selection多选框/index索引/expand展开的按钮、lable显示的标题、prop对应列的内容(与data绑定)、width对应列宽度、align对齐方式
        <template slot-scope="{row, column, $index}"></template>  //table-column作用域插槽

        form  //model表单数据对象、表单验证rules、.validate检验校验是否通过、inline行内表单
        form-item  //prop收集数据绑定对象、label标签文本、required是否必填

        upload  //action上传地址、show-file-list是否显示已上传文件列表:on-success=""上传成功回调、:before-upload=""上传之前回调
        
        dialog  //对话框  title标题、visible是否显示
        
        $message  //({type: success/warning/info/error, message: '提示信息'})
        messageBox
            $msgbox(options)  //自定义
            $alert(message, title, options)  //消息提示
            $confirm(message, title, options)  //确认消息
            $prompt(message, title, options)  //提交内容
                message消息内容、title标题、options{
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }
                .then()  //点击确定回调
                .catch()  //点击取消回调

        pagination  //分页器
            :current-page="page"当前页数
            page-size每页显示数据条数
            total数据总条数
            page-count分页器总页数
            pager-count页码按钮数量
            layout="prev, pager, next, jumper, sizes, total"  //组件布局
            :page-sizes="[3, 5, 10]"  //每页显示数量设置
            @current-change=""当前页数发生改变的回调
            @size-change=""  展示数据条数发生改变的回调

        150-200 后台管理系统  19h

        150-160  4h
        160-170  4h
        170-180  3.5h
        180-190  2.5h
        190-200  5h

## 开发流程
    <!-- npm install -g @vue/cli 全局安装Vue脚手架-->
    <!-- vue create name 脚手架vue-cli初始化项目 -->
    <!-- npm run serve 运行-->

    npm i less-loader

    项目上线、打包
        npm run build
        项目打包处理MAP文件
            vue.config.js:
            productionSourceMap: false,

    今日任务
        使用插件
        webpack打包
        不同屏幕适配rem
        浏览器兼容等问题

        手写深拷贝

## 购买服务器
    服务器打开端口号

    远程桌面连接
        登录服务器

    下载nginx配置： 
            cd /
            cd etc   *a安装nginx: yum install nginx
            cd nginx
            vim nginx.conf  //编辑
                location / {
                    root    /root/lsj/www/HelloKitty;
                    index   index.html;
                }
                反向代理
                location /api {
                    proxy_pass url;
                }
                
            3.nginx服务器跑起来
            liux: service nginx start
            windows: start ngnix



