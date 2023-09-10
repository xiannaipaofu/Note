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
