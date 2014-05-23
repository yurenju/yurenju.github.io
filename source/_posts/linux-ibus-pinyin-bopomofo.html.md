title: Linux 無調注音輸入法 - ibus-pinyin-bopomofo
date: 2010-10-06 15:04:00
tags: 
- ibus-pinyin-bopomofo
- 輸入法
- 注音
- ibus
- ibus-pinyin
- 拼音
---

前幾天，[Pingooo](http://pingyeh.blogspot.com/)、[Hychen](http://hychen.wuweig.org/)&nbsp;在 TOSSUG 討論最近 Ubuntu 10.04 的 ibus 輸入法有很多 issues，然後又聊到對岸的拼音輸入法比起注音輸入法少打了聲調速度好像快很多之後，我們三個就想說是不是自己來修一下 ibus 的問題，順便看有沒有可能寫出無調的注音輸入法。

無調注音輸入法的概念也很簡單，基本上跟使用新酷音用法差不多，但是不需要輸入一二三四聲，所以才稱爲無調注音。基本上拼音輸入法原本就不需要輸入聲調，理論上我們可以基於拼音輸入法把英文拼音轉換成注音這樣的基礎原理來創造無調注音輸入法。

沒想到前幾天 hychen 丟出了一個對岸同胞作出以[拼音爲基礎的注音輸入法](http://www.byvoid.com/blog/ibus-bopomofo-1-3-9-features/)，正巧是我們想要的無調注音輸入法！

這個注音輸入法是基於 ibus-pinyin 所作的注音輸入法，雖然說目前正在研發還不是很穩定，不過基本上方向是與我們心目中的無調注音輸入法是相同的。要在 Ubuntu 10.04 安裝也是相當容易，輸入以下指令即可安裝：

<pre class="brush: bash">sudo add-apt-repository ppa:shawn-p-huang/ppa
sudo apt-get update
sudo apt-get install ibus-gtk ibus-qt ibus-pinyin ibus-pinyin-db-open-phrase

</pre>
這兩天試用了一下發現有些問題先筆記起來，或許有機會可以提交到原作者的『[注音模式用戶交互設計方案](https://docs.google.com/document/edit?id=1x3JDrt4BuoupbK1p1jwyB1zSsu7eJcNxHnYlQO8hucU&amp;hl=zh_TW#)』，這些發現是基於一個新酷音使用者的意見回饋，或許拼音輸入法的使用者有更好的使用方式，只是我只試用兩天還沒發現罷了

1.  輸入完畢後，如果輸入法候選字都正確時，不能直接按下 enter 鍵直接輸出，需要先按空白鍵再選擇第一組正確的候選字組纔可以輸入（或者是連按兩下空白鍵）。
2.  輸入完畢後直接按 enter 會直接出現剛剛敲過的所有按鍵，看起來像這樣：d0fux9vu;5ku;。這個似乎不是使用者預期的輸出
3.  以上兩點如果將 enter 鍵改成直接輸出正確的候選字會比較快速。
4.  按着 shift + , 或者 shift + . 出現的並不是全形的逗號以及句號，而是『《』以及『》』，感覺不符合使用者預期
5.  使用 ` 鍵叫出符號表的時候，如果已經設定選字鍵爲 asdfghjkl;，但是符號表的選字鍵依然是 1234567890
6.  輸入了一個句子後，可以用左右鍵移動到注音符號的任意位置，但不清除功能爲何。看起來似乎可以用來決定切字點，但是移到要切字的位置後按下空白選字，接下來的字會變成注音符號。例如要輸入：十全路十五號，需要切字在『十五』之間。如果移到十五中間按下空白鍵選字，整串字會變成『十全路十ㄨㄏㄠ』
7.  按下空白鍵選字後，必須要按下 page up/down 跳頁選字。此時方向鍵之中的上下鍵並沒有功能，建議可以用來取代&nbsp;page up/down
8.  如果第一次選詞的時候沒有正確選擇，下次就算正確選詞也沒辦法更正。比如說我第一次選擇注音輸入法的時候選錯成『註音』，接下來就算我多選幾次注音也沒辦法讓註音慢慢消失。<div>接下來希望可以跟開發者有些聯絡，來協助改善這個無調注音輸入法 :-)</div>