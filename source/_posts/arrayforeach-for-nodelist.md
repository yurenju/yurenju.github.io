title: Array.forEach for NodeList
date: 2013-11-21 12:12:29
tags: Javascript
---
Javascript 裡面有個很實用的功能 forEach，跟其他語言的 for-each 一樣，你可以不需要 index 的狀況把陣列裡面的 object 一個個的丟出來，用法如下：

```javascript
var arr = [1, 2, 3, 4, 5, 6];
arr.forEach(function(num) {
  // do something...
});
```

但是有個小問題，當你用 `document.getElementsByTagName()` 或是 `document.querySelectorAll()` 的時候會回傳 `HTMLCollection` 或是 `NodeList`因為不是 Array 的關係所以無法使用 forEach 操作。

但我已經回不去用 index 做 loop 的方式了！[MDN][1] 上面很貼心地跟你說要如何透過 Array 的 prototype 操作 NodeList 與 HTMLCollection：

```javascript
var elements = document.getElementsByTagName('a');
Array.prototype.forEach.call(elements, function(a) {
    msg.innerHTML += a.innerHTML + '<br>';
});
```

你也可以直接在 [jsFiddle][2] 上面跑跑看。


  [1]: https://developer.mozilla.org/en-US/docs/Web/API/NodeList#Why_can%27t_I_use_forEach_or_map_on_a_NodeList.3F
  [2]: http://jsfiddle.net/ezV62/
