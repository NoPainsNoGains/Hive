#Hive
>1. hive简介
>>hive功能：数据ETL工具(抽取、转换、加载)、数据存储管理和大型数据集的查询和分析能力、Hive QL<BR>
>>hive缺点：
>>>不提供数据排序和查询cache功能<BR>
>>>不提供在线事务处理<BR>
>>>不提供实时的查询和记录级的更新<BR>
>
>>hive优点:<BR>
>>>可扩展性(可以自动适应机器数目和数据量的动态变化)<BR>
>>>可延展性(结合mapreduce和用户定义的函数库)
>>>良好的容错性和低约束的数据输入格式<br>
>
>2.hive的体系结构<br>
![](http://i.imgur.com/UIPxsJT.png)<br>
>3 hive的用户接口
>>3.1 命令行CLI--启动的时候 默认会启动一个hive服务<br>
>>3.2 客户端Client--用户连接至HiveServer <br>
>>3.3 web界面wui--浏览器<br>
>
>4.常用的进程和服务
>>4.1 HiveServer:让Hive提供Trift服务的服务器形式运行，可以允许用不同的语言编写的客户端进行通讯服务。通过设置HIVE_PORT环境变量设置服务器监听的端口号 默认为10000<BR>
>>4.2 metastore:默认下和Hive服务运行在同一个进程中。使用这个服务，可以让metastore作为一个单独的进程运行，通过指定METASTORE-PORT来指定监听的端口号<br>
>>4.3 metastore的三种连接方式:
>>>4.3.1 single user Mode:连接到derby内嵌的数据库 一般用于unitTest <br>
>>>4.3.2 Muti User Mode:通过网络连接到一个数据库中(经常使用) <br>
>>>4.3.3 Remote Server Mode: 用于非java客户端访问元数据库。在服务器方MetaStoreServer，客户端利用Thrift通过MetaStoreServer来访问元数据库 <br>
>![](http://i.imgur.com/kioZcpC.png) <br>
>注意:元数据要不断的更新、修改、读取(hive自身不能更实时新) 故而要单独用关系数据库进行存储<br>
>
>5.hive与常规数据库区别
>>5.1数据存储位置：hive的数据建立在hadoop的hdfs之上。数据库则存储在块设备或本地文件系统中<br>
>>5.2查询语言:hive的HQL很弱，update、delete不能使用。普通数据库则很强大<br>
>>5.3数据格式:hive没有专门的格式.可以用户自定义，需要指定三个属性:
>>>列分隔符<br>
>>>行分隔符<br>
>>>读物文件数据的方式(TextFile、SequenceFile、RCFile)<br>
>
>>&nbsp;&nbsp;&nbsp;&nbsp;hive加载数据过程中，不需要从用户数据格式转换到hive定义的数据格式，不会对数据本身进行任何修改，只是将数据内容复制或者移动到相应的HDFS目录中<br>
>
>>5.4数据更新:hive针对数据仓库而设计，故读多写少，hive不支持对数据的改写和添加，所有的数据在加载的时候已经确定好。普通数据库通过insert update<br>
>>5.5索引:hive不会对数据进行任何处理包括建立索引(hive采用暴力扫描 mapreduce)<br>
>>5.6执行时间:hive的执行时间有较高的延迟，产生的延迟原因:
>>>hive查询数据进行全表的扫描<br>
>>>MapReduce本身具有较高的延迟<br>
>
>>5.7可扩展性:Hive建立在hadoop上，结点可以任意增加删除.数据库因为ACID严格限制，扩展能力有限<br>
>>5.8数据规模:hive数据规模可以很大 达到TB。
