## Webpack5
    # webpakc是一个静态资源打包工具:
        压缩代码、兼容性处理、提升代码性能

        注: webpack默认对外暴露图片、JSON数据格式

    # 基础步骤
        npm init -y  // 初始化package.json
        npm i webpack webpack-cli -D  // 安装webpack依赖
        配置webpack.config.js文件
        npx webpack  //启用webpack  npx webpack ./src/main.js --mode=development

    # 配置webpack:
        webpack.config.js >
            const path = require('path')

            module.exports = {
                // 入口文件
                // entry: './src/main.js',  // 单入口
                // 多入口
                entry: {
                    app: './src/app.js',
                    main: './src/main.js',
                },
                // 输出位置
                output: {
                    path: path.resolve(__dirname, '../dist'),  // 目录
                    filename: 'static/js/[name].js',  // 文件输出路径/文件名  // [name]多入口输出
                    clean: true  // 清空上次打包
                },
                // 加载器(loader)
                module: {
                    // 加载规则
                    rules: [
                        // loader配置
                    ]
                },
                // 插件
                plugins: [
                    // plugins配置
                ],
                // 模式development|production
                mode: 'production'
            }

    # 处理样式资源
        css
            npm i css-loader style-loader

            {
                test: /\.css$/i,  // 只检测正则所匹配文件
                // loader: 'xxx',  // 只能使用一个loader
                use: [
                    // 使用多个loader
                    // 编译顺序 右(下)到左(上)
                    'style-loader',  // 将js中css通过创建style标签添加html文件中生效
                    'css-loader'  // 将css资源编译成commonjs的模块到js中
                ]
            }

        less
            npm i less less-loader

            {
                test: /\.less$/i,
                use: [
                  'style-loader',
                  'css-loader',
                  'less-loader'  // 将less编译成css
                ]
            }

            npm i -D postcss postcss-loader postcss-preset-env  //css兼容性处理

        sass
            npm i sass-loader sass

            {
                test: /\.s[ac]ss$/i,
                use: [
                    'style-loader',
                    'css-loader',
                    'sass-loader'  // 将 Sass编译成CSS
                ]
            }

    # 静态资源模块asset
        {
            test: /\.(png|gif)$/,
            type: "asset",
            parser: {
                dataUrlCondition: {
                    maxSize: 10 * 1024,  // 小于10kb转base64编码
                }
            },
            // 资源输出目录
            generator: {
                filename: "static/images/[hash:6][ext]",
            }
        }
    
    # 处理字体图标资源or其他资源
        {
            test: /\.(ttf|woff2?|mp3|mp4|avi)$/,
            type: "asset/resource",  // 不做base64编码,原封不动输出
            // 资源输出目录
            generator: {
                filename: "static/media/[hash:6][ext]"
            }
        }

    # eslint代码格式  // https://www.eslint.com.cn
        eslint常用指令:

        npm i eslint eslint-webpack-plugin --save-dev

        webpack.config.js:
            const ESLintPlugin = require('eslint-webpack-plugin');  // 引入插件
            module.exports = {
                // ...
                plugins: [
                    new ESLintPlugin({
                        context: path.resolve(__dirname, 'src')  // 检测哪些文件
                    })
                ],
                // ...
            };

        写法:
            .eslintrc
            .eslintrc.js  // js格式
            eslint.config.js
            .eslintrc.json  // json格式
            package.json 中 eslintConfig: 不需要创建文件,在原有文件基础写

        配置:
            module.exports = {
                // 继承其他规则
                extends: [
                    "eslint:recommended",  // eslint官方规则
                    // "plugin:vue/essential",  // Vue Cli官方规则
                    // "react-app"  // React Cli官方规则
                ],
                env: {
                    browser: true,  // 浏览器全局变量
                    node: true,  // nodejs全局变量
                    es6: true,  // 启用es6新特性
                },
                // 解析选项
                parserOptions: {
                    ecmaVersion: 6, // ES语法版本
                    sourceType: "module", // ES模块化
                    ecmaFeatures: {  // ES其他特性
                        jsx: true  // 如果是React项目,就要开启jsx语法
                    }
                },
                // 配置哪些文件不需要检测
                ignorePatterns: [
                    "dist",
                    "node_modules"
                ]
                // 具体检查规则
                rules: {
                    // 'off'或0 - 关闭警告
                    // 'warn'或1 - 开启规则(警告,不退出程序)
                    // 'error'或2 - 开启规则(触发时退出程序)
                    semi: "error",  // 默认末尾使用分号,否则警告
                    'array-callback-return': 'warn',  // 强制数组方法的回电函数中有return语句
                    'default-cace': [
                        'warn',  // 要求switch语句中有default分支,否则警告
                        {commentPattern: '^no default$'}  // 允许在最后注释no default,就不会有警告了
                    ],
                    eqeqeq: [
                        'warn',  // 强制使用===和!===,否则警告
                        'smart'  // 除了少数情况下不会有警告
                    ]
                }
                
            }

    # babel兼容性处理
        JavaScript编译器,主要用于将ES6语法编写的代码转换为向后兼容的JS语法,以便能够运行在当前和旧版本的浏览器或其他环境中。

        npm i babel-loader @babel/core @babel/preset-env -D

        写法:
            babel.config.*: 新建文件
                babel.config.js
                babel.config.json
            .babelrc.*: 新建文件
                .babelrc
                .babelrc.js
                .babelrc.json
            package.json中babel: 不需要创建文件,在原有文件基础上写

        配置:
            babel.config.js:
                module.exports = {
                    presets: ["@babel/preset-env"],  // 预设
                }

            注: presets预设,就是一组babel插件,扩展babel功能

        {
            test: /\.js$/,
            exclude: /node_modeles/,
            loader: "babel-loader",
            // options: {
            //     presets: ["@babel/preset-env"]  // 方法二
            // }
        }

        @babel/preset-env: 一个只能预设,允许你使用最新的JS
        @babel/preset-react: 一个用来编译react jsx语法的预设
        @babel/preset-typescript: 一个用来编译typescipt语法的预设
        @babel/core: 核心包

    # typescript
        npm i -D typescript ts-loader  //下载依赖包
        
    # 自动插入html:
        npm i html-webpack-plugin --save-dev  // 自动生成html文件

        const HtmlWebpackPlugin = require('html-webpack-plugin');
        ...
        plugins: [
            new HtmlWebpackPlugin({
                template: path.resolve(__dirname, 'public/index.html')  // 指定模板输出html文件
            }),
        ]
        ...

### 开发模式
    # webpack开发服务器(热更新)
        npm i webpack-dev-server --save-dev  // 开发服务器

        module.exports = {
            ...
            // 开发服务器
            devServer: {
                host: 'localhost',  // 启动服务器域名
                port: '3000',  // 端口号
                open: true,  // 自动打开
                // hot: true,  // HMR(默认打开)
            },
            ...
        }
        
        npx webpack serve  // 运行

### 生产模式
    配置指令:
        "start": "npm run dev",  // npm start
        "dev": "webpack serve --config ./config/webpack.dev.js",
        "build": "webpack --config ./config/webpack.prod.js"  // npm run build

    # 单独提出css文件
        npm i mini-css-extract-plugin --save-dev

        const MiniCssExtractPlugin = require("mini-css-extract-plugin");

        ...
        use: [MiniCssExtractPlugin.loader, "css-loader"],  // 替换style-loader
        ...
        plugins: [new MiniCssExtractPlugin({
            filename: "static/css/main.css"  // 指定输出位置
        })],
        ...

        css兼容性处理:(css-loader之后,less-loader之前)
            npm i postcss postcss-loader postcss-preset-env --save-dev

            ...
            {
                loader: 'postcss-loader',
                options: {
                    postcssOptions: {
                        plugins: [
                            'postcss-preset-env',  // 能解决大多数样式兼容问题
                        ],
                    },
                },
            },
            ...

        配置package.json:  
            "browserslist": [
                "last 2 version",
                "> 1%",
                "not dead"
            ]

    # 封装样式loader函数
        // 封装loader函数
        function getStyleLoader(pre) {
            return [
                MiniCssExtractPlugin.loader,
                'css-loader',
                {
                    loader: 'postcss-loader',
                    options: {
                        postcssOptions: {
                            plugins: ['postcss-preset-env']
                        },
                    },
                },
                pre,
            ].filter(Boolean);  // 过滤掉undefind
        }
        ...
        {
            test: /\.css$/i,
            use: getStyleLoader()
        }

    # css压缩
        npm i css-minimizer-webpack-plugin --save-dev

        const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");
        ...
        plugins: [new MiniCssExtractPlugin()]
        ...

    # html压缩
        注: 默认生产模式已经开启了html压缩和js压缩,不需要额外进行配置

## webpack5高级
    提升开发体验: SourceMap(源代码映射)
    提升打包构建速度: 
        HotModuleReplacement(HMR/热模块替换)
        OneOf、Include/Exclude
        Cache(缓存)
        Thead(多进程打包)
    减少代码体积:
        Tree Shaking(树摇)
        Babel
        Image Minimizer(压缩图片)
    优化代码运行性能:
        Code Split(代码分割)

### 提升开发体验
#### SourceMap(源代码映射)
    https://webpack.docschina.org/configuration/devtool/
    作用: 让开发或上线时代码报错能更加准错的错误提示

    开发模式: cheap-module-source-map
        优点: 打包编译速度快,只包含行映射
        缺点: 没有列映射

        module.exports = {
            ...
            mode: "development",
            devtool: "cheap-module-source-map"
        }

    生产模式: source-map
        优点: 包含行/列映射
        缺点: 打包编译速度更慢

        module.exports = {
            ...
            mode: "development",
            devtool: "source-map"
        }

### 提升打包构建速度
#### HMR(开发模式)
    原理: 在程序运行中,替换、添加或删除模块,而无需重新加载整个页面
    注: css默认开启,js则不行

    一般开发:
        if(module.hot){
            // 判断是否支持热模块替换功能
            module.hot.accept("./js/count");
            module.hot.accept("./js/sum");
        }

    项目开发:
        使用vue-loader、react-hot-loader

#### OneOf
    作用: 只匹配一次loader,提高打包速度

    ...
    module: {
        rules: [
            {
                oneOf: [  // 只匹配一次
                    {
                        test: /\.css$/,
                        use: [
                            'style-loader',
                            'css-loader'
                        ]
                    }
                ]
            }
        ]
    },
    ...

#### Include/Exclude
    注: 主要针对js文件(babel、eslint)

    include:
        包含,只处理xxx文件

    exclude:
        排除,除了xxx文件以外其他文件都处理

    ...
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modeles/,  // 排除mode_modules中的js文件
                // include: path.resolve(__dirname, "../src"),  // 只处理src下的文件,其他文件不处理
                loader: "babel-loader"
            }
        ]
    }
    ...

#### Cache(缓存)
    作用: 对eslint检查和babel编译结果进行缓存,提高二次打包速度

    ...
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modeles/,  // 排除mode_modules中的js文件
                loader: "babel-loader",
                options: {
                    cacheDirectory: true,  // 开启babel缓存
                    cacheCompression: false,  // 关闭缓存文件压缩
                }
            }
        ]
    },
    plugins: [
        new ESLintPlugin({
            context: path.resolve(__dirname, '../src'),  // 检测哪些文件
            cache: true,  // 开启缓存
            cacheLocation: path.resolve(__dirname, "../node_modules/.cache/eslint-webpack-plugin/.eslintcache")  // 指定缓存路径
        })
    ],
    ...

#### Thread(多线程)
    作用: 多进程打包,开启电脑的多个进程同时干一件事,速度更快
    注: 仅在特别耗时的操作中使用,因为每个进程启动就有大约600ms左右开销

    npm i thread-loader --save-dev

    const TerserPlugin = require("terser-webpack-plugin");  // 多进程压缩JS

    const os = require('os')
    const threads = os.cpu().length;  // 获取cpu核数

    ...
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modeles/,
                use: [
                    {
                        loader: 'thread-loader',  // 开启多进程
                        options: {
                            works: threads,  // 进程数量
                        }
                    },
                    {
                        loader: "babel-loader",
                        options: {
                            cacheDirectory: true,  // 开启babel缓存
                            cacheCompression: false,  // 关闭缓存文件压缩
                        }
                    }
                ]
            }
        ]
    },
    plugins: [
        new ESLintPlugin({
            context: path.resolve(__dirname, '../src'),  // 检测哪些文件
            threads,  // 开启多进程和设置进程数量
        })
    ],
    // webpack v5用法:
    optimization: {
        minimizer: [
            new TerserPlugin({
                parallel: threads  // 开启多进程和设置进程数量
            })
        ],
    },
    ...

### 减少代码体积
#### Tree Shaking(树摇)
    作用: 移除JavaScript中没有使用上的代码
    注: 依赖ES-Module

    webpack已经默认开启

#### Babel
    @babel/piugin-transform-runtime: 禁用了babel自动对每个文件的runtime注入,而是引入runtime,并且使所有辅助代码从这里引用。

    npm i @babel/plugin-transform-runtime --save-dev
    
    ...
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modeles/,  // 排除mode_modules中的js文件
                loader: "babel-loader",
                options: {
                    plugins: ["@babel/plugin-transform-runtime"],  // 减少代码体积
                },
            }
        ]
    },
    ...

#### Image Minimizer
    注: 如果是在线图片则不需要,本地项目静态图片才需要压缩

    npm i imagemin image-minimizer-webpack-plugin --save-dev

    // 无损压缩
    npm i imagemin-gifsicle imagemin-jpegtran imagemin-optipng imagemin-svgo --save-dev
    cnpm i imagemin-optipng --save-dev
    // 有损压缩
    npm install imagemin-gifsicle imagemin-mozjpeg imagemin-pngquant imagemin-svgo --save-dev
        注: 下载包会报错,需切换cnpm下载

    const ImageMinimizerPlugin = require("image-minimizer-webpack-plugin");

    ...
    new ImageMinimizerPlugin({
        minimizer: {
            implementation: ImageMinimizerPlugin.imageminGenerate,
            options: {
                plugins: [
                    ["gifsicle", { interlaced: true }],
                    ["jpegtran", { progressive: true }],
                    ["optipng", { optimizationLevel: 5 }],
                    [
                        "svgo",
                        {
                            plugins: [
                                'preset-default',
                                'prefixIds',
                                {
                                    name: 'sortAttrs',
                                    params: {
                                    xmlnsOrder: 'alphabetical',
                                    },
                                },
                            ],
                        },
                    ],
                ],
            },
        },
    })
    ...

### 优化代码运行性能
#### Code Split(代码分割)
    作用: 
        1、分割文件: 将打包生成的文件进行分割,生成多个js文件
        2、按需加载: 需要哪个文件就加载哪个文件

    SplitChunksPlugin:
        https://webpack.docschina.org/plugins/split-chunks-plugin/

    ...
    // webpack v5
    optimization: {
        // 代码分割
            splitChunks: {
                chunks: 'all',  // 对所有模块都进行分割
                // // 以下都是默认值
                // minSize: 20000,  // 分割代码最小的大小
                // minRemainingSize: 0,  // 类似于minSize《最后确保提取的文件大小不能为0
                // minChunks: 1,  // 至少被引用的次数,满足条件才会代码分割
                // maxAsyncRequests: 30,  // 按需加载时并行加载的文件的最大数量
                // maxInitialRequests: 30,  // 入口js文件最大的并行请求数量
                // enforceSizeThreshold: 50000,  // 超过50kb一定会单独打包(此时会忽略minRemainingSize、maxAsyncRequests、maxInitialRequests)
                // cacheGroups: {  // 组,哪些模块要打包到一个组
                //   defaultVendors: {  // 组名
                //     test: /[\\/]node_modules[\\/]/,  // 需要打包到一起的模块
                //     priority: -10,  // 权重(越大越高)
                //     reuseExistingChunk: true,  // 如果当前chunk包含已从主bundle中拆分出的模块,则它将被重用,而不是生成新的模块
                //   },
                //   default: {  // 其他没有写的配置会使用上面的默认值
                //     minChunks: 2,  // 这里的minChunks权重更大
                //     priority: -20,
                //     reuseExistingChunk: true,
                //   },
                // },
                // 修改配置
                cacheGroups: {
                    default: {  // 其他没有写的配置会使用上面的默认值
                        minSize: 0,  // 我们定义的文件体积太小了,所以要改打包的最小文件体积
                        minChunks: 2,  // 这里的minChunks权重更大
                        priority: -20,
                        reuseExistingChunk: true,
                    },
                },
            },
    }
    ...

#### Preload/Prefetch(预加载/懒加载)
    作用: 
        Preload: 告诉浏览器立即加载资源。(适用当前页面)
        Prefetch: 告诉浏览器在空闲时才开始加载资源。(适用下一个页面)

    注: 兼容性较差。

    cnpm i @vue/preload-webpack-plugin --save-dev

    const PreloadWebpackPlugin = require('@vue/preload-webpack-plugin');

    ...
    new PreloadWebpackPlugin({
        rel: 'preload',
        as: 'script'
        // rel: 'prefetch'
    })
    ...

#### Network Cache(chunkHash做单独文件)
    filename: 'static/js/[name].chunk.[contenthash:6].js',
    ...
    optimization: {
        runtimeChunk: {
            name: (entrypoint) => `runtime~${entrypoint.name}`,
        },
    },
    ...

#### Core-js
    作用: 专门用来做ES6以及以上API的polyfill
        polyill: 翻译过来叫做垫片/补丁。就是用社区上提供的一段代码,让我们在不兼容某些新特性的浏览器上,使用该特性。

    npm i core-js --save-dev

    // import 'core-js'  // 完整引入

    import 'core-js/es/promise'  // 按需引入(至少引入一次)

    babel.config.js:
        module.exports = {
            // 预设
            presets: [
                ["@babel/preset-env", {
                    useBuiltIns: "usage",  // corejs自动按需引入
                    corejs: 3
                }]
            ]
        }

#### PWA
    渐进式网络应用程序(progressive web application - PWA): 是一种可以提供类似于native app(原生应用程序)体验的Web App技术。
    作用: 在离线时应用程序能够继续运行功能,内部通过Service Workers技术实现

    npm i workbox-webpack-plugin --save-dev

    const WorkboxPlugin = require('workbox-webpack-plugin');

    plugins: [
        new HtmlWebpackPlugin({
            // title: 'Output Management',
            title: 'Progressive Web Application',
        }),
        new WorkboxPlugin.GenerateSW({
            // 这些选项帮助快速启用 ServiceWorkers
            // 不允许遗留任何“旧的” ServiceWorkers
            clientsClaim: true,
            skipWaiting: true,
        }),
    ],

    注册Service Worker: main.js:
    if ('serviceWorker' in navigator) {
        window.addEventListener('load', () => {
            navigator.serviceWorker.register('/service-worker.js').then(registration => {
                console.log('SW registered: ', registration);
            }).catch(registrationError => {
                console.log('SW registration failed: ', registrationError);
            });
        });
    }


## 解决动态引入import报错
    npm i @babel/eslint-parser eslint-plugin-import --save-dev

    .eslintrc.js:
        parser: "@babel/eslint-parser",  // 支持最新的ECMAScript标准
        plugins: ["import"],  // 解决动态导入import报错

## webpack魔法命名
    // /* webpackChunkName: "count" */,webpack魔法命名
    import(/* webpackChunkName: "count" */ "./js/count")
    .then((res)=>{
        console.log('模块加载成功', res.text())
    })

    webpack.prod.js:
        module.exports = {
            ...
            output: {
                ...
                chunkFilename: "static/js/[name].chunk.js",  // 打包输出的其他文件命名(魔法命名)
                ...
            }
            ...
        }

## 能够使用户在引入模块时不带扩展
    // 能够使用户在引入模块时不带扩展
    module.exports = {
        ...
        resolve: {
            extensions: ['.js', '.json', '.wasm'],
        },
        ...
    }

## VUE_webpack配置
    npm i vue

    Vue-Loader:
    npm install vue-loader vue-template-compiler -D

    // webpack.config.js
        // 处理页面警告
        const {DefinePlugin} = require('webpack')  // 专门用来定义环境变量
        const { VueLoaderPlugin } = require('vue-loader')

        module.exports = {
            module: {
                rules: [
                    // ... other rules
                    {
                        test: /\.css$/,
                        use: [
                        'vue-style-loader',  // 需要用vue-style-loader
                        'css-loader'
                        ]
                    },
                    {
                        test: /\.vue$/,
                        loader: 'vue-loader'
                    }
                ]
            },
            plugins: [
                new VueLoaderPlugin(),
                // cross-env定义的环境变量给webpack使用
                // DefinePlugin定义环境变量给源代码使用,解决vue3报警问题
                new DefinePlugin({
                    __VUE_OPTIONS_API__: true,  // 是否使用工具
                    __VUE_PROD_DEVTOOLS__: false  // 生产环境下是否出现警告
                })

            ]
        }

    // .eslintrc.js:
        module.exports = {
            root: true,
            // 继承其他规则
            extends: [
                "plugin:vue/vue3-essential",  // vue3规则  npm i eslint-plugin-vue -D
                "eslint:recommended",  // eslint官方规则
            ],
            parser: "@babel/eslint-parser",  // 支持最新的ECMAScript标准
            env: {
                browser: true,  // 浏览器全局变量
                node: true,  // nodejs全局变量
                es6: true,  // 启用es6新特性
            },
            // 解析选项
            parserOptions: {
                ecmaVersion: 6, // ES语法版本
                sourceType: "module", // ES模块化
            },
            // 具体检查规则
            rules: {
                "no-var": 1
            },
            plugins: ["import"],  // 动态导入import
            ignorePatterns: [
                "dist",
                "node_modules"
            ]
        }

    // babel.config.js:
        npm i @vue/cli-plugin-babel -D
        module.exports = {
            // 预设
            presets: [
                ["@vue/cli-plugin-babel/preset"]
            ]
        }



## 合并配置
    npm i cross-env -D

    package.json:
        // 定义环境变量  cross-env
        "dev": "cross-env NODE_ENV=development webpack serve --config ./config/webpack.config.js",
        "build": "cross-env NODE_ENV=production webpack --config ./config/webpack.config.js"

    // 获取环境变量
    const isProduction = process.env.NODE_ENV === "production"
