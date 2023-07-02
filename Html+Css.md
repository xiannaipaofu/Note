## HTML
    超文本标记语言: HyperText Markup Language

    <map></map>  地图

    <!-- button按钮 -->
        type='button|submit|reset'

     <!-- input输入框 -->
            <input type="text">  
                type='text|password|number|'
                    radio|checkbox  checked 默认选中
                    color颜色
                    range滑动条
                    file上传文件  accept='audio|video|image' 规定文件类型 multiple 允许上传多个文件
                    image显示图片 alt='' 图像提交文本 width='' 宽度 height
                    date年月日
                    datetime-local年月日-当地时间
                    time时间
                    month年月
                    week年周
                name=''  元素名称
                value=''  指定默认值
                placeholder=''  占位符
                autofocus  页面加载时自动获取焦点
                disabled  禁止
                autocomplete='on|off'  开启自动填充内容
                from=''  规定所属哪个表单
                max=''  最大值
                min=''  最小值
                maxlength=''  最长字符
                pattern=''  规定正则
                readonly  设置为只读
                required  设置必填
                size=''  可见宽度
                step=''  设置数字间隔

    <!-- table表格 -->
        <table border='1'>  //一个表格
            <tr>
                <th></th>  表头(有居中效果)  属性: colspan='2'  横跨列数  rowspan='2' 纵跨行数
            </tr>
            <tr>  //一行
                <td></td>  //一列  属性: colspan='2'  横跨列数  rowspan='2' 纵跨行数
            </tr>
        </table>

    <!-- ol/ul/dl列表 -->
        <ol>  属性: type='1|a|A|i|I|' start='1' reversed逆序
            <li></li>
        </ol>

        <ul>
            <li></li>
        </ul>

        <dl>
            <dt></dt>  表头
            <dd></dd>  列表
        </dl>

    <!-- form表单 -->
        <form>
            action='url'  发送请求
            method=''  请求类型
            name=''
            enctype='application/x-www-form-urlencoded|multipart/form-data|text/plain'  规定发送表单数据之前对其进行编码
            novalidate  提交表单不进行验证
            target='_self'  在何处打开action url

            <label>账号：</label>  //标题
        </form>

    <!-- textarea文本域 -->
        <textarea></textarea>

    <!-- select下拉框 -->
        <select>
            <optgroup label='性别'>下拉分组                                
                <option value="男">男</option>
                <option value="女">女</option>
                    selected 默认选项
            </optgroup>
            
        </select>

    <!-- fieldset表格分组 -->
        <fieldset>
            <legend>Personalia:</legend>
            Name: <input type="text">
        </fieldset>

    <!-- label标签 -->
        for='name'	规定哪个表单元素绑定

    <!-- 字符 -->
        https://www.runoob.com/html/html-entities.html
        &lt<;&gt>;

    ## HTML5
        <!-- 预选列表 -->
            <input type="text" list="ageList">
            <datalist id="ageList">预选列表
                <option value="男">男</option>
                <option value="女">女</option>
            </datalist>

        <!-- 音频 -->
            <audio>
                src
                autoplay 自动播放
                controls 音频控件
                loop 循环播放
                muted 静音
                preload='auto|metadata|none' 规定当网页加载时，音频是否默认被加载以及如何被加载。

                <source src="horse.mp3" type="audio/mpeg"> 多文件配置
            </audio>

        <!-- 视频 -->
            <video width="320" height="240">
                poster="./public/347075.jpg"  主界面图
                <source src="movie.mp4" type="video/mp4">
            </video>

        # HTML 音频/视频 DOM 参考手册
        https://www.runoob.com/tags/ref-av-dom.html

        <!-- canvas图形 -->
            https://www.runoob.com/html/html5-canvas.html

        <!-- SVG可缩放矢量图形 -->
            https://www.runoob.com/html/html5-svg.html

        <!-- 拖放 -->
            https://www.runoob.com/html/html5-draganddrop.html

        <!-- 地理位置 -->
            https://www.runoob.com/html/html5-geolocation.html


## CSS2
    拾色器
        https://www.runoob.com/tags/html-colorpicker.html
        
    width: calc(100% - 150px);  //平分宽度
    <a href="#"></a>  //可做锚点使用
    overflow: hidden;  //溢出隐藏、scroll滚动条、auto自适应滚动条
    opacity: 0.5;  //透明度
    z-index: 1; //调整显示层级
    cursor: pointer;  //鼠标形状
    vertical-align: 9px;  调整基线
        label{
            width: 100px;
            height: 30px;
            display: inline-block;
            text-align: justify;
            overflow: hidden;
            &::after{
                width: 100%;
                display: inline-block;
                content: '';
            }
        }  两端对齐
    
    <!-- 表单 -->
    vertical-align: middle；  // 将图片或表单元素（行内块）和文字垂直居中

    <!-- 列表 -->
    list-style-type: none;  //清除列表默认样式
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
    background: url() center no-repeat;  //以图换字,居中，图片不重复、repeat-x、repeat-y
    background: transparent;  //背景透明
    background-size:cover;  //背景图片尺寸  100% 100% 铺满比例

    <!-- 文本 -->
    text-indent: -100px;  //首行缩进
    text-decoration:none;  //删除a标签下划线、underline增加下划线
    text-transform:uppercase;  //英文大写、lowercase;英文小写、capitalize;首字母大写
    font-style: italic/oblique     //斜体
    font-weight: 200;  //字体粗细

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
    <!-- 边框 -->
        border-radius：0 0 0 0;  //圆角

    <!-- 渐变 -->
        线性渐变linear-gradient
            background-image: linear-gradient(direction/90deg, color1, rgba(255, 0, 0, 0.5), ...);
            background-image: repeating-linear-gradient(red, yellow 10%, green 20%);  重复线性渐变

        径向渐变radial-gradient
            background-image: radial-gradient(circle圆形/ellipse椭圆形, [farthest at position],color);
            closest-side at 50% 50%  向最近边渐变
            farthest-side at 50% 50%  向最远边渐变
            closest-corner at 50% 50%  向最近角渐变
            farthest-corner at 50% 50%  向最远角渐变 默认

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
            transition-property: width;  属性 or all
            transition-duration: 1s;  过渡时间
            transition-timing-function: linear;  过渡动画linear|ease|ease-in|ease-out|ease-in-out|cubic-bezier(n,n,n,n);
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

## Less
    @name: bule;
    div{
        color: @name;
    }

    # 变量
        声明变量
            属性值：@xxx：xxx；
            选择器：#@{xxxxx}
            url：@{url}

    # 混合
        div(@color){
            width: 100px;
            height: 100px;
            color: @color;
        }

        #ID{
            .class(red)
        }

    # 继承
        div{
            color: red;
        }
        div2:extend(div){
            width: 100px;
        }

## Sass
    https://www.sass.hk/
    Live Sass Compiler扩展
        配置
        // 定制样式
        "liveSassCompile.settings.formats":[
            // This is Default.
            {
                "format": "expanded",  //可定制的出口css样式（expanded展开格式、compact紧凑格式、compressed压缩格式、nested嵌套格式）
                "extensionName": ".css",
                "savePath": null  //为null，表示当前目录
            }
        ],
        // 排除目录
        "liveSassCompile.settings.excludeList": [
            "/**/node_modules/**",
            "/.vscode/**"
        ],
        //是否添加兼容前缀 例如：-webkit- -moz- ...等
        "liveSassCompile.settings.autoprefix": [
            "> 1%",
            "last 2 versions"
        ]

    语法扩展
        font-size: 16px;
        font-family: sans-serif;

        font: {
            size: 16px;
            family: sans-serif;
        }

    定义变量
        $color: red;

        div {
            color: $color;
            $width: 50px !global;  //全局变量
        }

    导入
        _pubilc.scss
        @import 'url';

    混合
        @mixin name{

        }
        @mixin name($a, $b, $c:10px){
            width: $a;
            height: $b;
            font-size: $c;
        }

        div{
            @include name;
        }
        div{
            @include name(10px, 20px);
        }

    继承
        @extend %class

    占位符
        必须配合继承使用
        %class

    运算
        and与、or或、not非
        @if 条件 {

        }
        @else {

        }
        三元表达式
            color: if(条件, true, false)

    插值语法
        #{$width}

    函数
        @function name(){
            @return
        }
        name();

    @for
        to 包含start不包含end
        through 包含start与end的值
        @for $i from 1 to 4{
            .p#{$1} {

            }
        }
