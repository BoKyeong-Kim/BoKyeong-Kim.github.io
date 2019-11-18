---
layout: post
title: github.io 개인 블로그 만들기(1)
feature-img: "assets/img/github-logo(1).png"
subtitle: < jekyll >
categories : [Dev/github]
tags: [github.io, gitblog, jekyll]
---

노트북을 맥으로 바꾸고 jekyll을 설치하는게 편해졌다. 
그래서 이용해서 블로그를 계속해서 써볼까하는 생각만하다가 실행에 옮기기로 했다! 




## github.io 블로그 만들기
----------------
### Jekyll 설치하기

* 터미널에서 RubyGems를 사용하여 jekyll을 설치한다.

```
sudo gem install jekyll
```


* blog 폴더를 만든다.
```
(base) ➜  ~ mkdir blog
```


* blog 폴더로 이동
```
(base) ➜  ~ cd blog
```


* 현재 blog 위치에 아래의 명령어를 입력한다.

```
(base) ➜  blog jekyll new bokyeong-kim.github.io
(base) ➜  blog jekyll new [github 사용자명].github.io

Running bundle install in /Users/gimbogyeong/blog/bokyeong-kim.github.io... 
```


* blog위치에 new로 생성한 디렉터리가 존재한다.
* 여기서 주의할 점 **bokyeong-kim.github.io** 디렉터리로 현재 위치를 옮겨줘야한다.

```
(base) ➜  blog cd bokyeong-kim.github.io 
(base) ➜  bokyeong-kim.github.io jekyll serve
Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop.
```


* **http://127.0.0.1:4000/** 에 접속하면 Jekyll 기본테마의 블로그가 나타난다.





-----------------
### theme 적용하기

(사실 깃블로그 테마때문에 계속 엎고 다시 적용하고를 반복했다.
한번에 잘 선택해서 진행하자!)


[jekyllthemes](http://jekyllthemes.org/) 홈페이지에 접속하여 사용하고 싶은 테마를 선택해서 다운받는다.


심플한 테마 찾다가 발견!
내가 적용한 테마: 
![theme_select]({{ site.baseurl }}/assets/img/theme_select.png)


github로 들어가면 **404 There isn't a GitHub Pages site here.**라는 페이지가 떠서
직접 압축파일을 다운받아서 잘 변경하여 사용중이다.


위와 같은 위치에다가 그대로 합쳐주면 된다!








