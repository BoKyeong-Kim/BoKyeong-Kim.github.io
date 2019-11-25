---
layout: post
title: github.io 구글 검색 엔진
feature-img: "assets/img/github-logo(1).png"
categories : [Dev/github]
tags: [github.io, gitblog, jekyll, Google Search Console]
---

구글 검색 엔진에 게시물 등록하기!


몰랐었는데 구글에서 검색하려면 검색엔진에 게시물을 등록해야한다!<br>
그래서 등록 과정을 포스팅하려고한다.


### 1. 구글 웹마스터도구 등록
우선 구글에 로그인을 한 뒤, [google search console](https://search.google.com/search-console/about?hl=ko)에 접속하여 시작하기를 누른다.

<br>

### 2. 소유권 확인
아래의 화면처럼 왼쪽 상단의 속성추가를 클릭한다.<br>


![size]({{ site.baseurl }}/assets/img/attribute_add.png)



속성 유형 선택이 나타나면 **URL 접두어** 방식에서 내 사이트의 URL을 입력하고 계속 버튼을 클릭한다.  
<br>

![size]({{ site.baseurl }}/assets/img/select_att.png)



소유권 확인 창이 화면에 출력되는데 화살표 옆에 google로 시작하는 html파일을 다운로드 한 뒤, 깃블로그 폴더에서 최상위에 저장한다.

<br>

![size]({{ site.baseurl }}/assets/img/download_att.png)

그리고 깃허브에 push 해준다!
```
git add *
git commit -m '커밋 메시지'
git push origin master
```

<br>

### 3. Sitemap.xml 
깃블로그 폴더 최상위에 sitemap.xml이름의 파일을 새로 만든 후 아래의 코드를 붙여넣는다.

![size_main]({{ site.baseurl }}/assets/img/sitemaps_code.png)


그리고 깃허브에 push 해준다!
```
git add *
git commit -m '커밋 메시지'
git push origin master
```



깃블로그 주소/sitemap.xml 로 접속했을 때 아래와 같은 화면이 나오면 정상적으로 sitemap이 등록된 것이다!


![size_main]({{ site.baseurl }}/assets/img/sitemaps_xml.png)

<br>

### 4. Sitemap 등록하기
왼쪽 상단에 메뉴를 클릭하면 아래와 같은 화면을 확인할 수 있다. **Sitemaps**를 클릭한다.
![size]({{ site.baseurl }}/assets/img/search_menu.png)


새 사이트맵 추가에 밑줄 부분에 sitemap.xml을 작성해서 **제출** 클릭


왼쪽 상단에 메뉴를 클릭하면 아래와 같은 화면을 확인할 수 있다. **Sitemaps**를 클릭한다.


그럼 아래와 같은 화면이 표시된다.

<br>
![size_main]({{ site.baseurl }}/assets/img/sitemaps.png)

<br>

### 5.robots.txt
**robots.txt** 파일에 **sitemap.xml** 파일의 위치를 등록해 두면 검색엔진의 크롤러들이 홈페이지를 크롤링하는데에 도움을 준다고 한다.<br>
![size]({{ site.baseurl }}/assets/img/robots.png)

<br>

<b>구글 검색엔진 등록 끝!</b>

