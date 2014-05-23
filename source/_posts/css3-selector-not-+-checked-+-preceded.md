title: CSS3 selector: not + checked + preceded
date: 2013-11-27 18:23:07
tags:
- css
- css3
---
CSS3 的 Selector 其實多了不少功能，以前需要用 javascript 才可以做出來的功能現在有時候只要用 CSS3 selector 就可以了，例如說：你有個 checkbox，如果按下這個 checkbox 後下面的 panel 才要顯示。一般來說我們可以用 javascript 對這個 panel 新增 class 來達到這個效果，不過用 CSS3 就又更簡單了。

你的 HTML 大概會長這樣：

```html
<input id="toggle" type="checkbox">
<label for="toggle">Show Panel</label>
<div id="panel">
Panel
</div>
```

而 CSS 只要這樣寫就可以控制 panel 顯示/隱藏了。下面 CSS 的意思是如果沒有 (:not) 選取 (:checked) 的時候，跟他同層 (~) 的 #panel 元素就隱藏起來。如果是緊鄰的元素也可以用 + 取代 ~。

```css
#toggle:not(:checked) ~ #panel {
  display: none;
}
```

你也可以在 jsFiddle 上面玩玩（點下面的 result）。

{% jsfiddle W4BrH %}