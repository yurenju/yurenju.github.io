title: Jenkins 系列 (1): 在終端機下設定 Android 模擬器
date: 2011-09-10 12:12:00
tags: 
- jenkins
- Android
---

命題的有點怪，不過基本上這是篇為了在&nbsp;Jenkins&nbsp;進行 unit test 以及 daily build 的前置動作。當在建立 Continuous Integration 的測試系統時，我希望可以在一台獨立的機器進行測試。而在遠端的伺服器不一定有 X Window 的狀況，這個時候就會需要在終端機上設定 Android Eumlator 環境。

首先是下載並且解壓縮 Android SDK

<pre class="brush: text">
$&nbsp;wget http://dl.google.com/android/android-sdk_r12-linux_x86.tgz
$ tar zxvf android-sdk_r12-linux_x86.tgz</pre>
切換到&nbsp;android-sdk-linux_x86/tools，並且用 --no-ui 選項來安裝 Android 3.2/2.3 或其他平台相關的 Platform SDK

<pre class="brush: text">
$ cd android-sdk-linux_x86/tool
$ ./android update sdk --no-ui
</pre><div>
</div><div>這個時候會從最新的平台（如 Android 3.2）開始下載安裝，一路從最新的下載到最舊的 SDK。我是在下載完 Android 2.2 的 Platform SDK 就按 Ctrl + C 終止安裝。</div><div>
</div><div>編輯家目錄的 ~/.bash_profile，加入執行路徑：</div><div>
</div><div><pre class="brush: text">PATH="$PATH:~/android-sdk-linux_x86/tools:~/android-sdk-linux_x86/platform-tools</pre></div><div>
</div><div>安裝完 platform SDK 之後，可以利用下面的指令看到安裝了哪些 platform SDK:</div><div>
</div><div><pre class="brush: text">$&nbsp;android list target</pre></div><div>
</div><div>輸出大略如下：

<pre class="brush: text">id: 4 or "android-8"
     Name: Android 2.2
     Type: Platform
     API level: 8
     Revision: 3
     Skins: QVGA, WVGA854, WQVGA432, HVGA, WVGA800 (default), WQVGA400
id: 5 or "android-9"
     Name: Android 2.3.1
     Type: Platform
     API level: 9
     Revision: 2
     Skins: QVGA, WVGA854, WQVGA432, HVGA, WVGA800 (default), WQVGA400
id: 6 or "android-10"
     Name: Android 2.3.3
     Type: Platform
     API level: 10
     Revision: 2
     Skins: QVGA, WVGA854, WQVGA432, HVGA, WVGA800 (default), WQVGA400
</pre>

用下面的指令就可以建立新的 Android 2.3.3 模擬器環境</div><div>
</div><div><pre class="brush: text">$ android create avd --name android-2.3 --target android-10</pre></div><div>
</div><div>這個時候就可以用不跑模擬器畫面的方式啟動 Android 模擬環境：</div><div>
</div><div><pre class="brush: text">$ emulator-arm -avd android-2.3 -no-window</pre></div> 想知道運行狀況，可以利用 adb logcat 瞭解。