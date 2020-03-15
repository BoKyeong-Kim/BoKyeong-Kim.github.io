---
layout: post
title: US Accidents (3.0 million records)
subtitle: < A Countrywide Traffic Accident Dataset (2016 - 2019) >
feature-img: "assets/img/sample_feature_img_2.png"
sitemap :
changefreq : daily
priority : 1.0
categories : [Data/kaggle]
tags: [kaggle, Accidents, US]
---


- US Accidents (3.0 million records)
	- A Countrywide Traffic Accident Dataset (2016 - 2019)

<br>

Kaggle로 공부하기!

아무래도 사고관련 업무이다보니 자연스럽게 캐글에서도 사고쪽 데이터와 컴퍼티션을 찾게된다. 그래서 찾게된 사고 심각도 예측 컴퍼티션! 캐글의 장점은 번역하면서 영어까지 공부할 수 있다. 차근차근 시작해보자!



-----------------------
### Data
#### Description
이것은 미국의 49개 주를 아우르는 전국적인 자동차 사고 데이터셋 입니다.

이 자료는 2016년 2월부터 2019년 12월까지 스트리밍 트래픽 사고 데이터를 제공하는 API 2개를 포함한 여러 데이터 공급자에 의해 수집됩니다.

이러한 APIs는 미국 및 주 교통부, 법 집행기관, 교통 카메라, 도로망 내의 교통 센서 등 다양한 기관이 캡쳐한 교통 데이터를 방송합니다.


현재 이 데이터셋에는 약 30만건의 사고기록이 있다. 이 데이터셋에 대한 자세한 내용은 [여기](https://smoosavi.org/datasets/us_accidents)를 참조하세요.


<br>

#### Acknowledgements 

이 데이터 세트를 사용하는 경우 다음 문서를 인용하세요.
- Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “[A Countrywide Traffic Accident Dataset.](https://arxiv.org/abs/1906.05409)”, 2019.
- Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "[Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights.](https://arxiv.org/abs/1909.09638)" In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.

<br>

#### Content
이 데이터는 다중 트래픽 API를 사용하여 실시간으로 수집되었다. 현재 이 자료에는 2016년 2월부터 2019년 12월까지 미국연방지역에 대해 수집된 자료가 들어있다. 이 데이터셋에 대한 자세한 내용은 [여기](https://smoosavi.org/datasets/us_accidents)를 참조하세요.

<br>

#### Inspiration

US의 사고들은 실시간 자동차 사고 예측, 자동차 사고 핫스팟 위치 연구, 교통사고 사상자 분석 및 원인 및 영향 규칙 추출, 강수량이나 기타 환경 자극이 사고 발생에 미치는 영향 연구와 같은 수많은 적용에 사용될 수 있다.


#### Usage Policy and Legal Disclaimer

이 데이터셋은 Creative Commons Attribution-Noncommercial-ShareAlike 라이선스(CC BY-NC-SA 4.0)에 따라 연구 목적으로만 배포되고 있다. 다운로드 버튼을 클릭하면 이 데이터를 비상업적, 연구 또는 학술적 응용 프로그램에만 사용하기로 동의할 수 있다. 이 데이터셋을 사용하는 경우 위의 문서를 인용해야 할 수 있다.


<br>

#### Columns
- ID : 사고 기록의 고유 식별자(unique)
- Source : 사고 보고서의 출처(사고를 보고한 API)
- TMC : 교통사고는 교통메시지채널(TMC) 코드를 가지고 있을수도 있으며, 이 코드는 사건에 대한 보다 상세한 설명을 제공
- Severity : 사고의 심각도, 1과 4 사이의 숫자는 교통에 가장 영향을 적게 미치는 숫자(즉, 사고로 인한 짧은 지연)를 나타내며, 4는 교통애 큰 영향을 미친다(즉 긴지연).
- Start_Time : 현지 시간대에서 사고의 시작 시간을 표
- End_Time : 지역 시간대에서 사고의 종료 시간
- Start_Lat : 시작점의 GPS 좌표에 위도 표시
- Start_Lng : 시작점의 GPS 좌표에 경도 표시
- End_Lat : 끝점의 GPS 좌표에 위도표시.
- End_Lng : 끝점의 GPS 좌표에 경도를 표시
- Distance(mi) : 사고의 영향을 받는 도로의 길이.
- Description : 사고에 대한 설명
- Number : 주소 필드에 거리 번호
- Street : 주소 필드에 거리 이름
- Side : 주소 필드에 거리의 상대적 측면(우측/좌측)을 표시
- City : 주소 필드에 도시 표시
- County : 주소 필드에 해당 카운티를 표시
- State : 주소 필드에 상태를 표시
- Zipcode : 주소 필드에 zipcode 표시
- Country : 주소 필드에 국가를 표시
- Timezone : 사고 위치(동부, 중부 등)를 기준으로 한 시간대를 표시
- Airport_Code : 사고 지점과 가장 가까운 공항 기반 기상 관측소를 의미
- Weather_Timestamp : 기상 관측 기록(현지 시간)을 표시
- Temperature(F) : 온도를 표시(화씨)
- Wind_Chill(F) : 바람의 냉기(화씨)
- Humidity(%) : 습도를 비율로 나타냄
- Pressure(in) : 공기의 압력을 표시(인치)
- Visibility(mi) : 가시성 표시(마일 단위)
- Wind_Direction : 바람의 방향 표시
- Wind_Speed(mph) : 풍속 표시(시속 마일 단위)
- Precipitation(in) : 강수량(인치)
- Weather_Condition : 날씨 상태(비, 눈 뇌우, 안개 등)
- Amenity : A POI(Point-Of-Intest) 주석으로, 가까운 위치에 편의성이 있음을 나타냄.
- Bump : 근처 위치에 속도 범프 또는 혹이 있음을 나타냄
- Crossing : A POI 주석(주변 위치에서 교차)
- Give_Way : 가까운 위치에 give_way 부호가 있음을 나타냄(A POI 주석)
- Junction : 가까운 위치에 접합부가 있음을 나타냄(A POI 주석)
- No_Exit : 가까운 위치에 no_exit 기호가 있음을 나타냄
- Railway : 인근 위치에 철도가 있음을 나타냄.
- Roundabout : 주변 위치에 원형 교차로 존재함을 나타냄(A POI 주석)
- Station : 가까운 위치에 스테이션(버스, 열차 등)이 있음을 나타냄(A POI 주석)
- Stop : 가까운 위치에 정지 기호가 있음을 나타냄(A POI 주석)
- Traffic_Calming : 가까운 위치에 traffic_calming 평균이 있음을 나타냄.(A POI 주석)
- Traffic_Signal : 가까운 위치에 traffic_signal이 있음을 나타냄.(A POI 주석)
- Turning_Loop : 주변 위치에서 turn_loop(A POI 주석)
- Sunrise_Sunset : 일출/태양을 기준으로 낮의 기간(즉, 낮이나 밤)을 보여줌
- Civil_Twilight : 민간의 황혼에 근거한 낮의 기간(즉, 낮이나 밤)을 보여줌
- Nautical_Twilight : 해상 박명에 근거한 낮의 기간(즉, 낮이나 밤)을 보여줌
- Astronomical_Twilight : 천문학적인 황혼에 근거한 낮의 기간(즉, 낮이나 밤)을 보여줌













