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

**守护容器**

长期运行的容器，没有交互式回话

docker run --name daemon_dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"

查看容器的运行日志

docker logs daemon_dave

监控docker日志

docker logs -f daemon_dave

跟踪日志的某一片段

docker logs -tail 10 daemon_dave 获取日志的最后10行

docker logs -tail 0 -f daemon_dave 跟踪最新的日志而不必读取整个日志文件

CTR + C 退出日志跟踪

查看容器内部运行的进程

docker top daemon_dave

显示一个或多个容器的统计信息

docker stats daemon_dave

docker stats daemon_kate daemon_clare daemon_sarah

在容器内运行进程

docker exec -d daemon_dave touch /etc/new_config_file

docker exec -d -t -i daemon_dave /bin/bash

停止守护容器

docker stop daemon_dave

自动重启容器

docker run --restart=always --name daemon_dave -d ubuntu /bin/bash

获取更多容器的信息

docker inspect daemon_dave

删除容器

docker rm daemon_dave

删除所有容器

docker rm `docker ps -a -q`

-a :列出所有容器

-q:只 返回容器的ID