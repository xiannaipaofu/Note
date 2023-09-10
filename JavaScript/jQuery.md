## jQuery
    JS函数库，封装简化DOM操作
    https://www.runoob.com/jquery/jquery-tutorial.html
    npm i jquery

    $('选择器').操作()
        选择器
            p
            #id
            .class

    事件
        $('p'),click(function(){})

    显示隐藏
        $('').hide(1000, callback);
        $('').show(1000, callback);
        $('').toggle(1000, callback);  //切换显示与隐藏

    淡入淡出
        $('').fadeIn(1000, callback);  //淡入
        $('').fadeOut(1000, callback);  //淡出
        $('').fadeToggle(1000, callback);  //切换淡入淡出
        $('').fadeTo(1000, opacity, callback);  //渐变至透明度(slow、fast、10000, 0.5, callback)

    滑动
        $('').slideDown(1000, callback);  //向下滑动
        $('').slideUp(1000, callback);  //向上滑动
        $('').slideToggle(1000, callback);  //切换

    动画
        $('').animate({}, 1000, callback);  {变换的css属性}
        $('').stop();  //停止动画

    jquery链式调用
        $('p').slideDown().slideUp

    捕获元素
        $('').html(callback(a, b));  //设置或返回元素的内容及标签 a:当前元素下标，b:旧的元素文本内容
        $('').text(callback(a, b));  //设置或返回元素的文本内容
        $('').val(callback(a, b));  //设置或返回元素的表单值

    修改属性值
        $('').attr('属性名', newValue/callback(a, b));

    添加元素
        $('').append('text');  //在元素结尾追加内容
        $('').prepend('text');  //在元素开头追加内容
        $('').after()  //在元素之后插入内容
        $('').before()  //在元素之前插入内容

    删除元素
        $('').remove();  //删除被选元素
        $('').empty();  //删除被选元素的子元素

    操作CSS
        $('.off').addClass('active')  //添加类名
        $('.on').removeClass('active')  //删除类名
        $('.on').toggleClass('active')  //切换添加删除类名
        $('').css()  //设置或返回css属性

    尺寸
        https://www.runoob.com/jquery/jquery-dimensions.html

    遍历
        $('').parent()  返回元素的父元素
        $('').children()  返回元素的所有直接子元素
        $('').find('span')  返回元素的所有后代子元素
        $('').siblings()  返回元素的所有兄弟元素
        $('').next()  返回元素的下一个兄弟元素
        $('').nextAll()  元素的后的所有兄弟元素
        $('').first()  选中元素的第一个元素
        $('').last()  选中元素的最后一个元素
        $('').eq(0)  选中元素的指定索引号元素
        $('').fiter('xxx')  过滤不匹配的元素
        $('').not  与fiter互逆

    $(this).prop('src', '../xxx');  //调用该对象的内置属性
    $(this).trim();  //用于去除字符串两端的空白字符

    const data = $('form').serialize()   // 采集用户信息
    const data = $('form').serializeArray();  //获取表单所有键值对

    #ajax
        $.get( url [, data ] [, callback ] [, dataType ] )
        $.post(url [, data ] [, callback ] [, dataType ] )
