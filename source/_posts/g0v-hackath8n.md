title: g0v Hackath8n
date: 2014-04-19 20:54:49
cover: https://farm4.staticflickr.com/3804/13911947031_3a2732df1a_c.jpg
tags:
- g0v
- hackath8n
---
<a href="https://www.flickr.com/photos/yurenju/13911947031" title="g0v Hackath8n by Yuren Ju, on Flickr"><img src="https://farm4.staticflickr.com/3804/13911947031_3a2732df1a_c.jpg" width="800" height="451" alt="g0v Hackath8n"></a>

今天去 g0v 真的是蠻有趣的，原本要幫 Kuang-Che Liu 弄鄉民關心你的聯絡人，不過因為他早上沒來的關係所以我就開始找看看有沒有其他有趣的 project 可以作。聽完大家非常大一輪的介紹後，我決定去找立委投票指南的朋友們看看那邊有沒有什麼需要幫忙的。

然後今天就幫忙弄了兩個小東西：
1. 從[陽光法案主題網][1]把所有立委的財產申報資料全部都爬下來
2. 指令界面版本的 __臺北市__ 地價公告現值查詢

這兩個是有相關的，因為陽光法案李立委的財產申報資料裡面是有含土地資訊的，所以可以利用這個資訊進一步查詢到公告地價現值。

第一個爬完的資料已經放到 github 上面了，你可以看到一堆立法委員的[公開財產資料][2]（笑）

![enter image description here][3]

接下來就是可以利用 PDF 裡面的資料進一步了解立委所持有的土地的目前公告現值。這個功能目前還沒 merge，不過 [pull request 在這][4]如果你有興趣的話。首先你要有 nodejs，接下來用 npm 把相依套件裝一裝～

```
npm i
```

好了，接下來就可以玩了，最近割闌尾的立委很夯，我就隨便挑一個來試試 XDD，我從他的公開財產資料表裡面得到一筆資訊：『臺北市信義區信義段三小段0018-0000』，而指令就是這樣下：

```
node lq 信義區,信義段三小段,0018-0000
```

答案就會出來了：`公告現值 (元/平方公尺): 848,000`，因為財產資料裡面提到面積為 891 平方公尺，權力範圍為 2287/100000，依照這些資訊我們可以算出該資產目前的現值是多少：

```
848000 * 2287/100000 * 891 = 17279840.16
```

而根據該筆受贈的土地原本價格約為 900 餘萬，所以這筆土地幾乎漲了兩倍，算是很不錯的投資呢～


  [1]: http://sunshine.cy.gov.tw/GipOpenWeb/wSite/sp?xdUrl=/wSite/SpecialPublication/baseQuery.jsp
  [2]: https://github.com/g0v/twly_crawler/tree/master/pdf
  [3]: http://i.imgur.com/kxKAYJo.png
  [4]: https://github.com/g0v/twly_crawler/pull/9
