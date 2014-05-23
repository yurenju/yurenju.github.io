title: 關於 glib signal 的 callback 參數
date: 2009-08-19 10:05:00
tags: 
- glib
- callback
---

當你自訂了一個信號時，會需要定義 callback 的參數為何。平常寫 GTK+ 時的 callback function 通常長這樣：
> <span style="font-family: 'Courier New', Courier, monospace;">gboolean callback (GtkWidget *widget, GdkEvent *event, gpointer data);</span>所以我剛開始實作完 signal 之後，我還以為所有 callback 都長這樣 XD，但其實不是的，callback 的參數為何，其實是看 g_signal_new 時傳入的 marshaller 為何。關於 gobject marshaller 的部份可以參考 olv 長輩的《[gobject 的 marshaller](http://olvaffe.blogspot.com/2008/01/gobject-marshaller.html)》。而我是直接使用 glib 給的 marshaller。我用的是 g_cclosure_marshal_VOID__VOID，而查詢 [API 手冊](http://library.gnome.org/devel/gobject/unstable/gobject-Closures.html#g-cclosure-marshal-VOID--VOID)後可得知他的 callback 參數為
> <span style="font-family: 'Courier New', Courier, monospace;">void (*callback) (gpointer instance, gpointer user_data)</span>所以調用的的時候傳入這種參數即可，不需要 GdkEvent，因為有 GdkEvent 參數是 gtk 自行定義的 marshaller。