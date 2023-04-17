## Webpack
    前端资源构建工具，一个静态模块打包器

    webpack默认对外暴露图片、JSON数据格式
    

        打包
            npm i browserify
            npm i babel-cli
            npm i bable-preset-es2015 

            //es6转换es5
            babel url -d url
            //打包
            browserify url -o url

    less
        npm i -D less less-loader css-loader style-loader
        npm i -D postcss postcss-loader postcss-preset-env