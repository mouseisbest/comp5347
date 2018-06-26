# MongoDB 教程
## connection
- ```mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]```

## create
- create DB: ```use DB_NAME```
- create collection: ```db.createCollection(name, options)```

## delete/drop
- drop DB: ```db.dropDatabase()```
- drop collection: ```db.collection.drop()```

## insert document (使用```insert()```和```save()```方法向集合插入文档）
- ```db.collection.insert(document)```
- 也可声明```document={...}```, ```db.collection.insert(document)```

## update()
- 语法格式：  
	```
	db.collection.update(
	   <query>,
	   <update>,
	   {
		 upsert: <boolean>,
		 multi: <boolean>,
		 writeConcern: <document>
	   }
	)

	//query : update的查询条件，类似sql update查询内where后面的。   
	//update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的  
	//upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。  
	//multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。  
	//writeConcern :可选，抛出异常的级别。  
	```
- 例：```db.collection.update( { field: value }, { $push: { field: value1 } } );```
- 修改器：
	- $inc: ```{$inc: {"key": NUM}``` //将key的值增减NUM(NUM是整数，可以为负)， key必须为满足条件的数字型
	- $set: 用来指定一个键并更新键值，若键不存在并创建。 ```{#set: {"key": "value"}``` value可以为数字, 可以改变value的类型
	- $unset: 使用修改器$unset时，不论对目标键使用1、0、-1或者具体的字符串等都是可以删除该目标键。 ```{$unset: {"key": 0/1/-1}}```
	- $push: 向文档的某个数组类型的键添加一个数组元素，不过滤重复的数据。添加时键存在，要求键值类型必须是数组；键不存在，则创建数组类型的键。 ```{$push: {"key": "value"}}```
	- $pop: 从数组的头或者尾删除数组中的元素
	- $upsert
	
- save() function 语法格式
```
db.collection.save(
	<document>,
	{
		writeConcern: <document>
	}
)
//document : 文档数据。  
//writeConcern :可选，抛出异常的级别。
```

## remove()
- 语法格式：>2.6版本
```
db.COLLECTION_NAME.deletMany({status: "A"})
or
db.COLLECTION_NAME.deleteOne({status: "D"})
```

## find()
- ```db.collection.find(query, projection)```  //query:查询条件, projection: 查询时返回文档中的所有键值
- pretty()方法：以格式化的方式显示所有文档。  ```db.COLLECTION_NAME.find().pretty()```
- ```findOne()```
- 查找条件 (where)
	- 等于     |  ```{<key>: <value>}```         |  ```db.col.find({"name": "hao"}).pretty()```
	- 小于     |  ```{<key>: {$lt: <value>}}```  |  ```db.col.find({"value": {$lt: 50}}).pretty()```
	- 小于等于 |  ```{<key>: {$lte: <value>}}``` |  ```db.col.find({"value": {$lte: 50}}).pretty()```
	- 大于     |  ```{<key>: {$gt: <value>}}```  |  ```db.col.find({"value": {$gt: 50}}).pretty()```
	- 大于等于 |  ```{<key>: {$gte: <value>}}``` |  ```db.col.find({"value": {$gte: 50}}).pretty()```
	- 不等于   |  ```{<key>: {$ne: <value>}}```  |  ```db.col.find({"value": {$ne: 50}}).pretty()```
- 查找条件 (AND)
	- ```db.COLLECTION_NAME.find({"key1": "value1", "key2": "value2"})```
- 查找条件 (OR)
```
>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```
- AND OR 联合使用
```
db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
```

## limit(), Skip()方法
- limit():
```db.COLLECTION_NAME.find().limit(NUMBER)```  //取前NUMBER个记录
- Skip():
```db.COLLECTION_NAME.find().limit(NUMBER1).skip(NUMBER2)```  //取前NUMBER1个，跳过前NUMBER2个

## sort()
- 语法：```db.COLLECTION_NAME.find().sort({KEY:1})``` //按KEY进行排序，1为升序，-1为降序

## aggregate(): 
- MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。
- 语法结构：```db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)```
- 聚合表达式：
	- $sum      |  求总和                                       |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])```
	- $avg      |  求平均值                                     |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])```
	- $min      |  获取集合中所有文档对应键最小值               |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])```
	- $max      |  获取集合中所有文档对应键最小值               |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])```
	- $push     |  在结果文档中插入值到一个数组中               |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])```
	- $addToSet |  在结果文档中插入值到一个数组中，不会重复     |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])```
	- $first    |  根据资源文档的排序获取第一个文档数据。       |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])```
	- $last     |  根据资源文档的排序获取最后一个文档数据       |  
	```db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])```
- pipeline: 将当前命令的输出结果作为下一个命令的参数。
	- $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
	- $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
	- $limit：用来限制MongoDB聚合管道返回的文档数。
	- $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
	- $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
	- $group：将集合中的文档分组，可用于统计结果。
	- $sort：将输入文档排序后输出。
	- $geoNear：输出接近某一地理位置的有序文档。
	- 例：
		- $project:
		```
		db.article.aggregate(
			{ $project : {
				title : 1 ,
				author : 1 ,
			}}
		);
		```
		- $match:
		```
		db.articles.aggregate([
			{ $match : { score : { $gt : 70, $lte : 90 } } },
			{ $group: { _id: null, count: { $sum: 1 } } }
		]);
		//注意，多个操作放到 [] 中，用 {} 包括， 用 , 隔开
		```
		- $skip
		```
		db.article.aggregate(
			{ $skip : 5 });
		```
		
		