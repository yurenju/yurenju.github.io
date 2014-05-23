title: Python 初體驗 (2) - BATON 演算法撰寫
date: 2007-05-27 22:21:00
tags: 
- linux
- graphviz
- python
- eog
---

之前的[文章](http://yurinfore.blogspot.com/2007/05/python.html)提到了用 Python 與 Gnuplot 解決作業之後，我就大量的使用 Python 來解決各項課業上的問題。

最近正在實作 [BATON](http://scholar.google.com/scholar?hl=en&lr=&amp;cluster=1332811958184336277) 的演算法，當仁不讓的還是使用 Python 來解決這個問題。以下是我要實作演算法的虛擬碼：
<div class="highlight"><pre>Algorithm: join(node n)
If (Full(LeftRoutingTable(n)) and
Full(RightRoutingTable(n)) and
((LeftChild(n)==null) or (RightChild(n)==null))
Accept new node as child of n
Else
If ((Not Full(LeftRoutingTable(n))) or
  (Not Full(RightRoutingTable(n))))
 Forward the JOIN request to parent(n)
Else
 m=SomeNodesNotHavingEnoughChildrenIn
      (LeftRoutingTable(n), RightRoutingTable(n))
 If (there exists such an m)
    Forward the JOIN request to m
 Else
    Forward the JOIN request to one of its
    adjacent nodes
 End If
End If
End If
</pre></div>而下面的則是 Python 實作的程式碼：
<div class="highlight"><pre><span style="color: rgb(0, 112, 32); font-weight: bold;">def</span> <span style="color: rgb(6, 40, 126);">join</span>(child, n):
<span style="color: rgb(0, 112, 32); font-weight: bold;">if</span> Full(n[<span style="color: rgb(64, 112, 160);">'LeftRoutingTable'</span>]) <span style="color: rgb(0, 112, 32); font-weight: bold;">and</span> \
Full(n[<span style="color: rgb(64, 112, 160);">'RightRoutingTable'</span>]) <span style="color: rgb(0, 112, 32); font-weight: bold;">and</span> \
((n[<span style="color: rgb(64, 112, 160);">'LeftChild'</span>] <span style="color: rgb(102, 102, 102);">==</span> <span style="color: rgb(0, 112, 32);">None</span>) <span style="color: rgb(0, 112, 32); font-weight: bold;">or</span> (n[<span style="color: rgb(64, 112, 160);">'RightChild'</span>] <span style="color: rgb(102, 102, 102);">==</span> <span style="color: rgb(0, 112, 32);">None</span>)):
 <span style="color: rgb(0, 112, 32); font-weight: bold;">print</span> <span style="color: rgb(64, 112, 160);">'    '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(n[<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">' -- '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(child[<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">';'</span>
 accept(child, n)
<span style="color: rgb(0, 112, 32); font-weight: bold;">else</span>:
 <span style="color: rgb(0, 112, 32); font-weight: bold;">if</span> <span style="color: rgb(0, 112, 32); font-weight: bold;">not</span> Full(n[<span style="color: rgb(64, 112, 160);">'LeftRoutingTable'</span>]) <span style="color: rgb(0, 112, 32); font-weight: bold;">or</span> <span style="color: rgb(0, 112, 32); font-weight: bold;">not</span> Full(n[<span style="color: rgb(64, 112, 160);">'RightRoutingTable'</span>]):
     join(child, n[<span style="color: rgb(64, 112, 160);">'Parent'</span>])
 <span style="color: rgb(0, 112, 32); font-weight: bold;">else</span>:
     m <span style="color: rgb(102, 102, 102);">=</span> NodesNotEnoughChildren(n[<span style="color: rgb(64, 112, 160);">'LeftRoutingTable'</span>], n[<span style="color: rgb(64, 112, 160);">'RightRoutingTable'</span>])
     <span style="color: rgb(0, 112, 32); font-weight: bold;">if</span>(m <span style="color: rgb(102, 102, 102);">!=</span> <span style="color: rgb(0, 112, 32);">None</span>):
         join(child, m)
     <span style="color: rgb(0, 112, 32); font-weight: bold;">else</span>:
         <span style="color: rgb(96, 160, 176); font-style: italic;"># Forward the JOIN request to one ofits adjacent nodes</span>
         <span style="color: rgb(0, 112, 32); font-weight: bold;">if</span> n[<span style="color: rgb(64, 112, 160);">'LeftAdjacent'</span>] <span style="color: rgb(102, 102, 102);">!=</span> <span style="color: rgb(0, 112, 32);">None</span>:
             join(child, n[<span style="color: rgb(64, 112, 160);">'LeftAdjacent'</span>])
         <span style="color: rgb(0, 112, 32); font-weight: bold;">else</span>:
             join(child, n[<span style="color: rgb(64, 112, 160);">'RightAdjacent'</span>])
</pre></div>
是不是與虛擬碼非常相似呢？撰寫完演算法後，還有一個工作就是要視覺化的表達樹的結構。正巧這幾個禮拜在[紅塵一隅間拾得](http://greenisland.csie.nctu.edu.tw/wp/)的[文章](http://greenisland.csie.nctu.edu.tw/wp/2007/04/13/989/)裡面提到了 [graphviz](http://www.graphviz.org/) 這個非常好用的工具，可以用來產生各種有向、無向圖形。所以就利用這個工具來產生圖形，而 Python 呼叫外部程式當然也是很簡單：
<div class="highlight"><pre><span style="color: rgb(0, 112, 32); font-weight: bold;">def</span> <span style="color: rgb(6, 40, 126);">node</span>(name):
<span style="color: rgb(0, 112, 32); font-weight: bold;">return</span> {
    <span style="color: rgb(64, 112, 160);">'Parent'</span> : <span style="color: rgb(0, 112, 32);">None</span>,
    <span style="color: rgb(64, 112, 160);">'LeftChild'</span> : <span style="color: rgb(0, 112, 32);">None</span>,
    <span style="color: rgb(64, 112, 160);">'RightChild'</span> : <span style="color: rgb(0, 112, 32);">None</span>,
    <span style="color: rgb(64, 112, 160);">'LeftRoutingTable'</span> : <span style="color: rgb(0, 112, 32);">list</span>(),
    <span style="color: rgb(64, 112, 160);">'RightRoutingTable'</span> : <span style="color: rgb(0, 112, 32);">list</span>(),
    <span style="color: rgb(64, 112, 160);">'LeftAdjacent'</span> : <span style="color: rgb(0, 112, 32);">None</span>,
    <span style="color: rgb(64, 112, 160);">'RightAdjacent'</span> : <span style="color: rgb(0, 112, 32);">None</span>,
    <span style="color: rgb(64, 112, 160);">'Name'</span> : name,
    <span style="color: rgb(64, 112, 160);">'Level'</span> : <span style="color: rgb(64, 160, 112);">0</span>
}

<span style="color: rgb(0, 112, 32); font-weight: bold;">def</span> <span style="color: rgb(6, 40, 126);">travel</span>(node, tstr):
<span style="color: rgb(0, 112, 32); font-weight: bold;">if</span> node[<span style="color: rgb(64, 112, 160);">'LeftChild'</span>] <span style="color: rgb(102, 102, 102);">!=</span> <span style="color: rgb(0, 112, 32);">None</span>:
    tstr <span style="color: rgb(102, 102, 102);">+=</span> <span style="color: rgb(64, 112, 160);">'    '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(node[<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">' -- '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(node[<span style="color: rgb(64, 112, 160);">'LeftChild'</span>][<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">';</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">'</span>
    tstr <span style="color: rgb(102, 102, 102);">=</span> travel(node[<span style="color: rgb(64, 112, 160);">'LeftChild'</span>], tstr)
<span style="color: rgb(0, 112, 32); font-weight: bold;">if</span> node[<span style="color: rgb(64, 112, 160);">'RightChild'</span>] <span style="color: rgb(102, 102, 102);">!=</span> <span style="color: rgb(0, 112, 32);">None</span>:
    tstr <span style="color: rgb(102, 102, 102);">+=</span> <span style="color: rgb(64, 112, 160);">'    '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(node[<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">' -- '</span> <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(0, 112, 32);">str</span>(node[<span style="color: rgb(64, 112, 160);">'RightChild'</span>][<span style="color: rgb(64, 112, 160);">'Name'</span>]) <span style="color: rgb(102, 102, 102);">+</span> <span style="color: rgb(64, 112, 160);">';</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">'</span>
    tstr <span style="color: rgb(102, 102, 102);">=</span> travel(node[<span style="color: rgb(64, 112, 160);">'RightChild'</span>], tstr)
<span style="color: rgb(0, 112, 32); font-weight: bold;">return</span> tstr

root <span style="color: rgb(102, 102, 102);">=</span> node(<span style="color: rgb(64, 112, 160);">'root'</span>)
child <span style="color: rgb(102, 102, 102);">=</span> node(<span style="color: rgb(64, 112, 160);">'child'</span>)
join(child, root)

<span style="color: rgb(0, 112, 32); font-weight: bold;">for</span> i <span style="color: rgb(0, 112, 32); font-weight: bold;">in</span> <span style="color: rgb(0, 112, 32);">range</span>(<span style="color: rgb(64, 160, 112);">0</span>, <span style="color: rgb(0, 112, 32);">int</span>(sys<span style="color: rgb(102, 102, 102);">.</span>argv[<span style="color: rgb(64, 160, 112);">1</span>])):
c <span style="color: rgb(102, 102, 102);">=</span> node(i)
join(c, root)
<span style="color: rgb(0, 112, 32); font-weight: bold;">print</span> <span style="color: rgb(64, 112, 160);">'Finish</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">'</span>

tstr <span style="color: rgb(102, 102, 102);">=</span> travel(root, <span style="color: rgb(64, 112, 160);">''</span>)

temp <span style="color: rgb(102, 102, 102);">=</span> Template(<span style="color: rgb(64, 112, 160);">'graph G{</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">$info</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">}</span><span style="color: rgb(64, 112, 160); font-weight: bold;">\n</span><span style="color: rgb(64, 112, 160);">'</span>)
s <span style="color: rgb(102, 102, 102);">=</span> temp<span style="color: rgb(102, 102, 102);">.</span>substitute(info<span style="color: rgb(102, 102, 102);">=</span>tstr)

<span style="color: rgb(0, 112, 32);">file</span> <span style="color: rgb(102, 102, 102);">=</span> <span style="color: rgb(0, 112, 32);">open</span>(<span style="color: rgb(64, 112, 160);">'temp.dot'</span>, <span style="color: rgb(64, 112, 160);">'w'</span>)
<span style="color: rgb(0, 112, 32);">file</span><span style="color: rgb(102, 102, 102);">.</span>write(s)
<span style="color: rgb(0, 112, 32);">file</span><span style="color: rgb(102, 102, 102);">.</span>close()

os<span style="color: rgb(102, 102, 102);">.</span>system(<span style="color: rgb(64, 112, 160);">'dot -Tsvg -o temp.svg temp.dot'</span>)
os<span style="color: rgb(102, 102, 102);">.</span>system(<span style="color: rgb(64, 112, 160);">'eog temp.svg'</span>)
</pre></div>執行完程式後 Eye of GNOME 就開啟了這張繪製好的 SVG 圖檔。

[![Screenshot-temp.svg](http://farm1.static.flickr.com/237/516142171_59697abbaf.jpg)](http://www.flickr.com/photos/yurenju/516142171/ "Photo Sharing")

Python 是個好東西阿！