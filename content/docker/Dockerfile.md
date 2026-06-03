---
title: Dockerfile
source: feishu
space: docker
---

Dockerfile
每条保留字指令必须大写且后面至少要跟随一个参数
指令从上到下执行
每条指令都会创建一个新的镜像层并对镜像进行提交
编写—>当前dockerfile目录下构建docker build -t 新镜像名字:TAG .
保留字
FROM：基础镜像，当前镜像基于哪个镜像，第一条必须FROM
MAINTAINER:镜像维护者的姓名和邮箱
RUN：容器构建时需要运行的命令，格式：shell、exec。RUN yum -y install vim在docker build时运行
EXPOSE：当前容器对外暴露的端口
WORKDIR：指定在创建容器后，终端默认登陆进来的工作目录，docker run bash进去的工作目录
USER：指定该镜像以什么样的用户去执行，默认root
ENV：用来构建镜像过程中设置的环境变量PATH
VOLUME：容器数据卷，用于数据保存和持久化工作
ADD：将宿主机目录下的文件拷贝进镜像且会自动处理URL和解压tar压缩包，使用相对路径的压缩包，那么包要和Dockerfile放在同一位置
COPY：拷贝文件和目录到镜像中。 COPY 源路径 目的路径
CMD：指定容器启动后要干的事情，dockerfile中可以有多个CMD命令，但只有最后一个生效，CMD会被docker run 之后的参数/bin/bash替换，在docker run时运行，变参
ENTRYPOINT：用来指定一个容器启动时要运行的命令，但是不会被docker run后面的命令覆盖，可以和CMD一起用，定参

