## 关于不同版本的Vue：
    因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用
    render函数接受到的createElement函数去指定具体内容。

## vue.config.js配置文件
> 使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
> 使用vue.config.js可以对脚手架进行个性化定制。

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

            //生命周期
            beforeCreate() {},  //数据代理初始化前                                   
            created() {},  //初始化后(虚拟DOM未开始)
            
            beforeMount() {},  //挂载之前（虚拟DOM完成）                      
            mounted() {},  //挂载完毕
            
            beforeUpdate() {},  //更新数据：更新之前（页面尚未和数据保持同步）  
            updated() {},  //更新数据：更新之后（页面尚和数据保持同步）
            
            beforeDestroy() {},  //销毁之前                                  
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

        *监视属性 or vm.$watch('isHot',function(newValue,oldValue){})
            watch:{
              简写(不需要配置的时候)
              isHot(){}

              完整写法
              isHot:{
                deep:true,  //深度监视
                immediate:false,  //初始化时先调用一下
                handler(newValue, oldValue){

                }
              }
            }

    ## 基本语法  
        指令语法 
            v-bind:xxx 简写为 :xxx  //单向
            v-model:value 可以简写为 v-model,因为v-model默认收集的就是value的值  //双向
            v-on 简写为@ //绑定事件监听
                @click="demo" 和 @click="demo($event)" 效果一致，但后置可以传参 //绑定事件

                修饰符： 
                    @click.prevent="" 取消默认行为
                    @click.noce="" 只触发一次
                    
                    

        条件渲染
            v-if="表达式"、v-else-if、v-else  //不展示的DOM元素直接被移除，可以一起使用，但要求结构不能被"打断"
            v-show="表达式"  //不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

        列表渲染
            v-for="p in persons" :key="p.id"  //展示列表数据，可遍历：数组、对象、字符串、指定次数

        基本语令
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

    三、基本原理

        Key的原理
            key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据[新数据]生成[新的虚拟DOM]，随后Vue进行[新虚拟DOM]与[旧虚拟DOM]的差异比较。

        数据代理原理
            Object.definePropety(obj, ){
                get(){

                },
                set(){

                }
            }
            Vue监视数据的原理：
                1. vue会监视data中所有层次的数据。

                2.如何监测对象中的数据？
                    通过srtter实现监测，且要在new Vue时就传入要监测的数据。
                        1.对象中后追加的属性，Vue默认不做响应式处理
                        2.如需给后添加的属性做响应式，请使用如下API：
                            Vue.set(target, propertyName/index,value) 或
                            vm.$set(target, propertyName/index,value)
                                    // Vue.set(vm.student,'sex','男')
                                    // vm.$set(vm.student,'sex','男')

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

        收集表单数据：
            若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。
            若：<input type="checkbox"/>
                1.没有配置input的value属性，name收集的就是checked（勾选 or 未勾选，是布尔值）
                2.配置input的value属性：
                    1.v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
                    2.v-model的初始值是数组，那么收集的就是value组成的数组
            备注：v-model的三个修饰符：
                lazy：失去焦点再收集数据
                number：输入字符串转为有效的数字
                trim：输入首尾空格过滤

## Vue-cli-API
    ## ref属性，id的替代者
          获取：this.$refs.xxx

    ## props
        场景：父子组件通信
          （1）.传递数据：
                <demo name="数据"/>
          (2).接受数据：
                第一种方式(只接收)：
                  props:['name']

                第二种方式(限制类型):
                  props:{
                    name:Number
                  }

                第三种方式(限制类型、限制必要性、指定默认值)：
                  props:[
                    name:{
                      type:String,//类型
                      required:true,//必要性
                      default:'xx',//默认值
                    }
                  ]

        备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，
              若业务需求确实需要修改，name请复制props的内容到data中一份，然后去修改data中
              的数据。

    
    ## 自定义事件$on、$emit
            子组件给父组件传递数据

            绑定：
                1.第一种方式，在父组件中：
                    <demo @atguigu="回调"/>
                    methods: {
                        test(name){
                            console.log(name)
                        }
                    }
                2.第二种方式，在父组件中：
                    this.$refs.demo.$on('atguigu', 回调)
                    
            子组件：
                this.$emit('atguigu',name)

            解绑：
                this.$off('atguigu')

            *组件上也可以绑定原生DOM事件，需要使用@click.native=""修饰符。

    ## 全局事件总线$bus
            Vue.prototype.$bus = this;

            this.$bus.$on('xxx',回调)

            this.$bus.$emit('xxx',数据)

    ## 消息订阅与发布pubsub-js
            步骤：
                1.安装pubsub: npm i pubsub-js

                2.引入：import pubsub form 'pubsub-js'

                3.接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。
                    methods:{
                    demo(data){......}
                    }
                    ......
                    mounted(){
                    this.pid = pubsub.subscribe('xxx',this.demo)//订阅消息
                    }

                4.提供数据：pubsub.publish('xxx',数据)

                5.最好在beforeDestroy钩子中，用pubsub.unsubscribe(pid)去取消订阅。

    ## 插槽
            1.默认插槽
                父组件：
                    <Category>
                        <div>html结构</div>
                    </Category>

                子组件：
                    <template>
                        <div>
                            <!-- 定义插槽 -->
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
                    <子组件>
                        <template slot-scope="{game}">
                            <ul>
                                <li v-for="(g,index) in games" :key="index"></li>
                            </ul>
                        </template>
                    </子组件>

                子组件：
                    <template>
                        <slot :game="games"></slot>  //回传数据
                    </template>

    ## mixin(混合)
        功能：可以把多个组件共用的JS逻辑配置提取成一个混入对象
        使用方式：
            第一步定义混合，例如：
                export default{
                  data(){....},
                  methods:{....},
                  ....
                }
            引入：
                (1).全局混入：Vue.mixin(xxx)
                import xxx from url;
                (2).局部混入：mixins:['xxx']

    ## nextTick（钩子）
        1.语法：this.$nextTick(回调函数)

        2.作用：在下一次DOM更新结束后执行其指定的回调。

        3.什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。

    ## 封装的过渡与动画
        1.作用：在插入、更新或移除DOM元素时，在合适的时候给元素添加样式类名。

        2.写法：
            1.装备好样式：
                ·元素进入的样式
                1.v-enter：进入的起点

                2.v-enter-active：进入过程中

                3.v-enter-to：进入的终点

                ·元素离开的样式
                1.v-leave：离开的起点

                2.v-leave-active：离开过程中

                3.v-leave-to：离开的终点

            2.使用<transition>包裹要过渡的元素，并配置name属性：
                <transition name="hello">
                  <h1 v-show="!isShow">你好啊！<h1>
                </transition>

            3.备注：若有多个元素需要过渡，则需要使用：<transition-group>,且每个元素都要指定key值。

    ## 插件
        功能：用于增强Vue
        本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数
        据。
        定义插件：
          对象.install = function(Vue,options){
            //插件配置

            //插件配置

            //插件配置
          }
        使用插件：Vue.use()

    ## Vue脚手架配置代理
        方法一
            在vue.config.js中添加以下配置：
              devServer：{
                proxy:"http://localhost:8080"
              }

            说明：
                1.优点：配置简单，请求资源时直接发给前端（8080）即可。

                2.缺点：不能配置多个代理，不能灵活的控制请求是否走代理。

                3.工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么请求会转发给服务器（优先匹配前端资源）

        方法二
            编写vue.config.js配置具体代理规则：
              devServer:{
                proxy:{
                  '/api':{
                    target:'<url>',
                    pathRewrite:{'^/api':''},//重写路径
                    ws:true,//用于支持websocket
                    changeOrigin:true//用于控制请求头中的host值
                  },
                  '/foo':{
                    target:'other_url'
                  }
                }
              }

            说明：
                1.优点：可以配置多个代理，且可以灵活的控制请求是否走代理。

                2.缺点：配置略微繁琐，请求资源时必须加前缀。
                
    ## Vue-resource
        与axios类似，用来发送ajax请求

## Vue-Vuex
        npm i vuex@3

        src/store/index.js
            import Vue from 'vue'
            import Vuex from 'vuex'
            Vue.use(Vuex)

            const actions = {}
            const mutations = {}
            const state = {}
            const getters = {};

            export default new Vuex.Store({
                actions,
                mutations,
                state,
                getters
            })

        main.js:
            import store from './store'

            new Vue({
                el:'#app',
                render: h => h(App),
                store
            })

        读取vuex中的数据：$store.state.sum

        修改vuex中的数据：$store.dispatch('函数',数据)或$store.commit('函数',数据)

        备注：若没有网络请求或其他业务逻辑，组件也可以越过actions,即不写dispatch,直接编写commit

            function(context){}:小仓库

        6.四个map方法的使用
            import {mapState,mapGetters,mapActions,mapMutations} from 'vuex'

            1.mapState方法：
                computed:{
                    // ...mapState({he:'sum',xuexiao:'school',xueke:'subject'})

                    ...mapState(['sum','school','subject'])
                }

            2.mapGetters方法：
                computed:{
                    // ...mapGetters({bigSum:'bigSum'})

                    ...mapGetters(['bigSum'])
                }

            3.mapActions方法：用于帮助我们生成与actions对话的方法，即包含：$store.dispatch(xxx)的函数
                methods:{
                    // ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'}),

                    ...mapActions(['jiaOdd','jiaWait']),
                }

            4.mapMutations方法：用于帮助我们生成与mutations对话的方法，即包含：$store.commit(xxx)的函数
                methods:{
                    // ...mapMutations({increment:'JIA',decrement:'JIAN'})

                    ...mapMutations(['JIA','JIAN'])
                }

            备注：mapActions与mapMutations使用时，若需要传递参数：在模板中绑定事件时传递好参数，否则参数是事件对象

        7.模块化+命名空间
            1.目的：让代码更好维护，让多种数据分类更加明确。

            2.store文件中
                //创建Count.js
                export default {
                    //开启命名空间
                    namespaced:true,
                    actions:{
                    },
                    mutations:{
                    },
                    state:{
                    },
                    getters:{
                    }
                }

                //index.js
                import Count from './Count'

                export default new Vuex.Store({
                    modules:{
                        Count
                    }
                })

            3.开启命名空间后，组件中读取state数据：
                1.方法一：this.$store.state.Count.sum

                2.方法二：...mapState('Count',['sum','school','subject'])

            4.开启命名空间后，组件中读取getters数据：
                1.方法一：this.$store.getters['Person/fistPersonName']

                2.方法二：...mapGetters('Count',['bigSum'])

            5.开启命名空间后，组件中读取dipatch数据：
                1.方法一：this.$store.dispatch('Person/addPersonWang',personObj)

                2.方法二： ...mapActions('Count',['jiaOdd','jiaWait']),

            6.开启命名空间后，组件中读取commit数据：
                1.方法一：this.$store.commit('Person/ADD_PERSON',personObj)

                2.方法二：...mapMutations('Count',['JIA','JIAN']),

## Vue-router
        ## 基本使用
            npm i vue-router@3  //安装

            import Vue from 'vue';
            import VueRouter from 'vue-router';
            Vue.use(VueRouter)  //应用

            import About from '../components/About'
            import Home from '../components/Home'

            export default new VueRouter({
                routes:[
                    {
                        name:'hello',  //命名路由
                        path:'/about',
                        component:About,
                        // 路由元信息
                        meta: {show: true},
                        <!-- 多级路由 -->
                        children:[
                            {
                                path:'news',  //此处一定不要写：/news
                                component:News
                            }
                        ]
                    }
                ]
            })

            4.实现切换（active-calss可配置高亮样式）
                <router-link active-calss="active" to="/About">About</router-link>

            5.指定展示位置
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

        ## 重写push|replace
            // 备份
                let originPush = VueRouter.prototype.push;
                let originReplace = VueRouter.prototype.originReplace;

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
                    //值为对象，该对象中的所有key-value都会以props的形式传给组件
                    props:{a:1,b:'hello'},  

                    //值为布尔值，若布尔值为真，就会把该路由组件收到的所有params参数，以props的形式传给组件
                    props:true
                    
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
                
        ## 两个新的生命周期钩子（路由独有）
            activated(){}  //路由组件激活时触发

            deactivated(){}  //路由组件失活时触发

        ## 路由守卫
            分类：全局守卫(前置、后置)、独享守卫、组件内守卫

            全局守卫：
                //全局前置路由守卫--初始化的时候被调用、每次路由切换之前被调用
                router.beforeEach((to, from, next) => {
                    console.log('前置路由守卫',to, from)
                    document.title = to.meta.title
                    if(to.meta.isAuth){
                        if(localStorage.getItem('school') === 'atguigu'){
                            next()  //放行
                            next(path)  //放行到指定路由
                            next(flase)  //
                        }else{
                            alert('学校名不对，无权限查看！')
                        }
                    }else{
                        next()
                    }
                })

                //全局后置路由守卫--初始化的时候被调用、每次路由切换之后被调用
                router.afterEach((to, from) => {
                    console.log('后置路由守卫', to, from)
                    document.title = to.meta.title || '硅谷系统'
                })
                
            4.独享守卫
                beforeEnter:(to, from, next) => {
                    console.log(to, from)
                    if(to.meta.isAuth){
                        if(localStorage.getItem('school') === 'atguigu'){
                            next()
                        }else{
                            alert('学校名不对，无权限查看！')
                        }
                    }else{
                        next()
                    }
                }

            5.组件内守卫
                beforeRouteEnter(to, from, next){
                    // 渲染该组件之前调用
                    // 不能获取当前组件实例this，因为组件实例还没创建
                    if(from.path == '/pay'){
                        next();
                    }else{
                        next(flase);
                    }
                },
                beforeRouteLeave(to, from, next){
                    // 离开组件前调用
                    console.log('hellokitty')
                }

        ## 路由器的两种工作模式
            1.hash模式：
                1.带#号，不美观

                2.若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。

                3.兼容性好。

            2.history模式：
                1.地址干净，美观

                2.兼容性略差

                3.应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

## Vue组件间通信方式
            props 
                场景：父子组件通信
                    函数：子组件给父组件传递数据（通过子组件调用父组件传递的函数传递数据）
                    非函数：父组件给子组件传递函数
                书写方式：
                    ['props'],{name: number},props: [name: {type: number, default: []}]
                路由中的props
                    方式：对象、布尔值、函数

            自定义事件
                场景：子组件给父组件传递数据
                    @on
                    @emit
                    
            全局事件总线$bus
                场景：全能
                Vue.prototype.$bus = this;
                this.$bus.$on('xxx', 回调)
                this.$bus.$emit('xxx', 数据)

            pubsub-js
                场景：全能
                    npm i pubsub-js

                    import pubsub form 'pubsub-js';

                    pubsub.subscribe('xxx', 回调)

                    pubsub.publish('xxx',数据)

                    pubsub.unsubscribe(pid)

            vuex
                场景：全能

            插槽
                场景：父子组件通信（结构）
                    默认插槽、具名插槽、作用域插槽

            v-model

            sync修饰符(与v-model相似)
                props:
                    :money.sync="money"
                    传递porps: money
                    绑定自定义事件：@update:monry="回调"

            $attrs
                获取父组件传递的props数据
                v-bind="$attrs"

            $listeners
                获取父组件传递的自定义事件
                v-on="$listeners"

            $children
                获取当前组件中全部子组件

            $parent
                获取当前组件的父组件

## 插件

    ElementUL
    nprogress 进度条
    swiper 轮播图
    qrcode 二维码
    vue-lazyload 图片懒加载(vue2使用 1.3.4版本)
    vee-validate 表单验证
    mock.js
        cnpm i mockjs
        创建mock文件夹
        准备JSON数据
        把mock数据需要的图片放置到public文件夹中【public在打包时会原封不动的打包到dist文件夹中】
        创建mockServe.js通过mock.js插件实现模拟数据
        入口文件引入mock
        渲染数据
    lodash防抖与节流
        import _ from 'lodash'
        <!-- 按需引入 -->
        import throttle from 'lodash/throttle'

        节流： 在规定的间隔时间范围内不会重复触发回调，只有大于这个时间间隔才会触发。(设置cd)
            _.throttle(function(){

            }, 1000)

        防抖： 前面的所有的触发都被取消，最后一次执行在规定的时间之后才会触发。（回城）
            _.debounce(function(){

            }, 1000)

## 前台项目：
        三级联动 轮播图 分页器 放大镜 面包屑 登录 注册 日历

## 后台项目：
        123-200 后台管理系统

## demo
    运行脚本文件
        以管理员权限打开windows powershell，输入set-ExecutionPolicy RemoteSigned，选择y或者a即可。

    <!-- npm install -g cnpm --registry=https://registry.npmmirror.com 淘宝镜像-->
    <!-- npm install -g @vue/cli 全局安装Vue脚手架-->
    <!-- vue create name 脚手架vue-cli初始化项目 -->
    <!-- npm run serve 运行-->

## 开发流程
    重写push与replace方法

    axios二次封装

    项目上线、打包
        npm run build
        项目打包处理MAP文件
            vue.config.js:
            productionSourceMap: false,

## 购买服务器
    设置安全组、打开一些端口号
    利用xhell工具登录服务器

    nginx反向代理
        配置： 
            cd /
            cd etc   *a安装nginx: yum install nginx
            cd nginx
            vim nginx.conf  //编辑
                1.一访问服务器地址就可以访问到项目
                location / {
                    root    /root/lsj/www/HelloKitty;
                    index   index.html;
                    try_files $uri $uri/ /index.html;
                }
                2.获取数据
                location /api {
                    proxy_pass url;
                }
                
            3.nginx服务器跑起来
            service nginx start

