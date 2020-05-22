---
本仓库主要提供使用weex多页面的配置demo


### 升级cli版本

```
npm i chameleon-tool@1.0.6-alpha.3 
```

```
chameleon-tool@1.0.6-alpha.5 版本支持配置name字段自定义bundle名称

```
### 配置router.config.json

* 选项 mpa.weexMpa,Array[{paths:[]}]表示要配置weex多个bundle

只能接受数组，数组中的每个元素为对象，接受一个key为 paths 的数组，该数组配置routes中哪些页面对应到某个bundle中

最终生成的bundle的名字会以 mpa.weexMpa 中数组的下标追加到目录名后面

比如项目目录名字是 cml-weex-mpa
如果配置了如下多bundle构建
那么 cml-weex-mpa0 对应的路由包括 mpa.weexMpa[0].paths 里的页面
那么 cml-weex-mpa1 对应的路由包括 mpa.weexMpa[1].paths 里的页面

以此类推


```json
{
  "mode": "history",
  "domain": "https://www.chameleon.com",
  "routes":[
    {
      "url": "/cml/h5/index",
      "path": "/pages/index/index",
      "name": "首页",
      "mock": "index.php"
    },
    {
      "url": "/cml/h5/index1",
      "path": "/pages/index/index1",
      "name": "首页",
      "mock": "index.php"
    },
    {
      "url": "/cml/h5/index2",
      "path": "/pages/index/index2",
      "name": "首页",
      "mock": "index.php"
    },
    {
      "url": "/cml/h5/index3",
      "path": "/pages/index/index3",
      "name": "首页",
      "mock": "index.php",
      "extra": {
        "version": {
          "main": "5.3.2",
          "blord": "30.0.4"
        }
      }
    }
  ],
  "mpa":{
    "weexMpa":[
      {
        "name":"addRoutes",
        "paths":["/pages/index/index","/pages/index/index3"]
      },
      {
        "paths":["/pages/index/index2"]
      }
    ]
  }
}
```

### 注意点

* 路由的跳转需要注意，多个bundle之间不能再使用 navigateTo  navigateBack  navigateBack
*  mpx.weexMpa 中为配置的在paths 中的页面将不会被构建进bundle中