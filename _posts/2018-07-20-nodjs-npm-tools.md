---
layout: post
title:  "nodjs's npm tools"
categories: nodejs npm
tags: nodejs npm
author: 若水三千
---

* content
{:toc}

1. nrm NPM registry manager   

npm 镜像仓库管理

install  

```shell
npm install -g nrm
```

show all registry

```shell
nrm ls
```

>      
>      npm ---- https://registry.npmjs.org/    
>      cnpm --- http://r.cnpmjs.org/    
>    &#10038; taobao - https://registry.npm.taobao.org/    
>      nj ----- https://registry.nodejitsu.com/    
>      rednpm - http://registry.mirror.cqupt.edu.cn/    
>      npmMirror  https://skimdb.npmjs.com/registry/    
>      edunpm - http://registry.enpmjs.org/
>     



swith registry  
```
nrm use npm
```

https://www.npmjs.com/package/nrm


手动下载地址格式：
https://registry.npmjs.org/element-ui/-/element-ui-1.2.8.tgz