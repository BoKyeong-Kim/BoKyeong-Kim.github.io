---
layout: post
title: 기초통계(12)
subtitle: < 분류모델 >
feature-img: "assets/img/sample_feature_img_2.png"
sitemap :
changefreq : daily
priority : 1.0
categories : [Data/Statistics]
tags: [데이터, 통계, 분류모델, 혼동행렬, 컨퓨전매트릭스, ROC곡선]
---

- 분류모델 성능평가
	- Confusion Matri(혼동행렬)


<br>

--------------------------------
### Confusion Matrix
#### 개념
- 머신러닝 혹은 통계학적 방법이 사용된 분류모델에서, 알고리즘의 성능을 보기 쉽게 시각화하는 테이블 형태의 레이아웃
- 혼동행렬이라고도 함

<br>

#### ROC 곡선
- 특정 진단 방법의 민감도와 특이도가 어떤 관계를 갖고있는지를 표현한 그래프

<br>

#### 형태
![size_main]({{ site.baseurl }}/assets/img/
Confusion_matrix(1).png)
- 민감도 : 어떤 진단법을 사용했을 때 실제로 이에 해당하는 사람들을 얼마나 잘 찾아내는가 하는 기준
	- 1인 케이스에 대해 1이라고 예측한 것
	- ex) 메르스 환자를 진찰해서 메르스라고 진단
- 특이도 : 어떤 진단법을 사용했을 때 실제로 이에 해당되지 않는 사람들을 얼마나 잘 분류하는가 하는 기준
	- 0인 케이스에 대해 0이라고 예측한 것
	- ex) 메르스 환자가 아닌데 메르스라고 진단

<br>

#### Confusion Matrix 주요 성능 지표
- Accuracy : 탐지율(맞게 검출한 비율)
	- (TP+TN)/(TP+TN+FP+FN)
	- 실제 악성/정상인지 맞게 예측한 비율
- Precision : 정확도(P로 검출한 것 중 실제 P의 비율)
	- TP/(TP+FP)
	- 악성으로 예측한 것 중 실제 악성인 샘플의 비율
- Recall : 재현율(실제 P를 P로 예측한 비율)
	- TP/(TP+FN) 
	- 실제 악성 샘풀 중 악성으로 예측한 비율
- False Alarm(Fall-out) : 오검출율(실제 N을 P로 예측한 비율)
	- FP/(FP+TN)
	- 실제 정상 샘플을 악성으로 예측한 비율
- TPR(True Positive Rate) = Recall : 예측과 실제 모두 P
	- TP/(TP+FN)
	- 실제 악성 샘플을 악성으로 예측한 비율
- TNR(True Negative Rate) : 예측과 실제 모두 N
	- TN/(TN+FP)
	- 실제 정상 샘플을 정상으로 예측한 비율
- FPR(False Positive Rate) = False Alarm : 실제 N인데 P로 검출
	- FP/(FP+TN)
	- 실제 정상 샘플을 악성으로 예측한 비율
- FNR(False Negative Rate) : 실제 P인데 N으로 검출
	- FN/(TP+FN) 
	- 실제 악성 샘플을 정상으로 예측한 비율

<br>

#### ROC곡선을 만들려면?
![size_main]({{ site.baseurl }}/assets/img/
Confusion_matrix(2).png)






-------------

* 출처 : 통계 기반 데이터 분석 강의 [https://e-koreatech.step.or.kr/page/lms/learning?m1=home%25&course_id=100168%25](https://e-koreatech.step.or.kr/page/lms/learning?m1=home%25&course_id=100168%25)






