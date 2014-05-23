title: 你愛 Javascript 的 Array 嗎？
date: 2010-05-14 15:29:00
tags: 
---

最近開始常寫 javascript 後，發現了不少好東西 -- 尤其是 Array。有幾個新 function 不得不提。<p>[filter]
可以把過濾用的 function 丟給 filter 去過濾，範例：<p><pre class="brush: js">let items = [1, 10, 20, 50, 80, 100];
function aFilter (element) {
  if (element &gt;= 50)
    return true;
  return false;
}
let filterItems = items.filter (aFilter);
</pre>
[some]
上面那篇已經提過了，如果有任何符合條件的就 return true:<p><pre class="brush: js">let items = [1, 10, 20, 50, 80, 100];
function someGreatThan50 (element) {
  if (element &gt; 50)
    return true;
  return false;
}

if (items.some (someGreatThan50)
  alert (&quot;some element great than 50&quot;);
</pre>像上面這兩個例子一樣好用的 function 有 forEach, every. 詳情請查閱 MDC
[https://developer.mozilla.org/En/Core_JavaScript_1.5_Reference/Objects/Array](https://developer.mozilla.org/En/Core_JavaScript_1.5_Reference/Objects/Array)