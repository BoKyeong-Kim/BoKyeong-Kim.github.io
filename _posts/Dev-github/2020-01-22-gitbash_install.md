---
layout: post
title: git 설치하기
feature-img: "assets/img/github-logo(1).png"
subtitle: < git >
categories : [Dev/github]
tags: [git, github, install, git설치]
---

**git bash 설치하기!**

<br>

1.git 홈페이지에 접속하여 [다운로드](https://git-scm.com/downloads)를 클릭


![size_main]({{ site.baseurl }}/assets/img/gitdown.PNG)


- 본인에게 맞는 OS를 선택하여 설치한다.

<br>

2.Next!

![size_main]({{ site.baseurl }}/assets/img/gitsetup.png)

<br>

3.설치할 항목들을 선택하고 Next! (저는 default로 진행)

![size_main]({{ site.baseurl }}/assets/img/gitsetup2.png)

<br>

4.계속 Next를 누르다보면 아래와 같은 화면을 볼 수 있는데, Git의 커맨드를 지정하는 부분이다. recommand를 선택하고 Next! 

![size_main]({{ site.baseurl }}/assets/img/gitsetup3.png) 

<br>

5.
- Use the OpenSSL library : OpenSSL 라이브러리를 사용
- Use the native Windows Secure Channel library : Windows 인증서 라이브러리를 사용

![size_main]({{ site.baseurl }}/assets/img/gitsetup4.png)

<br>

6.next를 눌러 설치를 완료한 후 git bash에 접속한다.

<br>

7.**git init** 


![size_main]({{ site.baseurl }}/assets/img/gitbash.png)

<br>

git 초기화 (버전관리 시작)<br>
git 명령어는 해당 프로젝트 디렉토리에서 입력해야한다. <bt>
(본인 같은 경우, 모든 파일이 올라가지 않도록 새롭게 mkdir로 github라는 폴더를 만들어준 후 진행하였다.)

init을 한번 더해서 Reinitalized라고 뜨는 것,,, <br>

<br>

8.**git status**
현재 git의 상태를 확인한다. 



처음에 접속하고 이름과 이메일을 작성한다.
```git 
git config --global user.name '이름'

git config --globall user.email '이메일'
```

<br>

9.기존에 깃에 올려두었던 파일을 pull한다.
깃허브 레파지토리에 들어가서 아래의 화면처럼 우측에 **Clone or download**를 클릭하여 주소 옆에 노트와화살표 아이콘을 클릭하여 주소를 복사한다.

![size_main]({{ site.baseurl }}/assets/img/gitpull.PNG)

<br>

10.그리고 아래와 같이 git pull을 작성한 뒤 뒤에 복사한 주소를 붙여넣으면 깃허브에 올라가있던 것들을 다운받을 수 있다. 

![size_main]({{ site.baseurl }}/assets/img/gitbash2.PNG)


<br> 

위와 같은 방식으로 git bash를 활용하여 명령어를 입력해서 깃허브에 push하면서 사용하면 된다!

<br> 

포스팅 끝!!!! 