FROM nginx:1.15

# 添加运行脚本
ADD start-client.sh /home/start-client.sh

# 安装 wget, lsb-release and curl
RUN apt-get update && apt-get install -y wget lsb-release curl fuse libfuse2 tree gnupg && \
# 添加 key
    wget -O - https://ppa.moosefs.com/moosefs.key | apt-key add - && \
    echo "deb http://ppa.moosefs.com/moosefs-3/apt/debian/stretch stretch main" > /etc/apt/sources.list.d/moosefs.list && \
# 安装 MooseFS client
    apt-get update && apt-get install -y moosefs-client && \
# 配置运行脚本
    chown root:root /home/start-client.sh && \
    chmod 700 /home/start-client.sh

RUN chown root:root /home/start-client.sh && \
    chmod 700 /home/start-client.sh

# 添加配置文件
ADD mfsmount.cfg /etc/mfs/mfsmount.cfg

# 设置数据卷
VOLUME /etc/mfs

CMD ["/home/start-client.sh"]