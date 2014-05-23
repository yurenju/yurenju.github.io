title: \[GAE筆記\] 相同的參考表格
date: 2008-09-08 00:39:00
tags: 
- GAE
- 筆記
---

如果你的資料表同時參照了另外一個表格很多次，GAE 會抱怨 class google.appengine.ext.db.duplicatepropertyerror。此時你只要給每個參考屬性不同的 collection_name 即可解決。

例如這樣：
<script src="http://gist.github.com/9284.js"></script>

更詳細請參考以下網址

*   [http://appengineguy.com/2008/06/mutual-model-relations.html](http://appengineguy.com/2008/06/mutual-model-relations.html)
*   [&nbsp;http://code.google.com/appengine/articles/modeling.html](http://code.google.com/appengine/articles/modeling.html)