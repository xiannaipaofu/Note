## MongoDB
    ## mongoose
        npm i mongoose

        const mongoose = require('mongoose')  // 引入mongoose
        mongoose.set('strictQuery', true)  // 关闭警告
        mongoose.connect('mongodb://127.0.0.1:27017/hellokittyDB')  // 连接数据库
        mongoose.connection.once('open', ()=>{})  // 连接成功回调
        mongoose.connection.on('error', ()=>{})  // 连接失败回调
        mongoose.connection.on('close', ()=>{})  // 连接关闭回调

        // 创建文档的结构对象, 设置集合中文档的属性及属性值类型
        let bookcase = new mongoose.Schema({name: String})
        // 创建模型对象, 对文档操作增删改查
        let bookModel = mongoose.model('bookcase', bookcase)  //第三个参数连接数据库已存在集合 

        BookModel.create({})  // 增
    
        BookModel.deleteOne({条件})  // 删,单条
        BookModel.deleteMany  // 批量

        BookModel.updateOne({条件}, {newValue})  // 改
        BookModel.updateOneMany 

        BookModel.findOne({条件})  // 查
        BookModel.findById('id')
        BookModel.find({})

        mongoose.disconnect()  // 关闭数据库连接

        ## mongoose字段类型
            type:
                String
                Number
                Boolean
                Array
                Date
                Buffer
                Mixed  // 任意类型, mongoose.Schema.Types.Mixed
                ObjectId  // 对象ID, mongoose.Schema.Types.ObjectId
                Decimal128  // 高精度数字, mongoose.Schema.Types.Decimal128

            options:
                required: true,  // 必填项
                default: '',  // 默认值
                enum: ['男', '女'],  // 枚举, 值必须是其中之一
                unique: true  // 唯一值, 需要重建集合才生效

    ## mongodb需使用替代符合
        例: {price: $gt: 20}
        $gt - >
        $lt - <
        $gte - >=
        $lte - <=
        $ne - !==

        $or  或  $or:[{age: 18}, {age: 20}]
        $and  与  $and: [{age: {$lt:20}, {age: {$gt: 15}}}]

        bookModel.find({name: new RegExp('')})  // 正则

    ## 个性化读取
        例: bookModel.find().select({name: 1, id: 0}).sort({prece: -1}).exec((err, data)=>{})

        .select({name: 1, id: 0})  // 筛选, 只返回name
        .sort({prece: -1})  // 排序, 1升序、-1降序
        .skip(3).limit(3)  // 数据截取(跳过/限定), 跳过前3条, 每次返回3条
        
    图形化工具
        Robo 3T 免费  https://github.com/Studio3T/robomongo/releases
        Navicat 收费  https://www.navicat.com.cn