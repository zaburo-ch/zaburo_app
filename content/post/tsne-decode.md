+++
date = "2016-06-29T13:06:24+09:00"
title = "t-SNE の逆変換を試してみた"
tags = ["Python", "機械学習", "可視化"]
+++
Parametric t-SNEでt-SNEの変換をニューラルネットで近似することができたので、  
その逆についてもやってみました。  

逆変換と言っても特に難しいことはやっておらず、  
まず普通にBarnes-Hut t-SNEで訓練データを2次元に変換して、  
変換後の座標を入力、変換前の座標を教師データとして教師あり学習を行います。  

今回は、変換後の座標のうち訓練データにないような座標について、  
どのように逆変換されるのかが気になるので汎化性能を高めるためにDropoutを入れました。  

コードは次の通りです。  
<script src="https://gist.github.com/zaburo-ch/591fd26eda1236a1721f5be5eb06ce6a.js"></script>  

t-SNEの結果がこんな感じで、  
![tsne_result.png](/images/tsne-decode-img01.png)  

適当に座標を指定して逆変換した結果がこれ  
![test_result.png](/images/tsne-decode-img02.png)  

かなり綺麗に逆変換できました。  
deconvolutionを使えばもっとうまく逆変換できるかもしれませんが、  
MNISTの結果としてはこれで十分だと思います。  
なんとかしてこの方針で画像生成とかできないのかなーと思っているのですが、  
まずはグレースケールでない画像をうまく変換できるようにt-SNE側を工夫しなければいけない気がします。  
