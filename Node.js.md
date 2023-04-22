## Node.js
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

    const buf = Buffer.from()

    Node.js 目前支持的字符编码包括：
        ascii - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。
        utf8 - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。
        utf16le - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。
        ucs2 - utf16le 的别名。
        base64 - Base64 编码。
        latin1 - 一种把 Buffer 编码成一字节编码的字符串的方式。
        binary - latin1 的别名。
        hex - 将每个字节编码为两个十六进制字符

## Stream流

## 路由

## util函数集合

## fs文件系统
    const fs = require('fs')

## 工具模块
    const url = require('url')  请求路径
        url.parse()  解析路径  url.format()  互逆


    const path = require('path')  拼接文件路径
        



    const http = require('http');  搭建 HTTP 服务端和客户端

## express
    以下几个重要的模块是需要与 express 框架一起安装的：

    body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。
    cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
    multer - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

    $ cnpm install body-parser --save
    $ cnpm install cookie-parser --save
    $ cnpm install multer --save

    npm install express

    // 引入express
        const express = require('express')

    // 创建应用对象
        const app = express()

    // 创建路由规则，request是请求报文的封装，response是响应报文的封装
    // app.all() 可以接受任意类型的请求
        app.get('/',(request, response)=>{

            let code = request.query  //获取前端发送过来的参数

            // 设置响应头 设置允许跨域
            response.setHeader('Access-Control-Allow-Origin','*')

            // 设置响应头 允许自定义
            response.setHeader('Access-Control-Allow-Headers','*')

            const data = {
                message: '恭喜你，登录成功了...',
                tips: '有效期是半小时',
                user: {
                    masg: '这是你当前账号的信息',
                    Id: 1,
                }
            }

            // 把对象转换成JSON格式
            let str = JSON.stringify(data)

            // 设置响应
            response.send(str)
        })

    // 监听端口
        app.listen(8000, (err)=>{
            if(!err) console.log('服务已经启动，8000 端口正在监听...')
        })

    node server.js 

    npm i -g nodemon  //服务器自动重启工具

    nodemon server.js

## MySQL

## MongoDB

