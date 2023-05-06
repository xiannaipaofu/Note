## ajax
    信息响应(100–199)，成功响应(200–299)，重定向(300–399)，客户端错误(400–499)和服务器错误 (500–599)：
    200 - 请求成功，301 - 资源（网页等）被永久转移到其它URL，404 - 请求的资源（网页等）不存在，500 - 内部服务器错误
    https://www.runoob.com/http/http-status-codes.html

    # 请求报文
        行      GET/POST（请求类型）    /s?ie=utf-8（url路径）     HTTP/1.1（协议版本）
        头      Host: atguigu.com（告知服务器请求体类型）
                Cookie: name=guigu
                Content-type: application/x-www-from-urlencoded
                User-Agent: chrome 83
        空行
        体      username=admin&password=admin(get请求此处为空，post请求可以不为空)

    # 响应报文
        行      HTTP/1.1(协议版本)      200（响应状态码）       OK（响应状态字符串）
        头      Content-Type: text/html;charset=utf-8（类型）(对响应体做相关描述) https://www.runoob.com/http/http-header-fields.html
                Content-length: 2048（长度）
                Content-encoding: gzip（压缩类型）
        空行
        体      
                <html>
                    <head>
                    </head>
                    <body>
                        <h1>尚硅谷</h1>
                    </body>
                </html>

    # 发送AJAX
        xhr = new XMLHttpRequest();  // 创建对象
    
        <!-- xhr.timeout = 2000;  // 网络超时设置、回调 -->
        <!-- xhr.ontimeout = function(){
            alert('网络超时啦...')
        }; -->
    
        <!-- xhr.onerror = function(){  // 网络异常回调
            alert('网络崩溃了')
        }; -->
    
        <!-- xhr.responseType = 'json';  // 设置响应体数据的类型(自动转换) -->
    
        xhr.open('get', 'http://127.0.0.1:8000/server?a=100&b=200');  //设置请求方法和url
    
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');  // 设置请求头
        <!-- xhr.setRequestHeader('name','atguigu'); -->
    
        xhr.send();  // 发送,xhr.send('xxxx');  post方式传递参数
        
        xhr.onreadystatechange = function(){
            if(xhr.readyState === 4){
                    // 判断响应状态码 200 404（找不到） 403（forbidden被禁止） 401（未授权） 500（内部错误）
                    if(xhr.status >= 200 && xhr.status < 300){
                        // 处理结果 行 头 空行 体
                        console.log(xhr.status);//状态码
                        console.log(xhr.statusText);//状态字符串
                        console.log(xhr.getAllResponseHeaders());//所有的响应头
                        console.log(xhr.response);//响应体
                        var res = JSON.parse(xhr.responseText)//响应体文本格式
                    }else{

                    }
                }
            }
        <!-- // xhr.onload = function(){} //响应接收完毕 -->

    # 解决跨域
        # JSONP
            1.非官方的跨域解决方案，只支持get请求

            2.利用img、link、iframe、script标签的跨域能力来发送请求

            3.使用
                创建标签、设置src、设置回调、插入标签

        # CORS跨域资源共享
            Access-Control-Allow-Origin  //允许跨域
            Access-Control-Allow-Headers  //允许请求头自定义
            Access-Control-Allow-Method  //配置请求类型

        # 代理服务器
            devServer:{
                proxy:{
                    '/api':{
                        target:'<url>',
                        // pathRewrite:{'^/api':''},//重写路径
                        // ws:true,//用于支持websocket
                        // changeOrigin:true//用于控制请求头中的host值
                    }
                }
            }

## axios
    axios({
            method: 'get查',/post增/put改/delete删
            url: 'http://localhost:3000/posts/2',
            data: {
                title: '初一就可以看电影啦！',
                author: '2023.01.21'
            },
            cancelToken: new axios.CancelToken(function(c){
                cancel = c;
            })
        }).then(respose => {
            console.log(respose)
        })

    请求拦截器、响应拦截器
        创建axios实例
        const request = axios.create({
            beseURL: '/api',
            timeout: 3000,
        });

        // 请求拦截器
        request.interceptors.request.use((config) => {
            return config;
        });

        // 响应拦截器
        request.interceptors.response.use((res) => {
            return res.data;
        }, (error) => {
            return Promise.reject(new Error('faile'));
        });
