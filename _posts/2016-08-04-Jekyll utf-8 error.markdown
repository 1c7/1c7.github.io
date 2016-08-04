---
layout: post
title:  "Jekyll 写中文报错 utf-8"
date:   2016-08-04 16:41:01 +0800
---



```
a@ubuntu:~/Desktop/1c7.github.io$ jekyll serve --host=0.0.0.0
Configuration file: /home/a/Desktop/1c7.github.io/_config.yml
            Source: /home/a/Desktop/1c7.github.io
       Destination: /home/a/Desktop/1c7.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
             Error: could not read file /home/a/Desktop/1c7.github.io/_posts/2016-08-03-ubuntu 16.04 ssh remote server use socks proxy to speed up.markdown: invalid byte sequence in UTF-8
  Liquid Exception: invalid byte sequence in UTF-8 in /home/a/Desktop/1c7.github.io/_posts/2016-08-03-ubuntu 16.04 ssh remote server use socks proxy to speed up.markdown
jekyll 3.1.6 | Error:  invalid byte sequence in UTF-8
```

解决方法:  
`_config.yml` 里最后一行加上 `encoding: utf-8`  

然后 markdown 文件以 utf-8 格式另存, 覆盖掉原来的文件即可 (我用的gedit)  

我的环境是 `jekyll 3.1.6` + `Ubuntu16.04` 管用  

