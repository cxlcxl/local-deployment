FROM nginx:latest

WORKDIR /usr/share/nginx/html

# 解决本地虚拟机共享文件夹权限问题
RUN groupadd --gid 994 vboxsf
RUN usermod -aG vboxsf nginx