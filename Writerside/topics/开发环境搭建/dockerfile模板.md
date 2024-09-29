***nodejs项目
```Dockerfile
FROM node:latest
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN mkdir -p /app
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 80
CMD ["npm","run","start"]
```

***golang项目
```Dockerfile

```

***react项目
```Dockerfile

```

