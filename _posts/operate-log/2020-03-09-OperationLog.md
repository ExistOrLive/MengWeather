---
title: 运维日志 2020/03/09
tags: 日志
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## 启动jekyll 静态博客服务 

- jekyll地址
  
  `/home/zhumeng/github/DocumentOfLinuxPlay`

- 启动服务 

```

jekyll serve -H 0.0.0.0 --detach

```

-  关闭服务

```
pkill -f jekyll
```