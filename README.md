# Solo CI

### Description###

一个轻量级的Golang CI/CD工具，全自动clone代码，构建，部署，只需要几行配置即可

```json
{
  "get_list":[
    "github.com/asaskevich/govalidator"
  ],
  "zip_list":[
    "conf"
  ],
  "after_script":"echo hello",
  "before_script":"pwd"
}
```

### Features###

- 完美集成Gitlab，Github（future），Bitbucket（future）
- 配置要求远低于主流CI工具（Jenkins etc.）内存占用低，可以运行在任何配置Linux主机中
- 一键开启，只需要Golang环境和Git环境，程序会自动获取自己所需要的环境
- 配制简单，只有四个配置项
- 一键clone，build，打包成tar，只需要写个SSH脚本部署到自己的机器即可
- 支持自定义脚本，构建前构建后触发均可自定义
- REST API支持，可以集成进任何系统
- 可以保存任意数量的构建，不丢任何构建

### Use###

1. 配置好主机的GOPATH，GOROOT，GIT环境 
2. 下载solo-ci编译好的程序
3. 使用REST API新建项目
4. 在你的项目中写个简单的solo.json，并且在代码管理中配置webhook (配置地址请看REST API)
5. push！触发CI

### REST API###

POST    http://your-ip:13233/v1/solohook/:project_id  触发Webhook

POST    http://your-ip:13233/v1/project 

Params in form

- name
- type
- url
- path
- branch
- secret_token (非必要)

DELETE      http://your-ip:13233/v1/project/:project_id     删除项目

PUT         http://your-ip:13233/v1/project/:project_id     更新项目

GET         http://your-ip:13233/v1/project/:project_id     获取项目信息

GET         http://your-ip:13233/v1/project                 获取项目列表
   
Params in query

- page (default 0)
- pageSize (default 20)

### solo-ci.json

- get_list：需要下载的Go包
- zip_list：构建完成需要打包进项目的文件或者目录
- before_script：构建之前执行的脚本
- after_script：构建之后执行的脚本

所有的选项都不是必须存在的，及时你什么都不写也可以，下面是一个空的配置文件例子

```json
{
  
}
```

### Next###

- Web GUI 支持
- Github，Bitbucket支持