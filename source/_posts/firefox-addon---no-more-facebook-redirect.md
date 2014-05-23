title: Firefox Addon - No more Facebook redirect
date: 2014-01-19 22:50:55
cover: http://i.imgur.com/4xM1CTC.jpg
tags:
  - Firefox
  - Addon
  - Facebook
---
![Ad-tech London 2010][1]

上週跟同事討論到 Facebook 的重導很慢（然後他也不想讓 Facebook 經手他看的內容），上週末的時候寫了一個簡單的 Firefox Addon，也跟大家分享一下 Firefox Addon 要怎麼開始。

[Addon 網址在這][2]。

<!-- more -->

簡單的說，當瀏覽 Facebook 的時候，如果點擊了任何外部連結，Facebook 會把你導到 [www|m].facebook.com/l.php，記錄瀏覽資訊後再重導到你真正要去的網頁，正常就算了，有時候這個網頁真的很慢，所以這個 Addon 的目的就是讓外部連結直接會連到你要去的網站，而不透過 l.php。

# 觀察

首先要知道的是 Facebook 到底是怎麼運作的，你可以用 Chrome 或 Firefox 的 Inspector 去看一下在 Facebook 上面的聯結，它們大概都長這樣：

```html
<a href="http://www.facebook.com/l.php?u=http%3A%2F%2Fwww.imdb.com%2Ftitle%2Ftt21322…VqWCyL6SFp8kx-LEqFueJpHHOgiCdehrkANpy9TmQPIwigdZlarFf-CE3OTdRtxkHw&amp;s=1" target="_blank" rel="nofollow" onmouseover="LinkshimAsyncLink.swap(this, &quot;http:\/\/www.imdb.com\/title\/tt2132285\/&quot;);" onclick="LinkshimAsyncLink.referrer_log(this, &quot;http:\/\/www.imdb.com\/title\/tt2132285\/&quot;, &quot;\/si\/ajax\/l\/render_linkshim_log\/?u=http\u00253A\u00252F\u00252Fwww.imdb.com\u00252Ftitle\u00252Ftt2132285\u00252F&amp;h=5AQHzTjjK&amp;rend…s6tVqWCyL6SFp8kx-LEqFueJpHHOgiCdehrkANpy9TmQPIwigdZlarFf-CE3OTdRtxkHw&quot;);">http://www.imdb.com/title/tt2132285/</a>
```

簡單的說他會把 href 改成重導要去的網頁，以上面這個例子原本的網頁是
```
http://www.imdb.com/title/tt2132285/
```
Facebook 會把這個網址用 u 這個變數傳給 l.php，然後再加點料
```
http://www.facebook.com/l.php?u=http%3A%2F%2Fwww.imdb.com%2Ftitle%2Ftt0335266%2F%3Fref_%3Dnm_flmg_dr_5&h=NAQFr_7Es&enc=AZOPR95X8Izo4FNz_xIAWKmxnZtiLORKXsBt5y9tDUyKGxr9M_aK-BYpiNfmXZUjl6zBJeO8ybY0L6GeQxfcjstytlfv7rPp_j2uWRG--l0ooqXVawG5xUeoa2G5sAjAymHJrNkknafihUn_e7z1jOYs7pTILelDMboyyRuMGo47aw&s=1
```
但是當你滑鼠移上去的時候看起來卻是原本的網址，其實是因為他用了 onmouseover，當你滑鼠移上去的時候他會換正確的網址給你，當點擊的時候，又把 l.php 換給你。

# 實作

經過試了幾次之後，其實要做的事情很簡單，只要看到 facebook.com/l.php 就直接把 u 參數的字串做 url decode，接著把 onclick 移除掉就大功告成了。

接下來的事情就簡單了，到 Firefox 官網[下載 Addon 開發套件 cfx][3]，下載解壓縮後，執行下面的指令進入開發環境：

```bash
source CFX_DIR/bin/activate
```

這時候 shell propmt 會多出 `(addon-sdk-VERSION)` 代表你已經進入了開發環境。接下來照著官網的步驟就可以建立你自己的 Addon。

然後我們使用到最主要的 module 是 `page-mod`，這個模組可以在瀏覽特定網站時執行指定的 javascript，所以我們就使用這個模組，讓瀏覽器開啟 Facebook 之後執行下面的 Javascript （這個 Addon 簡單到我可以直接把主要的源碼貼上來 XD）：

```js
const RE_REDIRECT = new RegExp('[?|&]u=([^&;]+?)(&|#|;|$)');

MutationObserver = window.MutationObserver || window.WebKitMutationObserver;
var observer = new MutationObserver(function(mutations, observer) {
  var links = document.querySelectorAll('a[href*="facebook.com/l.php"]');

  Array.prototype.forEach.call(links, function(link) {
    var matched = link.search.match(RE_REDIRECT);
    if (matched) {
      link.removeAttribute('onclick');
      link.href = decodeURIComponent(matched[1]);
    }
  });
});

observer.observe(document, {
  subtree: true,
  attributes: true
});
```

特別感謝 `朕知道了` 擴充套件，我看了一下才知道用 `MutationObserver` 可以偵測 DOM 改變，好用！

MutationObserver 的用途是偵測到 DOM 有改變的時候就執行對應的代碼，而我們這邊直接聽 document 改變的事件。當 DOM 改變的時候，我們就直接找出 a tag 裡面的 href 包含 facebook.com/l.php 的所有 elements，所以不管是 http, https 或是 www.facebook.com, m.facebook.com 都可以用這個條件選取，CSS selector 長這樣：

```js
document.querySelectorAll('a[href*="facebook.com/l.php"]');
```

`*=` 真是好物啊，大家可以讀一下 [w3schools][4] 上面的說明，可以讓你選取屬性包含特定字串的 element。選取到之後要做的事情就簡單啦，用 Regular Expression 把 `u` 拿出來，再透過 `decodeURIComponent()` 把 uri encode 的字串解回來，放到 href，最後移除掉 onclick 就收工了！

最後 source code 放在 [github][5] 上面，有興趣的就載來看看吧。

  [1]: http://i.imgur.com/4xM1CTC.jpg
  [2]: https://addons.mozilla.org/firefox/addon/flink-removal/
  [3]: https://developer.mozilla.org/en-US/Add-ons/SDK
  [4]: http://www.w3schools.com/cssref/sel_attr_contain.asp
  [5]: https://github.com/yurenju/nomore-fb-redirect