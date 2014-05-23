title: Get origin from an URL
date: 2013-11-25 11:46:06
tags:
- Firefox
- Nightly
---
假設今天你有這個網址：

```
https://twitter.com/yurenju/status/402368329135816704
```

你要怎麼取得 `https://twitter.com` 呢？一般來說你可以用 regex 來達成：

```javascript
function getOrigin(url) {
  if (!url) {
    return null;
  } else {
    var matched = url.match(/^([a-zA-Z]+:\/\/.[^/]+).*/);
    return (matched.length > 1) ? matched[1] : null;
  }
}
```

不過如果你使用 Firefox 最新的 Nightly 就可以用 [URL()](https://developer.mozilla.org/en-US/docs/Web/API/URL) 來達到這件事情（Chrome 似乎可以用 webkitURL）。

```javascript
var url = new URL(YOUR_URL);
console.log(url.origin);
```

有興趣可以到 jsFiddle 上面用 Nightly 玩玩。

{% jsfiddle 6q7W2 %}