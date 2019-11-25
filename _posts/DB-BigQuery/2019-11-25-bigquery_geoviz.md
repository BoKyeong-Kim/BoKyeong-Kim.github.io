---
layout: post
title: 빅쿼리(BigQuery) Geo Viz 사용하기
subtitle: < GCP >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [DB/BigQuery]
tags: [BigQuery,google,GCP,GeoViz]
---

빅쿼리(BigQuery) 사용하기 2탄!
**Geo Viz**를 사용하여 지도에 정류장 위치 표시하기

현재 가지고 있는 데이터 중 버스 정류장의 X좌표, Y좌표의 컬럼을 가지고 있는 데이터를 활용하여 Geo Viz를 활용하여 지도에 정류장 위치를 표시해보려고 한다.

<br>
아래와 같이 x좌표와 y좌표를 가지고 있는 데이터를 불러온다.

![size_main]({{ site.baseurl }}/assets/img/geo_xy.png)

<br>
BigQuery GIS함수를 사용하여 위도와 경도 열을 지리적 점으로 변환한다.

![size_main]({{ site.baseurl }}/assets/img/gis_func.png)

```
ST_GEOGPOINT(longitude, latitude)
```
: 단일 점을 사용하여 GEOGRAPHY를 생성합니다. ST_GEOGPOINT는 지정된 FLOAT64 경도 및 위도 매개변수를 사용하여 단일 점을 생성한 후 GEOGRAPHY 값으로 반환합니다.

<b>더 자세한 사항은 [표준 SQL의 지리 함수](https://cloud.google.com/bigquery/docs/reference/standard-sql/geography_functions?hl=ko) 참고!</b>


더 자세한 사항은 [bigquerygeoviz](https://bigquerygeoviz.appspot.com/?hl=ko)에 들어가서 
아래와 같은 코드를 작성하여 정류장의 위치를 지도에 표시해본다.
![size_main]({{ site.baseurl }}/assets/img/geogPoint.png)

한 사람의 이동 패턴을 보고 싶으면 그에 맞는 조건을 주어 쿼리문을 작성하여 Geo Viz에서 다루면 정류장 위치가 표시될 것이다!


