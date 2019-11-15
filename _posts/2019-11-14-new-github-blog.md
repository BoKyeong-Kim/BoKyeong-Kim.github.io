---
layout: post
title: create github.io
tags: [github.io, gitblog]
---

## github.io 블로그 만들기

### Jekyll 설치하기

- 터미널에서 RubyGems를 사용하여 jekyll을 설치한다.
```
sudo gem install jekyll
```

- blog 폴더를 만든다.
```
(base) ➜  ~ mkdir blog
```

- blog 폴더로 이동
```
(base) ➜  ~ cd blog
```

- 현재 blog 위치에 아래의 명령어를 입력한다.
```
(base) ➜  blog jekyll new bokyeong-kim.github.io
(base) ➜  blog jekyll new [github 사용자명].github.io

Running bundle install in /Users/gimbogyeong/blog/bokyeong-kim.github.io... 
.
.
.
``` 

- blog위치에 new로 생성한 디렉터리가 존재한다.
- 여기서 주의할 점 `bokyeong-kim.github.io` 디렉터리로 현재 위치를 옮겨줘야한다.

```
(base) ➜  blog cd bokyeong-kim.github.io 
(base) ➜  bokyeong-kim.github.io jekyll serve               
.
.
.
Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop.
.
.
.
```

- `http://127.0.0.1:4000/` 에 접속하면 Jekyll 기본테마의 블로그가 나타난다.

(사실 깃블로그 테마때문에 계속 엎고 다시 적용하고를 반복했다.
한번에 잘 선택해서 진행하자!)
