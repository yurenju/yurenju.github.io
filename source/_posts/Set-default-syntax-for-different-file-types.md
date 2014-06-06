title: 'Set default syntax for different file types in sublime text'
date: 2014-06-06 10:55:48
tags:
- sublime text
---
用 sublime text 一直有個小問題，就是我有個檔案是 .mk 副檔名，不過 Sublime 一直都沒辦法正確辨識他的 syntax 該用 Makefile，所以每次我都要手動切換。爬了爬文發現在有篇 Stack Overflow 下面的 [comment][1] 寫出了一個很簡單的解法。

首先打開你要設定的檔案，比如說我的例子是 common.mk，打開後先選擇你要指定的 syntax highlight，這個例子就是 Makefile Syntax。

指定完成後，到 Preferences-> Settings - More -> Syntax Specific - User，他會幫你建立一個新檔案在正確的位置還有正確的檔名，只要用以下的格式設定就可以增加新的副檔名了。

```json
{
  "extensions": [ "mk" ]
}
```

重起 Sublime Text 之後就會用正確的 syntax highlight 顯示檔案囉。

  [1]: http://stackoverflow.com/questions/7574502/set-default-syntax-to-different-filetype-in-sublime-text-2#comment24797511_7588849