## HTML
    <!-- ol有序、ul无序、dl定义列表 -->
        <dl>
            <dt>xxx</dt>  //项目
            <dd>xxx</dd>  //描述项目
            <dd>xxx</dd>
        </dl>

    <!-- table表格 -->
        <table>  //一个表格
            <tr>  //一行
                <td></td>  //一列
            </tr>
        </table>

    <!-- form表单 -->
        <form action="">
            <label>账号：</label>  //标题
            <input type="text" disabled(不可修改)>           //text文本、password密码、
                                                            //submit提交按钮、radio单选、checkbox复选
                                                            //date日期、datetime-local日期和时间、
                                                            //number数字、range滑动条、time时间
                                                            //属性 autofocus自动获取焦点
            <textarea></textarea>  //文本框

            <select>  //下拉框
                <optgroup>  //下拉分组                                
                    <option value="男">男</option>
                    <option value="女">女</option>
                </optgroup>
                <datalist></datalist>  //预选列表
            </select>
        </form>

    <!-- 字符 -->
        &lt<;&gt>;

    <!-- 音频 -->
    <audio controls>
        <source src="horse.mp3" type="audio/mpeg">
    </audio>

    <!-- 视频 -->
    <video width="320" height="240" controls>
        <source src="movie.mp4" type="video/mp4">
    </video>

## Less
    npm i less less-loader@5
    weback.config.js
        module: {
            rules: [
                {
                    test: /\.less$/,
                    loader: 'style-loader!css-loader!less-loader'
                }
            ]
        }
    main.js
        import '../node_modules/less'

    # 注释
        以//开头的注释，不会编译到css文件中
        以/**/开头的注释会编译到css文件中

    # 变量
        声明变量
            属性值：@xxx：xxx；
            选择器：#@{xxxxx}
            url：@{url}

    # 嵌套
        &

    # 混合
        .class(@color){
            width: 100px;
            height: 100px;
            color: @color;
        }

        #ID{
            .class(red)
        }

    # 继承
        .color{
            color: red;
        }
        #ID2：(.color){
            .class(pink)
        }

## CSS2
    权重


    !important
    width: calc(100% - 150px);  //平分宽度
    line-height  //导致盒子变高
    <a href="#"></a>  //可做锚点使用
    overflow: hidden;  //溢出隐藏、scroll滚动条、auto自适应滚动条
    opacity: 0.5;  //透明度
    z-index: 1; //调整显示层级
    cursor: pointer;  //鼠标形状
    
    <!-- 表单 -->
    vertical-align: middle；  // 将图片或表单元素（行内块）和文字垂直居中

    <!-- 列表 -->
    list-style-type: none;  //清除列表默认样式
    list-style-image: url()
    list-style-position: 
    li::marker{content: '😅';}  //更改li前面的圆点

    <!-- 定位 -->
    position: absolute;  //绝对定位(父级)
    position: relative;  //相对定位(自身)
    position： flxed;   //广告定位
    position: sticky;  //粘性定位

    <!-- 输入框 -->
    outline: none;  //去除聚焦边框
    placeholder=""   //输入框显示文字
    resize: none;  //禁止文本框重置大小

    <!-- 背景 -->
    background: url() center no-repeat;  //以图换字,居中、图片不重复 
    background-color: red; //背景颜色
    background-image: url();  //背景图片
    background-repeat: no-repeat;  //平铺方式、repeat-x、repeat-y
    background: transparent;  //背景透明
    background-position:        //定位
    background-attachment:
    background-size:cover;  //背景图片尺寸  100% 100% 铺满比例
    background-origin: border-box、padding-box、content-box;  指定背景图片位置，边框区、padding区、内容区
    background-clip: border-box、padding-box、content-box;  从指定位置开始绘制背景图片

    <!-- 文本 -->
    text-indent: -100px;  //首行缩进
    text-align: center;  //文本对齐方式
    text-decoration:none;  //删除a标签下划线、underline增加下划线
    text-transform:uppercase;  //英文大写、lowercase;英文小写、capitalize;首字母大写
    line-height: 35px;  //字体行高（实际开发中常用line-height=height来垂直居中文字）
    font-size: 12px;  //字体大小
    font-style: italic/oblique     //斜体
    font-weight: 200;  //字体粗细
    color: red;  //字体颜色

    <!-- 空白字符/作用于空格和回车 -->
    white-space: normal;  //连续的空白符会被合并，换行符会被当作空白，宽度不够时会折行。
    white-space: nowrap;  //同normal，但不会折行。
    white-space: pre;  //连续的空白符会被保留，换行符、<br>也会引起换行，但不会折行。
    white-space: pre-wrap;  //同pre，但是会折行
    white-space: pre-line;  //同pre-wrap，但是连续的空白符会被合并

    <!-- 伪类 -->
    :before{}  //在元素之前插入内容
    :after{}  //在元素之后插入内容
    a:link{}  //未访问链接
    a:visited{}  //访问过的链接
    a:active{}  //正在活动的链接
    a:hover{}  //鼠标划过的状态

    :last-child  父元素的最后一个子元素
    :first-child  父元素的第一个子元素

    :not(selector)	:not(p)	选择所有p以外的元素
    :nth-child(n)	p:nth-child(2)	选择所有 p 元素的父元素的第二个子元素
    :nth-last-child(n)	p:nth-last-child(2)	选择所有p元素倒数的第二个子元素
    https://www.runoob.com/css/css-pseudo-classes.html

## Css3
    box-sizing: border-box;  //定义一个怪异盒模型
    
    <!-- 边框 -->
        border-radius：0 0 0 0;  //圆角
        
        border-image:url(border.png) 30 30 round;  //边界图片

    <!-- 渐变 -->
        线性渐变linear-gradient
            background-image: linear-gradient(direction/90deg, color1, rgba(255, 0, 0, 0.5), ...);
            background-image: repeating-linear-gradient(red, yellow 10%, green 20%);  重复线性渐变

        径向渐变radial-gradient
            background-image: radial-gradient(circle圆形/ellipse椭圆形, farthest at position,color);
            closest-side at 50% 50%  向最近边渐变
            farthest-side at 50% 50%  向最远边渐变
            closest-corner at 50% 50%  向最近角渐变
            farthest-corner at 50% 50%  向最圆角渐变 默认

            background-image: repeating-radial-gradient(red, yellow 10%, green 20%);  重复径向渐变

    <!-- 文本 -->
        text-shadow: 10px 10px 10px red;  x、y、z、color,阴影
        box-shadow：10px 10px 10px color;  //盒阴影
        // 单行文本溢出隐藏
            display: block;  //内联元素不生效
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis、clip;  ...展示、剪切

        // webkit内核浏览器专用方法多行溢出隐藏
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;  //行数
            -webkit-box-orient: vertical;  //对齐模式

    <!-- 换行/单词 -->
        单词换行
            word-break: normal;  //默认换行
            word-break: break-all;  //拆分换行
            word-break: keep-all;  //不拆分换行

        文本换行
            word-wrap: normal;  //默认
            word-wrap: break-word;  //长度超过一行的单词拆分换行

    <!-- 字体 -->
        @font-face{
            font-family: myFirstFont;
            src: url();
        }
        div{
            font-family: myFirstFont;
        }

    <!-- 2D/3D转换 -->
        transform: 
            rotate(0deg)翻转角度
            transfrom-origin: 0, 0;  //旋转中心角
            translate(X, Y)移动位置
            scale(2, 3)缩放元素大小的倍数(宽， 高)
            shew(10deg, 20deg);  X、Y轴倾斜角度
            matrix()方法将2D变换方法合并成一个，有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。

            matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)	定义 3D 转换，使用 16 个值的 4x4 矩阵。
            translate3d(x,y,z)	定义 3D 转化。
            translateX(x)	定义 3D 转化，仅使用用于 X 轴的值。
            translateY(y)	定义 3D 转化，仅使用用于 Y 轴的值。
            translateZ(z)	定义 3D 转化，仅使用用于 Z 轴的值。
            scale3d(x,y,z)	定义 3D 缩放转换。
            scaleX(x)	定义 3D 缩放转换，通过给定一个 X 轴的值。
            scaleY(y)	定义 3D 缩放转换，通过给定一个 Y 轴的值。
            scaleZ(z)	定义 3D 缩放转换，通过给定一个 Z 轴的值。
            rotate3d(x,y,z,angle)	定义 3D 旋转。
            rotateX(angle)	定义沿 X 轴的 3D 旋转。
            rotateY(angle)	定义沿 Y 轴的 3D 旋转。
            rotateZ(angle)	定义沿 Z 轴的 3D 旋转。
            perspective(n)	定义 3D 转换元素的透视视图。

    <!-- 过渡 -->
        transition: width 1s linear 1s;
            transition-property: width;  属性
            transition-duration: 1s;  过渡时间
            transition-timing-function: linear;  过渡动画
            transition-delay: 2s;  何时开始

    <!-- 动画 -->
        @keyframes myfirst{
            from{background: red;}
            to{background: yellow;}
            or
            0%   {background: red;}
            25%  {background: yellow;}
            50%  {background: blue;}
            100% {background: green;}
        }
        div{
            animation: myfirst 5s linear 0s ;
                animation-name: myfirst;  动画名字
                animation-duration: 5s;  动画时间
                animation-timing-function: linear;  速度曲线
                animation-delay: 2s;  何时开始 默认0
                animation-iteration-count: infinite;  播放次数无限播放 默认1
                animation-direction: alternate;  下一周期是否逆向播放  默认normal
                animation-play-state: running;  规定动画是否正在运行或暂停  paused暂停
        }

    <!-- 多列 -->
        columns: 100px 3;
        column-width: 100px;  指定列的宽度
        column-count: 3;  需要分隔的列数
        column-gap: 20px;  列与列之间的间隙
        column-rule: 1px solid color;
        column-span: all;  指定元素跨域多少列

    <!-- 用户界面 -->
        resize:both;  允许用户调整大小

        outline:2px solid red;
        outline-offset: 15px;  规定边框边缘之外 15 像素处的轮廓：

    <!-- 图片滤镜 -->
        https://www.runoob.com/cssref/css3-pr-filter.html

    <!-- 弹性盒子 -->
        display: flex;  //开启弹性盒子

        换行
            flex-wrap: nowrap|wrap|wrap-reverse|initial默认|inherit继承;  //换行方式，默认单行、多行、反转多行

        排列
            flex-direction: row | row-reverse | column | column-reverse;  //弹性盒子排列方式，默认横向左→右、反转，纵向上到下、反转

        属性应用在弹性容器上
            justify-content: flex-start | flex-end | center | space-between | space-around；  //横轴元素对齐方式，向前、向后、居中、平均、平均（两边有空隙）
            align-content: flex-start | flex-end | center | space-between | space-around;  //纵轴元素齐方式,头、尾、居中、平均、平均（两边有空隙）

        弹性子元素
            align-items: flex-start | flex-end | center | baseline（基线） | stretch（拉伸）;  //子元素在纵轴的对齐方式，头、尾、居中、基线、拉伸
            align-self: auto | flex-start | flex-end | center | baseline（基线） | stretch（拉伸）;  //子元素自身在横轴方向上的对齐方式，前、后、居中、基线、拉伸

            flex: auto | initial | none | inherit |  [ flex-grow ] || [ flex-shrink ] || [ flex-basis ];  //属性用于指定弹性子元素如何分配空间。
            
            order: -1;  //盒子排序，数值小往前排

    <!-- 视觉宽度 -->
        @media screen and (max-width: 699px) and (min-width: 520px){
            ul li a {
                padding-left: 30px;
                background: url(email-icon.png) left center no-repeat;
            }
        }
        all	用于所有多媒体类型设备
        print	用于打印机
        screen	用于电脑屏幕，平板，智能手机等。
        speech	用于屏幕阅读器

    <!-- 网格布局 -->
        display: grid or inline-grid;
        grid-template: '九宫格' 
        grid-template-columns: auto auto auto auto;  定义列的数量
        grid-template-rows: 100px 300px;  行的高度
        grid-gap: 10px 50px;  行和列的间隙

        设置网格元素列的开始与结束
        grid-colimn: 1 3;

        设置网格元素行的开始与结束
        grid-row: 1 3;

        简写
            grid-area: 1 / 2 / 5 / 6;  从第 1 行开始和第 2 列开始， 第 5 行和第 6 列结束