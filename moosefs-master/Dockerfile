FROM ubuntu:16.04

# 添加运行脚本
ADD start.sh /home/start.sh

# 安装 wget, lsb-release 和 curl
RUN apt-get update && apt-get install -y wget lsb-release curl && \
# 添加 key
    wget -O - https://ppa.moosefs.com/moosefs.key | apt-key add - && \
    echo "deb http://ppa.moosefs.com/moosefs-3/apt/ubuntu/xenial xenial main" > /etc/apt/sources.list.d/moosefs.list && \
# 安装 MooseFS master and CGI
    apt-get update && apt-get install -y moosefs-master moosefs-cgi moosefs-cgiserv && \
# 设置运行脚本
    chown root:root /home/start.sh && \
    chmod 700 /home/start.sh

#开启 CGI Serv
ADD moosefs-cgiserv /etc/default/moosefs-cgiserv

# 设置配置文件
ADD mfsmaster.cfg /etc/mfs/mfsmaster.cfg
ADD mfsexports.cfg /etc/mfs/mfsmaster.cfg

# 设置数据卷
VOLUME /etc/mfs
VOLUME /var/lib/mfs

# 暴露端口
EXPOSE 9420 9421 9422 9423 9424 9425

# 运行脚本
CMD ["/home/start.sh", "-d"]
