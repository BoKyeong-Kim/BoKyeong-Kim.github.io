---
layout: post
title: 빅쿼리(BigQuery) 다루기(CASE문)
subtitle: < Data upload >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Data/BigQuery]
tags: [BigQuery,google,GCP, SQL]
---

이번 포스팅은 **빅쿼리 다루기**편!



<br>
**데이터 분석을 위한 SQL 레시피** 책을 참고하여 작성
<br>

#### 빅쿼리에 데이터업로드하기
우선 빅쿼리 콘솔로 접속하여 새로운 데이터를 생성<br>
지정한 데이터에서 **테이블만들기**를 클릭한다.<br>

![size_main]({{ site.baseurl }}/assets/img/bigquerytable.png)

<br>

빈테이블로 지정하고 테이블 이름을 지정해주고 스키마를 정의해준다. 


빅쿼리에서는 컬럼의 이름과 유형을 지정해주면 되기 때문에 간단하다.

<br>


MySQL에서 스키마를 정의할 때는 아래와 같은 코드로 정의해줘야한다.
<br>
```mysql
CREATE TABLE mst_users(
    user_id        string,
    register_date   string,
    register_device integer
);
```
<br>
그리고 쿼리편집기로 넘어와서 데이터를 INSERT 해준다.<br>

![size_main]({{ site.baseurl }}/assets/img/bigquery_adddata.png)


여기서 주의할 점은 **경로 전체를 적어줘야한다**는 점이다. 콘솔화면에서 테이블 쿼리를 누르면 테이블의 경로가 자동으로 표시된다. 그냥 테이블 이름만 작성하면 빅쿼리에서는 오류를 발생시킨다


현재 테이블에 저장된 데이터는 아래와 같다.


![size]({{ site.baseurl }}/assets/img/result_adddata.png)


<br>
MySQL에서는 아래와 같은 코드로 추가가 가능하다.

```mysql
INSERT INTO mst_users
VALUES
    ('U001', '2016-08-26', 1)
    ('U002', '2016-08-26', 2),
    ('U003', '2016-08-27', 3),
;
```


<br>

#### 코드 값을 레이블로 변경

- 로그 데이터 또는 업무 데이터로 저장된 코드 값을 그대로 집계에 사용하면 리포트의 가독성이 낮아진다.<br>

코드 값을 레이블로 변경하는 것처럼 **특정 조건을 기반으로 값을 결정**할 때는 **CASE** 문을 사용
<br>

CASE 문은 CASE 뒤에 ‘WITH 조건식 THEN 조건을 만족할 때의 값을 나열하고 마지막을 END로 끝내는 형태'이다. 현재 테이블에 저장된 데이터는 아래의 화면과 같다. register_device의 숫자 값을 레이블을 지정해주어 데이터를 변환하려고 한다. 아래와 같이 코드를 작성해주면 지정해준 값에 따라 레이블 된 것을 확인할 수 있다.<br>


![size_main]({{ site.baseurl }}/assets/img/case_query.png)



> CASE문은 데이터변환에 가장 많이 사용되니까 익혀두는 것이 좋다.

<br>

CASE문을 활용해 코드값을 레이블로 변경하기 끝
