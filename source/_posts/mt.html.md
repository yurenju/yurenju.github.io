title: 如何結合線上書籤與MT?
date: 2004-08-26 06:52:00
tags: 
- blog
---

今天心情特好，來講解一下如何把這兩個東西兜在一起。

其實很簡單 :D

一開始，得先把rss feed plugin安裝進去MT中，你可以到[MT Plugin Directory](http://mt-plugins.org/archives/entry/rss_feed.php)中找到這個模組以及安裝說明。不過我看了一下發現原本中文化的MT 2.661當中就已經包含了rss feed，所以假如說您是採用這個版本的MT就不需要在另外安裝rss feed plugin。

還有一個前置動作，就是必須擁有http://del.icio.us的線上書籤。
<a name='more'></a>
接下來呢，你只要照著[RSS Tutorial](http://deanmckenzie.org/howtofeed.txt)的範例，把tutorial中的第一個範例填在主索引樣版的右欄(如果你的side bar在左邊就是左欄)，然後在把我的線上書籤的RSS填進MTList的標籤之間就可以啦。

以下是我的範例：
&lt;div class="sidetitle"&gt;Blog&lt;/div&gt;
        &lt;MTList name="feeds"&gt;
        http://del.icio.us/rss/yurenju/blog
        &lt;/MTList&gt;
        &lt;MTListLoop name="feeds"&gt;
        &lt;MTRSSFeed&gt;

                &lt;div class="side"&gt;
                &lt;MTRSSFeedItems lastn="30"&gt;
                &lt;a href="&lt;$MTRSSFeedItemLink$&gt;"&gt;&lt;$MTRSSFeedItemTitle$&gt;&lt;/a&gt;&lt;br /&gt;
                &lt;/MTRSSFeedItems&gt;

        &lt;/MTRSSFeed&gt;
        &lt;/MTListLoop&gt;
&lt;div align="center"&gt;&lt;a href="http://del.icio.us/yurenju/blog"&gt;----- 更多部落格 -----&lt;/a&gt;&lt;/div&gt;
&lt;/div&gt;

延伸閱讀：[文森咖啡館](http://www.winsoncafe.com/)::[美味的Blogrolling](http://www.winsoncafe.com/archives/001190.html)

文森咖啡館提供了一個更方便的用法 :-)