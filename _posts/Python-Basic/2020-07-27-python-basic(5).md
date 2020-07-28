---
layout: post
title: Python IMAP - 이메일 가져오기
subtitle: < time, datetime >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Basic]
tags: [python, basic, 기초, IMAP, email, 이메일가져오기]
---

- IMAP(Internet Message Access Protocol)
    - imapclient : 복잡한 형식의 IMAP 서버에서 이메일 다운로드
    - pyzmail : 이메일 메세지를 구분 분석 작업


----

<br>

#### IMAP(Internet Message Access Protocol)
SMTP가 이메일을 보내기 위한 프로토콜인 것처럼, 인터넷 메세지 액세스 프로토콜(IMAP)은 이메일 주소로 전송된 이메일을 가져오기 위해 이메일 서비스 업체의 서버와 통신하는 방법을 지정한다.
- 파이썬은 imaplib 모듈을 제공하고 있지만 다른 곳에서 만든 imapclient 모듈이 사용하기에는 더 쉽다고한다.
    - imapclient 모듈은 다소 복잡한 형식의 IMAP 서버에서 이메일을 다운로드한다.
    - 대부분의 경우, 복잡한 형식을 간단한 문자열 값으로 변환하고 싶을 것이다.
    - pyzmail 모듈은 이러한 이메일 메세지를 구분 분석하는 작업을 해준다.

모듈설치
```
pip install imapclient
pip install pyzmail
```

<br>

#### IMAP 서버 연결
- SMTP 서버에 연결하고 이메일을 보내기 위해서는 SMTP 객체를 필요로 하는것처럼, IMAP 서버에 연결하고 이메일을 받으려면 IMAPClient 개체가 필요하다.
- 이메일 서비스 업체의 IMAP 서버 도메인 이름이 필요하다.
    - 지메일(Gmail) : imap.gmail.com
    - 아웃룩(outlook) : imap-mail.outlook.com
- IMAP 서버의 도메인 이름을 알았다면 imapclient.IMAPClient() 함수를 호출해서 개체를 만든다.
- 대부분의 이메일 서비스 업체는 SSL 암호화를 필요로 하기 때문에 ssl=True 키워드 매개변수를 전달한다.

```python
import imapClient
imap_obj = imapclient.IMAPClient('imap.gmail.com', ssl=Ture)
```

<br>

#### IMAP 서버 로그인
- IMAPClient 개체를 만들었다면 login() 메소드를 호출하면서 사용자이름(보통 이메일 주소) 및 암호를 문자열로 전달한다.

```python
imap_obj.login('email_address@gmail.com', 'MY_SECRET_PASSWORD')
'email_address@example.com boka poki authenticated (Success)'
```

코드에 비밀번호를 적지않도록 주의 !

- IMAP 서버가 전달한 사용자 이메일/암호 조합을 거부한다면 파이썬은 imaplib.error 예외를 일으킨다.
    - 지메일 계정이라면 응용프로그램 비밀번호를 사용해야 할 수도 있다.
    - [만약 이메일 발송 코드를 작성해서 실행했을 때 오류가 발생하면 링크 참조](https://bokyeong-kim.github.io/python/basic/2020/07/26/python-basic(4).html)

<br>


#### 이메일 검색하기
- 로그인 후, 이메일을 가져오기 위해서 두 단계를 거쳐야한다.
    - 1) 검색할 폴더 선택
    - 2) IMAPClient 객체의 search() 메소드 호출 : IMAP 검색어 문자열 전달


<br>

#### 1)폴더 선택하기
- 거의 모든 계정은 기본적으로 받은 편지함 폴더를 가지고 있지만, IMAPClient 객체의 list_folders() 메소드를 불러서 폴더의 목록을 얻을 수도 있다.
    - 반환 : 튜플의 리스트
    - 각 튜플은 하나의 폴더에 대한 정보를 포함하고 있다.

```python
import pprint
pprint.pprint(imap_obj.list_folders())
>> [(('\\HasNoChildren',), '/', 'Drafts'),
    (('\\HasNoChildren',), '/', 'Filler'),
    (('\\HasNoChildren',), '/', 'INBOX'),
    (('\\HasNoChildren',), '/', 'Sent'),
    --snip--
    (('\\HasNoChildren', '\\Flagged'), '/', 'Starred'),
    (('\\HasNoChildren', '\\Trash'), '/', 'Trash')]
```

- 지메일 계정이 있다면 출력은 위와 비슷할 것이다.
    - 지메일은 폴더를 라벨이라고 부르지만 폴더와 같은 방식으로 사용된다.
- 각 튜플에는 세가지 값이 있다.
    - ex. (('\\HasNoChildren',), '/', 'INBOX')
        - 1) 폴더의 플래그 튜플
        - 2) 이름 문자열에서 상위폴더와 하우ㅏ폴더를 구분하는데 쓰이는 문자
        - 3) 폴더 전체의 이름
- 검색할 폴더를 선택하려면 IMAPClient 개체의 select_folders()메소드에 문자열로 폴더의 이름을 전달한다.
```python
imap_obj.select_folders('INBOX', readonly=True)
```
- 선택한 폴더가 없는 경우 파이썬은 imaplib.error를 일으킨다. 
- readonly = True 키워드 매개변수는 그 이후로 다른 메소드를 호출할 때 이 폴더 안에 있는 이메일을 실수로 변경하거나 지우는 사고를 막아준다.(이메일을 지울목적이 아니라면 readonly=True는 필수)





