## uni-app
    condition启动模式配置
        "condition": {
            "current": 0,
            "list": [
                {
                    "name": "详情页",
                    "path": "pages/detail/detail",
                    "query": "id=80"
                }
            ]
        }

    生命周期
        应用
            onLaunch //加载
            onShow  //显示
            onHide  //隐藏
        页面
            onLoad  //加载
            onReady  //初次渲染
            onShow  //显示
            onHide  //隐藏
            onUnload  //页面卸载
            
    发送请求
        uni.request({
            url: '',
            success(){

            }
        })

    缓存
        uni.setStorage({
            key: '',
            data: '',
            success(){

            }
        })

    跨端兼容
        <!-- #ifdef H5 -->
        <!-- #endif -->
        // #ifdef H5
        // #endif

    路由跳转
        声明式导航
            <navigator url=""></navigator>
        编程式导航
            uni.navigateTo({
                url: '',

            })

    注册组件
        注册的组件创建方式和生命周期和vue一致

    组件间通讯
        props
        自定义事件
            uni.$on('', 回调)
            uni.$emit('', 参数)

    uni-ui
        插件库

    提示框
        uni.showToast({
            title: ''
        })

    下拉刷新、上拉触底
        onPullDownRefresh(){
            
        }
        onReachBottom(){

        }

    