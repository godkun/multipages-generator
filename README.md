multipages-generator [![NPM version](https://badge.fury.io/js/multipages-generator.png)](http://badge.fury.io/js/multipages-generator)
======

[![NPM](https://nodei.co/npm/multipages-generator.png?downloads=true&stars=true)](https://nodei.co/npm/multipages-generator)

multipages-generator （MG） 🤡是一个像express-generator一样快速生成网站开发脚手架的npm模块，可以全局安装。只要一个命令即可生成多页面的express工程，是多页面webpack编译的最佳实践模板，最适合多个独立的移动端h5项目，有几个特点：

## 适合场景
如美柚，淘宝，今日头条，微信内分享的等独立的，小的h5，可以是广告，营销，活动，展示页，秀肌肉，好玩的h5，如[这些](http://www.ih5.cn/not-logged-in/template)。
还有我们的例子：
[美柚吃鸡游戏](https://uedkit.meiyou.com/annualmeeting/game/)

## 优势是 什么？
完整的h5解决方案，快速开发，自动完成性能优化（目前只是基本功能，未完持续，后面支持[google web 性能优化](https://developers.google.com/web/fundamentals/performance/why-performance-matters/)

## 特点

1. 使用Node.js，是一个JavasScript的全栈的H5解决方案，工程可直接部署
2. 高效率开发，支持一键创建模块（业务模块）、一键创建新模块、一键编译发布等快捷命令
3. 工程结构良好划分，结构清晰，可维护。
4. 支持development,producton环境区分
5. 支持sass、less、postcss
6. 开发环境CSS、JS热编译
7. 文件上传支持阿里OSS，七牛云等
8. 🔥 (新) 加入[手淘flexible布局方案](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html)，适配不同尺寸和DPI的屏幕
9. 支持pm2集群启动


## Document
* [全局安装](#全局安装)
* [创建一个工程](#创建一个工程)
* [指令介绍](#指令介绍)
* [新建一个模块](#新建一个模块)
* [指定模块启动](#指定模块启动)
* [指定模块编译](#指定模块编译)
* [上传](#上传说明)
    * [七牛云CDN](#七牛云cdn)
    * [阿里云OSS](#阿里云oss)
* [配置](#配置)
* [TodoList](#TodoList)

## 全局安装 ⚙️

### 环境要求

node环境：node.js 6.11.0

操作系统：支持 mac，windows，centos

### 全局安装

```bash
npm install multipages-generator -g  //目前最新版本为1.5.x
```

## 创建一个工程 📽

步骤一：执行multipages-generate创建网站
```bash
multipages-generate

```
步骤二：出现输入项目名提示，并输入您的项目名称
```bash
? Project name: <输入项目名>

```

步骤三：进入工程名，并下载依赖包
```bash
     cd {你的项目名}
     npm install
```

步骤四: 启动指定的h5应用
```
    npm run dev:demo //根据你自己的webpack配置而定

```
四步骤之后，localhost:2000

==注意，目前发现demo例子的素材图片（在/client/demo/imgs 目录下）经过全局安装会编码出问题。不影响运行，但是如果想看到上面的demo页面请从[我的网盘](https://pan.baidu.com/s/1GyIunAicYsS3dCtJx-9hkg) 下载素材图片，解压放到/client/demo/imgs 目录下全部替换那些出问题的图片==

将来会选用更加适当的demo做演示

## 运行与开发
### 启动指定应用
经过上面的步骤，你已经启动了指定的应有，前端代码支持热更新，修改html，css，js等文件都会触发浏览器热更新

![image](http://oflt40zxf.bkt.clouddn.com/HRM.gif)

服务端使用nodemon热启动，需要刷新页面

```
    npm run start
```

## 新增一个项目
1. client 目录下已有个demo应用，新增一个应用demo2（名称随意），目录结构需参考demo
    ```bash
    demo
     ├─css
     ├─imgs
     └─js
    ```

    html 为了支持模板引擎，则把页面放在server/views/dev/demo 下

2. package.js 新增对应的开发指令，参考demo的配置方式
```bash
    "dev:demo2": "cross-env ENV=dev PROJECT_NAME=demo2 node app.js",
```
3.  配置对应应用的生产编译指令，参考demo的配置方式
```bash
    "release:demo2": "cross-env ENV=prod PROJECT_NAME=demo2 node ./config/release.js",

```
配置完成之后，就可以进行启动和开发了

```
    npm run dev:demo2
```

## 示例页面
![image](http://ovn18u9yn.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20180328152125.jpg?imageView2/1/w/375/h/667)

查看DEMO用手机chrome，淘宝，微信等扫下二维码查看

![image](http://oflt40zxf.bkt.clouddn.com/1522288108.png)

## 配置
mg.config.js 根目录下有个mg.config.js

这是整个项目的配置文件，目前配置了七牛云CDN上传的凭证配置，如果要增家redis，mysql，mongodb等配置，也建议放在这里；

postcss.config.js 同样在根目录下，是postcss.config.js的配置文件

process.json 同样在根目录下，是部署时的pm2启动配置文件

### Release模式上传到CDN
MG支持开发模式，也支持发布生产模式，生产模式编译出来的资源会发布到CDN，目前默认是七牛云，需要配置七牛云的相关信息，当然你也可以选择
阿里OSS等其他静态文件存储方式

示例demo项目编译命令
```
  npm run release:demo
```
编译后的文件输出到dist下，分为imgs,js,css

添加新项目时，请参考示例demo的配置方式添加

#### 七牛云CDN
MG目前支持发布时自动上传七牛云，需要配置七牛云的accesskey，secretkey等。在根目录下的mg.config.js中，修改如下配置(⚠️下面的信息只是胡写例子)
```
// 七牛云CDN上传配置
module.exports.qconfig = {
    ACCESS_KEY: 'ei1uOdGpVLliA7kb50si4wfYLPwt5v0shU10',
    SECRET_KEY: '-pFFIY-ew35Exyfcd40k15ah3UfZTFWFKF',
    bucket:'hotsts-image',
    origin:'http://ofltzxf.bkt.clouddn.com'
};

// js，css，图片等资源文件编译后增加的前缀
module.exports.cdnPath = '//ofltzxf.bkt.clouddn.com/';

```
cdnPath与qconfig.origin相对应

#### 阿里云OSS
即将支持

#### 其他CDN
如果你需要其他云服务器，那么你可以这样修改来支持
在/tools/release.js 中的上传代码做修改
```
webpacker.run((err,status)=>{
    if (util.runCallback(err, status)) {

        if(err){
            console.log(chalk.red('[webpack]：编译失败 ' + err.toString()));
            return;
        }

        console.log(chalk.magenta('[webpack]：编译完成！\r\n'));

        qupload('./dist')
    }
});
```
将qupload 方法改成你的云服务器上传的代码，核心思想是遍历dist下的所有文件，如果是文件，则上传，否则继续遍历文件夹下的内容；可参考/tools/qupload.js的逻辑来写

## Todo List
1. 性能优化加入手淘的一些方案，以及google的性能优化内容
2. 服务端增加mongodb，mysql，redis等可选配置
3. 不再仅限于h5，新增vue/react + node.js SPA可选方案
4. 文档完善

## Contribution

[吴俊川](https://github.com/wujunchuan)

感谢俊川提供的热更新方案的建议，以及对项目某些细节的改进

## 配套部署方案请参考
[30分钟快速部署到云服务器上](http://medium.yintage.com/?p=248)


## License

The MIT License 请自由享受开源。




