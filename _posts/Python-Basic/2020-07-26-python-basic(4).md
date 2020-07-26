---
layout: post
title: Python SMTP - 이메일 보내기
subtitle: < time, datetime >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Basic]
tags: [python, basic, 기초, smtp, email, 이메일보내기]
---

- SMTP(Simple Mail Transfer Protocol)
    - SMTP 서버 연결하기 : smtplib.SMTP() 
    - 이메일 서버에 hello 메세지 보내기 : ehlo()
    - SMTP 서버의 포트 연결 : starttls()
    - 이메일 보내기 : sendmail()



----

<br>

#### SMTP(Simple Mail Transfer Protocol)
: HTTP가 인터넷을 통해 웹 페이지를 전송하기 위해 컴퓨터가 사용하는 프로토콜인 것처럼 단순 메일 전송 프로토콜(SMTP)은 이메일을 전송할 때 사용되는 프로토콜이다.
- 이메일 메시지의 형식, 암호화 및 메일 서버 간에 전달과 방법, 그밖에 보내기 버튼 클릭 후 컴퓨터가 메일을 처리하는 방법을 정한다.
- 또다른 프로토콜인 IMAP는 이메일을 가져올 때 관여한다.

<br>

#### SMTP 서버 연결하기 : smtplib.SMTP()
- SMTP 서버의 도메인 이름은 보통 이메일 서비스 업체의 도메인 이름 앞에 smtp가 붙은 형태
    - 지메일(Gmail) : smtp.gmail.com
    - 아웃룩(outlook) : smtp-mail.outlook.com

- 사용하는 이메일 서비스 업체의 도메인 이름 및 포트정보를 찾았다면 smtplib.SMTP()를 호출하면서 문자열 매개변수로 도메인이름을 전달하고, 정수 매개변수로 포르를 전달하여 SMTP 개체를 만든다.

- Gmail로 연결하는 SMTP 객체
```python
smtp_obj = smtplib.SMTP('smtp.gmail.com', 587)
```

- 서버에 로그인하고 이메일을 보내는 메소드를 부르려면 이 SMTP 개체가 필요하다.
- smtplib.SMTP() 호출이 성공하지 못한경우 SMTP서버가 포트 587에 TLS를 지원하지 않기 때문일 수 있다. 
    - 위와같은 경우, smtplib.SMTP_SSL()함수와 포트 465를 사용하여 SMTP 개체를 만들어야한다.

<br>

#### ehlo(Extended Hello)
- SMTP개체를 얻고나면 ehlo() 메소드를 호출하여 SMTP 이메일 서버에 Hello 메세지를 보낸다.
- Hello 메세지는 SMTP에서 첫번째 단계이자 서버 연결을 설정하는 중요한 단계이다.

```python
smtp_obj.ehlo()
>> (250, b'mx.example.com at your service, [216.172.148.131]\nSIZE 35882577\
n8BITMIME\nSTARTTLS\nENHANCEDSTATUSCODES\nCHUNKING')
```
- 돌려받는 튜플의 첫번째 항목은 정수값 250 - SMTP에서 성공을 뜻하는 코드.

<br>

#### TLS 암호화
- SMTP 서버의 포트 587에 연결할 때(TLS 암호화 사용)에는 starttls() 메소드를 호출해야한다.
- 위 필수단계를 통해 연결을 암호화할 수 있다.
- 포트 465(SSL사용)에 연결할 때에는 이미 암호화가 설정되어있으므로 이 단계는 넘어가도된다.

```python
stmp_obj.starttls()
>> (220, b'2.0.0 Ready to start TLS')
```

- starttls()는 SMTP연결을 TLS모드로 설정한다. 돌려받은 값에 220은 서버가 준비되었다는 것을 뜻한다.

<br>

#### SMTP 서버에 로그인하기
- SMTP서버로 암호화된 연결을 설정하고 나면 login() 메소드를 호출하여 사용자이름(보통 이메일 주소) 및 이메일 비밀번호를 사용하여 로그인할 수 있다.

```python
smtpObj.login('email_address@gmail.com', 'MY_SECRET_PASSWORD')
>> (235, b'2.7.0 Accepted')
```
- Gmail에는 구글계정에 대한 추가 보안기능이 있으므로 허용을 미리 해주어야한다.
- 첫번째 매개변수로는 이메일 주소 문자열을, 두번째 매개변수로는 비밀번호 문자열을 전달한다.
- 235값을 돌려받는 것은 인증이 성공했다는 뜻이다.
- 잘못된 암호에 대해서는 **smtplib.SMTPAuthenticationError** 에러를 일으킨다.
- 소스코드 자체에 비밀번호를 작성하는 것은 위험한 방법이므로, sys.argv 또는 dotenv를 사용하여 비밀번호를 따로 입력해주거나 비공개 파일에 저장하는 방법을 사용하는 것이 좋다.


<br>

#### 이메일 보내기
- 이메일 서비스 업체의 SMTP 서버에 로그인하면 실제로 이메일을 보낼 수있는 sendmail() 메소드를 호출할 수 있다.

```python
smtp_obj.sendmail('email_address@gmail.com', 'recipient@gamil.com', 'Subject: So long.\nDear Alice, so long and thanks for all the fish. Sincerely, Bob'))
>> {}
```
- sendmail() 메소드는 3개의 매개변수를 필요로 한다.
    - 보내는 사람(발신 또는 from)의 이메일 주소 문자열
    - 받는 사람의 이메일 주소(수신 또는 to) 문자열일수도 있고, 받는 사람이 여러명이라면 리스트일 수 있다.
    - 이메일 본문 문자열
        - 이메일 본문 문자열의 시작은 'Subject: \n' 또는 이메일의 제목줄로 시작해야한다.
        - '\n' 줄바꿈 문자는 이메일의 본문에서 제목을 분리한다.
- sendmail()이 돌려주는 값은 사전유형. 사전안에는 이메일 전송에 실패한 수신자가 각각 키-값 쌍으로 들어있다. 
    - 사전이 비어있다면 모든 수신자에서 성공적으로 이메일을 발송했다는 뜻이다.

<br>

#### SMTP 서버 연결 끊기
- 이메일을 보내는 작업을 끝마쳤다면 quit() 메소드를 호출해야한다.
- 프로그램과 SMTP 서버의 연결을 끊는다.

```python
smtp_obj.quit()
>> (221, b'2.0.0 closing connection ko10sm23097611pbd.52 - gsmtp')
```

- 돌려받은 값에 있는 221은 세션이 종료되었다는 것을 뜻한다.


<br>

#### smtplib.SMTPAuthenticationError
- 이메일 발송 코드를 작성해서 실행했는데, 아래와 같은 오류가 발생하는 경우가 있다.

> smtplib.SMTPAuthenticationError: (535, b'5.7.8 Username and Password not accepted. Learn more at\n5.7.8  https://support.google.com/mail/?p=BadCredentials f72sm11666756pfa.66 - gsmtp')

- [보안 수준이 낮은 앱 허용
](https://myaccount.google.com/lesssecureapps)을 사용으로 체크해주어야한다.
- [IMAP 액세스 설정](https://support.google.com/mail/answer/7126229?hl=ko&visit_id=637313623975529006-3687967315&rd=2)
    - 1단계: IMAP이 켜져 있는지 확인 - 컴퓨터에서 Gmail을 엽니다.
    - 2단계: 오른쪽 상단에서 설정 설정 다음 모든 설정 보기를 클릭합니다.
    - 3단계: 전달 및 POP/IMAP 탭을 클릭합니다.
    - 4단계: 'IMAP 액세스' 섹션에서 IMAP 사용을 선택합니다.
    - 5단계: 변경사항 저장을 클릭합니다.