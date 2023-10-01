## Node.js
    ## node全局变量
        global  // nodejs顶级对象
        process  // 
            process.memoryUsage()  // 获取代码运行内存使用量  rss代表字节/1024/1024 = MB
        Buffer  // 缓存区
        __dirname  // 当前目录绝对路径
            (__dirname + '/text.js')
        __filename  // 当前文件的绝对路径

    ## 常用配置
        -v  查看版本号
        -g  全局安装
        --save  默认值,依赖写入package.json → dependencies  注: 适合生产环境需要的包
        --save-dev/-D  开发环境依赖,依赖写入package.json → devDependencies  注: 适合在开发环境的包
        
    ## 常用指令
        npm init -y  // 初始化package.json
        npm install|i  // 下载package.json依赖
        npm i <name>@versions  // 下载包以及指定包版本
        npm uninstall|remove|rm|r|un <name>  //删除
        npm update|up <name> --save  // 更新包,注: save为false.
        npm ls  // 查看所有已安装包
        npm list <name>  // 查询某个模块版本号
        npm view <name> versions  // 查看包的所有版本
        npm cache clean --force  // 清除缓存

    ## 全局
        npm list -g  // 查询全局包
        npm root -g  // 查看全局安装包位置

    ## 命令
        npm help  可查看所有命令
        npm help <command>  // 可查看某条命令的详细帮助，例如npm help install

        npm config set registry https://registry.npmmirror.com/  // 设置npm命令服务器源
        npm config get registry  // 获取npm命令服务器源

    ## 项目
        npm run serve/npm start  // 启动
        npm run build  // 打包
        npm run lint  // 检查修复

    ## 切换镜像
        npm i cnpm --registry=https://registry.npmmirror.com -g   // 淘宝镜像
        npm i nrm -g
        npm i nrm open@8.4.2 -g
        nrm use cnpm  // 切换镜像源
        nrm ls  // 查看正在使用的镜像源

        npm get registry  // 查看当下镜像源
        npm config list  // 查看当下镜像源npm

    ## nvm  nodejs版本管理工具
        https://github.com/coreybutler/nvm-windows/releases 
            nvm-setup.exe

        nvm list available  显示所有可下载的nodejs版本
        nvm list 显示已安装版本
        nvm install 1.1.1  安装某个版本
        nvm install latest  安装最新版本nodejs
        nvm uninstall 1.1.1  删除某个版本nodejs
        nvm use 1.1.1 切换某个版本nodejs
    
    ## yarn
        npm i -g yarn
        yarn init
        yarn add 包名
        yarn 下载package.json依赖

    ## 安装依赖报错
        通过https://www.ipaddress.com/ 网查询raw.githubusercontent.com使用的ip地址
            raw.githubusercontent.com
        修改HOSTS文件
        C:\Windows\System32\drivers\etc 下的hosts
             199.232.28.133 raw.githubusercontent.com

## Buffer缓冲区
    在v6.0之前创建Buffer对象直接使用new Buffer()构造函数来创建对象实例，但是Buffer对内存的权限操作相比很大，可以直接捕获一些敏感信息，所以在v6.0以后，官方文档里面建议使用 Buffer.from() 接口去创建Buffer对象。

    一个字节 = 一个二进制数字

    创建
        let buf = Buffer.alloc(10)  // 创建并分配10个二进制字节(终端显示十六进制)
        let buf = Buffer.allocUnsafe(10)  // 创建并分配10个字节(速度快，但不安全，不会将过去内存纪录归零)
        let buf = Buffer.from(xxx)  // 将内容(字符串/数组)转换成二进制存储到缓存区
        buf.toString()  // 将buffer转换成字符串

## file system文件系统
    const fs = require('fs');  // 导入模块

    ## 文件写入
        fs.writeFileSync(file, data[, options])  // 同步
        fs.writeFile('fs.txt', data[, options], callback(err))  // 异步
            options: <Object> | <string>
                encoding <string> | <null> 默认值： 'utf8'
                mode <integer> 默认值： 0o666
                flag: <string> 参见 支持文件系统 flags。 默认值：'w'写入模式, 'a'追加模式, 'r'读取模式。
                signal <AbortSignal> 允许中止正在进行的写入文件
        
        fs.appendFileSync(file, data[, options])  // 同步追加写入
        fs.appendFile(file, data[, options], callback(err))  // 追加写入

    ## 文件读取
        fs.readFileSync(path)  // 同步
        fs.readFile(path[, oprions], callback(err, data))  // 异步
            data: bufer格式数据(需要.toString()转换utf-8)

    ## 流式对象
        const ws = fs.createWriteStream(path[, options])  // 创建写入流
        ws.write('')  // 写入内容
        ws.close()  // 关闭通道
        
        const rs = fs.createReadStream(path[, options])  // 创建读取流
        rs.on('data', (chunk)=>{ws.write(chunk)})  // 绑定data事件(每读取一块内容触发一次)  chunk: 每次读取的内容
        rs.on('end', (err)=>{ws.close()})  // end事件,读取结束触发

        rs.pipe(ws)  // 把rs读取内容交接给ws写入

    ## 文件移动与重命名
        fs.rename(oldPath, newPath, callback(err))

    ## 文件删除
        fs.unlink(path, callback(err))

    ## 文件夹操作
        fs.mkdir(path[, options], callback(err))  // 创建
            options:
                {recursive: true}开启递归创建

        fs.rm(path[, options], callback(err))  // 删除
            options:
                {recursive: true}开启递归删除
        
        fs.readdir(path, callback(err, data))  // 读取

    ## 查看资源状态
        const data = fs.stat(path, callback(err, data))
            size  文件体积
            birthtime  创建时间
            atime  最后访问时间
            mtime  最后修改文件时间
            ctime  最后修改文件状态时间
            .isFile()  是否为文件
            .isDirectory()  是否为文件夹

    注: 相对路径是基于命令行运行目录

## path模块
    const path = require('path');

    const p = path.resolve(__dirname, 'NewFile/file.text')  // 拼接规范的绝对路径

    // path.parse(p)  // 解析路径并返回对象
            // {
            //     root: 'E:\\',  // 根目录
            //     dir: 'E:\\JavaScript\\nodejs\\mp3',  // 目录绝对路径
            //     base: '难却-mp3.ogg',  // 路径的基础名称
            //     ext: '.ogg',  // 后缀
            //     name: '难却-mp3'  // 名称
            // }

    // path.basename(p)  // 获取路径的基础名称
    // path.dirname(p)  // 获取目录的绝对路径
    // path.extname(p)  // 获取文件的后缀名
    // path.sep  // 获取当前系统路径分隔符  :\

## url模块
    const urlObj = new URL(url, 'http://127.0.0.1:8000')  // 创建URL对象, 传入对象需是完整url
        URL {
            href: 'http://127.0.0.1:8000/api/home',
            origin: 'http://127.0.0.1:8000',       
            protocol: 'http:',
            username: '',
            password: '',
            host: '127.0.0.1:8000',
            hostname: '127.0.0.1',
            port: '8000',
            pathname: '/api/home',
            search: '',
            searchParams: URLSearchParams {},  // url.searchParams.get('')获取查询字符串的值
            hash: ''
        }

## os操作系统模块
    const os = require('os')

    cosnt threads = os.cpu().length;  // 获取cpu核数

## express
    ## 以下几个重要的模块是需要与 express 框架一起安装的：
    body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。  *express4.0-4.16版本
        $ npm i body-parser  获取请求体数据
            const bodyParser = require('body-parser')
            var jsonParser = bodyParser.json()  //解析json格式请求体
            var urlencodedParser = bodyParser.urlencoded({ extended: false })  //解析querystring格式请求体
            app.ues(bodyParser.json())
            app.ues(bodyParser.urlencoded({ extended: false }))

    cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
        $ npm i cookie-parser  解析cookie
            const cookieParser = require('cookie-parser');
            app.use(cookieParser())
            res.cookies

    express-session - 生成sid唯一标识
        $ npm i express-session connect-mongo  生成sid
            const session = require('express-session')
            const MongoStore = require('connect-mongo')
            app.use(session({
                name: 'sid',  //设置cookie的名字
                secret: 'atguigu',  //参与加密的字符串(密钥)
                saveUninitialized: false,  //是否为每次请求都设置一个cookie来存储session的id
                resave: true,  //是否在每次请求时重新保存seesion
                store: MongoStore.create({
                    mongoUrl: 'mongodb://127.0.0.1:27017/project',  //数据库的链接配置
                }),
                cookie: {
                    httpOnly: true,  //开启后前端无法通过JS操作
                    maxAge: 1000 * 300  //控制cookie生命周期
                }
            }))

    http-proxy-middleware  代理服务器中间件
        $ npm i http-proxy-middleware 
                const express = require('express')
                const app = express()
                const { createProxyMiddleware } = require('http-proxy-middleware');
                app.use(
                    '/api',
                    createProxyMiddleware({
                        target: 'http://127.0.0.1:8080',
                        pathRewrite: {'^/api' : '/api/new-path'},  //重写路径
                        changeOrigin: true,  //用于控制请求头中host的值
                        ws: true,  //用于支持websockets
                        router: {
                            // when request.headers.host == 'dev.localhost:3000', 
                            // override target 'http://www.example.org' to 'http://localhost:8000' 
                            'dev.localhost:3000' : 'http://localhost:8000'
                        }
                    })
                );
                app.listen(3000)

    ## 使用步骤:
        npm i express -g
        npm i nodemon -g  // 服务器自动重启工具
            
        const express = require('express')  // 引入模块
        const app = express()

        function recordMiddleware(req, res, next){ next()}  // 全局中间件
        
        app.use(recordMiddleware)  // 使用中间件
        app.use(express.static(__dirname + '/public'))  // 静态资源中间件,文件夹目录

        app.<method>(path, callback(request, reponse)=>{}) // 路由
        app.listen(8000, (err)=>{})  // 监听端口

    ## request:
            console.log(req.method)  // 请求方式  GET
            console.log(req.url)  // 请求路径以及查询字符串  /api
            console.log(req.path)  // 请求路径  /api
            console.log(req.query)  // 请求参数
            console.log(req.params)  // 路由参数
            console.log(req.ip)  // 请求ip
            console.log(req.headers)  // 所有的请求头
            console.log(req.get('host'))  //host请求头  localhost:8000

            req.httpVersion  // http版本
            req.hostname  // localhost
            req.baseUrl
            req.body
            req.cookies
            req.originalUrl  http
            
            Methods
            req.accepts()
            req.acceptsCharsets()
            req.acceptsEncodings()
            req.acceptsLanguages()
            req.get()
            req.is()
            req.param()
            req.range()

    ## response:
        res.statusCode = 404  // 设置状态码
        res.statusMessage = 'xxx'  // 响应描述
        res.set('Access-Control-Allow-Origin','*')  // 设置响应头 设置允许跨域
        res.set('Access-Control-Allow-Headers','*')  // 设置响应头 允许自定义
        res.write('响应体')  拼接res.end
        res.end('xxx')

        Methods
        res.set()  设置响应头
        res.cookie()
        res.clearCookie()
        res.json()  响应json
        res.send()  设置响应
        res.status(500)  设置响应状态码
        res.end()  设置响应
        res.render()  响应模板
        res.sendFile(__dirname + '/file')  响应文件内容
        res.download(__dirname + '/file')  下载响应
        res.redirect('url')  重定向

        res.append()
        res.attachment()
        res.format()
        res.get()
        res.jsonp()
        res.links()
        res.location()
        res.sendStatus()
        res.type()
        res.vary()


    路由模块化
        const express = require('express')
        const router = express.Router()
        routrer.get('/', callback)
        module.exports = router

        引入
            const homeRouter = require('./')
            app.use(homeRouter)

    模板引擎EJS
        分离用户界面和业务数据的一种技术
        npm i ejs
        const ejs = require('ejs')

        语法:
            const china = '中国'
            ejs.render('我爱你 <%= china %>', {china: china})

            列表渲染
                <%  ......  %>
                <%  ...  %>

        // 设置当前express使用的模板引擎为jade(pug|twing|ejs)
        app.set('view engine', 'jade');
        // 设置模板引擎文件存放位置
        app.set('views', path.resolve(__dirname, 'views'));

        res.render('模板文件名', '数据')

    express快速生成工具express-generator
        npm i -g express-generator
        express -e name
        npm i

    文件上传处理
        npm i formidable
        const formidable = require('formidable')
        app.post('', (req, res)=>{
            //创建表单对象
            const form = formidable({
                multiples: true,
                //设置上传文件的保存目录
                uploadDir: __dirname + '/../public/images'
            })
            //解析请求报文
            form.parse(req, (err, fields, files) => {
                if(err){
                    next(err)
                    return;
                }
                // fields  text|radio|checkbox
                // fiels  file
                let url = '/images/' + files.portrait.newFilename  //把路径保存至数据库
                res.json({fields, files})
            })
        })

    ## cmd ipconfig  //当下ip地址
        
## linux
    linux:  /根目录

    指令:   
        pwd  返回当前路径的绝对路径
        cd xx       跳转目录
        ls          查看当前目录所有文件、-R列出子目录中的所有文件|-a列出隐藏文件|-al
        cat file  查看文件内容
        mkdir xxx   创建文件夹
        rmdir name  删除文件夹
        touch name.txt  新建文件

        clear  清屏

    vim操作
        进入编辑器 vi/vim，vim三种模式：命令模式、插入模式、编辑模式。使用ESC或i或：来切换模式。

        进入编辑模式插入 i
        退出编辑模式 esc
        保存:后面输入w
        退出:后面输入q
        不保存退出:后面输入q!
        显示行号 set number
        查找关键字 /xxxx 按n跳到下一个，shift+n上一个
        复制光标所在行，并粘贴 yyp
        h(左移一个字符←)、j(下一行↓)、k(上一行↑)、l(右移一个字符→)


## windows
    指令
        .  当前目录
        ..  上一级目录
        D:  切换盘符
        dir  查询当下目录  /s盘点目录下所有文件  color 02  修改颜色
        cd  切换目录

    /r/n  换行