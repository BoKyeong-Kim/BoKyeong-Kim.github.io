---
layout: post
title: ML with Python(1)
subtitle: < 파이썬 라이브러리를 활용한 머신러닝 >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [AI/ML]
tags: [AI,ML, machine learing, python]
---


**머신러닝 공부하기** 1탄!

<br>

**파이썬 라이브러리를 활용한 머신러닝** 책을 참고하여 작성하였다.

<br>

#### 머신러닝 프로세스에서 가장 중요한 과정은 사용할 데이터를 이해하고 그 데이터가 해결해야할 문제와 어떤 관련이 있는지 이해하는 일

- 1) 어떤 질문에 대한 답을 원하는가? 가지고 있는 데이터가 원하는 답을 줄 수 있는가?
- 2) 내 질문을 머신러닝의 문제로 가장 잘 기술하는 방법은 무엇인가?
- 3) 문제를 풀기에 충분한 데이터를 모았는가?
- 4) 내가 추출한 데이터의 특성은 무엇이며 좋은 예측을 만들어낼 수 있을 것인가?
- 5) 머신러닝 애플리케이션의 성과를 어떻게 측정할 수 있는가?
- 6) 머신러닝 솔루션이 다른 연구나 제품과 어떻게 협력할 수 있는가?

<br>

### 1) 첫번째 애플리케이션 : 붓꽃의 품종 분류
- 목표 : 어떤 품종인지 구분해놓은 측정 데이터를 이용해 서로 채집한 붓꽃의 품종을 예측하는 머신러닝 모델을 만드는 것
- 지도학습(붓꽃의 품종을 정확하게 분류한 데이터를 가지고 있기 때문)
- 분류(Classification)문제 : 몇가지 선택사항(붓꽃의 품종) 중 하나를 선택하는 것
- 클래스(Class) : 출력될 수 있는 값(붓꽃의 종류)들
    - 데이터셋에 있는 붓꽃 데이터는 모두 세클래스 중 하나에 속한다.(세 개의 클래스는 분류하는 문제)
- 레이블(label) : 특정 포인트에 대한 출력 (여기서는 품종)


<br>

#### 1-1) 데이터 적재
- 붓꽃(iris) 데이터셋
- 사이킷런(scikit-learn)의 데이터셋(datasets) 모듈에 포함

<br>

- 필요한 라이브러리 import
```python
import pandas as pd
import mglearn
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import display
```

```python
from sklearn.datasets import load_iris
iris_datasets = load_iris()
```
<br>

- load_iris가 반환한 객체는 파이썬의 딕셔너리와 유사한 Bunch 클래스의 객체.(키와 값으로 구성)


```python
print("iris_datasets의 키 : \n{}".format(iris_datasets.keys()))
```

```
iris_datasets의 키 : 
dict_keys(['data', 'target', 'target_names', 'DESCR', 'feature_names', 'filename'])
```

<br>

-- DESCR 키에는 데이터셋에 대한 간략한 설명이 들어있다.

```python
print(iris_datasets['DESCR'])
```

```
.. _iris_dataset:

Iris plants dataset
--------------------

**Data Set Characteristics:**

    :Number of Instances: 150 (50 in each of three classes)
    :Number of Attributes: 4 numeric, predictive attributes and the class
    :Attribute Information:
        - sepal length in cm
        - sepal width in cm
        - petal length in cm
        - petal width in cm
        - class:
                - Iris-Setosa
                - Iris-Versicolour
                - Iris-Virginica
                
    :Summary Statistics:

    ============== ==== ==== ======= ===== ====================
                    Min  Max   Mean    SD   Class Correlation
    ============== ==== ==== ======= ===== ====================
    sepal length:   4.3  7.9   5.84   0.83    0.7826
    sepal width:    2.0  4.4   3.05   0.43   -0.4194
    petal length:   1.0  6.9   3.76   1.76    0.9490  (high!)
    petal width:    0.1  2.5   1.20   0.76    0.9565  (high!)
    ============== ==== ==== ======= ===== ====================

    :Missing Attribute Values: None
    :Class Distribution: 33.3% for each of 3 classes.
    :Creator: R.A. Fisher
    :Donor: Michael Marshall (MARSHALL%PLU@io.arc.nasa.gov)
    :Date: July, 1988

The famous Iris database, first used by Sir R.A. Fisher. The dataset is taken
from Fisher's paper. Note that it's the same as in R, but not as in the UCI
Machine Learning Repository, which has two wrong data points.

This is perhaps the best known database to be found in the
pattern recognition literature.  Fisher's paper is a classic in the field and
is referenced frequently to this day.  (See Duda & Hart, for example.)  The
data set contains 3 classes of 50 instances each, where each class refers to a
type of iris plant.  One class is linearly separable from the other 2; the
latter are NOT linearly separable from each other.

.. topic:: References

   - Fisher, R.A. "The use of multiple measurements in taxonomic problems"
     Annual Eugenics, 7, Part II, 179-188 (1936); also in "Contributions to
     Mathematical Statistics" (John Wiley, NY, 1950).
   - Duda, R.O., & Hart, P.E. (1973) Pattern Classification and Scene Analysis.
     (Q327.D83) John Wiley & Sons.  ISBN 0-471-22361-1.  See page 218.
   - Dasarathy, B.V. (1980) "Nosing Around the Neighborhood: A New System
     Structure and Classification Rule for Recognition in Partially Exposed
     Environments".  IEEE Transactions on Pattern Analysis and Machine
     Intelligence, Vol. PAMI-2, No. 1, 67-71.
   - Gates, G.W. (1972) "The Reduced Nearest Neighbor Rule".  IEEE Transactions
     on Information Theory, May 1972, 431-433.
   - See also: 1988 MLC Proceedings, 54-64.  Cheeseman et al"s AUTOCLASS II
     conceptual clustering system finds 3 classes in the data.
   - Many, many more ...
```

<br>

- target_names의 값은 우리가 예측하려는 붓꽃의 품종의 이름을 문자열 배열로 가지고 있다.

```python
print(iris_datasets['target_names'])
```

```
['setosa' 'versicolor' 'virginica']
```

<br>

- feature_names의 값은 각 특성을 설명하는 문자열 리스트

```python
print(iris_datasets['feature_names'])
```

```
['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)', 'petal width (cm)']
```
<br> 

- 실제 데이터는 target과 data 필드에 들어있다. data는 꽃잎의 길이와 폭, 꽃받침의 길이와 폭을 수치 값으로 가지고있는 Numpy 배열.


```Python
print("data의 타입:{}".format(type(iris_datasets['data'])))
```

```
data의 타입:<class 'numpy.ndarray'>
```

<br>
- data 배열의 행은 개개의 꽃이 되며 열은 각 꽃에서 구한 네개의 측정치이다.
- 이 배열은 150개의 붓꽃 데이터를 가지고 있다.
- data 배열의 크기는 샘플의 수에 특성의 수를 곱한 값.(머신러닝에서 각 아이템은 샘플이라고 하고 속성은 특성이라고 부른다.)


```python
print("data의 shape:{}".format(iris_datasets['data'].shape))
```

```
data의 shape:(150, 4)
```
<br>

```python
print("data의 처음 다섯 행:\n{}".format(iris_datasets['data'][:5]))
```

```
data의 처음 다섯 행:
[[5.1 3.5 1.4 0.2]
 [4.9 3.  1.4 0.2]
 [4.7 3.2 1.3 0.2]
 [4.6 3.1 1.5 0.2]
 [5.  3.6 1.4 0.2]]
```

<br>
- 위의 데이터를 봤을 때 다섯 붓꽃의 꽃잎 폭은 모두 0.2cm이고 첫번째 꽃이 가장 긴 5.1cm의 꽃받침을 가졌음을 알 수 있다.
- target 배열도 샘플 붓꽃의 품종을 담은 Numpy배열.
- target은 각 원소가 붓꽃하나에 해당하는 1차원 배열 (붓꽃의 종류는 0에서 2까지의 정수로 기록되어있다.)
- 숫자의 의미는 iris_datasets['target_names'] 배열에서 확인할 수 있다.


<br>

```python
print('target의 타입:{}'.format(type(iris_datasets['target'])))
```

```
target의 타입:<class 'numpy.ndarray'>
```

<br>

```python
print('target의 shape:{}'.format(iris_datasets['target'].shape))
```

```
target의 shape:(150,)

```

<br>

```python
print('target:\n{}'.format(iris_datasets['target']))
```

```
target:
[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2
 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2]
```


<br>

#### 1-2)성과측정 : 훈련데이터와 테스트 데이터

- 이 데이터로 머신러닝 모델을 만들고 새로운 데이터의 품종을 예측하려한다.
- 만든 모델을 새 데이터에 적용하기 전에 이 모델이 진짜 잘 작동하는지 알아야한다.(신뢰할 수 있는지)
- 모델을 만들 때 사용한 데이터는 평가 목적으로 사용할 수 없다.(오버피팅!!)
- 모델이 훈련데이터를 전부 기억할 수 있다. 데이터를 기억한다는 것은 모델을 잘 **일반화**하지 않았다는 뜻.

- 모델의 성능을 측정하려면 레이븛을 알고 있는 새 데이터를 모델에 적용해봐야한다. 
    - 훈련 데이터(train data) : 머신러닝 모델을 만들 때 사용
    - 테스트 데이터(test data) : 모델이 얼마나 잘 작동하는지 측정할 때 사용

<br>

- scikit-learn은 데이터셋을 섞어서 나눠주는 train_test_split 함수를 제공
- 일반적으로 train data 75%, test data 25%로 나눠서 사용한다.(상황에 따라 다를 수 있다.)
- scikit-learn에서 **데이터(2차원 배열-행렬)는 대문자 X**로 표시, **레이블(1차원 배열-벡터)은 소문자 y**로 표기

<br>

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(
    iris_datasets['data'], iris_datasets['target'], random_state=0)
```

- train_test_split 함수의 반환값은 X_train, X_test, y_train, y_test이며 모두 Numpy 배열.
- train_test_split 함수로 데이터를 나누기 전에 유사 난수 생성기를 사용하여 데이터 셋을 무작위로 섞어야한다.


<br>

```python
print("X_train의 shape {}".format(X_train.shape))
print("y_train의 shape {}".format(y_train.shape))
print('-----------------------')
print("X_test의 shape {}".format(X_test.shape))
print("y_test의 shape {}".format(y_test.shape))
```

```
X_train의 shape (112, 4)
y_train의 shape (112,)
-----------------------
X_test의 shape (38, 4)
y_test의 shape (38,)
```

<br>

#### 1-3) 가장 먼저 할 일 : 데이터 살펴보기 


- 머신러닝 모델을 만들기 전에 머신러닝이 없이도 풀 수 있는 문제는 아닌지, 혹은 필요한 정보가 누락되지 않았는지 데이터를 조사해보는것이 좋다.
- 또한 데이터를 탐색하면서 비정상적인 값이나 특이한 값을 찾을 수도 있다.(일관성이 없거나 범위가 다른 경우 등)
- 시각화는 데이터를 조사하는 가장 좋은 방법

<br>

#### 산점도 
- 데이터에서 한 특성을 x축에 놓고 다른 하나는 y축에 놓아 각 데이터 포인트를 하나의 점으로 나타내는 그래프
- 모든 특성을 짝지어 만드는 **산점도 행렬**을 사용할 수 있다.
- 하지만 산점도 행렬은 한 그래프에 모든 특성의 관계가 나타나는 것이 아니기 때문에 각각의 나누어진 산점도 그래프에는 드러나지 않은 중요한 성질이 있을 수도 있다.


<br>

데이터 포인트의 색은 붓꽃의 품종에 따라 구분.
- 1) X_train 데이터를 사용하여 데이터 프레임 생성
- 2) 열의 이름은 iris_datasets.feature_names에 있는 문자열을 사용
- 3) 데이터 프레임을 사용해 y_train에 따라 색으로 구분된 산점도 행렬을 만든다.


```python
iris_df = pd.DataFrame(X_train, columns=iris_datasets.feature_names)

iris_df.head()
```


![size_main]({{ site.baseurl }}/assets/img/iris_feature_name.png)
<br>






