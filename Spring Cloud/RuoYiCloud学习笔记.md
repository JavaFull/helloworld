# 架构

[架构图](https://processon.com/view/link/5f4f4b2b0791296b0ef439c9)



swagger访问地址

http://localhost:8080/swagger-ui/index.html



spring boot admin页面

http://localhost:9100/

用户名和密码的配置在nacos中

ruoyi/123456



由于是微服务项目，需要启动多个服务，占用多个端口，有可能端口被本地程序占用，导致某个微服务启动不了，可以使用

```
lsof -i:8080
# list of open files
```

命令来查看占用端口的程序，kill -9 pid杀掉

