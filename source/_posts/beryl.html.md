title: \[解決\] 使用 Beryl 後最大化視窗後標題列空白
date: 2007-04-24 01:01:00
tags: 
- ThinkPad
- radeon
- ati
- Xserver
- linux
- beryl
- ubuntu
- X-Window
---

在我的 ThinkPad X31 開啟 beryl 一直以來都有一個問題，就是最大化視窗後，視窗的標題列會變成空白，如下圖所示：

[![Screenshot](http://farm1.static.flickr.com/200/470109440_63cdb4904f.jpg)](http://www.flickr.com/photos/yurenju/470109440/ "Photo Sharing")

後來找了很多資料，終於知道該怎麼解決這個問題，其實只要在 xorg.conf 設定裡面加上下面的設定即可！
> Section "Device"
>       Identifier      "ATI Technologies Inc Radeon Mobility M6 LY"
>       Driver          "ati"
>       BusID           "PCI:1:0:0"
>       Option          "XAANoOffscreenPixmaps" "true"
>       <span style="font-weight: bold; color: rgb(255, 0, 0);">Option          "AGPSize" "32"</span>
> EndSection加入後重新啟動 X 即可！

[![Screenshot-2](http://farm1.static.flickr.com/229/470109450_3609201e72.jpg)](http://www.flickr.com/photos/yurenju/470109450/ "Photo Sharing")

參考資料：[Emerald White Window Borders](http://forum.beryl-project.org/viewtopic.php?f=36&t=320&amp;start=0&st=0&amp;sk=t&amp;sd=a)