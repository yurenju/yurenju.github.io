title: 寫 HTML/XML 讓你很煩心嗎？你需要 zen coding
date: 2010-05-13 19:44:00
tags: 
---

http://code.google.com/p/zen-coding/

他有 vim 外掛，裝上去後，開啟你的 XML/HTML。如果你想要以下結構
<pre class="brush: html">&lt;div class=&quot;main&quot;&gt;
  &lt;p&gt;&lt;/p&gt;
  &lt;p&gt;&lt;/p&gt;
  &lt;p&gt;&lt;/p&gt;
&lt;div&gt;
</pre>
只要打
<pre class="brush: text">div.main&gt;p*3
</pre>按下 Ctrl + Y，再按下逗點就可以展開成上面的語法了。