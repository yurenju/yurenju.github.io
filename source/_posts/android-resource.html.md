title: Android 小技巧：找出未用的 Resource
date: 2011-10-17 17:34:00
tags: 
- Android
---

記得好像有其他 Android 內建的方法可以哪些 resource 沒有被使用。一時找不到，Google 一下發現另外一套：[Android Resource Tracker](http://code.google.com/p/androidresourcetracker/)。

使用方法也很簡單，在 project 目錄底下執行：
<pre class="brush: text">$ java -jar &lt;PATH_TO_JAR&gt;/AndroidUnusedResources1.4.jar
</pre>
接著就會列出未被使用的資源：

<pre class="brush: text">Running in: /Users/yurenju/git/YOUR_PROJECT
242 resources found

44 unused resources were found:
array     : upload_photo_options
    /Users/yurenju/git/YOUR_PROJECT/res/values/arrays.xml
...
</pre>