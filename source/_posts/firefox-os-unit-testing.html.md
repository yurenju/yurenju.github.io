title: 威能的 Firefox OS unit testing
date: 2013-01-22 12:16:00
tags: 
- javascript
- Firefox OS
---

今天在謀智台客發表了篇文章，主要是講 Firefox OS 在 unit testing 有個不錯的機制，就是設定妥當後，當你在任何編輯器或 IDE 按下儲存後，unit testing 就會自動開始測試跟你剛剛儲存的那個 javascript 相關的測項，最後用 Mac 的 notification center 或是 Linux 的 libnotify 告訴你測試結果，像下面這樣：

<div class="separator" style="clear: both; text-align: center;">[![](http://1.bp.blogspot.com/-WkH5O65cUrs/UP4nMKvEUPI/AAAAAAAAYdY/p1kMQMujjzs/s640/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7+2013-01-22+%E4%B8%8B%E5%8D%881.43.46.png)](http://1.bp.blogspot.com/-WkH5O65cUrs/UP4nMKvEUPI/AAAAAAAAYdY/p1kMQMujjzs/s1600/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7+2013-01-22+%E4%B8%8B%E5%8D%881.43.46.png)</div><div class="separator" style="clear: both; text-align: center;"></div><span id="goog_2092831299"></span><span id="goog_2092831300"></span>

可以讓你隨時都知道自己有沒有把任何東西搞爆了。

有興趣的可以看一下

[缺它不可！靈活運用 Firefox OS Gaia 的單元測試](http://tech.mozilla.com.tw/posts/1470)