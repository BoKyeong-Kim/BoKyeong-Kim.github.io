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

AWS Lambda 홈페이지에 접속하여 로그인한다.

그리고 상단위 서비스 버튼을 클릭하면 아래와 같은 화면이 나타난다.<br>
**컴퓨팅 - Lambda** 클릭!

![size_main]({{ site.baseurl }}/assets/img/awsmain.png)

