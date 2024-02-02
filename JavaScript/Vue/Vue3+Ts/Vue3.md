## 基本流程
    vue3(vite):
        npm create vue@latest  // 通过vite创建Vue3项目
        npm i  // 安装项目依赖
        npm run dev
        npm run build  // 项目打包

    Vue.js devtools 6.2.1  // Chrome安装扩展程序

## 生命周期
    beforeCreate()、created()  // 创建,setup代替
    onBeforeMount(()=>{})  // 真实DOM挂载之前（虚拟DOM完成）
    onMounted(()=>{})  // 挂载完毕(虚拟DOM替换成真实DOM)
    onBeforeUpdate(()=>{})  // 更新数据：更新之前（页面尚未和数据保持同步）  
    onUpdated(()=>{})  // 更新数据：更新之后（页面和数据保持同步）
    onBeforUnmounted(()=>{})  // 卸载之前
    onUnmouted(()=>{})  // 卸载之后

## Vue组件间通信方式

### defineProps(父←→子)
    <Home :name="name"></Home>
    defineProps(['myCar'])
    defineProps({myCar: String, data: String})
    defineProps({
        myCar: {
            type: String, 
            required: true, 
            default: '奥迪'
        }
    })

    路由props:
        方式：对象、布尔值、函数

### defineEmits自定义事件(子→父)
    <Child @send-toy="getToy"></Child>
    function getToy(){}

    let emit = defineEmits(['send-toy'])
    emit('send-toy', data)
            
### mitt(全能)
    npm i mitt

    utils/emitter.ts:
        import mitt from 'mitt'
        export default mitt()

    Child1.vue:
        import emiiter from 'path'
        // emitter.all.clear()  // 获取所有事件
        emitter.on('event', (value)=>{})  // 绑定事件
        onUnmounted(()=>{
            emitter.off('event')  // 解绑事件
        })

    Child2.vue:
        emitter.emit('event', data)  // 触发事件

### v-model(场景:封装UI组件)
    <标签>:
        <input type="text" v-model="data">  // 原型
        <input type="text" :value='data' @input="data=$event.target.value">  // v-model底层原理
            ((<HTMLInputElement>$event.target).value)  // ts断言

    <组件>:
        <Father v-model='data'></Father>  // 原型
        <Father 
            :modelValue='data'   // props
            @update:modelValue='data=$event'  // 自定义事件名($event:触发自定义事件回传的值)
        >
        </Father>  // v-model底层原理

        <Child>:
            <input type='text' 
                :value=modelValue  // 接收props
                @input="emit('update:modelValue', (<HTMLInputElement>$event.target).value)"  // 触发自定义事件
            >
            defineProps(['modelValue'])
            let emit = defineEmits(['update:modelValue'])
        </Child>

    同时传多个model:
        <Father v-model:username='data' v-model:pasworrd='pas'></Father>  // 定义modelValue名称

### $attrs(祖←→孙)
    没有声明接收的props参数会存到$attrs里
    <Father/>  <Child/>  <Son/>
 
    获取祖组件传递的props数据并传递给孙组件
        <Child v-bind="$attrs"/>

### $refs(所有子组件实例)/$parent(获取父组件实例)
    $refs:
        <button @click="getAllChild($refs)"></button>  // 获取组件所有的子组件实例{}
        $refs.CHILD1.name  // 获取数据

    $parent:
        <button @click="getParent($refs)"></button>  // 获取父组件实例
        $parent.name  // 获取数据

### provide()/inject()(祖←→孙)
    父组件provide提供数据,子组件inject使用数据
    provide('name', data)  // 祖组件, data:值/函数
    let name = inject('name', default)  // 孙组件, default:默认值

### pinia数据集中式管理(全能)
    npm i pinia

    main.js:
        import {createPinia} from 'pinia'
        const pinia = createPinia()
        app.use(pinia)

    store/count.ts:
        import {defineStore} from 'pinia'
        组合式
        // export default defineStore('count',()=>{
            const sum = reactive({})
            return {}
        })
        export default defineStore('count',{
            actions:{
                add(){
                    this.sum+=
                }// countStore.add()
            },
            state(){
                return {
                    sum:0
                }    
            },
            getters:{
                bigSum(state){
                    return state.sum += 10
                }
            }
        })

        import {storeToRefs} from 'pinia'  // 只会转换数据
        import {useCountStore} from 'path'
        const countStore = useCountStore()

    修改数据:
        countStore.$patch({
            sum: 666
        })

    $subscribe: (订阅)
        contStore.$subscribe((mutate, state)=>{

        })

### 插槽(父子结构通信)
    默认插槽
        父组件：
            <Child>
                <div>html结构、数据、样式</div>
            </Child>
        子组件：
            <slot>插槽默认内容</slot>  // 插槽展示位置

    具名插槽: v-slot:简写: #
        父组件：
            <Child>
                <template v-slot:center>
                    <div>html结构</div>
                </template>
                <template #center>
                    <div>html结构</div>
                </template>
            </Child>

        子组件：
            <slot name="center">插槽默认内容</slot>

    作用域插槽:
        父组件：
            <Child>
                <template v-slot="params">  // {game}: 解构
                    <div>{{params.game}}</div>
                </template>
            </Child>

        子组件：
            <slot :game="game"></slot>  //回传数据

## API
    import {} from 'vue'
    export default {
        name: 'app',
        components: {},
        setup(){}
    }

### setup()/<script lang='ts' setup></script>
    注意: 
        在beforeCreate(){}数据代理初始化前调用,this为undefine
        可以和data()、methods()同时存在,data里可以读取setup里的数据,反之不行。

    <script setup name='自定义名字'>  // 需要依赖插件,setup标签简化return
        plugin:
            npm i vite-plugin-vue-setup-extend
            vite.config.ts:
                import vueSetupExtend from 'vite-plugin-vue-setup-extend'
                vueSetupExtend()

        import Person from 'path'  // 引入组件时不需要注册,可以直接使用(不需要再注册公共组件)
    </script>

### defineProps
    defineProps(['data'])  
    // let data = defineProps([''])

    // 接受数据类型限制
    import { Persons} from 'path'  // ts数据类型限制
    defineProps<{data?:Persons}>()  // ?可选

    // 设置默认值
    import {withDefaults} from 'vue'
    withDefaults(defineProps<{data?:Persons}>(),{
        data:()=>[{id: 'wwhm0',name: '谭松韵',age: 16}]
    })

### ref唯一标识
    <div ref='title'></div>
    let title = ref()  // 获取dom元素,title.value

    <Child1 ref='CHILD1'></Child1>
    <Child2 ref="CHILD2"></Child2>
    let CHILD1 = ref()
        CHILD1.value  // 获取组件实例
        CHILD1.value.data  // 获取子组件数据
            defineExpose({data})  // 允许外部访问数据

### ref()/reactive()/toRef()/toRefs()
    ref()
        原理: 通过Object.definePropety()的get、set实现

        读取数据时需要.value
        通常定义基础数据类型
    
    reactive()
        原理: 通过new Proxy实现

        数据可以直接使用
        通常定义对象(数组)数据类型

            注意: 
                重新分配一个新对象时,会失去响应式(用Object.assgin()整体替换)(ref则可以)
                Object.assign(obj, obj2)  // 后续对象覆盖前面第一个对象

    toRef(obj, '属性')  // const name = toRef(person, 'name')  // 让其指向另一个对象(修改其引用地址)
    toRefs(obj)  // let p = toRefs(person),  {...toRefs(obj)}  // 让其指向另一个对象(修改其引用地址)

### computed()计算函数
    computed(()=>{})  // 只读
    computed(()=>{  // 读写
        get(){},
        set(value){}
    })

### watch()/watchEffect()监视函数
    watch(data, (newValue, oldValue)=>{}, {deep:true,immediate:false})
        vue3里只能监视以下数据:
            ref定义的数据  // watch(refData, ()=>{}),监视对象数据需开启深度监视{dee[:true]}
            reactive定义的数据:
                1.无法正确的获取oldValue,并且强制开启deep深度监视
                2.监视某个/多个属性,()=>person.name/[()=>person.name, ()=>person.age],需开启deep
            函数返回的值(getter()函数,参考reactive单属性监视)
            一个包含上述内容的数组

        停止监视:
            const stopWatch = watch(data, ()=>{})  // watch()返回一个函数,调用则停止监视
            stopWatch()  // 停止监视

    watchEffect(()=>{})  // 立即运行一个函数,同时响应式地追踪其依赖(用到哪个属性就监视哪个属性)
    
### hook自定义函数
    hooks/use.js:
        import {ref} from 'vue'
        export default ()=>{return {data, data1}}

        import use from '../hooks/use.js'
        let {data, data1} = use()

### composition API
    readonly()  // 让一个响应式数据变更为只读(深只读),p = readonly(person)

#### shallow(浅层次的)
    shallowRef()  // 只处理基本类型数据,不进行对象的响应书处理
    shallowReactive()  // 只处理第一层数据
    shallowReadonly()  // 第一层只读

#### toRaw/markRaw
    toRaw()  // 将一个由reactive生成的响应式对象转变为普通对象
    markRaw()  // 标记一个对象,使其永远不会再成为响应式对象

#### customRef()  
    创建一个自定义的ref,并对其依赖项跟踪和更新触发进行显示控制
    import {customRef} from 'vue'
    let name = myRef('hello')
        function myRef(value){
            return customRef((track, trigger)=>{
                return {
                    get(){
                        track()  // 通知vue追踪value的变化
                        return value
                    },
                    set(newValue){
                        value = newValue
                        trigger()  // 通知vue去重新解析模板
                    }
                }
            })
        }

#### 判断
    isRef()  // 检查一个值是否为ref对象
    isReactive()  // 检查一个值是否为isReactive响应式代理
    isReadonly()  // 检查一个值是否为isReadonly只读代理
    isProxy()  // 检查一个值是否为isReactive响应式代理、isReadonly只读代理

#### API转移
    Vue.  ===>>>  app.
    Vue.prototype  ===>>>  app.config.globalPropertes

### 新组件
    Teleport(传送门)
        能让html结构移动到指定位置
        <teleport to='body'>html</teleport>

    Suspense(异步组件)
        等待异步组件时渲染一些额外内容,让应用有更好的用户体验
        import {Suspense} from 'vue'
        <Suspense>
            <template v-slot='default'>  // 需要展示的组件
                <Child/>
            </template>
            <template v-slot='fallback'>  // 展示正在加载中...
                <div>正在加载中...</div>
            </template>
        </Suspense>

    defineAsyncComponent()动态引入组件
        const child = defineAsyncComponent(()=>import('./'))

## Vue-router
    路由组件一般放在pages/views文件夹下

    工作模式:
        history: 路径不带#号,比较美观,需配合好后端处理路径问题  // history: createWebHistory()
        hash: 兼容性好,但不美观,且seo优化方面相对较差  // history: createWebHashHistory()

    注意:
        1.每个组件都有自己的$route（路由）属性，一般获取路由信息【path、query、params等等】
        2.整个应用只有一个$router（路由器），一般进行编程式导航进行路由跳转【push|replace】

### 基本使用
    npm i vue-router
    src/router/index.js:
        import {createRouter, createWebHistory} from 'vue-router'
        improt Home from 'path'
        const router = createRouter({
            history: createWebHistory(),  // 指定路由器的工作模式
            routes: [
                {
                    name: '',
                    path: '',
                    component: ()=>import('path'),
                    children:[{}],
                    meta: {},
                    beforeEnter: ()=>{}  // 路由独享守卫,进入之前
                },
                {path: '/',redirect: '/person'}  // 重定向
            ]
        })
        router.beforeEach((to, from, next) => {})  // 全局前置路由守卫--初始化的时候被调用、每次路由切换之前被调用
        router.afterEach((to, from) => {})  // 全局后置路由守卫--每次路由切换之后被调用
        export default router

    main.js:
        import router from 'path'
        app.use(router)

### 展示/切换 
    <RouterLink to='/home'></RouterLink>  // 字符串
    <RouterLink to='{path: '/home'/name:'首页'}'></RouterLink>  // 对象
    <RouterView></RouterView>

### query/params传参/路由props
    import {useRoute} from 'vue-router'
    let route = useRouter()

    query传参:
        <router-link :to="`/home?id=${person.id}&title=${person.name}`"></router-link>  // 字符串写法
        <router-link :to="{path:'',query:{id:person.id,name:person.name}}"></router-link>  // 对象写法
        
    params参数：
        routes: [{path:'home/:id/:name?'}]  // 路由占位,占位符声明接受params参数
        传递参数:
            <router-link :to="`/home/${person.id}/${person.name}`"></router-link>  // 字符串写法

            // 对象写法
            <router-link :to="{
                name:'hello',  // params对象写法，必须使用name配置，不能使用path
                params:{id:m.id,title: '' || undefined}  // 当参数是空串的时候，用undefined解决
            }">
            </router-link>

    路由中的props:
        方式：对象、布尔值、函数
        {
            path:'/detail',
            component:Detail,
            props:true,   //布尔值，把该路由组件收到的所有params参数，以props的形式传给组件
            props:{a:1,b:'hello'},  //对象，所有key-value都会以props的形式传给组件
            //函数，每一组key-value都会通过props传给组件
            props($route){
                return{
                    id:$route.query.id,
                    title:$route.params.title
                }
            }
        }

    获取参数:
        route.query.id
        route.params.id
        let {query} = roRefs(route)  // 解构赋值

### 编程式导航
    import {useRouter} from 'vue-router'
    let router = useRouter()

    router.push()
    router.replace()
    
    router.back()  // 后退
    router.forward()  // 前进
    router.go(-1/2/3)  // 前进/后退

### 缓存路由组件，让不展示的路由组件保持挂载，不被销毁。
    1.具体编码：
        <keep-alive include="News">
            <router-view></router-view>
        </keep-alive>
            
    ## 两个新的生命周期钩子（路由组件独有）
        activated(){}  //路由组件激活时触发
        deactivated(){}  //路由组件失活时触发

### 组件内守卫: 进入之前，离开之前  // 不能获取当前组件实例this，因为组件实例还没创建
    beforeRouteEnter(to, from, next){}
    beforeRouteLeave(to, from, next){}

### 样式
    active-calss可配置高亮样式
        <router-link active-calss="active" to=""></router-link>
        <style>.active{color: pink;}</style>

## 原理

### Key的原理
    key是虚拟DOM对象的标识，状态中的数据发生变化时，Vue会根据[新数据]生成[新的虚拟DOM]，[新虚拟DOM]与[旧虚拟DOM]进行差异比较。
    index作为key，当进行破坏数组顺序的操作时，会产生没有必要的真实DOM更新，效率低。
    如果结构中还包含输入类的DOM：会产生错误DOM更新 ==> 界面有问题

### 数据代理原理
    原生js Object.defineProperty()、Reflect.definePropety():
        Object.defineProperty(obj, 'name'){
            value: '杨超越',  // 设置初始值,默认值undefine
            enumerable: true,  // 控制属性是否可以枚举，默认值false
            writable: true,  // 控制属性是否可以修改，默认值false
            configurable: true,  // 控制属性是否可以被删除，默认值false
            get(){},  // 读取时触发
            set(value){}  // 修改时触发
        }  // 没有返回值,不方便捕获错误

        Reflect.definePropety(obj, 'name', {})  // 反射对象,有返回值,方便捕获错误

    es6 Proxy(代理): 
        const p = new Proxy(person, {
            get(target, propName){return Reflect.get(target, propName)},  // 读取属性时触发
            set(target, propName, value){return Reflect.set(target, propName, value)},  // 添加、修改属性时触发
            deleteProperty(target, propName){return Reflect.deleteProperty(target, propName, value)}  // 删除属性时触发
        })

    通过Proxy(代理): 拦截对象中任意属性的变化。
    通过Reflect(反射)：对被代理对象属性进行操作。




