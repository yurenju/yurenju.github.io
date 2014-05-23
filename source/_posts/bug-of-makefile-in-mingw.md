title: Bug of Makefile in MinGW
date: 2014-02-07 10:56:50
tags:
- MinGW
- Make
---
昨天踩到了一個讓人很沮喪的 bug。

一般來說在 Makefile 我們可以用 $(shell pwd) 拿到像這樣 style 的路徑
```
$(shell pwd)
/home/yurenju/gaia
```
如果要在 Windows 的 MinGW 底下用的話，可以用大寫 W 參數可以拿到這樣 style 的路徑：
```
$(shell pwd -W)
C:/home/yurenju/gaia
```

然後昨天踩到的雷是，如果你用 `-include` 引入了另外一個 Makefile 後（比如說 common.mk），你在 common.mk 裡面執行 `$(shell pwd -W)` 竟然會出錯！而且同樣的用法如果沒有用 -include 的時候是完全會動的。

解法呢？感謝 [PostgreSQL][1] 的先烈告訴我們了答案，用 `sh -c` 去執行竟然就好了
```
$(shell sh -c "pwd -W")
```

見鬼了，這哪招啊...

  [1]: http://www.postgresql.org/message-id/4D0BF549.6030600@dunslane.net