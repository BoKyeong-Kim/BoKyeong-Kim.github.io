---
layout: post
title: github.io 개인 블로그 만들기(2)
feature-img: "assets/img/github-logo.png"
tags: [github.io, gitblog, jekyll]
---

앞서 jekyll을 이용하여 테마를 적용하였다.

이제 github에 업로드하여 github.io도메인을 가진 홈페이지를 만들어보려고한다.

상단 이미지 출처 : https://www.zdnet.com/article/github-sued-for-aiding-hacking-in-capital-one-breach/



# github.io 생성하기


## github repository 생성 

1) github에 접속하여 **Repositories**에 들어간다.

2) 오른쪽 상단에 **New** 버튼을 클릭

3) 아래와 같은 화면이 표시되는데 **Repository name**에 **[github 사용자명].github.io**를 적은 뒤 아래에 **Create repository** 버튼 클릭

![create_repo]({{ site.baseurl }}/assets/img/create_repo.png)

4) 생성된 레파지토리를 확인할 수 있다. 



## github upload

1) 현재 위치를 bokyeong-kim.github.io 디렉터리에 둔다.

`git init` 으로 현재 디렉터리를 초기화 해준다.


2) 현재 깃의 상태를  `git status` 확인해준다. 


3) `git add *` 를 통해 업로드할 파일 전부(`*`)를 add 해준다.


4) `git commit -m '커밋 메세지'` 왜 업로드를 하는지에 대한 메세지를 적어 커밋해준다.


5) `git push origin master` 로 깃에 업로드 해주면 적용했던 테마의 코드가 github.io에 적용된다.


6) 검색창에 본인이 만들었던 [github 사용자명].github.io를 입력하여 접속하면 테마를 적용시킨 블로그가 나타난다.



끝! 




### (추가) 리모트 저장소 추가하려면

1) 레파지토리에 들어가면 오른쪽 상단에 **Clone or download** 버튼이 있는데 그걸 클릭해주면 아래와 같은 화면이 보일 것이다.


오른쪽에 노트와 화살표가 있는 아이콘을 클릭해서 URL을 복사한다.

![url_repo]({{ site.baseurl }}/assets/img/url_repo.png)








2) `git remote add 단축이름 복사한 URL` 명령을 실행하면 새로운 리모트가 추가된다.




