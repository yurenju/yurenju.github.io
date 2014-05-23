title: Bugzilla requests to trello
date: 2014-05-23 16:37:13
cover: http://i.imgur.com/D8fn0aT.png
tags:
- bugzilla
- trello
---
自從在 Mozilla 工作一陣子後開始會有很多 bugzilla 來的 request，像是 review, needinfo 或是 feedback feedback request 之類的，之前我一直用 bugzilla 上面的 My Dashboard 來管理這件事情，不過後來我發現除了 request 以外，Dashboard 並不能幫我管理其他的工作項目，所以我就開始尋找我的 task 管理之路⋯。

之前雖然就有用過 trello 管理各式各樣的事情（結婚、COSCUP、工作上的事情），不過後來因為他不能自動把 bugzilla request 轉換成 trello card 後就比較少用了，而這次又回頭來想想是不是有辦法用 trello 來管理，仔細想想我只要用 ifttt 把信箱裡面出現 "review requested:" 這個字串的寄到 trello 提供的信箱就收工啦！所以我就開始這樣設定了

不過首先我第一個遇到的問題是，當你收到出現 "review requested:" 就寄到 trello 提供的信箱會遇到無窮重寄的問題，因為就算你寄了 "review requested:" 的信之後，gmail 的 search query 還是會 filter 到一樣的關鍵字，然後 ifttt 又會重複寄一次，所以每次收到 review request 就會不同的鬼打牆重複寄⋯，還好 ifttt 寄信的時候可以更改信件標題內文，所以我只要加入特殊的字串（像是 #trello）到信件內文，接著過濾條件用減號 -trello 即可。

首先先到 trello 的側邊欄找出 trello 提供的 email，寄過去就會自動轉成 card：

![Trello email][1]

接下來就是 ifttt 發揮的時候了，建立一個新的 recipe，並且選擇用 gmail 作為來源，條件是 New email from search，並且用 subject:(review-requested:) -trello 作為過濾條件：

![gmail trigger][2]

動作則是用 gmail 寄送郵件寄到 trello 提供的 email，並且在內文多加一個 #trello 讓前面的搜尋條件可以排除這封信件，另外我的 trello 有開一個 review 的標簽，所以我還在標題多加了 #review：

![Send email to trello][3]

這樣就好了，之後 review request 就會自動加到 trello 裡面，而我也可以把自己的工作手動輸入。

![trello screenshot][4]

另外這邊有另外一個 trello 的 [bookmarklet][5] 也很好用，可以把網頁轉換成 trello card。


  [1]: http://i.imgur.com/cUNRyr7.png
  [2]: http://i.imgur.com/4hAgEKe.png
  [3]: http://i.imgur.com/jgu3q7D.png
  [4]: http://i.imgur.com/D8fn0aT.png
  [5]: https://github.com/thedufer/Trello-Bookmarklet-Maker
