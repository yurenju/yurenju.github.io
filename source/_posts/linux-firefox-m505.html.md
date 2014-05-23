title: Linux 設定 Firefox 羅技 M505 滑鼠按鈕成上下頁
date: 2010-02-12 17:56:00
tags: 
- logitech
- mouse
---

<div class="separator" style="clear: both; text-align: center;">[![](http://1.bp.blogspot.com/_iOO0fC4NKLE/S3UT7alQXeI/AAAAAAAAIGU/x2GdoJnZUdc/s320/P1000884.JPG)](http://1.bp.blogspot.com/_iOO0fC4NKLE/S3UT7alQXeI/AAAAAAAAIGU/x2GdoJnZUdc/s1600-h/P1000884.JPG)</div>

今天買了個新滑鼠 [Logitech M505](http://www.logitech.com/index.cfm/mice_pointers/mice/devices/5870&amp;cl=us,en)，插上 Linux 的機器基本上沒什麼問題。不過以前用 [MX510](http://yurinfore.blogspot.com/2008/05/mx510.html) 時滑鼠翻上一頁、下一頁不需要設定的便利卻消失了。用 xev 看了一下，發現滑鼠的按鈕已經全部都可以使用，編號是按鈕 6, 7。

所以基本上只是 Mapping 的問題。上網 Google 一下發現 Firefox 從 3.0 開始上/下一頁全部都改成按鈕 8/9。所以只要照著 [Firefox 說明](http://support.mozilla.com/zh-TW/kb/Mouse+buttons+do+not+work+as+Back+and+Forward)改成 6/7 馬上就可以使用。

1.  打開 Firefox，在網址列輸入 about:config
2.  鍵入過濾條件為 mousewheel.horizscroll.withnokey
3.  <span class="prf">mousewheel.horizscroll.withnokey.action 改成 2</span>
4.  <span class="prf">mousewheel.horizscroll.withnokey.numlines 改成 -1</span>
5.  <span class="prf">mousewheel.horizscroll.withnokey.sysnumlines 改成 false&nbsp;</span><span class="prf"> </span><span class="prf">&nbsp;</span>
這樣就 OK 囉。