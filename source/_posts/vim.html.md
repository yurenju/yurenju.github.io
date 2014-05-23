title: \[筆記\] vim 儲存/還原開啟的分頁
date: 2010-06-23 13:02:00
tags: 
- vim
---

來源:&nbsp;[http://www.cs.utah.edu/~kad/vim/vimnotes.shtml](http://www.cs.utah.edu/~kad/vim/vimnotes.shtml)

當要儲存 vim 分頁時，輸入 :mks &lt;filename&gt; 即可。下次要開啟的時候，使用 vim -S &lt;filename&gt; 即可還原</filename></filename>��標注最前面的一個字元。比如說

<pre class="brush: js">var width = aWin.document.documentElement.scrollWidth;
var height = aWin.document.documentElement.scrollHeight;
if (effect.viewCanvas == null)
&nbsp; &nbsp;effect.viewCanvas = this.createCanvas (width, height);
</pre>
就選取 v, v, i 和空白。按下大寫 I，輸入你正在寫得程式語言的註解，javascript 就是 //。最後按下 Esc 就完成了。

不過如果要像 eclipse 按一次 ctrl + / 就註解，再按一次取消註解就要寫 vim script 了。