FROM golang:alpine as builder

MAINTAINER xiaoliang.cheng@idreamsky.com

# 指定工作目录
WORKDIR /go/src/hicrm

# 复制所有当前文件夹目录文件到工作目录
COPY . .

# 环境变量
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64 \
    GOPROXY=https://goproxy.cn/

# CGO_ENABLED禁用cgo 然后指定OS等，并go build
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -a -installsuffix cgo -o hicrm ./public/main.go
# 创建发布专用文件夹，并复制项目运行所需要的文件目录，public 文件夹中的软链不需要【-r】，否则代码运行时重新创建会报错
RUN mkdir -p publish/public && cp hicrm publish
RUN mkdir -p publish/storage/templates
RUN mkdir publish/storage/logs
RUN mkdir publish/storage/app

FROM scratch

WORKDIR /go/src/hicrm

COPY --from=builder /go/src/hicrm/publish .
#COPY --from=builder /go/src/hicrm/hicrm .
#COPY --from=builder /go/src/hicrm/storage/ /storage/
#COPY --from=builder /go/src/hicrm/storage/ ./storage/
#COPY --from=builder /go/src/hicrm/public/ .
#COPY --from=builder /go/src/hicrm/config/ ./config

EXPOSE 8088

# 运行
CMD ["./hicrm"]