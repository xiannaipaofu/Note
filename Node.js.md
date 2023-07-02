## Node.js
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

    全局变量
        __dirname  当前目录绝对路径
            (__dirname + '/text.js')
        __filename  当前文件的绝对路径

    <!-- npm install -g cnpm --registry=https://registry.npmmirror.com 淘宝镜像-->
    npm i -g nrm
    npm i -g nrm open@8.4.2 --save
    nrm use cnpm  // 切换镜像源
    npm config list  查看镜像源

    npm init -y  初始化package.json
    npm i  下载package.json依赖
    npm i name@versions
    npm remove name  //删除

    npm root -g  查看全局安装包位置
    npm list -g  查询全局包
    npm ls  所有已安装包
    npm list name  查询某个模块版本号
    npm update name  更新包
    
    npm help  可查看所有命令
    使用npm help <command>可查看某条命令的详细帮助，例如npm help install。

    npm view name versions  查看包的所有版本

    清除缓存
        npm cache clean --force

    删除文件包
        npm i rimraf
        rimraf xxxx

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
            fs.writeFile('fs.txt', data[, options], callback(err))

            追加写入
                fs.appendFile(file, data[, options], callback(err))

        文件读取
            fs.readFile(path, callback(err, data))
                data： bufer格式数据(需要.toString()转换utf-8)

        // 流式写入
        const ws = fs.createWriteStream(path[, options]) 
        // 流式读取
        const rs = fs.createReadStream(path[, options])
            // 绑定data事件(每读取一块内容触发一次)
            rs.on('data', chunk => {
                ws.write(chunk)  // 写入内容
            })
            rs.on('end', (err)=>{
                ws.close()  // 关闭通道
            })  // 读取结束回调

        rs.pipe(ws)  // 把rs读取内容交接给ws写入


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
        path.resolve(__dirname, path)  // 拼接规范的绝对路径

        let str = path
        let urlObj = path.parse(urlPath)  // 解析路径并返回对象
            {
                root: 'E:\\',
                dir: 'E:\\JavaScript\\nodejs\\mp3',
                base: '难却-mp3.ogg',
                ext: '.ogg',
                name: '难却-mp3'
            }

        path.basename(urlPath)  // 获取路径的基础名称
        path.dirname(urlPath)  // 获取路径的目录名
        path.extname(urlPath)  // 获取路径的后缀名
        path.sep  // 获取当前系统路径分隔符

## url模块
    导入=>  
        const urlObj = new URl(url)
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
                searchParams: URLSearchParams {},
                hash: ''
            }
        const url = require('url')  
            const objUrl = url.parse(url)  解析url  url.format()  互逆
                Url {
                    protocol: 'http:',
                    slashes: true,
                    auth: null,
                    host: '127.0.0.1:8000',
                    port: '8000',
                    hostname: '127.0.0.1',
                    hash: null,
                    search: null,
                    query: null,
                    pathname: '/api/home',
                    path: '/api/home',
                    href: 'http://127.0.0.1:8000/api/home'
                }

## express
    ## http协议
        https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers
        https://www.runoob.com/tags/html-httpmessages.html  http状态码

    原生http模块
        导入
        const http = require('http');
        创建服务对象
        const server = http.createServer((request, response) => {response.end('')  //设置响应体})
        监听端口，启动服务
        server.listen(8000, ()=>{})

        request.on('data', function(chunk){})  请求体
        request.on('end', function(){})

    https://www.expressjs.com.cn
    以下几个重要的模块是需要与 express 框架一起安装的：
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

    使用步骤:
        npm install express
        npm i -g nodemon  //服务器自动重启工具
            
        const express = require('express')

        const app = express()


        // 全局中间件
        function recordMiddleware(req, res, next){  
            next();
        }
        //使用中间件`
        app.use(recordMiddleware)
    
    //静态资源中间件
    app.use(express.static(__dirname + '/public'))  文件夹目录

    //路由
        app.<method>(path, callback(request, reponse)=>{

        req:
            console.log(req.method)  //请求方式  GET
            console.log(req.url)  //请求路径  /api
            console.log(req.path)  //请求路径  /api
            console.log(req.httpVersion)  //http版本  
            console.log(req.query)  //请求参数
            console.log(req.params)  //路由参数
            console.log(req.ip)  //请求ip
            console.log(req.headers)  //所有的请求头
            console.log(req.get('host'))  //host请求头  localhost:8000
            req.hostname  localhost

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

        res:
            res.statusCode = 404  
            res.statusMessage = 'xxx'
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
        })

    // 监听端口
        app.listen(8000, (err)=>{
            if(!err) console.log('服务已经启动，8000 端口正在监听...')
        })

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

## MongoDB
    cmd 
        mongod  // 连接数据库
        mongo  // 操作数据库
    https://www.mongodb.com/try/download/community
    原生命令
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

        bin/www
            const db = require('../db/db')
            db(
                ()=>{},  // 成功回调
                ()=>{}  // 失败回调
            )

        db/db.js
            module.exports = function(success, error){
                if(typeof error !== 'function'){
                    error = () => {}
                }
                const mongoose = require('mongoose')  //引入mongoose
                mongoose.set('strictQuery', true)  //关闭警告
                mongoose.connect('mongodb://127.0.0.1:27017/hellokittyDB')  //连接数据库
                //连接成功回调
                mongoose.connection.once('open', ()=>{
                    success()
                })
                //连接失败回调
                mongoose.connection.on('error', ()=>{
                    error()
                })
                //连接关闭回调
                mongoose.connection.on('close', ()=>{
                    console.log('连接关闭')
                })
            }

        modules/linkageModule.js
            const mongoose = require('mongoose')  // 引入mongoose
            // 创建文档的结构对象
            // 设置集合中文档的属性及属性值类型
            let linkageList = new mongoose.Schema({
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
            // 创建模型对象  对文档操作增删改查
            let linkageModel = mongoose.model('linkageList', linkageList, 'linkageList')  //第三个参数连接数据库已存在集合
             
            module.exports = linkageModel

        routes/linkage.js
            import linkageModel from '../modules/linkageModule.js'
            
            增
                BookModel.create({})
            删
                BookModel.deleteOne({条件})  // 单条
                BookModel.deleteMany  // 批量
            改
                BookModel.updateOne({条件}, {newValue})
                BookModel.updateOneMany 
            查
                BookModel.findOne({条件})
                BookModel.findById('id')
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
        
        mongoose.disconnect()  //关闭数据库连接

    图形化工具
        Robo 3T 免费  https://github.com/Studio3T/robomongo/releases
        Navicat 收费  https://www.navicat.com.cn

## MySQL
    https://dev.mysql.com/doc.refman/8.0/en/
    MySQL是怎样运行的

    gu

    SQL语法:
        
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
    
    git init  初始化仓库
    git config --list  // 显示当前git配置信息
    设置提交代码时的用户信息/修改
    git config --global user.name "MacBook Pro"
    git config --global user.email "1367682868@qq.com"
    获取SSH  ssh-keygen -t rsa   enter>>>  配置SSH
    克隆远程仓库git clone git@github.com:xiannaipaofu/JavaScript.git

    git status  //查看状态
    git add README.md
    git commit -m "first commit"
    git remote add origin git@github.com:xiannaipaofu/JavaScript.git  // 配置远程连接为origin
        git remote -v  查看远程连接
        git remote remove hello  删除远程连接
        git remote rename old_name new_name  # 修改仓库名

    git push -u origin master  上传至master分支
        -u: 简化之后push操作
        -f: 覆盖
        git push --set-upstream origin 本地:远程  关联远程仓库上的分支
        git push <远程主机名> <本地分支名>:<远程分支名>
        git push origin --delete master  // 删除远程仓库的分支

    git pull origin master  //拉取远程代码与当前分支合并
        git pull <远程主机名> <远程分支名>:<本地分支名>  拉取到指定分支
    git pull origin master --allow-unrelated-histories  允许不相关历史提交，并强制合并
    git fetch origin master:demo  拉取远程代码到本地master并创建一个demo分支
    git merge 主 副  //合并分支

    git branch name  创建分支
        -v查看所有分支
        -d name删除分支
        -m oldBranch newBranch  分支重命名
        
    git checkout name  切换分支
        -b name创建并切换

    git blame <file>  //查看指定文件修改记录

    git log --oneline/--graph  //历史提交记录、历史记录何时出现分支合并
    git reset --soft/--hard <hash>  //不带参数(还原)、回退版本、回退并删除之前提交的所有版本

    git rm <>  //删除文件
    git mv <oldFile> <newFile>  //移动文件/重命名

    git cat-file -p hash  //
    git rm -r -f --cached ./   (删除缓存)

    git diff file1.ext file2.ext  //比较文件的不同
    git diff  显示工作空间和暂存区的差异
    git diff --cached  比较暂存区和提交的差异

    1. git 开启代理
        git config --global http.proxy http://127.0.0.1:41091
        git config --global https.proxy http://127.0.0.1:41091

    2. git 取消代理
        git config --global --unset http.proxy
        git config --global --unset https.proxy

    关闭SSI验证
        git config --global http.sslVerify "false"
        git config --global https.sslVerify "false"

    gitee  //国内仓库
    IDEA  //集成仓库

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
        D:
        dir  查询当下目录
        cd  


