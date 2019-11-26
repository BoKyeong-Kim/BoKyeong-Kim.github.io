---
layout: post
title: 빅쿼리(BigQuery) 환경 셋팅하기
subtitle: < GCP >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Data/BigQuery]
tags: [BigQuery,google,GCP]
---

빅쿼리(BigQuery) 사용하기 1탄!

<br>
## 빅쿼리(BigQuery)란? 
: 위키백과에 따르면 'BigQuery는 RESTful 웹 서비스로 Google 스토리지와 함께 작동하는 대규모 데이터 세트를 대화식으로 분석 할 수 있고 MapReduce와 함께 사용될 수있는 서버리스 서비스로서의 소프트웨어' 라고 쓰여있다.

<br>
## 빅쿼리(BigQuery)의 특징

	- 클라우드기 때문에 별도의 설치과정이 필요없다.
	- SQL언어로 사용되기 때문에 접근하기 쉽다.
	- 클라우드 스케일의 인프라를 통해 대용량의 데이터를 다룰 수 있다.

<br>
구글 클라우드는 각종의 자원들을 프로젝트라는 개념으로 묶어서 사용한다. 만약 계정을 처음 생성했다면 프로젝트를 생성해줘야한다.


오른쪽 상단 메뉴에 프로젝트 생성 메뉴를 클릭해서 프로젝트 이름을 작성한 뒤 만들기를 클릭하면 프로젝트가 생성된다.


왼쪽 상단에 -가 3개 그려져 있는 메뉴를 클릭하여 밑으로 내리면 **BigQuery** 메뉴가 있고 선택하면 빅쿼리 콘솔로 이동하게 된다.


![size]({{ site.baseurl }}/assets/img/bigquery_menu.png)

<br>
메뉴로 들어가면 작업창이 나타난다. 
GoogleCloudPlatform 옆에 프로젝트를 선택할 수 있는 버튼과
왼쪽에 있는 메뉴에서는 쿼리 history를 확인할 수 있다.
그리고 쿼리 입력창과 하단에 쿼리 결과를 나타내주는 화면이 있다.

![size_main]({{ site.baseurl }}/assets/img/newquery.png)
<br>


* 우선 2GB 이상의 데이터를 다룰 것이기 때문에 파일 업로드를 클릭하여 구글 스토리지에 데이터를 업로드 해준다.

![size_main]({{ site.baseurl }}/assets/img/data_upload.png)
<br>

* 빅쿼리 콘솔로 돌아와 테이블 만들기를 클릭한다.

![size_main]({{ site.baseurl }}/assets/img/add_table.png)
<br>


* 구글 클라우드 스토리지에 있는 데이터로 테이블을 구성하기 위해 Google Cloud Storage를 클릭한다.

![size_main]({{ site.baseurl }}/assets/img/GCS.png)
<br>

* 구글 스토리지에 올려놓은 데이터를 선택한다.

![size_main]({{ site.baseurl }}/assets/img/GCS2.png)
<br>

* 테이블의 이름과 스키마를 지정해주고 테이블 만들면 셋팅 끝!

![size_main]({{ site.baseurl }}/assets/img/GCS3.png)
<br>

(테이블의 컬럼이름이 한글이면 스키마가 자동감지가 안되는 것 같다... 자동감지를 안하고 테이블 이름을 직접 입력해주거나 기존의 데이터 컬럼들을 영어로 바꿔주는 방법이 있다.)

![size_main]({{ site.baseurl }}/assets/img/query_data.png)
<br>

: 위와 같이 쿼리문을 사용하여 결과를 추출할 수 있다.
사용자의 카드를 그룹으로 묶어 하루의 승하차 금액을 집계해보았다.

주의할 점!
<br>
: From절에서 그냥 테이블 이름으로 작성하면 데이터를 불러올 수가 없기 때문에  
아래의 화면에서 테이블 쿼리를 클릭해주면 쿼리 입력창에 From절이 자동으로 작성된다.

![size_main]({{ site.baseurl }}/assets/img/auto_from.png)
<br>

<h4>빅쿼리 환경 셋팅 끝!</h4>

