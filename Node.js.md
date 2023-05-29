## Node.js

    全局变量
        require
        __dirname  当前目录绝对路径
            (__dirname + '/text.js')
        __filename  当前文件的绝对路径

    <!-- npm install -g cnpm --registry=https://registry.npmmirror.com 淘宝镜像-->

    npm list -g  查询全局包
    npm list name  查询某个模块版本号
    npm uninstall name  卸载包
    npm update name  更新包
    npm search name  搜索包
    npm ls  所有已安装包
    npm init  初始化package.json
    npm help  可查看所有命令
    使用npm help <command>可查看某条命令的详细帮助，例如npm help install。

    npm view name versions  查看包的所有版本

    npm adduser  注册用户
    npm publish  发布模块
    使用npm unpublish <package>@<version>可以撤销发布自己发布过的某个版本代码。

    删除包
        npm i rimraf

        rimraf xxxx

    清除缓存
        npm cache clean --force

## Buffer缓冲区
    在v6.0之前创建Buffer对象直接使用new Buffer()构造函数来创建对象实例，但是Buffer对内存的权限操作相比很大，可以直接捕获一些敏感信息，所以在v6.0以后，官方文档里面建议使用 Buffer.from() 接口去创建Buffer对象。

    创建
        let buf = Buffer.alloc(10)  创建并分配10个字节
        let buf = Buffer.allocUnsafe(10)  创建并分配10个字节(速度快，但不安全，不会将过去内存纪录归零)
        let buf = Buffer.from(xxx)  将内容转换成二进制存储到缓存区

## fs文件系统
    导入
        const fs = require('fs');

    文件操作
        异步写入
            fs.writeFile(file, data[, options], callback(err))

            追加写入
                fs.appendFile(file, data[, options], callback(err))

        流式写入
            const ws = fs.createWriteStream(path[, options])  
            ws.write('')  写入内容
            ws.close()  关闭通道

        文件读取
            fs.readFile(path, {}, callback(err, data))  异步读取
                data： bufer格式数据(需要.toString()转换utf-8)

            流式读取
            const rs = fs.createReadStream()  创建读取流对象
                绑定data事件(每读取一块内容触发一次)
                rs.on('data', chunk => {

                })
                rs.on('end', ()=>{})  读取结束回调

        rs.pipe(ws)  把rs读取内容交接给ws写入

        文件移动与重命名
            fs.rename(oldPath, newPath, callback(err))

        文件删除
            fs.unlink(path, callback(err))

    文件夹操作
        创建
            fs.mkdir(path, callback(err))

        读取
            fs.readdir(path, callback(err, data))

        删除
            fs.rm(path, callback(err))

    查看资源状态
        const data = fs.stat(path, callback(err, data))
            size  文件体积
            birthtime  创建时间
            mtime  最后修改时间
            .isFile()  是否为文件
            .isDirectory()  是否为文件夹

    批量重命名

## path模块
    const path = require('path');
        path.resolve  拼接规范的绝对路径
            path.resolve(__dirname, path)
        path.parse  解析路径并返回对象
            let str = path
            path.parse(str)
        path.basename  获取路径的基础名称
        path.dirname  获取路径的目录名
        path.extname  获取路径的后缀名
        path.sep  获取路径分隔符

## http协议
    https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers
    https://www.runoob.com/tags/html-httpmessages.html  http状态码

## http模块
    导入
        const http = require('http');
    创建服务对象
        const server = http.createServer((request, response) => {
            response.end('')  //设置响应体
        })
    监听端口，启动服务
    server.listen(8000, ()=>{

    })

    获取http请求报文
        request.method  请求方法
        request.url  请求路径(只包含路径与查询字符串)
        request.headers  请求头

        request.on('data', function(chunk){})  请求体
        request.on('end', function(){})

    响应报文
        response.statusCode  设置响应状态码
        response.statusMessage  设置响应状态描述
        response.setHeader('名', '值')  设置响应头信息
        response.write('')  设置响应体
        response.end('')

## url模块
    导入=>  new URl()
        const url = require('url')  
            url.parse(url)  解析url  url.format()  互逆
            url.parse(url).pahtname  获取路径
            url.parse(url, true).query  获取查询字符串

## 包管理工具 
    npm 
    yarm
    cnpm

    初始化
        npm init -y

    npm root -g  查看全局安装包位置

    npm i nodemon  服务器热启动

    npm i  下载package.json依赖

    npm i 包名@版本号

    npm remove 包名

    配置别名

    npm i -g nrm
        npm install -g nrm open@8.4.2 --save

    nrm use npm

    npm config list  查看镜像源
    

    yarn
        npm i -g yarn

        yarn init

        yarn add 包名

        yarn 下载package.json依赖

    nvm  nodejs版本管理工具
        https://github.com/coreybutler/nvm-windows/releases 
            nvm-setup.exe

        nvm list available  显示所有可下载的nodejs版本
        nvm list 显示已安装版本
        nvm install 1.1.1  安装某个版本
        nvm install latest  安装最新版本nodejs
        nvm uninstall 1.1.1  删除某个版本nodejs
        nvm use 1.1.1 切换某个版本nodejs


## express
    https://www.expressjs.com.cn
    以下几个重要的模块是需要与 express 框架一起安装的：

    body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。
    cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
    express-session - 生成sid唯一标识
    multer - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

    $ npm i body-parser  获取请求体数据
        const bodyParser = require('body-parser')
        var jsonParser = bodyParser.json()  //解析json格式请求体
        var urlencodedParser = bodyParser.urlencoded({ extended: false })  //解析querystring格式请求体
    $ npm i cookie-parser  解析cookie
        const cookieParser = require('cookie-parser');
        app.use(cookieParser())
        res.cookies
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
    $ npm i multer

    npm install express

    // 引入express
        const express = require('express')
        const app = express()


    // 全局中间件
    function recordMiddleware(req, res, next){  
        let { url, ip} = req
        fs.appendFileSync(path.resolve(__dirname, './access.test'), `${url}  ${ip}\r\n`)
        next();
    }
    //使用中间件
    app.use(recordMiddleware)
    //路由中间件
        app.<method>(path, recordMiddleware, callback)

    //静态资源中间件
        app.use(express.static('url'))  文件夹目录

    //路由app.<method>(path, callback)
        app.get('/',(request, response)=>{  // app.all() 可以接受任意类型的请求
            let code = request.query  //获取前端发送过来的参数

            response.setHeader('Access-Control-Allow-Origin','*')  // 设置响应头 设置允许跨域
            response.setHeader('Access-Control-Allow-Headers','*')  // 设置响应头 允许自定义

        req:
            console.log(request.method)  请求方式
            console.log(request.url)  请求路径
            console.log(request.httpVersion)  http版本
            console.log(request.headers)  请求头
            console.log(request.path)  请求路径
            console.log(request.query)  请求参数
            console.log(request.params)  路由参数
            console.log(request.ip)  请求ip
            console.log(request.get('host'))  某个请求头

        res:
            //原生
            res.statusCode = 404  
            res.statusMessage = 'xxx'
            res.setHeader('abc', 'xyz')
            res.write('响应体')
            res.end('xxx')

            //express封装
            res.status(500)  设置响应状态码
            res.set('xxx', 'xxx')  设置响应头
            res.send('')  响应体

            //其他响应
            res.redirect('url')  重定向
            res.download('url')  下载响应
            res.json();  响应json
            res.sendFile(__dirname + 'url')  响应文件内容

            response.send(str)  // 设置响应
        })

    // 监听端口
        app.listen(8000, (err)=>{
            if(!err) console.log('服务已经启动，8000 端口正在监听...')
        })

    路由模块化
        const express = require('express')
        const router = express.Router()
        routrer.get('', callback)
        module.exports = router

        引入
            const homeRouter = require('./')
            app.use(homeRouter)

    node server.js 

    npm i -g nodemon  //服务器自动重启工具
    nodemon server.js

    cmd ipconfig  //当下ip地址

    模板引擎EJS
        分离用户界面和业务数据的一种技术

    express-generator
        express快速生成工具
        npm i -g express-generator
        express name
        npm i

    文件上传处理
        npm i formidable


## MongoDB
    https://www.mongodb.com/try/download/community
    命令
        show dbs  //显示所有的数据库
        use name  //切换数据库
        db  //当前所在数据库
        db.dropDatabase()  //删除当前数据库

        db.createCollection('集合名称')  //创建集合
        show collections  //显示当前数据库中的所有集合
        db.集合名.drop()  //删除某个集合
        db.集合名.renameCollection('newname')  重命名集合名

        db.集合名.insert(文档对象)  //插入文档
        db.集合名.find(查询条件)  //查询文档
        db.集合名.update(查询条件, 新的文档)  //更新文档
            db.集合名.update({name: '张三'}, {$set:{age: 19}})
        db.集合名.remove(查询条件)  //删除文档

    mongoose
        npm i mongoose
        const mongoose = require('mongoose')
        mongoose.set('strictQuery', true)  //关闭警告
        mongoose.connect('mongodb://127.0.0.1:27017/bilibili')  //连接数据库
        mongoose.connection.on('open/error/close', ()=>{})  //设置回调

        mongoose.disconnect()  //关闭数据库连接

            mongosse.connection.once('open', () => {
                创建文档的结构对象
                设置集合中文档的属性及属性值类型
                let BookSchema = new mongoose.Schema({
                    name: {
                        type: String,
                        required: true,  //必填项
                        default: '',  //默认值
                        enum: ['男', '女'],  //枚举  值必须是其中之一
                        unique: true  //唯一值
                    },
                    author: String,
                    price: Number
                })

                创建模型对象  对文档操作增删改查
                let BookModel = mongoose.Model('books', BookSchema)

                增
                    BookModel.create({})
                删
                    BookModel.deleteOne({条件}, (err, data)=>{})  单条
                    BookModel.deleteMany  批量
                改
                    BookModel.updateOne({条件}, {newValue}, (err, data)=>{})
                    BookModel.updateOneMany 
                查
                    BookModel.findOne({条件}, (err, data)=>{})
                    BookModel.findById('id', (err, data)=>{})
                    BookModel.find({})

                条件
                    {price: $gt: 20}
                    $gt  >
                    $lt  <
                    $gte  >=
                    $lte  <=+
                    $ne  !==

                    $or  或  $or:[{age: 18}, {age: 20}]
                    $and  与  $and: [{age: {$lt:20}, {age: {$gt: 15}}}]

                个性化读取
                    BookModel.find().select({name: 1, id: 0}).sort({prece: -1}).exec((err, data)=>{})
                    筛选.select({name: 1, id: 0})
                    排序.sort({prece: -1})
                    数据截取(跳过/限定).skip(3).limit(3)
            })

    图形化工具
        Robo 3T 免费  https://github.com/Studio3T/robomongo/releases
        Navicat 收费  https://www.navicat.com.cn

## API 接口
    测试工具
        apipost  https://www.apipost.cn/
        apifox  https://www.apifox.cn/
        postman  https://www.postman.com/

## 会话控制
    Cookie
    session
    token

    登录/注册流程            服务器                  数据库
        用户申请----    向数据库发请求----     生成唯一id标识并返回

## Webpack
    webpack默认对外暴露图片、JSON数据格式

    npm init -y  //初始化package.json
    npm i webpack webpack-cli -D  //webpack依赖
    npx webpack  //启用webpack

    webpack.config.js
        module.exports = {
            // 入口文件
            entry: './src/main.js',
            //输出位置
            output: {
                path: './dist',  // 目录
                filename: 'main.js'  // 文件
                clean: true  // 清空上次打包
            },
            // 加载器
            mudule: {
                // 加载规则
                rules: [
                    {
                        test: /\.less$/,
                        use: [
                            'css-loader',
                            'less-loader',
                        ]
                    }
                ]
            },
            //插件
            plugins: [

            ],
            //模式development|production
            mode: 'production'
        }
        
    loder
        https://webpack.docschina.org/loaders/
        静态资源asset
            {
                test: /\.(png|gif)/,
                type: "asset",
                parser: {
                    dataUrlCondition: {
                        maxSize: 10 * 1024,  //小于10kb转base64编码
                    }
                },
                <!-- 资源输出目录 -->
                generator: {
                    filename: "static/images/[hash:6][ext]",
                }
            }
        less
            npm i -D less less-loader css-loader style-loader
            npm i -D postcss postcss-loader postcss-preset-env  //css兼容性处理

        babel
            @bable/preset-env  //智能预设js
            npm install -D babel-loader @babel/core @babel/preset-env  //js兼容性处理(高级语法编译成低级)、@babel/core(核心包)

        eslint  //js语法检测
            https://www.eslint.com.cn
            npm install eslint --save-dev
            npm i eslint-webpack-plugin --save-dev

        typescript
            npm i -D typescript ts-loader  //下载依赖包
        
    插件
        html
            npm i -D html-webpack-plugin  //自动生成html文件

        单独提取Css文件
                npm i mini-css-extract-plugin --save-dev
            压缩css
                npm i css-minimizer-webpack-plugin --save-dev

    webpack开发服务器
        npm i -D webpack-dev-server  //开发服务器，npx webpack serve

## Git
    http://git-scm.com/docs/git-log

    ssh-keygen -t rsa -Cgit@github.com:xiannaipaofu/demo.git  //生成安全认证  
 
    git init  //初始化仓库

    git clone <仓库地址>  //克隆仓库
    git pull  //下载远程代码并合并
    git add <>  //添加文件到缓存区
    git commit -m 备注  //将缓存区内容添加到仓库中
    git push <仓库地址>  //上传远程代码并合并
    git publish  //上传仓库
    
    git status  //查看当前仓库状态是否有变更文件
    git log --oneline/--graph  //历史提交记录、历史记录何时出现分支合并
    git reset --soft/--hard <hash>  //不带参数(还原)、回退版本、回退并删除之前提交的所有版本

    git blame <file>  //查看指定文件修改记录
    git diff <>  //比较文件的不同
    git rm <>  //删除文件
    git mv <> <>  //移动文件

    git branch <>  //创建分支、-v查看所有分支、-d <> 删除分支
    git checkout <>  //切换分支、-b <> 创建并切换
    git merge <>  //合并分支

    git tag  //查看标签、-d <>删除标签
    git tag 别名 hash  //配置标签

    git cat-file -p hash  //

    git config --list  //显示当前git配置信息
    设置提交代码时的用户信息：
    git config --global user.name "runoob"
    git config --global user.email test@runoob.com

    1. git 开启代理
        git config --global http.proxy http://127.0.0.1:41091
        git config --global https.proxy http://127.0.0.1:41091

    2. git 取消代理
        git config --global --unset http.proxy
        git config --global --unset https.proxy

    gitee  //国内仓库
    IDEA  //集成仓库

## linux
    linux:  /根目录

    指令:   
        cd xx       跳转
        ls          查看
        vim xxxx    编辑文件
        mkdir xxx   创建文件夹
        pwd         查看绝对路径

## CMD
    指令
        D:
        dir  查询当下目录
        cd  


