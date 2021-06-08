通过docker部署的php7.3、nginx、redis、mysql等环境。

## 1、介绍
```
	php7.3支持swoole扩展。
	redis 集成集群部署。
```

## 2、目录结构
```
├── mysql                               # mysql目录
│   └── ...                     
├── nginx                               #nginx目录
│   ├── conf   
		├── conf.d 						#其他目录
		├── vhost						#nginx站点配置目录
		├── Dockerfile					#nginx构建文件
		├── nginx.conf   				#nginx配置文件
├── php                                 #php目录
│   ├── conf
		├── php.ini 					#php配置文件
	├── Dockerfile 						#php构建文件
├── redis                               #redis目录
│   ├── config							#redis配置文件目录
	├── sh 								#redis脚本文件目录   
	├── Dockerfile 						#php构建文件
├── .env								#环境变量配置文件
├── docker-compose.yaml 				#docker-compose配置文件
```

## 3、使用
```
	注意：启动服务前需要进入到当前根目录下。
	docker-compose build				# 安装

	docker-compose up -d 				# docker-compose配置里启动所有服务


	docker-compose ps 					# 查看所有服务

	docker-compose images				# 查看所以镜像
	
	docker-compose restart php 			# 重启php务

	docker-compose restart nginx 		# 重启nginx服务

	其他命令课参考docker-compose的文档：https://docs.docker.com/compose/
	或者--help查看相关命令
```

## 4、总结

docker run --name zk1 -v /home/xiaowu/PHP/github/docker/zk/zk1/conf:/apache-zookeeper-3.7.0-bin/conf -v /home/xiaowu/PHP/github/docker/zk/zk1/data:/apache-zookeeper-3.7.0-bin/data  -d zookeeper
docker run --name zk2 -v /home/xiaowu/PHP/github/docker/zk/zk2/conf:/apache-zookeeper-3.7.0-bin/conf -v /home/xiaowu/PHP/github/docker/zk/zk2/data:/apache-zookeeper-3.7.0-bin/data  -d zookeeper
docker run --name zk3 -v /home/xiaowu/PHP/github/docker/zk/zk3/conf:/apache-zookeeper-3.7.0-bin/conf -v /home/xiaowu/PHP/github/docker/zk/zk3/data:/apache-zookeeper-3.7.0-bin/data  -d zookeeper