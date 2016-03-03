Base on version 3.2
* 设置MongoDB的环境
设置DB的存储路径，可以通过下面的命令指定db的存储路径
```
mongod.exe --dbpath d:\test\mongodb\data
```
如果路径中包含空格，需要将路径用引号

* 启动MongoDB
```
mongod.exe --dbpath ""
```

* 连接MongoDB
```
mongo.exe
```

### 以服务的方式启动MongoDB
* 创建目录存储 数据和log信息
```
mkdir d:\data\db
mkdir d:\data\log
```

* 创建配置文件
比如 mongod.cfg
```
systemLog:
  destination:file
  path: d:\data\log\mongo.log
storage:
  dbpath: d:\data\db
```

* 安装MongoDB的服务

```
mongod.exe --config d:\data\mongod.cfg --install
```

* 启动MongoDB服务
```
net start MongoDB
```
* 停止、去除服务
```
net stop MongoDB

mongod.exe --remove
```

### 创建能够自启动的Windows服务
* 创建数据和log目录
```
mkdir d:\data\db\
mkdir d:\data\log
```
* 创建配置文件 mongod.cfg
配置相关的美容
```
systemLog:
  destination: file
  path: d:\data\log\mongod.log
storage:
  dbpath: d:\data\db
```
* 创建MongoDB服务
```
sc create MongoDB binPath= "..\bin\mongod.exe" --service --config= "..\mongod.cfg" DisplayName= "MongoDB" start= "auto"
```
* 启动服务
```
net start MongoDB
```
* 停止、移除MongoDB服务
```
net stop MongoDB

sc delete MongoDB
```


### MongoDB的配置选项
version 2.6之后支持YAML格式的配置文件
YAML不支持tab，缩进请使用空格

example:
```
systemLog:
  destination: file
  path: "d:\data\log\mongod.log"
  logAppend:true
storage:
  journal:
    enabled: true
  dbpath: d:\data\db
```

使用配置文件：
```
mongod --config "d:\data\mongod.cfg"
mongod -f "d:\data\mongod.conf"
```
