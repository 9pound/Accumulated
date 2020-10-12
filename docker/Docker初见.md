# Docker

常用命令

**启动**

sudo systemctl start docker 

**开机启动**

sudo systemctl enable docker

**看docker运行没有，info命令返回所有容器和镜像的数量，驱动，基本配置信息。**

docker info

**创建容器**

docker run

docker run -i -t ubuntu /bin/bash

-i：开启标准输入stdin

-t：为容器分配伪tty终端

**创建容器时给他命名**

docker run --name bob_the_container -i -t ubuntu /bin/bash

**容器的命名必须是唯一的可以使用docker rm删除容器**

docker rm

**停止容器**

exit

**查看当前系统中的容器列表**

docker  ps -a

**列出最后一个运行的容器，无论其正在运行还是已经停止**

docker ps -l 

**启动容器**

docker start ID/name

**重启容器**

docker restart

**重新附着到容器会话上**

docker attach bob_the_container

