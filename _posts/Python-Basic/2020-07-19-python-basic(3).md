---
layout: post
title: Python 시간함수
subtitle: < time, datetime >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Basic]
tags: [python, basic, 기초, 시간함수, time, datetime]
---

파이썬 시간함수 정리
    - time
    - datetime
    - timedelta

<br>
------

#### 파이썬 시간함수
파이썬에서 날짜와 시간은 몇 가지 다른 데이터 유형 및 함수와 연관될 수 있다.

##### 시간을 나타내는데 사용되는 유형
- 유닉스 시간 기점 타임스탬프(time 모듈에서 사용)는 UTC기준 1970년 1월 1일 자정으로부터 경과된 초수를 뜻하는 부동소수점 또는 정수값
- datetime 객체(datetime 모듈)
    - year, month, day, hour, minute, second 속성에 저장된 정수값을 가짐
- timedelta 객체(datetime 모듈)
    - 특정한 시각이 아닌 지속시간을 나타냄

<br>

##### 시간함수와 매개변수 및 돌려받는 값 정리
- time.time()
    - 현재 시각 시간 기점 타임스탬프의 부동소수점 값을 알려줌
- time.sleep(seconds)
    - seconds 매개변수로 지정된 초만큼 프로그램을 일시정지 시킴
- datetime.datetime(year, month, day, hour, minute, second)
    - 매개변수로 지정된 시각에 해당되는 datetime 객체를 돌려준다.
    - 만약, hour, minute, second이 지정되지 않았으면 기본값은 0
- datetime.datetime.now()
    - 현재시각의 datetime 객체를 돌려줌
- datetime.datetime.fromtimestamp(epoch)
    - epoch 타임스탬프 매개변수로 표현되는 시각의 datetime을 돌려줌
- datetime.timedelta(weeks, days, hours, minutes, seconds, milliseconds, microseconds)
    - 시간 기간을 나타내는 timedelta 객체를 돌려줌.
    - 함수의 키워드 인수는 모두 선택사항이며 년 또는 월은 포함되어 있지 않음
- timedelta의 total_seconds()
    - timedelta 객체가 나타내는 초 단위 시간을 돌려줌.
- strftime(format)
    - 서식 문자열을 기반으로 사용자 정의형식으로 datetime 객체를 표시하는 문자열을 돌려줌
    - **strftime() 지시자** 참고
- datetime.datetime.strftime(time_string, format)
    - time_string으로 지정된 시각에 대한 datetime 객체를 돌려줌.
    - format 문자열 매개변수를 사용하여 구문 분석을 함.
    - **strftime() 지시자** 참고
    
<br>

#### strftime() 지시자
- %Y : 세기를 포함한 연도, (ex. '2020')
- %y : 세기를 포함하지 않은 연도, '00'부터 '99'까지(ex. 1970년부터 2069년까지)
- %m : 십진수로 표현한 월. '01'부터 '12'까지
- %B : 완전한 영어식 월 이름. (ex. 'November) 
- %b : 약식으로 표기한 영어식 월이름 (ex.Nov)
- %d : 월 안의 일자. '01'부터 '31'까지
- %j : 1년 안의 일자. '001'부터 '366'까지
- %w : 요일. '0'(일요일)부터 '6'(토요일)까지
- %A : 완전한 영어식 요일 이름. (ex. 'Monday')
- %a : 약식으로 표기한 영어식 요일이름 (ex. 'Mon')
- %H : 시(24시간 방식), '00'부터 '23'까지
- %l : 시(12시간 방식), '01'부터 '12'까지
- %M : 분. '00'부터 '59'까지
- %S : 초. '00'부터 '59'까지
- %p : 'AM'(오전) 또는 'PM'(오후)
- %% : '%'글자
