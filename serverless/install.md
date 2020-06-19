# serverless
本文为入坑serverless时，记录使用步骤和问题。

serverless即无服务器云计算，其不是前端技术，是云服务中支持的一项，为了提升开发效能，使其能主要关注业务开发，减少不必要的资源消耗。

## 安装
可根据[serverless官网](https://www.serverless.com/cn/)进行快速开始。
1. 安装nodejs和npm
2. 通过nodejs全局安装serverless。npm i -g serverless
3. 安装完成后，通过 serverless -v 查看版本

## 创建serverless模板
1. 通过serverless create -h命令可以查看现有serverless支持的模板
2. 根据命令创建一个腾讯云的serverless服务。path指定生成的路径
```
serverless create -t tencent-nodejs --path ./my-service
```
>> 也可以直接输入serverless,然后根据提示，选择相应的模板.

3. 运行sls dev命令，启动开发环境。其中sls为serverless缩写
4. 如果没有配置权限，则会显示扫描二维码图片,扫描后，会进行云上安装，此时如果直接退出，在后续访问地址，还是能访问到。
5. 运行sls info ,显示系统信息。如下：
```
localhost:my-express caoxiaopeng$ sls info

serverless ⚡ framework


Last Action:  deploy (2 minutes ago)
Deployments:  2
Status:       active
More Info:    Full details: https://sls.cloud.tencent.com/instances/appDemo%3Adev%3AexpressDemo

region: ap-guangzhou
apigw:
  serviceId:   service-dq8szo8e
  subDomain:   service-dq8szo8e-1253669783.gz.apigw.tencentcs.com
  environment: release
  url:         https://service-dq8szo8e-1253669783.gz.apigw.tencentcs.com/release/
scf:
  functionName: express_component_b38hqi5
  runtime:      Nodejs10.15
  namespace:    default

expressDemo › Info successfully loaded
```
6. 配置appsecret
  在项目目录下新建.env文件，填写如下信息：
```
TENCENT_SECRET_ID=123  //您的SecretId 
TENCENT_SECRET_KEY=123 //您的SecretKey
SERVERLESS_PLATFORM_VENDOR=tencent // 如果ip是国外，又需要国内serverless环境，需要配置此项
```

