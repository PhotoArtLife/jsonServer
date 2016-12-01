## 使用 NodeJs 实现本地或线上及线上自我学习测试接口系统 ##

无数据库的情况下，实现数据持久化，通过`api url`返回`json` 数据，提高前端开发效率！
## 实现功能 ##
 1. 完整的操作页面
 2. 首页展示所有保存的接口列表
 3. 创建的接口保存到本地或线上
 4. 支持重新编辑
 5. 编辑过程实时预览和错误提示
 6. 根据接口名称或者url进行检索
 7. 提供url跨域调用
 
## 前言 ##


## 背景 ##
前端开发工作中一个重头戏就是和后台实现数据交互。
很多前端入门不久的同学在涉及到和后台交互的时候，都需要等待后端开发做好，给了数据才可以继续，就是所谓的串行开发。

![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/1.jpg)

实际上我们并不需要等后台开发完成，只要一开始的时候双方约定好数据格式，前端自己模拟一些数据就可以投入工作，这样就可以并行开发,效率可以显著提高
![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/2.jpg)
## 方案 ##
上面的问题可以有多种解决方案

 1. 直接代码里面js本地或线上造数据

    ```
    ...
    var data = {...}
    ...
    //这种方案适合小型结构的数据，一旦数据过于庞大，不适合放在js文件里面，不利于维护
    //不能很好的模拟ajax
    $.ajax({
        url:'..'//这个时候ajax接口不存在，调不通
    })
    //不能重复利用，上生产肯定要删掉
    ```
 2. 使用mockjs：http://mockjs.com
 生成随机数据，拦截 Ajax 请求
 这个网上有丰富的介绍，可以直接百度

## 实现本地或线上化接口服务 ##
本文介绍了一个简单的平台化方案，创建一个本地或线上化的服务系统，你也可以把它布到线上，用于相应的http或https服务，这样得到数据格式之后，本地或线上生成一个可用的 `url` 用于`ajax`请求，而且还可以让数据持久化，如果放在局域网内，接口还可以共享给小伙伴。

说到持久化，那么必须涉及到数据的存储，用于存储的数据库有很多，我以前用过`mongodb`结合`nodejs`使用，也是蛮好的，但是数据库安装也蛮麻烦的，我们这里有一个更简便的，硬盘本身就是一个`“数据库”` ，所以我们可以使用`nodejs`的`fs`模块直接创建`json`文件，读取`json`文件。这样创建的每一个`json`文件都对于一个接口服务，只要不删除，就可以一直重复利用。

## 使用方法介绍 ##

 1. `github`下载源码，并执行 `npm install` 安装
 2. 启动node服务，`node app.js`。  （建议使用 `supervisor app.js` 可以自行重启服务，通过`npm install supervisor -g`  安装模块）
 3. 打开首页  http://localhost:3000/或http://你的域名/端口号（https://你的域名/端口号）  建议用chrome访问

   ![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/3.jpg)

 4. 点击创建接口，`API`名称用来描述接口左右，`API url`用来调用数据，都是必填。如图，我们创建一个接口 `testapi` 可以实时预览json格式，可以快速定位格式错误。也可以借助网上更多的格式化工具。

    ![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/4.jpg)

    创建完成点击最下面的保存按钮，提示保存成功就完成了接口的创建！

    ![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/5.jpg)

 5. 使用接口，根据刚刚创建的`url：testapi` 生成一个链接  http://localhost:3000/getjson/testapi
可以在控制台调用一下这个`url`可以看出就是我们刚刚存储的`json`数据。
   ![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/6.jpg)
 6. 搜索功能：在搜索框输入接口中文描述名称或者`apiurl`的名称即可。

 7. 二次编辑功能：创建完成接口之后，首页或者搜索结果会显示二次编辑入口，点击就会显示上次保存的数据和格式
   ![image](https://github.com/PhotoArtLife/jsonServer/blob/master/public/images/7.jpg)

 8. 注意：`ajaxapilist.json` 存着一张关系表，对应所有的接口描述名称和`url`，用于查询，建议不要修改，



## 总结 ##
二次开发，作为学习node的笔记

  [1]: https://github.com/kliuj/local-ajax-api
