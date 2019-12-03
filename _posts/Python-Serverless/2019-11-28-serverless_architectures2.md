---
layout: post
title: 서버리스 애플리케이션(2)
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Serverless]
tags: [Python, Serverless, 서버리스애플리케이션]
---

서버리스 애플리케이션 2탄! **AWS편**.

<br>

### AWS에서 서버리스 애플리케이션 함수 만들기

#### AWS Lambda란?
: AWS Lambda는 Amazon Web Services의 일부로 Amazon에서 제공하는 **이벤트 중심 서버리스 컴퓨팅 플랫폼**. 이벤트에 응답하여 코드를 실행하고 해당 코드에 필요한 컴퓨팅 리소스를 자동으로 관리하는 컴퓨팅 서비스 (위키백과)

<br>

#### AWS Lambda 트리거
: 서버리스 함수는 온디맨드(On-demand) 컴퓨팅 개념을 기반으로 한다.<br>
(온디맨드(On-demand):주문형 서비스)


Lambda 함수는 트리거 이벤트가 필요하며 이를 통해 전체 컴퓨팅 프로세스가 시작된다.
AWS Lambda는 트리거로서 동작할 수 있는 몇 가지 이벤트를 갖고 있으며, 대부분 AWS의 모든 서비스는 AWS Lambda 트리거로서 동작이 가능하다.

<br>

Lambda 트리거 페이지는 아래의 화면과 같다.

![size_main]({{ site.baseurl }}/assets/img/lambdamain.png)
<br>

#### 1) Lambda console로 이동

AWS Lambda 홈페이지에 접속하여 로그인한다.

그리고 상단위 서비스 버튼을 클릭하면 아래와 같은 화면이 나타난다.<br>
**컴퓨팅 - Lambda**를 클릭하여 AWS Lambda 콘솔을 연다.

![size_main]({{ site.baseurl }}/assets/img/awsmain.png)


<br>

#### 2)Lambda Blueprint 선택

Buleprint는 최소한의 처리를 수행할 수 있는 예제 코드를 제공한다.
대부분의 블루프린트는 Amazon S3, DynamoDB 또는 사용자 정의 애플리케이션과 같은 특정 이벤트 소스의 이벤트를 처리한다.

<br>

* 콘솔 화면에서 **함수** 목록에 들어와 오른쪽에 **함수생성**을 클릭한다.

![size_main]({{ site.baseurl }}/assets/img/selectfunc.png)

<br>

* buleprint를 선택하고 필터 상자에 hello-world-python을 입력하여 선택한 뒤, 구성 버튼을 누른다.

![size_main]({{ site.baseurl }}/assets/img/selectblueprint.png)

<br>

#### 3)Lambda 함수 구성 및 생성

Lambda 함수는 사용자가 제공한 코드, 관련 종속성 및 구성으로 이뤄진다. 사용자가 제공한 구성 정보에는 할당하려는 컴퓨팅 리소스, 실행 제한시간, 사용자 대신 Lambda 함수를 실행할 수 있도록 AWS Lambda가 맡는 IAM의 역할이 포함된다고 한다.

아마존에서 기본적으로 제공하는 예제를 참고하여 함수를 구성해보려고 한다.


![size_main]({{ site.baseurl }}/assets/img/createfunc.png)


기본적으로 아래의 코드가 자동으로 구성된다.

![size_main]({{ site.baseurl }}/assets/img/createfunc2.png)


<br>

#### 4)Lambda 함수 호출 및 결과 확인

콘솔에 hello-world-python Lambda함수가 표시된다. 함수를 테스트하고 결과를 확인하며 로그를 검토할 수 있다.


아래의 화면에서 우측 상단 테스트 버튼 클릭

![size_main]({{ site.baseurl }}/assets/img/testlambda.png)

아래의 화면처럼 이벤트를 입력하여 함수를 테스트할 수 있도록 편집기가 표시된다.
![size_main]({{ site.baseurl }}/assets/img/testevent.png)


함수가 성공적으로 실행되면, 콘솔에서 결과를 확인한다.

<br>

#### 5)지표 모니터링

테스트를 반복하여 클릭하면 지표가 생성된다. 모니터링 탭을 선택하여 Lambda함수의 지표를 확인한다.
Lambda 지표는 Amazon CloudWatch를 통해 보고되며 이 지표를 활용하여 사용자 정의 경보를 설정할 수 있다. CloudWatch에 대한 자세한 내용은 더 자세한 정보는 [Amazon CloudWatch Developer Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html
)에서 확인할 수 있다.
<br>

![size_main]({{ site.baseurl }}/assets/img/testmonitor.png)

AWS Lambda를 사용하면 사용한 만큼만 비용을 지불한다.

<br>

#### 6)Lambda 함수 삭제

Lambda 함수를 유지하는데 바용이 부과되지않으므로 콘솔에서 함수를 쉽게 삭제할 수 있다.


![size_main]({{ site.baseurl }}/assets/img/deletefunc.png)

<br>

**AWS Lambda 함수 생성 완료!**