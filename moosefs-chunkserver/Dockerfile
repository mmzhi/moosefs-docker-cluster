FROM ubuntu:16.04

# 添加运行脚本
ADD start-chunkserver.sh /home/start-chunkserver.sh

# 安装 wget, lsb-release 和 curl
RUN apt-get update && apt-get install -y wget lsb-release curl && \
# 添加 key
    wget -O - https://ppa.moosefs.com/moosefs.key | apt-key add - && \
    echo "deb http://ppa.moosefs.com/moosefs-3/apt/ubuntu/xenial xenial main" > /etc/apt/sources.list.d/moosefs.list && \
# 安装 MooseFS chunkserver
    apt-get update && apt-get install -y moosefs-chunkserver && \
# 设置运行脚本
    chown root:root /home/start-chunkserver.sh && \
    chmod 700 /home/start-chunkserver.sh && \
    sed -i '/MFSCHUNKSERVER_ENABLE=false/c\MFSCHUNKSERVER_ENABLE=true' /etc/default/moosefs-chunkserver

# 设置配置文件
ADD mfschunkserver.cfg /etc/mfs/mfschunkserver.cfg
ADD mfshdd.cfg /etc/mfs/mfshdd.cfg

# 设置数据卷
VOLUME /etc/mfs
VOLUME /var/lib/mfs
VOLUME /data

# 暴露端口
EXPOSE 9419 9420 9422

# 运行脚本
CMD ["/home/start-chunkserver.sh", "-d"]
