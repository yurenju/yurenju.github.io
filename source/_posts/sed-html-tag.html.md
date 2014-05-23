title: \[筆記\] 使用 sed 轉換 HTML tag
date: 2010-05-21 13:16:00
tags: 
---

貼 blog 時常用到 html/xml tag 的時候，直接貼上去 blogger 都會很聰明的當成你要使用 html tag。有個轉換小工具可以處理這件事情總是好的。

源自 [http://www.html-tags-guide.com/html-xmp-tag.html](http://www.html-tags-guide.com/html-xmp-tag.html)

建立檔案 convert.sed:
<pre class="brush: text">s/&amp;/\&amp;amp;/g
s/&quot;/\&amp;quot;/g
s/&lt;/\&amp;lt;/g
s/&gt;/\&amp;gt;/g
</pre>
使用以下指令來轉換你的 XML/HTML
<pre class="brush: bash">sed -f convert.sed &lt;your-xml-file&gt;
</pre>