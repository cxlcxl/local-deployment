FROM mysql:5.7

COPY my.cnf /etc/mysql/conf.d/
RUN mkdir -p /var/lib/mysql

# 解决本地虚拟机共享文件夹权限问题
RUN groupadd --gid 994 vboxsf
RUN usermod -aG vboxsf mysql

EXPOSE 3306