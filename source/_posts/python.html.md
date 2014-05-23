title: Python 初體驗 - 好吃不黏牙！
date: 2007-05-03 21:00:00
tags: 
- python
---

這幾天上課的老師出了幾個需要畫圖的習題，大致上是要用常態分佈取樣幾個點，X 軸跟 Y 軸給不同的 mean 跟 standard  deviation 繪製圖形。另外一個作業是繪出高斯分佈取樣的點的 probability density function。 <span style=""><span style="color: rgb(204, 0, 51);"></span></span>剛開始還考慮用 perl 來解題，後來想說順便學一下 python，就試著用它來寫寫看。

跟 [TimChen](http://timchen119.blogspot.com/) 要了些初學者用的網站，就開始看著 [咬一口 python 程式語言](http://limodou.51boo.com/book/8/)這本線上書籍學 Python。看完幾頁之後，就發現 python 比想像中的好上手，程式碼也很簡潔。接下來就開始思考要如何解題。

第一個，我需要有高斯分佈的取樣點，馬上查了 "[python gaussian distribution](http://www.google.com.tw/search?q=python+gaussian+distribution)"，有內建函式！很好很好，馬上就先解決取樣的問題。取樣完後需要 gnuplot 來畫圖。剛開始我打算先輸入到檔案裡面，再用 os module 來呼叫 gnuplot。在這個時候我又查了 "[python gnuplot](http://www.google.com.tw/search?q=python+gnuplot)"，沒想到又有！原來 python 有提供 gnuplot 的橋接，只要安裝 python-gnuplot 就可以使用了。所以這個問題就解決了，大約花了 30 行左右：

<pre><tt>_<span style="color: rgb(154, 25, 0);">#!/usr/bin/env python</span>_

**<span style="color: rgb(0, 0, 128);">import</span>** random<span style="color: rgb(153, 0, 0);">,</span> os<span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(0, 153, 0);">Gnuplot</span>

mean <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(153, 51, 153);">3</span>
strdev <span style="color: rgb(153, 0, 0);">=</span>  <span style="color: rgb(153, 51, 153);">10</span>
ns <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(153, 0, 0);">[</span><span style="color: rgb(153, 51, 153);">10</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">100</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">1000</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">10000</span><span style="color: rgb(153, 0, 0);">]</span>
g <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(0, 153, 0);">Gnuplot</span><span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">Gnuplot</span>**<span style="color: rgb(153, 0, 0);">()</span>
**<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set multiplot'</span><span style="color: rgb(153, 0, 0);">)</span>
**<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set size 0.5,0.5'</span><span style="color: rgb(153, 0, 0);">)</span>

**<span style="color: rgb(0, 0, 255);">for</span>** i **<span style="color: rgb(0, 0, 255);">in</span>** **<span style="color: rgb(0, 0, 0);">range</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">4</span><span style="color: rgb(153, 0, 0);">):</span>
 gauss <span style="color: rgb(153, 0, 0);">=</span> **<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">()</span>
 **<span style="color: rgb(0, 0, 255);">for</span>** j **<span style="color: rgb(0, 0, 255);">in</span>** **<span style="color: rgb(0, 0, 0);">range</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">,</span> ns<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">]):</span>
     gauss<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>**<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">())</span>
     gauss<span style="color: rgb(153, 0, 0);">[</span>j<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>random<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">gauss</span>**<span style="color: rgb(153, 0, 0);">(</span>mean<span style="color: rgb(153, 0, 0);">,</span> strdev<span style="color: rgb(153, 0, 0);">))</span>
     gauss<span style="color: rgb(153, 0, 0);">[</span>j<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>random<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">gauss</span>**<span style="color: rgb(153, 0, 0);">(</span>mean<span style="color: rgb(153, 0, 0);">,</span> strdev<span style="color: rgb(153, 0, 0);">))</span>

 **<span style="color: rgb(0, 0, 255);">if</span>** i <span style="color: rgb(153, 0, 0);">==</span> <span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">:</span>
     **<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set origin 0,0.5'</span><span style="color: rgb(153, 0, 0);">)</span>
 **<span style="color: rgb(0, 0, 255);">elif</span>** i <span style="color: rgb(153, 0, 0);">==</span> <span style="color: rgb(153, 51, 153);">1</span><span style="color: rgb(153, 0, 0);">:</span>
     **<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set origin 0.5,0.5'</span><span style="color: rgb(153, 0, 0);">)</span>
 **<span style="color: rgb(0, 0, 255);">elif</span>** i <span style="color: rgb(153, 0, 0);">==</span> <span style="color: rgb(153, 51, 153);">2</span><span style="color: rgb(153, 0, 0);">:</span>
     **<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set origin 0,0'</span><span style="color: rgb(153, 0, 0);">)</span>
 **<span style="color: rgb(0, 0, 255);">else</span>**<span style="color: rgb(153, 0, 0);">:</span>
     **<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'set origin 0.5,0'</span><span style="color: rgb(153, 0, 0);">)</span>

 g<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">plot</span>**<span style="color: rgb(153, 0, 0);">(</span>gauss<span style="color: rgb(153, 0, 0);">)</span>

**<span style="color: rgb(0, 0, 0);">g</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'unset multiplot'</span><span style="color: rgb(153, 0, 0);">)</span>
**<span style="color: rgb(0, 0, 0);">raw_input</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'Please press return to continue...\n'</span><span style="color: rgb(153, 0, 0);">)</span> </tt></pre>

[![Screenshot-Gnuplot](http://farm1.static.flickr.com/226/482615464_8231d4344c.jpg)](http://www.flickr.com/photos/yurenju/482615464/ "Photo Sharing")

Cool, 很好用。第二題要畫高斯分佈的 PDF，算這東西真的還蠻花時間的，後天就要交作業還是抱一下佛腳好了…。搜尋一下發現[這東西](http://bonsai.ims.u-tokyo.ac.jp/%7Emdehoon/software/python/Statistics/)，可以直接算出 PDF，當然又是直接拿來用…。

<pre><tt>_<span style="color: rgb(154, 25, 0);">#!/usr/bin/env python</span>_

**<span style="color: rgb(0, 0, 128);">import</span>** statistics<span style="color: rgb(153, 0, 0);">,</span> random<span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(0, 153, 0);">Gnuplot</span>

gauss <span style="color: rgb(153, 0, 0);">=</span> **<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">()</span>
gauss2 <span style="color: rgb(153, 0, 0);">=</span> **<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">()</span>
gpdf <span style="color: rgb(153, 0, 0);">=</span> **<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">()</span>
gpdf2 <span style="color: rgb(153, 0, 0);">=</span> **<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">()</span>
g <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(0, 153, 0);">Gnuplot</span><span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">Gnuplot</span>**<span style="color: rgb(153, 0, 0);">()</span>

**<span style="color: rgb(0, 0, 255);">for</span>** i **<span style="color: rgb(0, 0, 255);">in</span>** **<span style="color: rgb(0, 0, 0);">range</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">1000</span><span style="color: rgb(153, 0, 0);">):</span>
 gauss<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>random<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">gauss</span>**<span style="color: rgb(153, 0, 0);">(-</span><span style="color: rgb(153, 51, 153);">2</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">1</span><span style="color: rgb(153, 0, 0);">))</span>
 gauss2<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>random<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">gauss</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">2</span><span style="color: rgb(153, 0, 0);">,</span> <span style="color: rgb(153, 51, 153);">2</span><span style="color: rgb(153, 0, 0);">))</span>
 _<span style="color: rgb(154, 25, 0);">#gauss.append(random.gauss(2, 1))</span>_
 _<span style="color: rgb(154, 25, 0);">#gauss2.append(random.gauss(-2, 1))</span>_

y<span style="color: rgb(153, 0, 0);">,</span> x <span style="color: rgb(153, 0, 0);">=</span> statistics<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">pdf</span>**<span style="color: rgb(153, 0, 0);">(</span>gauss<span style="color: rgb(153, 0, 0);">,</span> kernel <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(255, 0, 0);">'Gaussian'</span><span style="color: rgb(153, 0, 0);">)</span>
w<span style="color: rgb(153, 0, 0);">,</span> z <span style="color: rgb(153, 0, 0);">=</span> statistics<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">pdf</span>**<span style="color: rgb(153, 0, 0);">(</span>gauss2<span style="color: rgb(153, 0, 0);">,</span> kernel <span style="color: rgb(153, 0, 0);">=</span> <span style="color: rgb(255, 0, 0);">'Gaussian'</span><span style="color: rgb(153, 0, 0);">)</span>

**<span style="color: rgb(0, 0, 255);">for</span>** i **<span style="color: rgb(0, 0, 255);">in</span>** **<span style="color: rgb(0, 0, 0);">range</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">,</span> **<span style="color: rgb(0, 0, 0);">len</span>**<span style="color: rgb(153, 0, 0);">(</span>x<span style="color: rgb(153, 0, 0);">)):</span>
 gpdf<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>**<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">())</span>
 gpdf<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>x<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">])</span>
 gpdf<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>y<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">])</span>

**<span style="color: rgb(0, 0, 255);">for</span>** i **<span style="color: rgb(0, 0, 255);">in</span>** **<span style="color: rgb(0, 0, 0);">range</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(153, 51, 153);">0</span><span style="color: rgb(153, 0, 0);">,</span> **<span style="color: rgb(0, 0, 0);">len</span>**<span style="color: rgb(153, 0, 0);">(</span>w<span style="color: rgb(153, 0, 0);">)):</span>
 gpdf2<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>**<span style="color: rgb(0, 0, 0);">list</span>**<span style="color: rgb(153, 0, 0);">())</span>
 gpdf2<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>z<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">])</span>
 gpdf2<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">].</span>**<span style="color: rgb(0, 0, 0);">append</span>**<span style="color: rgb(153, 0, 0);">(</span>w<span style="color: rgb(153, 0, 0);">[</span>i<span style="color: rgb(153, 0, 0);">])</span>

g<span style="color: rgb(153, 0, 0);">.</span>**<span style="color: rgb(0, 0, 0);">plot</span>**<span style="color: rgb(153, 0, 0);">(</span>gpdf<span style="color: rgb(153, 0, 0);">,</span> gpdf2<span style="color: rgb(153, 0, 0);">)</span>
**<span style="color: rgb(0, 0, 0);">raw_input</span>**<span style="color: rgb(153, 0, 0);">(</span><span style="color: rgb(255, 0, 0);">'Please press return to continue...\n'</span><span style="color: rgb(153, 0, 0);">)</span> </tt></pre>

[![Screenshot-Gnuplot-1](http://farm1.static.flickr.com/191/482615466_dc45e2493a_m.jpg)](http://www.flickr.com/photos/yurenju/482615466/ "Photo Sharing") [![Screenshot-Gnuplot-2](http://farm1.static.flickr.com/210/482615468_b5125a68c0_m.jpg)](http://www.flickr.com/photos/yurenju/482615468/ "Photo Sharing")

作業完成！

結論，Python 真的是好物阿！如果有寫其他程式語言的經驗，Python 是相當好學的東西！