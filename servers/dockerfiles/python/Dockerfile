FROM python:3.9

#RUN python -m venv /app/venv
#RUN source /app/venv/bin/activate

RUN python -m pip install --upgrade pip

#RUN mkdir -p /var/run/uwsgi/
WORKDIR /app/hidata

### ********* dockerfile 注释请另起一行 *********
# 当前 dockerfile 为起始地址
COPY . /app/hidata/
RUN pip install -r /app/hidata/serve/requirements.txt

# 解决本地虚拟机共享文件夹权限问题
RUN groupadd --gid 994 vboxsf
RUN usermod -aG vboxsf www-data

#RUN uwsgi --ini /app/hidata/serve/resources/uwsgi/uwsgi.dev.ini
EXPOSE 50000

#CMD ["python3"]