---
title: node脚本自动生成代码 解放50%的生产力(一)
date: 2019-01-10 20:55:49
tags: node 
---
> 发现不管是写前端(vue,react,angular)还是后端(egg,thinkphp,laravel)这种mvvm和mvc的框架，封装的越深，写起来越繁琐，特别是写管理后台的时候(ant desgin pro),模块化导致封装了很多层(接口的url层、ajax层、router、 model、view)每次添加都要文件一个个找，添加这么多层，而且基本上有50%以上的代码是重复的，一些常规的页面，除了接口和字段，别的都是一样的。直到我用到了angular 和 laravel，它们有命令行生成工具,但是对于已有的项目，再去搭建自己的脚手架不太合适，而且生成的代码不够全面，我就想自己也定制自己的生成代码的脚本来解决这个痛点,生成好之后基本改下字段就可以完事了

<!-- more -->

## 生成接口URL层代码 
URL层原始代码 config.js

```
const APIV1 = '/api/v1';

module.exports = {
  name: '管理后台',
  logo: '/logo.png',
  openPages: ['/login'],
  apiPrefix: '/api/v1',
  APIV1,
  api: {
    // 商品管理
    classificationItem: `${APIV1}/classification`,
    classificationBrand: `${APIV1}/brand`,
    classificationSeries: `${APIV1}/brandseries`,
    classificationGoods: `${APIV1}/productClassification`,
    classificationProperty: `${APIV1}/attributeController`,
    classificationCommodity: `${APIV1}/productController`,
  },
};
```
## 1.思路
  1.通过node 的bash交互，用户输入要生成的模块的名称，
  2.在该文件下面自动加入代码(倒数第二个}前面),
  如下：
  ```
  用户输入的模块名: `${APIV1}/用户输入的模块名`,
  ```
## 2.实现
  1.在项目根目录下创建如下文件：

    —cli
      -config.text    //源文件，把里面的代码插入到config.js
      -index.js       //node文件
