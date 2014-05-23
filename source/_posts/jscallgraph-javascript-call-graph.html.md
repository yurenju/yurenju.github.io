title: jscallgraph - Javascript Call Graph 靜態分析
date: 2012-10-17 15:04:00
tags: 
- Firefox OS
- node.js
- javas
---

最近用 xmind 追 code 追得很辛苦，跟[幾位朋友](https://www.facebook.com/photo.php?fbid=10151149547596631&amp;set=a.144732831630.122857.700771630&amp;type=1)討論過後，不知不覺就開始寫起了靜態分析用的程式。昨天先用 python 驗證了一下概念，深夜開完會議之後就決定用 node.js 來寫個程式會比起用 python 更為合適。目前已經放上 npm，要安裝只要你已經裝好了 node.js 跟 npm，輸入以下指令就可以安裝了。

<pre class="brush: shell">$ sudo npm -g install jscallgraph
$ sudo apt-get install graphviz
</pre>
第二行是安裝 graphviz，主要的用途是拿來產生分析完的圖形用的。使用上很簡單，舉例來說你想要對 Firefox OS 的 system app 裡面的 [window_manager.js](https://github.com/mozilla-b2g/gaia/blob/master/apps/system/js/window_manager.js) 作靜態分析，把檔案抓下來，用以下指令產生 dot file

<pre class="brush: shell">$ jcg window_manager.js WindowManager &gt; window_manager.dot
</pre>
第一個參數是要分析的檔案，第二個參數是要分析的物件，這邊可以參考一下 window_manager.js 的檔案，裡面宣告了 WindowManager 物件，並且把相關 method 都包裝在裡面。

接下來用 graphviz 的 dot 指令產生 png 圖檔

<pre class="brush: shell">$ dot -Tpng -o window_manager.png window_manager.dot</pre>

這樣就完成了！

<div class="separator" style="clear: both; text-align: center;">[![](http://2.bp.blogspot.com/-4SoKRhsK5xg/UH5XSdQQQWI/AAAAAAAAUQw/hgQWEGFqMjA/s640/window_manager.png)](http://2.bp.blogspot.com/-4SoKRhsK5xg/UH5XSdQQQWI/AAAAAAAAUQw/hgQWEGFqMjA/s1600/window_manager.png)</div>

Source code 放在 [github](https://github.com/yurenju/jscallgraph), 請大家自由取用！另外這程式不是什麼 javascript 都可以分析，有興趣的請送 patch! :D