---
title: For The King 學識商店全開
layout: post
tagline: 作弊囉~
tags: For-The-King cheat hack Reflector Reflexil
---
## 前言
我很討厭浪費時間在做無意義的事情。  
For the king這款遊戲很好玩，但那個學識商店實在血尿...  
前期沒學識點數腳色就不夠OP，對新手來說通關是天方夜譚R，與其用各種方法刷學識點數催眠自己好像是自己農的一樣，那倒不如直接作弊改比較快是吧？
  
## 思路
最一開始，直覺的作法當然就Cheat Engine開下去啦，不過FTK對學識點數有做簡單的加密(貌似對經驗、金錢、血量等等沒有加密，不過改那個我沒興趣)，又不可能手動弄一堆學識點數來測位址的情況下，CE Out。  
  
接下來，稍微搜尋一下，在對岸百度論壇發現有人提到，這種Unity的遊戲貌似透過修改Assembly-CSharp.dll就可以快速達成。  
(這邊不得不發個牢騷，對岸在破解這方面資訊真的很多，台灣人貌似把作弊這檔事當作罪大惡極一樣XDD實在不怎麼流行)  
有了這個線索，就開始吧！  
  
## 如何做？
準備的東西有.Net Reflector及Reflexil  
顧名思義.Net Reflector可以反編譯.Net寫的各種軟體，當然如果有加殼加密混淆等就要先處理了。不過根據網路的說明，Unity加殼貌似不太切實際，加密跟混淆也不常見，因此通常是可以修改的。  
  
.Net Reflector開啟後，先至工具(Tools)->插件(Addins)將Reflexil加入  
![reflector-addin-tab]({{ site.baseurl }}/assets/img/reflector-addin-tab.jpg)  
![reflector-addin-window]({{ site.baseurl }}/assets/img/reflector-addin-window.jpg)  
  
之後將FTK的Assembly-CSharp.dll拖進去.Net Reflector  
Assembly-CSharp.dll位在 (你安裝的磁碟槽):\Steam\steamapps\common\For The King\FTK_Data\Managed裡面  
![assembly-csharp-into-reflector]({{ site.baseurl }}/assets/img/assembly-csharp-into-reflector.jpg)  
  
在上面搜尋"lore"，並找到這次要修改的關鍵函數Boolean IsUnlock(FTK_loreItem)
![reflector-search-lore]({{ site.baseurl }}/assets/img/reflector-search-lore.jpg)  

仔細看此函數，只有一種情況會導致return false  
他判斷FTK_loreItem的某StatisticID小於0的時候，表示此項目尚未解鎖  
那思路就很簡單啦，看是要讓不等號左邊改成正整數或者改右邊使不等式恆為真  
  
**修改**  
首先先開啟Reflexil插件  
![reflexil-open]({{ site.baseurl }}/assets/img/reflexil-open.jpg)  

打開就會看到下面的MSIL指令  
由於沒啥看過這種指令，我選擇破壞度比較小的修改方法，直接將不等式右邊的0改為-2147483648  
只需要動到一行指令即可使不等式恆為真  

此函數的pseudocode  
![ftk-loreitem-code]({{ site.baseurl }}/assets/img/ftk-loreitem-code.jpg)  

相對於最後一行return (playerStatistic?.Value > 0)的MSIL指令  
![ftk-modify-loreitem-before]({{ site.baseurl }}/assets/img/ftk-modify-loreitem-before.jpg)  
我們修改的是39行，原本ldc.i4.0表示push 0至stack中，現在改成ldc.i4 -2147483648，也就是push最小Int32進stack中。  
修改如圖  
![ftk-modify-msil]({{ site.baseurl }}/assets/img/ftk-modify-msil.jpg)  

修改之後的pseudocode  
![ftk-modify-loreitem-after]({{ site.baseurl }}/assets/img/ftk-modify-loreitem-after.jpg)  
之後再重新打包就好啦  
![ftk-loreitem-repack]({{ site.baseurl }}/assets/img/ftk-loreitem-repack.jpg)  

完成圖  
![ftk-loreitem-finish]({{ site.baseurl }}/assets/img/ftk-loreitem-finish.jpg)  