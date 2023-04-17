## 微信小程序

    1vh = 1%的视口高度

    绑定事件
        bindtap="回调"  //冒泡
        catchtap="回调"  //非冒泡
        
        bindinput=""  //实时获取输入框value

        bindtouchstart=""  //用户点击起始位置
        bindtouchmove=""  //用户滑动位置
        bindtouchend=""  //用户抬起动作

    event
        指南--小程序框架--事件系统
            event.touches[0].clientY;  //获取坐标(数组代表可能多个手指同时点击)

   * 生命周期函数--监听页面加载
    onLoad(options) {},

   * 生命周期函数--监听页面初次渲染完成
    onReady() {},

   * 生命周期函数--监听页面显示
    onShow() {},

   * 生命周期函数--监听页面隐藏
    onHide() {},

   * 生命周期函数--监听页面卸载
    onUnload() {},

   * 页面相关事件处理函数--监听用户下拉动作
    onPullDownRefresh() {},

   * 页面上拉触底事件的处理函数
    onReachBottom() {},

   * 用户点击右上角分享
    onShareAppMessage() {}

    微信授权getUserProfile
            wx.getUserProfile({
                desc: '音乐',
                success: (res) => {}
            })

        用户唯一标识openID
            API--开放接口--登录--wx.login
        code
            wx.login({})
        APPID
            wx7ed06deaaa9e080a
        密钥
            bc95329a43e778ee4a446fc669fe504a

    路由跳转
        API--路由--wx.navigateTo
            保存当前页面进行跳转
                wx.navigateTo({})
            关闭当前页面进行跳转
                wx.redirectTo({})
            关闭所有页面进行跳转
                wx.reLaunch({})
            跳转至tabBar,并关闭其他所有非 tabBar 页面
                wx.switchTab({})
            关闭所有页面，打开到应用内的某个页面
                wx.reLaunch(Object object)

    提示框
        API--界面--交互
            wx.showToast({
                title: "出错啦！！",
                icon: 'none'
            })
            wx.showLoading

            wx.showModal  //模态对话框

    taBar底部栏
        框架--小程序配置--全局配置

    轮播图
        组件--视容器图--swiper

    可滚动视图
        组件--视容器图--scroll-view
            refresher-enabled  //开启下拉刷新
            bindrefresherrefresh  //下拉刷新回调
            上拉加载

    music
        API--媒体组件--音频
            创建音频实例
                let backgroundAudioManager = wx.getBackgroundAudioManager();

    video
        组件--媒体组件--video
            多个视频同时播放
            poster  //封面图片 
            object-fit  //视频视宽
            bindtimeupdata  //播放时触发
            bindended  //播放结束触发

        APi--视频--VideoContext
            创建实例--进行控制对应的video播放、暂停、停止、跳转
            
    button
        open-type="share"  //转发分享

    发送请求
        API--网络--wx.request
            注意: 协议必须是https协议，需先配置授权

    自定义组件
        框架--框架接口--自定义组件
        注册：json
            "navHeader": "../../components/navHeader/navHeader"

    自定义模板
        框架--WXML--模板

    内网穿透

    正则
        phone：/^1(3|4|5|6|7|8|9)\d{9}$/;

    全局实例
        const appInstance = getApp();

    本地存储
        API--数据缓存--
        wx.setStorageSync('key', value)  //添加本地存储
        wx.removeStorageSync
        wx.getStorageSync
        wx.clearStorageSync

    API--界面--导航栏
        wx.setNavigationBarTitle({})  //动态展示设置当前页面标题

    小程序npm
        npm init  //初始化
        构建npm

        pubsub.js  //消息订阅与发布
            npm i pubsub-js
            import PubSub from 'pubsub-js'

            订阅
                PubSub.subscribe('fun', () => {})

            发布
                PubSub.publish('fun', '参数')

        Moment.js
            专门处理日期时间的库
                npm i moment
                    moment(毫秒).format('mm:ss');

        flyio
            请求库

        jsonwebtoken
            加密库

    分包

    86-94 服务器

    