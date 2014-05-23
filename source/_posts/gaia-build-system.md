title: Gaia Build System
date: 2014-01-02 11:37:14
cover: http://i.imgur.com/hdrxYfT.png
tags:
- Firefox OS
- Gaia
- Build system
---
(這篇部分的資訊我也寫到 [MDN](https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Build_System_Primer#Build_process) 上面去了。）

Gaia Build System 基本上是由 make, node.js script 跟 xpcshell script 所構成的（以前還有 Python Script 不過已經被消滅了）。前兩個大家都清楚，所以只介紹一下 xpcshell。

xpcshell 是一個放在 xulrunner 裡面的一個執行環境，它的用處跟 node.js 一樣，可以直接執行 javascript，所以可以拿它來處理一些 build system 要做的一些工作，另外 gaia 的 build system 也有使用 commonjs 的環境，所以基本上使用 xpcshell 跟用 node.js 寫東西差不多，只是可以用的 library 跟 API 不同。

<!-- more -->

當你執行 `make` 的時候實際上會發生的事情是 make 會去設置 xpcshell 跟 node.js 的執行環境，並且在不同的地方他們兩種執行環境，我相信 node.js 比較容易理解，但為什麼需要在 xpcshell 上面可以跑呢？因為這樣 build system 就可以在 firefox extension 上面跑，下面的影片展示了如何在 Firefox extension 裡面直接造出並且執行 Gaia。

{% youtube cDz7YORcm3k %}

## Build process

當你執行 `make` 會發生的事情如下：

![Gaia build process][1]
{% rawblock %}
<dl>
 <dt>
  Looking for .b2g.mk &amp; local.mk</dt>
 <dd>
  build system 會去找 local.mk 跟 .b2g.mk 是否存在，有找到的話會引入他們</dd>
 <dt>
  Download xulrunner</dt>
 <dd>
  因為 xpcshell scripts 全都要在 xulrunner 上面跑，所以要先下載 xulrunner</dd>
 <dt>
  preference.js</dt>
 <dd>
  產生給 Firefox OS 用，預設的 preferences，最後的產出是 user.js，Gaia 執行的時候 gecko 會讀取這個檔案，另外環境變數（像是 DEBUG=1）會影響到這些數值。</dd>
 <dt>
  variant.js</dt>
 <dd>
 會從 GAIA_DISTRIBUTION_DIR/variant.json 讀取客製化 gaia 所需的設定資訊，這可以拿來針對不同電信商以及區域產生不同的 app 集合，桌布以及鈴聲。
  </dd>
 <dt>
  applications-data.js</dt>
 <dd>
 有些 app 會需要一些初始化的資訊如 homescreen 要如何排列 app 跟網頁瀏覽器預設的搜尋引擎，這個 script 會負責產生這些資料檔案
  </dd>
 <dt>
  app makefiles</dt>
 <dd>
 如果 app 的目錄底下有 makefile 的話在這個時間點會被執行
  </dd>
 <dt>
  setup test-agent</dt>
 <dd>
 設置 test-agent 是兩個 make rules "test-agent-config" 跟 "test-agent-bootstrap-apps"，這兩個會針對每個 app 設定測試所需的環境。
</dd>
 <dt>
  webapp-optimize.js</dt>
 <dd>
 拿來做 minify javascript，把 l10n 的檔案集合成一個 json 以及產生預設語言的 HTML 檔案等等最佳化的一些步驟。
  </dd>
 <dt>
  webapp-zip.js</dt>
 <dd>
 把每個 app 壓縮成 application.zip 並且放到 profile 目錄底下</dd>
 <dt>
  optimize-clean.js</dt>
 <dd>
  如果針對預設語言有產生 html 檔案的話，會在這邊被刪除</dd>
 <dt>
  contact</dt>
 <dd>
 如果 GAIA_DISTRIBUTION_DIR 裡面有預設的聯絡人資訊在這邊會被複製到 profile 目錄
  </dd>
 <dt>
  extensions</dt>
 <dd>
 複製 GAIA_DIR/tools/extensions 裡面的擴充套件到 profile，不同的設定會複製不同的擴充套件。
  </dd>
 <dt>
  settings.js</dt>
 <dd>
  產生給 Gaia 用預設的 settings</dd>
 <dt>
  create-default-data</dt>
 <dd>
 把一些預設的複製到 profile 目錄底下
  </dd>
 <dt>
  additional-extensions.js</dt>
 <dd>
 下載特定的擴充套件並且複製到 profile 目錄</dd>
</dl>
{% endrawblock /%}
  [1]: http://i.imgur.com/hdrxYfT.png