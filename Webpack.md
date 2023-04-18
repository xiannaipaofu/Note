## Webpack
    webpack默认对外暴露图片、JSON数据格式

    npm init -y  //初始化package.json
    npm i webpack webpack-cli -D  //webpack依赖
    npx webpack url --mode=development  //启用webpack，url设置入口文件，配置环境/production(生产环境)

    五大核心
        entry  //入口
        output  //输出
        loader  //加载器
        plugins  //插件
        mode  //模式，development生产/production开发
    
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

    loader https://webpack.docschina.org/loaders/

    html
        npm i -D html-webpack-plugin  //自动生成html文件

    单独提取Css文件
            npm install mini-css-extract-plugin --save-dev
        压缩css
            npm install css-minimizer-webpack-plugin --save-dev

    less
        npm i -D less less-loader css-loader style-loader
        npm i -D postcss postcss-loader postcss-preset-env  //css兼容性处理

    typescript
        npm i -D typescript ts-loader  //下载依赖包

    babel  
        @bable/preset-env  //智能预设js
        npm install -D babel-loader @babel/core @babel/preset-env  //js兼容性处理(高级语法编译成低级)、@babel/core(核心包)

    eslint  //js语法检测
        https://www.eslint.com.cn
        npm install eslint --save-dev
        npm i eslint-webpack-plugin --save-dev

    webpack开发服务器
        npm i -D webpack-dev-server  //开发服务器，npx webpack serve