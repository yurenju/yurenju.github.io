title: 用 eclipse 開發 Firefox/Thunderbird Extension
date: 2010-05-21 15:14:00
tags: 
---

再次聲明，我自己是用 vim 寫 mozilla application，搞 eclipse 純粹只是自 high。

## 前置作業

要用 eclipse 開發 Mozilla Application，首先需要 WTP (Web Tools Platform)。一樣也是 [help] → [Install New Software], work with 填入 [http://download.eclipse.org/webtools/updates](http://download.eclipse.org/webtools/updates)，接著安裝最新的 WTP。在撰文時最新的版本是 Web Tools Platform (WTP) 3.1.2。

安裝完畢後，或許你還會有興趣安裝 [XulBooster](http://cms.xulbooster.org/)。請到 [Sourceforge 下載](http://sourceforge.net/projects/xulbooster/)最新版本的 XulBooster，並且在&nbsp;&nbsp;[help] → [Install New Software] 按下 Add&nbsp;→ Archive，選擇剛下載的 XulBooster 的 zip file 安裝。

## 開發延伸套件

通常會有兩個狀況：（一）你已經自己有 extension，只是想轉換開發環境為 eclipse。（二）你想要全新開發一個 extension。如果你是第二種狀況，XulBooster 有提供 XUL project 幫你建立簡單的 extension 結構。或是也可以用 [Extension Wizard](http://ted.mielczarek.org/code/mozilla/extensionwiz/) 建立，不過用 Extension Wizard 建立的話，要在自己建立 .project file，在你匯入專案時他才會認得你的 project，請參考 [[筆記] 在 eclipse 用 git](http://yurinfore.blogspot.com/2010/05/eclipse-git.html)。

如果你是第一種狀況的使用者，同樣的你也要[建立 .project file](http://yurinfore.blogspot.com/2010/05/eclipse-git.html)。接下來就可以在 eclipse 開發了。

## 安裝延伸套件

安裝套件很麻煩。這邊我寫了兩個 script 分別處理 windows 跟 linux 的安裝。EXTENSION_NAME 請自行取代成你的 extension 名稱。使用方式都一樣：

Linux:
./install.sh trxw3c99.default

Windows:
install.bat trxw3c99.default

trxw3c99.default 請改成在你電腦上的目錄名稱。

Linux 版 (Linux 版我多處理了 vim 的暫存檔問題, 刪除 compreg.dat 等問題)
<pre class="brush: shell">#!/bin/bash

FF_PROFILE="$HOME/.mozilla/firefox/$1"
FF_EXT="extensions/EXTENSION_NAME"

echo "copy files...."
find . -maxdepth 1 -mindepth 1 \
        ! -name '.git' ! -name '*.swp' \
        -printf "\t%f\n" -exec cp -r {} $FF_PROFILE/$FF_EXT \;

if [ -e "$FF_PROFILE/compreg.dat" ]; then
    echo "remove compreg.dat"
    rm "$FF_PROFILE/compreg.dat"
fi

echo "delete vim swap files..."
find $FF_PROFILE/$FF_EXT -name *.swp \
     -printf "\t%f\n" -exec rm {} \;
</pre>
Windows 版本要有兩個檔案 exculude.txt 跟 install.bat
exclude.txt 裡面指包含一行： .git

install.bat:
<pre class="brush: text">xcopy * %APPDATA%\Mozilla\Firefox\Profiles\%1\extensions\EXTENSION_NAME /E /Y /EXCLUDE:exclude.txt
</pre>

## 在 eclipse 安裝延伸套件

寫好安裝 script 之後，在 eclipse 的安裝就簡單的多。在 [Run] → [External Tools] → [External Tools Configurations] 在 Program 按右鍵選擇 New，取名為 Install。Location 按 Browse Workspace 選擇 install.bat，Working Directory 按 Browse Workspace 選擇你的 extension project。選擇完畢之後應該長這樣：

<div class="separator" style="clear: both; text-align: center;">[![](http://1.bp.blogspot.com/_iOO0fC4NKLE/S_Yw-ih7_3I/AAAAAAAAIm4/mpz_vyM8ZY8/s400/external-configuration.png)](http://1.bp.blogspot.com/_iOO0fC4NKLE/S_Yw-ih7_3I/AAAAAAAAIm4/mpz_vyM8ZY8/s1600/external-configuration.png)</div>
設定完畢後，按下 toolbar 上面的 ![](http://3.bp.blogspot.com/_iOO0fC4NKLE/S_Yxcx-X9-I/AAAAAAAAIm8/39o1jFmbcmk/s1600/Screenshot-Java+-+Eclipse+.png) 選擇 install 就可以安裝了。

相同的如果你想跑 Firefox 也可以用相同的設定方式跑 Firefox :)