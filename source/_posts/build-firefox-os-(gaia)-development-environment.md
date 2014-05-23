title: Build Firefox OS (Gaia) development environment
date: 2013-11-20 16:33:57
tags:
- Firefox OS
- Gaia
---
開發 Gaia 可以在三種環境裡面開發：實體裝置、b2g desktop (Simulator) 或是 Firefox Nightly browser。我想要介紹的是如何在 Firefox Nightly 開發。

在作業系統的選擇上，我強烈建議使用 Mac OS 或是 Linux 其中一種。Windows 雖然也可以開發（而且我也經常測試這個平台）不過由於大多數的 Gaia Developer 都沒有使用 Windows，如果有任何問題也是比較不容易被發現並修正的，所以選擇 Mac OS or Linux 可以踩到比較少雷。

<!-- more -->

至於所需的軟體你需要以下軟體：

1. git
2. make
3. [Firefox Nightly Browser][1]

首先你需要登入你的 github 帳號，並且到 [Gaia 專案頁面][2]，按下右上角的 **Fork** 可以將 Gaia fork 到自己 github 帳號底下，結束後將會被導到你自己的 gaia repository，這個時候右邊中間會有一個 **XXX clone URL**，XXX 可能是 https or ssh。如果你設定好了正確的 ssh key 的話你可以用 ssh 的方式，否則請選擇 https 模式。

將該網址複製下來，並且打開終端機鍵入：

    $ git clone <CLONE_URL>

第一次 clone 要非常非常久，請去喝個下午茶再回來。結束後請用 git remote 來看你現在已經設定的 remote

    $ git remote -v
    origin  git@github.com:<USERNAME>/gaia.git (fetch)
    origin  git@github.com:<USERNAME>/gaia.git (push)

接下來你需要把 mozilla-b2g 的 repository 加入 remote

    $ git remote add b2g git@github.com:mozilla-b2g/gaia.git

需要這樣做的原因是因為我們需要用 pull request 把你的 change 發送到 github，你可以參考這張圖。

![Gaia development workflow][3]

接下來只要打 DEBUG=1 make 就可以開始產生 gaia 的 profile 目錄了。指令完成後會產生一個 profile-debug 的目錄，最後用 Nightly Browser 打開它即可。

    $ nightly -profile ABSOLUTE_GAIA_PROFILE_PATH

![Running Gaia on Nightly][4]

  [1]: http://nightly.mozilla.org/
  [2]: https://github.com/mozilla-b2g/gaia/
  [3]: http://1.bp.blogspot.com/-geO9X_h7_u8/UdVIBLDGqlI/AAAAAAAAeUU/9a51bh2FujM/s1375/Gaia+Development+workflow.png
  [4]: http://i.imgur.com/kKucvG6.png