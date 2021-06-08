
docker run --name zk1 -p 2181:2181 -v /home/xiaowu/PHP/github/docker/zk/zk1/conf/zoo.cfg:/conf/zoo.cfg -v /home/xiaowu/PHP/github/docker/zk/zk1/data:/data  -d zookeeper
docker run --name zk2 -p 2182:2181 -v /home/xiaowu/PHP/github/docker/zk/zk2/conf/zoo.cfg:/conf/zoo.cfg -v /home/xiaowu/PHP/github/docker/zk/zk2/data:/data  -d zookeeper
docker run --name zk3 -p 2183:2181 -v /home/xiaowu/PHP/github/docker/zk/zk3/conf/zoo.cfg:/conf/zoo.cfg -v /home/xiaowu/PHP/github/docker/zk/zk3/data:/data  -d zookeeper

echo stat | nc 172.17.0.2 2181




