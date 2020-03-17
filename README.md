# aws-vue-study

学了vue有几个月了，整理一下学习思路，并结合aws来实现一个小栗子。  
For Neusoft Study

## 目录

* vue介绍
  * 什么是vue？针对于HTML视图的一种框架
  * 工作原理？观察者模式，数据劫持
* vue实例讲解
  * vue-cli + vue-router + vuex创建框架，运行并显示hello world
  * vue讲解
    * 具体讲啥还没想好，照着[官方指南](https://cn.vuejs.org/v2/guide/list.html)左侧的列表都讲？
  * vue-router讲解
    * 动态路由
    * 路由嵌套
    * 路由守卫
    * 其余的还讲吗？
    * 如何再在vue中使用
  * vuex讲解
    * state
    * getter
    * mutation
    * action
    * module
    * 如何在vue中使用
  * vue-cli配置讲解
    * 常用配置
    * 解决本地开发的服务器代理
    * Node环境变量
  * 对于前端页面的单元测试
    * jest
* AWS介绍
  * 账号的创建与IAM的初步设定
  * 快速建立各个AWS服务(CloudFormation的使用)
    * 参照[AWS CloudFormation](https://docs.aws.amazon.com/zh_cn/AWSCloudFormation/latest/UserGuide/Welcome.html)来搭建DB，Lambda,
  * 快速建立一套后端服务器接口
    * CodeStar的使用
      * CodeCommit代码仓库
      * CodeBuild代码编译
      * CodeDeploy代码发布
    * 使用[Swagger](https://petstore.swagger.io/)来建立API Gateway
    * 用户的验证[AWS Cognito](https://docs.aws.amazon.com/zh_cn/cognito/?id=docs_gateway)
      * JWT认证
        * token处理与超时
    * 如何在本地搭建lambda的执行环境
      * 参照[AWS SAM](https://github.com/awslabs/serverless-application-model)
    * 对于Lambda的测试