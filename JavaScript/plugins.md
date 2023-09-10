## nprogress 进度条
    npm i nprogress

    import nprogress from 'nprogress';  // 引入进度条
    import 'nprogress/nprogress.css';  // 引入进度条样式
    
    nprogress.start();  // 进度条开始
    nprogress.done();  // 进度条结束

## lodash防抖与节流
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

## swiper 轮播图
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

## vue-lazyload 图片懒加载(vue2使用 1.3.4版本)
    npm i vue-lazyload@1.3.4

    main.js
        import VueLazyload from 'vue-lazyload'
        Vue.use(VueLazyload, {
            loading: require('@/assets/GIF.gif')  // 懒加载默认图片
        })

    <img v-lazy="img" alt="">

## moment.js/dayjs  生成日期对象
    npm i moment

    import moment from 'moment'

    moment().format('YYYY年MM月DD日, hh:mm:ss a')  // 2023年06月16日, 02:49:16 am

    moment().day(0).format('YYYY-MM-DD')  // 获取现在的周数
    
    moment().startOf('month').format('YYYY-MM-DD')  // 获取开始时间

    moment().endOf('year').format('YYYY-MM-DD')  // 获取结束时间

## qrcode 二维码
    npm i qrcode.js

    import QRCode from 'qrcode';
    QRCode.toDataURL('I love you!')
    .then(url => {
        console.log(url)
        this.img = url
    })
    .catch(err => {
        console.error(err)
    })

    <img :src="img" alt="">

## vee-validate 表单验证
    npm i vee-validate@2  //vue2.0使用2 or 3 版本

    import VeeValidate from 'vee-validate';
    import zh_CN from 'vee-validate/dist/locale/zh_CN';  // 显示中文信息
    Vue.use(VeeValidate);

    // 校验规则
    VeeValidate.Validator.localize('zh_CN', {
    messages: {
        ...zh_CN.messages,
        is: (field) => `${field}必须与密码相同`,  //修改内置规则的 message，让确认密码与密码相同
    },
    attributes: { //给校验的 field 属性名映射中文名称
        phone: '手机号',
        code: '验证码',
        password: '密码',
        password1: '确认密码',
        agree: '协议'
    }
    })

    // 自定义校验规则
    VeeValidate.Validator.extend('agree', {
    validate: (value) => {
        return value;
    },
    getMessage: (field) => field + "必须同意"
    })

    账号<input type="text" v-model="username" name="username" v-validate="{ required: true, regex: /^[a-z][a-z][0-9]{5}$/}" :class="{ invalid: errors.has('username')}">
    <p>
        <span class="error">{{ errors.first('username') }}</span>
    </p>

    const success = await this.$validator.validateAll();  // 全部表单验证通过才可以注册
    if(success){}

## ElementUL
    标签
        ## <el-row :gutter=''>  // 栅格间距
                <el-col :span='24'></el-col>  // 平分
            </el-row>

        ## el-card

        ## dr  //下拉菜单
            <el-dropdown >
                <i class="el-icon-more"></i>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item>黄金糕</el-dropdown-item>
                    <el-dropdown-item>狮子头</el-dropdown-item>
                    <el-dropdown-item>螺蛳粉</el-dropdown-item>
                    <el-dropdown-item>双皮奶</el-dropdown-item>
                    <el-dropdown-item>蚵仔煎</el-dropdown-item>
                </el-dropdown-menu>
            </el-dropdown>


        ## button
            type=""  类型  primary/success/warning/danger/info/text
            icon=""  图标
            disabled  是否禁用

        ## input
            type=""  text、textarea和其他原生input的type值
            placeholder=""  占位符
            label=""  输入框关联的label文字

            event:
                blur	失去焦点时触发	(event: Event)
                focus	获得焦点时触发	(event: Event)
                change	仅在输入框失去焦点或用户按下回车时触发	(value: string | number)
                input	值改变时触发	(value: string | number)

            methods:
                focus	获取焦点
                blur	失去焦点
                select	中的文字

        ## table
            data=""  绑定的数据
            border  纵向边框

            table-column  
                type=""
                    selection  多选框
                index索引
                expand展开的按钮
                lable显示的标题
                prop对应列的内容(与data绑定)
                width对应列宽度
                align对齐方式

            <template slot-scope="{row, column, $index}">  // table-column作用域插槽
                {{ row }}
            </template>

        ## form
            model表单数据对象
            rules表单验证
            .validate检验校验是否通过
            inline行内表单

            form-item  //prop收集数据绑定对象、label标签文本、required是否必填


        ## upload  //action上传地址、show-file-list是否显示已上传文件列表:on-success=""上传成功回调、:before-upload=""上传之前回调
        
        ## dialog  //对话框  title标题、visible是否显示
    
    方法
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

## ECharts
    import * as echarts from 'echarts';

    <div class="charts" ref="charts"></div>
    mounted(){
        // 初始化实例
        const lineCharts = echarts.init(this.$refs.charts)
        // 配置对象
        lineCharts.setOption({
            title: {
                text: '',  // 标题
                subtext: '',  // 子标题
                left: 'center',  // 位置
            }
            <!-- 图表配置 -->
            grid: {
                top: 0,
                right: 0,
                bottom: 0,
                left: 0,
                width: 0,
                height: 0
            },
            // x轴配置
            xAxis: {
                data: [],  // 数据
                // show: false,
                // type: 'category'  // 类目轴
            },
            // y轴配置
            yAxis: {
                // show: false,
                // 是否显示y轴轴线
                axisLine: {
                    show: true
                },
                // 是否显示y轴刻度
                axisTick: {
                    show: true
                }
            },
            // 系列的设置： 绘制图表类型、数据展示
            series: [
                {
                    type: 'line',
                    data: [50, 65, 35, 99, 33, 66, 40, 75, 20, 82],
                    // 拐点样式
                    itemStyle: {
                        opacity: 0
                    },
                    // 线条样式
                    lineStyle: {
                        color: 'pink'
                    },
                    // 填充颜色
                    areaStyle: {
                        color: {
                            type: 'linear',
                            x: 0,
                            y: 0,
                            x2: 0,
                            y2: 1,
                            colorStops: [{
                                offset: 0, color: 'pink' // 0% 处的颜色
                            }, {
                                offset: 1, color: 'white' // 100% 处的颜色
                            }],
                            global: false // 缺省为 false
                        }
                    },
                    // 平滑曲线
                    smooth: true
                },
                {
                    type: 'bar',
                    data: [50, 65, 35, 99, 33, 66, 40, 75, 20, 82],
                    color: 'cyan'
                },
                {
                    name: '饼状图',
                    type: 'pie',
                    data: [
                        {name: '衣服', value: 10},
                        {name: '直播', value: 20},
                        {name: '游戏', value: 30},
                        {name: '电影', value: 40}
                    ],
                    width: 250,
                    height: 250,
                    radius: 50,
                    left: 700,
                }
            ],
            // 提示组件
            tooltip: {},
            // 切换组件
            legend: {
                data: ['柱状图', '折线图', '饼状图']
            },
            // 工具栏组件
            toolbox: {
                show: true,
                feature: {
                dataZoom: {
                    yAxisIndex: "none"
                },
                dataView: {
                    readOnly: false
                },
                magicType: {
                    type: ["line", "bar"]
                },
                restore: {},
                saveAsImage: {}
                }
            }
        })
    }