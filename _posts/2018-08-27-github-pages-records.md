---
title: Github-Pages筆記(1)
layout: post
tagline: 透過jekyll簡單架設部落格
tags: jekyll github-pages blog lanyon
---
## 1. Introduce

>Github-Pages提供非常簡便的方式即可架設網站(靜態網站)，而參考過許多教學以後，在這裡稍微整理記錄一下步驟及遇到的問題。

## 2. Environment

>OS: Windows 10 x64

## 3. Steps

>a. 前往[https://github.com/poole/lanyon](https://github.com/poole/lanyon){:target"_blank"}並fork
![fork-lanyon]({{ site.url }}/assets/img/fork-lanyon.jpg)

>b. 至branch刪除gh-pages
![del-gh-pages]({{ site.url }}/assets/img/del-gh-pages.jpg)

>c. clone專案至電腦(當然你可以先改專案名稱)

>d. 打開_config.yml並註解掉"relative_permalinks: true"這行
![comment-out-permalinks]({{ site.url }}/assets/img/comment-out-permalinks.jpg)

>e. 新增"paginate: cnt"在config內(cnt為一次最多顯示幾篇文章，依個人喜好)
![add-paginate]({{ site.url }}/assets/img/add-paginate.jpg)
***加上這行之後新增文章才會在首頁顯示***

>f. config其他部分隨個人喜好更改

>g. push commit

>h. 至專案的Setting檢查Github pages那裡Source是否為master branch，成功的話應該會顯示如圖
![github-pages-setting]({{ site.url }}/assets/img/github-pages-setting.jpg)
此時網站就架好囉~