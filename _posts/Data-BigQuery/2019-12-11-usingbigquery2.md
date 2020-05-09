---
layout: post
title: 빅쿼리(BigQuery) 다루기(URL)
subtitle: < URL >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Data/BigQuery]
tags: [BigQuery,google,GCP, SQL]
---

이번 포스팅은 **빅쿼리 다루기(URL)**편!



<br>
**데이터 분석을 위한 SQL 레시피** 책을 참고하여 작성
<br>

#### URL에서 요소 추출하기
URL처리는 웹서비스 로그분석에서 많이 쓰이는 기술이다.
분석현장에서는 최소한의 요건으로 레퍼러와 페이지 URL을 저장해두는 경우가 있다고한다. 그리고 이후에 저장한 URL로 요소들을 추출한다.
<br>
위에서 했던 방식으로 스키마를 지정해준뒤, 아래와 같이 데이터를 INSERT해준다.
<br>

![size_main]({{ site.baseurl }}/assets/img/insert_data.png)
<br>


<br>

##### 레퍼러로 어떤 웹페이지 거쳐왔는지 판별

어떤 웹페이지를 거쳐 넘어왔는지 판별할 때는 레퍼러를 집계한다. 페이지 단위로 집계하면 복잡해지므로 호스트 단위로 집계하는 것이 일반적

빅쿼리에서는 URL을 다루는 함수가 있다.(구현되지 않은 미들웨어에서는 정규표현식을 사용해서 호스트의 이름 패턴을 추출해야한다.)
<br>

아래의 사진처럼 FORMAT을 지정해주고 NET.HOST 함수를 사용하여 표준URL을 추출할 수 있다.

<br>

![size_main]({{ site.baseurl }}/assets/img/format_data.png)

<br>

자세한 사항은[BigQuery 표현식](https://cloud.google.com/bigquery/docs/reference/standard-sql/functions-and-operators?hl=ko&_ga=2.29653436.-285742386.1564620370) 참고!

<br>

##### URL에서 경로와 요청 매개변수 값 추출
URL을 로그 데이터로 저장해두었으면 URL경로를 가공해서 리포트를 만들 수 있다.

아래의 코드는 URL경로와 GET 요청 매개변수에 있는 특정 키를 추출하는 코드이다. 
**REGEXP_EXTRACT**함수를 사용하여 지정한 값에서 정규표현식과 일치하는 첫 번째 하위 문자열을 반환한다.(일치하지않으면 NULL값 반환)
<br>


![size_main]({{ site.baseurl }}/assets/img/REGEXP_EXTRACT.png)
<br>

 BigQuery는 re2 라이브러리를 사용하여 정규 표현식을 지원한다. 더 자세한 정규 표현식 구문은
[Syntax](https://github.com/google/re2/wiki/Syntax) 참고!

<br>

정규표현식으로 URL 전처리하기 끝