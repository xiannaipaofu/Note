## HTML
    超文本标记语言: HyperText Markup Language

### 标签:
    <base>  // 定义页面中所有链接默认的链接目标地址
    // 描述HTML文档的描述，关键词，作者，字符集等
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  // 移动端适配
    // 定义了HTML文档的标题
    <title>Document</title>
    // 引入外部资源
    <link rel="stylesheet" href="../index.css">
    <link rel="stylesheet" href="./audio.css">
    <style></style>  // 样式
    <script>  定义了客户端脚本
    <noscript>  定义了不支持脚本浏览器输出的文本

    <b></b>  // 粗体文本
    <strong></strong>  // 加重语气
    <em></em>  // 着重文字
    <i></i>  // 斜体
        
    <!-- button -->
        <button></button>
            type='button|submit|reset'  // 默认值submit

    <!-- input输入框 -->
        <input type="text">  
            type=''
                text
                password
                number
                radio|checkbox  checked 默认选中
                file上传文件  accept='audio|video|image' 规定文件类型 multiple 允许上传多个文件
                image显示图片 src='' alt='' 图像提交文本 width='' height=''
            name=''  元素名称
            value=''  指定默认值
            disabled  禁止
            readonly  设置为只读
            maxlength=''  最长字符
            size=''  可见宽度
            from='formId'  规定所属哪个表单

    <!-- form表单 -->
        <form>
            属性:
                action='url'  发送请求
                method=''  请求类型
                name=''
                enctype=''  规定发送表单数据之前对其进行编码
                    application/x-www-form-urlencoded
                    multipart/form-data
                    text/plain
                target=''  在何处打开action url
                    _self  在同一框架中打开（默认）
                    _blank  在新窗口/选项卡中打开
                    _parent  在父框架中打开
                    _top  在整个窗口中打开
                    framename  在指定的 iframe 中打开
        </form>

    <!-- table表格 -->
        <table border='1'>
            <caption>Monthly savings</caption>  // 定义表格标题
            // 对表格中的列进行组合
            <colgroup>  
                <col span="2" style="background-color:red">
                <col style="background-color:yellow">
                属性:
                    span='2'  // 规定列组应该横跨的列数
            </colgroup>
            // 行
            <tr>
                // 列(表头)
                <th></th>
                属性:
                    colspan='2'横跨列数
                    rowspan='2'纵跨行数
            </tr>
            <tr>
                <td></td>
            </tr>
        </table>

    <!-- <label></label>定义标签 -->
        for='name'	规定哪个表单元素绑定
        
    <!-- select下拉菜单 -->
        <select>
            // 定义选项组
            <optgroup label="German Cars">
                // 下拉选项
                <option value="mercedes">Mercedes</option>
                <option value="audi">Audi</option>
            </optgroup>
            <option value="mercedes">Mercedes</option>
            <option value="audi">Audi</option>
                属性:
                    disabled  规定此选项应在首次加载时被禁用。
                    label  定义当使用 <optgroup> 时所使用的标注。
                    selected  规定选项（在首次显示在列表中时）表现为选中状态。
                    value  定义送往服务器的选项值。
        </select>
            属性:
                autofocus  规定在页面加载时下拉列表自动获得焦点
                disabled  当该属性为 true 时，会禁用下拉列表
                multiple  当该属性为 true 时，可选择多个选项
                required  规定用户在提交表单前必须选择一个下拉列表中的选项
                size  规定下拉列表中可见选项的数目

    <!-- textarea文本域 -->
        <textarea></textarea>

    <!-- fieldset表格分组 -->
        <fieldset>
            <legend>Personalia:</legend>  // 表格标题
            Name: <input type="text">
        </fieldset>

    <!-- map地图 -->
        <map>
            <area></area>  // 带有可点击区域的图像映射
        </map>

    属性:
        id='HOME'
        class='home'
        style='color: pink;'
        name='home'

## HTML5
    元素:
    https://www.runoob.com/html/html5-new-element.html

    <form>新属性：
        autocomplete  // 自动填充 on/off
        novalidate  // 设置表单不进行表单验证true/false

    <input>新属性：
        autocomplete  // 自动填充 on/off
        autofocus  // 自动获取焦点
        placeholder  // 占位符
        pattern (regexp)  // 规定正则
        required  // 必填
        step  // 规定数字间隔
        height 与 width
            type='image'
        list
            list='datalistId'  配合预选列表使用
        min 与 max
            适用于以下类型的 <input> 标签：date pickers、number 以及 range
        multiple  // 选择多个值
            type='file|email'

    <datalist>预选列表:
        <input type="text" list="ageList">
        <datalist id="ageList">预选列表
            <option value="男">男</option>
            <option value="女">女</option>
        </datalist>

    <progress>进度条:
        <progress value="22" max="100"></progress>  
            max  规定需要完成的值
            value  规定进程的当前值

    属性:
    data-name='value'
        event.target.dataset
        event.target.getAttribute('data-name')

### HTML 音频/视频 DOM 参考手册API
    https://www.runoob.com/tags/ref-av-dom.html

    <!-- 音频 -->
    <audio
        src
        autoplay 自动播放
        controls 音频控件
        loop 循环播放
        muted 静音
        preload='auto|metadata|none' 规定当网页加载时，音频是否默认被加载以及如何被加载。
    >
        <source src="horse.mp3" type="audio/mpeg|audio/ogg|audio/wav"> 多文件配置
    </audio>

    <!-- 视频 -->
    <video
        width="320"
        height="240"
        poster="./public/347075.jpg"  主界面图
    >
        <track></track> // 定义在媒体播放器文本轨迹(字幕)
        <source src="movie.mp4" type="video/mp4|video/webm|video/ogg">
    </video>

    属性:
        src  设置或返回音频/视频元素的当前来源  url
        currentSrc  返回当前音频/视频的URL  url
        autoplay  设置或返回是否自动播放  true/false
        loop  设置或返回是否循环播放  true/false
        controls  设置或返回是否显示控件  true/false
        paused  设置或返回是否暂停  true/false
        muted  设置或返回是否静音  true/false
        defaultMuted  设置或返回默认是否静音  true/false
        volume  设置或返回音量  number
        playbackRate  设置或返回播放的速度  number
        defaultPlaybackRate  设置或返回默认播放速度  number
        duration  返回当前音频/视频的长度（以秒计）  number
        currentTime  设置或返回音频/视频中的当前播放位置（以秒计）  number
        ended  返回音频/视频的播放是否已结束  true/false
        seeking  返回用户是否正在移动/跳跃到音频/视频中的新位置  true/false

        preload  设置或返回音频/视频是否应该在页面加载后进行加载
            auto  指示一旦页面加载，则开始加载音频/视频
            metadata  指示当页面加载后仅加载音频/视频的元数据
            none  指示页面加载后不应加载音频/视频
        readyState  返回音频/视频当前的就绪状态
            0 = HAVE_NOTHING - 没有关于音频/视频是否就绪的信息
            1 = HAVE_METADATA - 关于音频/视频就绪的元数据
            2 = HAVE_CURRENT_DATA - 关于当前播放位置的数据是可用的，但没有足够的数据来播放下一帧/毫秒
            3 = HAVE_FUTURE_DATA - 当前及至少下一帧的数据是可用的
            4 = HAVE_ENOUGH_DATA - 可用数据足以开始播放
        mediaGroup  设置或返回音频/视频所属的组合（用于连接多个音频/视频元素）  ?
            audio.mediaGroup = 'text'
        networkState  返回音频/视频的当前网络状态  1
            0 = NETWORK_EMPTY - 音频/视频尚未初始化
            1 = NETWORK_IDLE - 音频/视频是活动的且已选取资源，但并未使用网络
            2 = NETWORK_LOADING - 浏览器正在下载数据
            3 = NETWORK_NO_SOURCE - 未找到音频/视频来源
        crossOrigin  设置或返回音频/视频的 CORS 设置  ?
        seekable  返回表示音频/视频可寻址部分的 TimeRanges 对象
            length - 获得音频/视频中可寻址范围的数量
            start(index-1) - 获得可寻址范围的开始位置
            end(index-1) - 获得可寻址范围的结束位置
        played  返回表示音频/视频已播放部分的 TimeRanges 对象
            let index = audio.played.length
            audio.played.length  // 获得音频/视频中已播范围的数量
            audio.played.start(index-1)  // 获得某个已播范围的开始位置
            audio.played.end(index-1)  // 获得某个已播范围的结束位置
        buffered  返回表示音频/视频已缓冲部分的 TimeRanges 对象
            length - 获得音频/视频中已缓冲范围的数量
            start(index) - 获得某个已缓冲范围的开始位置
            end(index) - 获得某个已缓冲范围的结束位置
        textTracks  返回表示可用文本轨道的 TextTrackList 对象
            TextTrackList 对象	表示音频/视频的可用文本轨道。
                length - 获得音频/视频中可用的文本轨道的数量
                [index] - 根据下标 index 来获得 TextTrack 对象
                注释：第一个可用文本轨道的下标 index 是 0。
            TextTrack 对象	表示一个文本轨道
                kind - 获得文本轨道的类型（可以是 "subtitles"、"caption"、"descriptions"、"chapters" 或者 "metadata"）
                label - 获得文本轨道的标签
                language - 获得文本轨道的语言
                mode - 获得或设置该轨道是否是活动的（"disabled"|"hidden"|"showing"）
                cues - 获得 TextTrackCueList 对象的 cues 列表
                activeCues - 获得 TextTrackCueList 对象形式的当前活动文本轨道 cues
                addCue(cue) - 向 cues 列表添加一个 cue
                removeCue(cue) - 从 cues 列表删除一个 cue

        error  返回表示音频/视频错误状态的 MediaError 对象  (只有IE9支持)
            audio.error.code
        
    方法:
        audio.play()  // 播放媒介
        audio.pause() // 暂停播放媒介
        audio.load()  // 重新加载媒介
        addTextTrack()  // 向音频/视频添加新的文本轨道
        canPlayType()  // 检测浏览器是否能播放指定的音频/视频类型。

    事件:
        // 提示视频已开始加载
        audio.onloadstart = ()=>{console.log('loadstart')}
        // 提示视频的时长已改变（NaN→实际时长）
        audio.ondurationchange = ()=>{console.log('durationchange')}
        // 提示视频的元数据已加载
        audio.onloadedmetadata = ()=>{console.log('loadedmetadata')}
        // 提示当前帧的数据是可用的
        audio.onloadeddata = ()=>{console.log('loadeddata')}
        // 提示视频正在下载中
        audio.onprogress = ()=>{console.log('progress')}
        // 提示该视频已准备好开始播放
        audio.oncanplay = ()=>{console.log('canplay')}
        // 提示视频能够不停顿地一直播放
        audio.oncanplaythrough = ()=>{console.log('canplaythrough')}

        onplay  当音频/视频已开始或不再暂停时触发
        onpause  当音频/视频已暂停时触发
        onvolumechange  当音量已更改时触发
        onratechange  当音频/视频的播放速度已更改时触发
        ontimeupdate  当目前的播放位置已更改时触发

        onplaying  当音频/视频在因缓冲而暂停或停止后已就绪时触发
        onwaiting  当视频由于需要缓冲下一帧而停止时触发
        onseeking  当用户开始移动/跳跃到音频/视频中的新位置时触发
        onseeked  当用户已移动/跳跃到音频/视频中的新位置时触发
        
        onended  当目前的播放列表已结束时触发
        onemptied  当目前的播放列表为空时触发

        onabort  当音频/视频的加载已放弃时触发
        onsuspend  当浏览器刻意不获取媒体数据时触发

        onstalled  当浏览器尝试获取媒体数据，但数据不可用时触发
        onerror  当在音频/视频加载期间发生错误时触发
        
        onreadystatechange  当就绪状态（ready-state）改变时运行脚本
        onseeked  当媒介元素的定位属性 [1] 不再为真且定位已结束时运行脚本

### canvas图形
    https://www.runoob.com/html/html5-canvas.html
    https://www.runoob.com/tags/ref-canvas.html

    弧度
        360/(2*Math.PI)=弧度

    必须指定宽高
        <canvas id='charts' width='800' height='800'></canvas>

    样式:
        需在绘制之前设置

    <canvas id="CANVAS" width="800" height="600"></canvas>
    
    const canvas = document.querySelector('#CANVAS')  // 获取元素
    const ctx = canvas.getContext('2d')  // 获取画布的笔(上下文)

    颜色、样式和阴影ctx.
        属性:
            fillStyle  设置或返回用于填充绘画的颜色、渐变或模式
            strokeStyle  设置或返回用于线段的颜色、渐变或模式

            shadowColor  设置或返回用于阴影的颜色
            shadowBlur  设置或返回用于阴影的模糊级别
            shadowOffsetX  设置或返回阴影与形状的水平距离
            shadowOffsetY  设置或返回阴影与形状的垂直距离

        方法:
            createLinearGradient()	创建线性渐变（用在画布内容上）
            createRadialGradient()	创建放射状/环形的渐变（用在画布内容上）
            addColorStop()	规定渐变对象中的颜色和停止位置

            createPattern()	在指定的方向上重复指定的元素

            创建线条渐变ctx.createLinearGradient(x, y, x1, y1) 
                // x、y: 开始线性渐变起始坐标
                // x1、y1: 开始线性渐变结束坐标
                let grd = ctx.createLinearGradient(0, 0, 800, 600)  // 创建线条渐变
                grd.addColorStop(0, 'pink')  // 指定颜色停止，参数使用坐标来描述，可以是0至1
                grd.addColorStop(1, 'white')
                ctx.fillStyle = grd
                ctx.fillRect(110, 300, 100, 250)

                createRadialGradient(x,y,r,x1,y1,r1)  // 创建一个径向/圆渐变

    线条样式ctx.
        属性
            lineWidth  设置或返回当前的线条宽度

            lineCap  设置或返回线条的结束端点样式
            lineJoin  设置或返回两条线相交时，所创建的拐角类型
            miterLimit  设置或返回最大斜接长度

    矩形ctx.
        方法
            rect()  创建矩形
            fillRect()  绘制"被填充"的矩形
            strokeRect()  绘制矩形（无填充）
            clearRect(x, y, w, h)  在给定的矩形内清除指定的像素

            绘制矩形(描边)ctx.strokeRect(x, y, width, height)
                ctx.strokeRect(300, 300, 100, 100)
            绘制矩形(填充颜色)ctx.fliiRect(x, y, width, height)
                ctx.fillRect(300, 300, 100, 100)

    路径ctx.
        方法
            moveTo(x, y)  把路径移动到画布中的指定点，不创建线条
            lineTo(x, y)  添加一个新点，然后在画布中创建从该点到最后指定点的线条
            closePath()  创建从当前点回到起始点的路径
            fill()  填充当前绘图（路径）
            stroke()  绘制已定义的路径

            beginPath()  起始一条路径，或重置当前路径
            arc()  创建弧/曲线（用于创建圆形或部分圆）
            arcTo()  创建两切线之间的弧/曲线
                绘制圆形ctx.arc(x, y, radius, starAngle, endAngle, anticlockwise:true/false)
                    x: 圆心x坐标
                    y: 圆心y坐标
                    radius: 园半径
                    starAngle: 开始绘制弧度
                    endAngle: 结束绘制弧度
                    anticlockwise: 是否逆向
                ctx.beginPath()  // 绘制圆形
                ctx.arc(100, 100, 100, 0, 2*Math.PI, false)

            clip()  从原始画布剪切任意形状和尺寸的区域
            quadraticCurveTo()  创建二次贝塞尔曲线
            bezierCurveTo()  创建三次贝塞尔曲线
            isPointInPath()  如果指定的点位于当前路径中，则返回 true，否则返回 false

    转换
        方法
            scale()  缩放当前绘图至更大或更小
            rotate()  旋转当前绘图
            translate()  重新映射画布上的 (0,0) 位置
            transform()  替换绘图的当前转换矩阵
            setTransform()  将当前转换重置为单位矩阵。然后运行 transform()

    文本
        属性
            font='20px 微软雅黑'  设置或返回文本内容的当前字体属性
            textAlign  设置或返回文本内容的当前对齐方式
            textBaseline  设置或返回在绘制文本时使用的当前文本基线

        方法
            fillText('数据可视化', x, y)  在画布上绘制"被填充的"文本
            strokeText(text,x,y)  在画布上绘制文本（无填充）
            measureText()  返回包含指定文本宽度的对象

    图像绘制
        方法
        drawImage()  向画布上绘制图像、画布或视频

    像素操作
        属性
        width  返回 ImageData 对象的宽度
        height  返回 ImageData 对象的高度
        data  返回一个对象，其包含指定的 ImageData 对象的图像数据

        方法
            createImageData()  创建新的、空白的 ImageData 对象
            getImageData()  返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据
            putImageData()  把图像数据（从指定的 ImageData 对象）放回画布上

    合成
        属性
        globalAlpha  设置或返回绘图的当前 alpha 或透明值
        globalCompositeOperation  设置或返回新图像如何绘制到已有的图像上

    其他
        方法
            save()  保存当前环境的状态
            restore()  返回之前保存过的路径状态和属性
            createEvent()	 
            getContext()	 
            toDataURL()

### SVG可缩放矢量图形
    https://www.runoob.com/html/html5-svg.html
    <svg id="SVG">
        <!-- 
            stroke=''  线段颜色
            stroke-width=''  线段宽度
            fill=''  填充颜色
            fill-opacity=''  填充透明度
        -->
        <!-- 
            矩形<rect>
            圆形<circle>
            椭圆<ellipse>
            线<line>
            折线<polyline>
            多边形<polygon>
            路径<path>
         -->
        <!-- 直线 -->
            <line x1="100" y1="100" x2="200" y2="200" stroke="red"></line>

        <!-- 折线 -->
            <polyline points="200 200, 300 200, 400 400" stroke="red" fill-opacity="0.5"></polyline>

        <!-- 矩形 -->
            <rect x="100" y="100" width="100" height="100" fill="pink"></rect>

        <!-- 圆 -->
            <circle cx="50" cy="50" r="50" stroke="pink" fill="skyblue"></circle>

        <!-- 圆或椭圆 -->
        <!-- 
            cx="150" cy="50"  圆心坐标
            rx="150"  x轴半径
            ry="50"  y轴半径
        -->
        <ellipse cx="150" cy="50" rx="50" ry="50" fill="skyblue"></ellipse>

        <!-- 多边形 -->
            <polygon points="0 0, 10 20, 30 30" stroke="red"></polygon>

        <!-- 任意图形 -->
        <!-- 
            M 移动到初始位置
            L 画线
            Z 将结束和开始点闭合
        -->
            <path d="
                M 100 0
                L 100 200
                L 150 500
                L 200 200
                Z 300 0
            ">
            </path>

        <!-- 文本<text> -->
    </svg>

### 地图
    https://www.runoob.com/html/html5-geolocation.html

## 字符集
    https://www.runoob.com/charsets/html-charsets.html
        <  &lt;  
        >  &gt;

## XML
    可扩展标记语言（EXtensible Markup Language）
    https://www.runoob.com/xml/xml-tutorial.html

## <!--  -->
### HTML
    元素:
    <!-- fieldset定义了一组相关的表单元素，并使用外框包含起来 -->
        <fieldset>
            <legend>Personalia:</legend>  // 定义了 <fieldset> 元素的标题
            Name: <input type="text"><br>
        </fieldset>

    <!-- object嵌入对象 -->
        标签用于包含对象，比如图像、音频、视频、Java applets、ActiveX、PDF 以及 Flash
        <object width="400" height="400" data="helloworld.swf">
                data  // 对象url
                form  // 所属表单
                height  // 
                width  //
                name  // 
                type  // 规定的数据的 MIME 类型
                usemap  // 规定与对象一同使用的客户端图像映射的名称
            <param name='autoplay' value='true'></param>
        </object>

    <!-- param -->
        为包含它的 <object> 标签提供参数
        <param name='autoplay' value='true'></param>
            name  // 定义参数名称
            value  // 描述参数值

    <!-- <iframe></iframe> -->
        一个内联框架被用来在当前 HTML 文档中嵌入另一个文档。
        height  规定 <iframe> 的高度。
        name  规定 <iframe> 的名称。
        sandbox  对<iframe> 的内容定义一系列额外的限制。
            'allow-forms'
            'allow-same-origin'
            'allow-scripts'
            'allow-top-navigation'	
        seamlessNew	seamless	规定 <iframe> 看起来像是父文档中的一部分。
        src	URL	规定在 <iframe> 中显示的文档的 URL。
        srcdocNew	HTML_code	规定页面中的 HTML 内容显示在 <iframe> 中。
        width	pixels	规定 <iframe> 的宽度。

    属性:
    accesskey='b'  // 设置访问元素的快捷键
        <a href="//www.runoob.com/html/html-tutorial.html" accesskey="b"></a>

### HTML5
    元素:
    <keygen name='mycookie'>  // 生成密钥

    <output>定义一个计算结果:
        <form oninput="x.value=parseInt(a.value)+parseInt(b.value)">
            0<input type="range" id="a" value="50">100
            +<input type="number" id="b" value="50">
            =<output name="x" for="a b"></output>
                属性:
                for  描述计算中使用的元素与计算结果之间的关系。
                name  定义对象的唯一名称（表单提交时使用）
        </form>
    
    <details>定义一个可见的标题,当用户点击标题时会显示出详细信息:
        <details>
            <summary>Copyright 1999-2011.</summary>
            <p> - by Refsnes Data. All Rights Reserved.</p>
            <p>All content and graphics on this web site are the property of the company Refsnes Data.</p>
        </details>

    <figure>给图片定义标题:
        <figure>
            <img decoding="async" src="img_pulpit.jpg" alt="The Pulpit Rock" width="304" height="228">
            <figcaption>Fig1. - A view of the pulpit rock in Norway.</figcaption>
        </figure>

    <meter>定义度量衡,仅用于已知最大和最小值的度量:
        <meter vlaue='num'></meter>
            highNew	number	规定被界定为高的值的范围
            lowNew	number	规定被界定为低的值的范围
            maxNew	number	规定范围的最大值
            minNew	number	规定范围的最小值
            optimumNew	number	规定度量的最优值

    <ruby>显示拼音(注释):
        <ruby>  
            汉 <rp>(</rp><rt>Han</rt><rp>)</rp>
            字 <rp>(</rp><rt>zi</rt><rp>)</rp>
        </ruby>

    属性:
    contenteditable="true|false"  // 指定元素是否可编辑

    draggable="true|false|auto"  // 设置元素是否可拖动

#### 拖放
    https://www.runoob.com/html/html5-draganddrop.html

#### MathML
    数学标记语言，是一种基于XML（标准通用标记语言的子集）的标准，用来在互联网上书写数学符号和公式的置标语言

#### WebSocket
    HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议(Ajax)

#### SSE服务器发送事件(Server-Sent Events)
    Server-Sent 事件指的是网页自动获取来自服务器的更新

#### Web Workers
    web worker 是运行在后台的 JavaScript，不会影响页面的性能

#### Web SQL 数据库


    