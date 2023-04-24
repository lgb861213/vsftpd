# Dockerfile for vsftpd on CentOS
FROM centos/systemd


ENV PASV_MIN_PORT=30001 \
    PASV_MAX_PORT=30020 \
    PASV_ADDRESS=127.0.0.1

#安装软件
RUN yum -y update; yum -y install vsftpd net-tools; yum clean all

#创建虚拟用户
COPY vusers.txt /etc/vsftpd/
RUN db_load -T -t hash -f /etc/vsftpd/vusers.txt /etc/vsftpd/vsftpd-virtual-user.db; rm -v /etc/vsftpd/vusers.txt; \ 
	chmod 600 /etc/vsftpd/vsftpd-virtual-user.db
# 配置 vsftpd 服务器
COPY vsftpd.conf /etc/vsftpd/
COPY vsftpd.virtual /etc/pam.d/
RUN  mkdir -p /var/ftp/pub
RUN  mkdir -p /var/run/vsftpd/empty
RUN mkdir -p /etc/vsftpd/vsftpd_user_conf
#拷贝虚拟用户的配置文件
COPY user1 /etc/vsftpd/vsftpd_user_conf
COPY user2 /etc/vsftpd/vsftpd_user_conf
#创建虚拟用户的家目录
RUN mkdir -p /var/ftp/user1
RUN mkdir -p /var/ftp/user2
RUN chown -R ftp:ftp /var/ftp


EXPOSE 20 21 $PASV_MIN_PORT-$PASV_MAX_PORT

# 启动服务
#CMD ["/usr/sbin/vsftpd", "/etc/vsftpd/vsftpd.conf", "&"]
CMD ["/usr/sbin/vsftpd","-obackground=NO"]

