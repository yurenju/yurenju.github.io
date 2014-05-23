title: \[筆記\] android WebView 遇到網頁重導後開新視窗的問題
date: 2010-09-28 15:35:00
tags: 
- Android
---

塞個 WebViewClient 給他。

<pre class="brush: java">WebView web = (WebView)findViewById(R.id.WebPages);
web.setWebViewClient(new WebViewClient());
</pre>
最近會筆記些零碎的 android 問題。