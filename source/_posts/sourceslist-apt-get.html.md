title: 指定 sources.list 的 apt-get
date: 2008-06-30 21:50:00
tags: 
- apt
- apt-get
- sources.list
---

今天在讀 apt-get 的 man，發現了有趣的東西。原來 apt-get 可以輕易的變更 sources.list 位置。只需要以下指令：

apt-get update -o Dir::Etc::SourceList=<path/to/sources.list>

apt-get 就會乖乖的用指定的檔案更新了 :D