# application

go 框架 revel 配合 swagger-ui 应用骨架搭建介绍

## [当前项目](project.md)

## 使用技术

- `revel` go 框架 
- `go-swagger` swagger.json 生成 
- `swagger-ui` 显示API文档 

## revel

### 安装revel

```sh
go get -u -v github.com/revel/cmd/revel
revel -h
```

### 创建项目

```sh
cd $GOPATH/src
revel new {PROJECT_NAME}
ll {PROJECT_NAME}
```

### 运行项目

转到项目目录下执行 `revel run` 访问 `http://localhost:9000/`

### 链接

- github https://github.com/revel/revel
- 官方模块 https://github.com/revel/modules
- 官方文档 https://revel.github.io
- 另一份文档 https://git-books.github.io/books/revel/

## go swagger

用于生成 swagger-ui 可读的json 文档文件

- 文档 https://goswagger.io/
- Github https://github.com/go-swagger/go-swagger

### 安装 

```sh
go get -u -v github.com/go-swagger/go-swagger/cmd/swagger
swagger -h
```

### 文档生成

在项目目录执行

```sh
swagger generate spec -o swagger-ui/docs/swagger.json
swagger generate spec -i ./swagger.yml -o swagger-ui/docs/swagger.json
```

> 因为 revel 的 `main.go` 是自动生成到 `app/tmp` 的，所以需要到 `main.go` 所在目录运行上述命令才行

```sh
cd app/tmp
swagger generate spec -o ../../swagger-ui/docs/swagger.json
```

### swagger-ui 

swagger-ui 下载 `npm install swagger-ui-dist`。或者到 github 下载

拷贝 `dist` 下的所有文件到项目目录下 `swagger-ui` 目录

- github https://github.com/swagger-api/swagger-ui

## 文档查看

- 配置静态资源访问

路由配置 `conf/routes`

```
# For swagger UI
GET    /swagger-ui/*filepath                   Static.Serve("swagger-ui")
GET    /swagger-ui/                            Static.Serve("swagger-ui","index.html")
```

- 访问： `127.0.0.1:9000/swagger-ui/`
