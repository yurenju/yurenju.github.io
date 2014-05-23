title: \[筆記\] GNOME 顯示 Notify 訊息 — libnotify
date: 2006-04-24 17:09:00
tags: 
- development
- software
---

[![libnotify.png](http://static.flickr.com/53/134059341_2ef8dc1a5a_o.png)](http://www.flickr.com/photos/yurenju/134059341/ "Photo Sharing")

最近為了想做出跟 rhythmbox 一樣的 notify 訊息，研究了一下 code。後來發現只要使用 [libnotify](http://galago.sf.net/) 這個函式庫就可以做出這樣的效果。

源碼也很短，就下面這些：
<pre><tt>**<font color='#000080'>#include&lt;libnotify/notify.h&gt;</font>**
**<font color='#000080'>#include&lt;gdk-pixbuf/gdk-pixbuf.h&gt;</font>**

<font color='#009900'>int</font> **<font color='#000000'>main</font>**<font color='#990000'>(</font><font color='#990000'>)</font> <font color='#FF0000'>{</font>
	NotifyNotification <font color='#990000'>*</font>not<font color='#990000'>;</font>
	GdkPixbuf <font color='#990000'>*</font>pixbuf<font color='#990000'>;</font>
	_<font color='#9A1900'>//GdkPixbufLoader *loader;</font>_

	**<font color='#000000'>notify_init</font>**<font color='#990000'>(</font><font color='#FF0000'>'test'</font><font color='#990000'>)</font><font color='#990000'>;</font>
	_<font color='#9A1900'>//loader = gdk_pixbuf_loader_new_with_type('png', NULL);</font>_
	_<font color='#9A1900'>//gdk_pixbuf_loader_write(loader, 'icon.png'</font>_
	pixbuf <font color='#990000'>=</font> **<font color='#000000'>gdk_pixbuf_new_from_file</font>**<font color='#990000'>(</font><font color='#FF0000'>'logo.png'</font><font color='#990000'>,</font> NULL<font color='#990000'>)</font><font color='#990000'>;</font>
	not <font color='#990000'>=</font> **<font color='#000000'>notify_notification_new</font>**<font color='#990000'>(</font><font color='#FF0000'>'測試訊息'</font><font color='#990000'>,</font> <font color='#FF0000'>'這是一個測試訊息'</font><font color='#990000'>,</font> NULL<font color='#990000'>,</font> NULL<font color='#990000'>)</font><font color='#990000'>;</font>
	**<font color='#000000'>notify_notification_set_timeout</font>**<font color='#990000'>(</font>not<font color='#990000'>,</font> <font color='#993399'>10000</font><font color='#990000'>)</font><font color='#990000'>;</font>
	**<font color='#000000'>notify_notification_set_icon_from_pixbuf</font>**<font color='#990000'>(</font>not<font color='#990000'>,</font> pixbuf<font color='#990000'>)</font><font color='#990000'>;</font>
	**<font color='#000000'>notify_notification_set_hint_int32</font>** <font color='#990000'>(</font>not<font color='#990000'>,</font> <font color='#FF0000'>'x'</font><font color='#990000'>,</font> <font color='#993399'>1000</font><font color='#990000'>)</font><font color='#990000'>;</font>
	**<font color='#000000'>notify_notification_set_hint_int32</font>** <font color='#990000'>(</font>not<font color='#990000'>,</font> <font color='#FF0000'>'y'</font><font color='#990000'>,</font> <font color='#993399'>50</font><font color='#990000'>)</font><font color='#990000'>;</font>
	**<font color='#000000'>notify_notification_show</font>**<font color='#990000'>(</font>not<font color='#990000'>,</font> NULL<font color='#990000'>)</font><font color='#990000'>;</font>

	**<font color='#0000FF'>return</font>** <font color='#993399'>0</font><font color='#990000'>;</font>
<font color='#FF0000'>}</font>
</tt></pre>

相當的簡單。不過花了我好多天的時間 trace, 功力真是不足 :(