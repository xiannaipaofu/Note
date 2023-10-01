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