---
layout:     post
title:      "mongodb字段操作"
date:       2022-02-21 17:45:00 +0800
author:     "True-Think"
header-img: "img/new/green_kimtour.jpg"
catalog: true
tags:
    - 技术
    - mongodb
---
## 重复字段去除
### （1）、查重
```shell
db.getCollection('doc_base_info').aggregate([
{       '$group':{
            _id:{doc_id: '$doc_id'}, 
            count:{'$sum':1}
        }
},  {'$match': {count:{'$gt':1}}}
], {allowDiskUse:true})
```


### （2）、去重

```shell
db.getCollection('doc_base_info').aggregate([
{       '$group':{
            _id:'$doc_id', 
            count:{'$sum':1}, 
            dups:{'$addToSet':'$_id'}
        }
},  {'$match': {count:{'$gt':1}}}
], {allowDiskUse:true}).forEach(function(doc){
    doc.dups.shift();
    db.doc_base_info.remove({_id:{'$in':doc.dups}}); # 注意修改名字
});
```
doc.dups.shift(); // 保留一个


## 2、不含有某字段查询
```shell
db.getCollection('doc_base_info').find({ "category_id":{"$exists": false} }, {"doc_id": 1}).count()
```

## 3、更新字段
```shell
db.getCollection('train_status_test').update({}, {"$set":{"finished": 1}}, {"multi":true})
```
pymongo
```shell
self.doc_db_info.update({"doc_id": {"$in": doc_ids}}, {"$set": {"is_train": 1}},
                                multi=True, upsert=False)
```

## 4、类型转换
```shell
db.doc_base_info.find({doc_id:{$type:2}}) //查询doc_id字段数据类型为字符串
db.doc_base_info.find({doc_id:{$type:"string"}}) //查询doc_id字段数据类型为字符串
```
doc_id字段从string转为int型
```shell
db.getCollection('doc_base_info').find({'doc_id' : { "$type" : 2 }}).forEach(function(x) {
    x.doc_id = NumberInt(x.doc_id);
    db.getCollection('doc_base_info').save(x);
})
```

## 5、更新 不同的每条
每条不同更新
```shell
update_data = []  # 待更新列表
doc_up_dict = []  # 单条待更新字段

update_data.append(pymongo.UpdateMany({"_id": item["_id"]}, {'$set': doc_up_dict}))
mongo_db.bulk_write(update_data)
```