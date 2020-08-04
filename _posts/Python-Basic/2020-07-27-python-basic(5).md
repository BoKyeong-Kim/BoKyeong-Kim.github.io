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
import imapclient
imap_obj = imapclient.IMAPClient('imap.gmail.com', ssl=True)
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
- 검색할 폴더를 선택하려면 IMAPClient 개체의 select_folder()메소드에 문자열로 폴더의 이름을 전달한다.
```python
imap_obj.select_folder('INBOX', readonly=True)
```
- 선택한 폴더가 없는 경우 파이썬은 imaplib.error를 일으킨다. 
- readonly = True 키워드 매개변수는 그 이후로 다른 메소드를 호출할 때 이 폴더 안에 있는 이메일을 실수로 변경하거나 지우는 사고를 막아준다.(이메일을 지울목적이 아니라면 readonly=True는 필수)

<br>

#### 검색 수행하기
- 폴더 선택하면 IMAPClient 객체의 search() 메소드로 이메일을 검색할 수 있다.
- 검색키는 다양하다.
    - 'ALL' : 폴더의 모든 메세지를 돌려줌
    - 'BEFORE data.', 'ON data', 'SINCE date' : 각각 IMAP 서버가 주어진 날짜 이전, 바로 그 날짜, 또는 그 날짜 이후에 받은 메세지를 돌려줌
    - 'SUBJECT string', 'BODY string', 'TEXT string' : 주어진 문자열이 각각 제목 또는 본문에서 발견되는 메세지를 돌려줌. 문자열에 빈칸이 있을 때에는 겹따옴표로 묶어서 'TEXT "search with spaces"'와 같이 지정해야한다.
- 일부 IMAP 서버는 플래그 및 검색 키를 처리하는 방법을 약간 다르게 구현할 수도 있다는 점 유의
    - search() 메소드에 리스트를 전달함으로써 IMAP 검색 키 문자열을 여러 개 전달할 수도 있다.
    - 돌려받는 메세지는 전달된 모든 검색 키와 일치하는 메세지이다. 검색키 중 어느것이든 일치하는 메세지를 돌려받으려면 OR 검색 키를 사용해야한다.
    - ex) imap_obj.search(['ALL']) : 현재 선택된 폴더 안에 있는 모든 메세지를 돌려줌.   
    - ex) imap_obj.search(['ON 05-May-2020']) : 2020년 05월 05일에 발송된 모든 메세지를 돌려줌.
- search() 메소드는 이메일 자체를 돌려주는 것이 아니라, 각 이메일의 유일한 ID 값(Unique ID,UID)를 돌려준다. 
    - 이메일 내용을 가져오려면 fetch() 메소드에 UID 값을 전달하면 된다.

```python
UIDs = imap_obj.search(['FROM', 'no-reply@accounts.google.com'])
UIDs
>> [6, 7, 9, 11, 14, 18, 34, 45, 59, 65, 92, 95, 96, 218, 219, 220, 225, 232, 235, 302, 303, 304, 308, 405, 435, 439, 474, 475, 480, 517, 539, 633, 636, 711, 712, 777, 836, 841, 851, 904, 908, 939, 968, 1037, 1077, 1080, 1088, 1113, 1267, 1300, 1338, 1492, 1560, 1567, 1573, 1770, 1771, 1922, 1923, 1933, 1960]
```
- no-reply@accounts.google.com로부터 받은 메시지가 UIDs에 저장된다.
- 각각의 UID는 특정 이메일에 고유하다.

<br>

#### 크기 제한
- 검색 조건과 일치하는 이메일 메시지가 많을 경우, 파이썬은 imaplib.error: got more than 10000 bytes와 같은 예외를 일으킬 수 있다.
- 위의 예외 경우 IMAP 서버와 연결을 끊었다가 다시 연결을 시도해야한다.
    - 이러한 제한은 파이썬 프로그램이 많은 메모리를 잡아먹는 일을 막기위해서 설정되어있다.
- 10,000 바이트 제한을 10,000,000 바이트로 바꿀 수 있다.

```python
import imaplib
imaplib._MAXLINE = 10000000
```

<br>

#### 읽은 메일로 표시하기
- UID 리스트를 받았다면 IMAPClient 객체의 fetch() 메소드를 호출해서 실제 이메일 내용을 가져올 수 있다.
- UID 리스트는 fetch()의 첫 번째 매개변수가 되고 두번째 매개변수는 ['BODY[]'] 리스트 이다. 이는 fetch()에게 지정한 UID 리스트에 해당하는 이메일의 모든 본문 내용을 가져오라고 지시하는 의미이다.

```python
import pprint
raw_msg = imap_obj.fetch(UIDs, ['BODY[]'])
pprint.pprint(raw_msg)
>> defaultdict(<class 'dict'>,
            {6: {b'BODY[]': b'Delivered-To: bokyeong3659@gmail.com\r\nReceiv'
                            b'ed: by 10.181.80 with SMTP id c16csp164y'
                            b'wk;\r\n        Mon, 26 Jun 2017 05:46:07 -0700'
                            b' (PDT)\r\nX-Received: by 10.37.73 with SMT'
                            b'P id c9mr252ybj.144.1498467372;\r\n      '
                            ...
                            b'tml>\r\n--94eb2c0998ef0552dc5516--\r\n',
                 b'SEQ': 6}})
```
- 출력값은 중첩된 딕셔너리 값으로, 사전의 키 값은 메세지의 UID이다.
- 각 메세지는 두 개의 키, 'BODY[]' 및 'SEQ'를 가진 사전에 저장된다.
- 'BODY[]' 키는 이메일의 실제 본문에 대응된다. 
    - 메세지의 내용은 IMAP 서버가 읽어들이기 위한 목적으로 설계된 RFC 822라는 형식이라 한다.
    - pyzmail 모듈을 사용하면 해당 메세지를 볼 수 있다.

<br>

#### pyzmail 사용
- pyzmail 모듈은 원시 메세지를 분석하고 결과를 PyzMessage 객체로 돌려주며, 이 객체를 사용하면 제목, 본문, 발신 및 수신 주소 등을 알 수 있다.

```python
import pyzmail
msg = pyzmail.Pyzmessage.factory(raw_msg[6]['BODY[]'])
```

- pyzmail 모듈을 가져온 후, pyzmail.Pyzmessage.factory() 함수를 호출하며 원시 메세지의 'BODY[]'부분을 전달하여 해당 이메일의 Pyzmessage 객체를 만든다.

```python
>>> msg.get_subject()
'Hello!'
>>> msg.get_addresses('from')
[('','no-reply@accounts.google.com')]
>>> msg.get_addresses('to')
[('bokyeong3659@gmail.com')]
>>> msg.get_addresses('cc')
[]
>>> msg.get_addresses('bcc')
[]
```

- get_addresses() 함수의 매개변수는 from(발신), to(수신), cc(참조), bcc(숨은 참조)이다. 
- 요청된 필드에 주소가 없으면 get_addresses()는 빈 리스트를 돌려준다.

<br>

#### 본문 가져오기
- 이메일은 일반 텍스트, HTML, 또는 양쪽 모두에 걸친 형식으로 보낼 수 있다.
- 일반 텍스트 이메일은 텍스트만 포함하는 반면 HTML 이메일은 색상, 글꼴, 이미지 등을 가질 수 있기 때문에 이메일 메시지를 웹페이지처럼 보이게 한다.
    - 이메일이 일반 텍스트라면 Pyzmessage 객체의 html_part 속성은 None으로 설정된다.
    - 이메일이 HTML으로만 되어있다면 Pyzmessage 객체의 text_part 속성은 None으로 설정된다.

```python
msg.text_part != None
>> True
msg.text_part.get_payload().decode(message.text_part.charset)
>> 'send to PyZmessage!\r\n\r\n-Al\r\n'
msg.html_part != None
>> True
msg.html_part.get_payload().decode(message.html_part.charset)
>> '<div dir="ltr"><div>send to PyZmessage!<br><br></div>-Al
   <br></div>\r\n'
```

- 위 예제의 이메일은 일반 텍스트 및 HTML을 모두 가지고 있으므로 text_part, html_part 둘 다 None이 아니다.
- 메시지의 text_part에 get_payload()를 호출하고 돌려받은 바이트 값에 decode() 메소드를 호출하면 이메일의 텍스트 버전에 대한 문자열을 돌려받는다.


