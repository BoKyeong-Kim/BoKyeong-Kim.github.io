---
layout: post
title: Python 딕셔너리
subtitle: < Dictionary >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Basic]
tags: [python, basic, 기초, 딕셔너리, Dictionary]
---

- get()
- setdefault()
- 문자개수 카운팅 프로그램


<br>


### Dictionary
- 리스트의 인덱스와는 달리 사전의 인덱스는 정수만이 아닌 다양한 데이터 유형을 사용할 수 있다.
- 사전을 위한 인덱스를 Key라고 하고, 키와 그에 연관된 값을 키-값 쌍(key-value pair)라고 한다.
- 중괄호{}로 정의
- 리스트와는 달리 사전의 아이템들은 순서가 없다.
    - 순서가 없으므로 리스트처럼 슬라이스를 만들 수 없음
    - 순서가 없지만 키로 임의의 값을 쓸 수 있다는 사실 덕에 데이터를 강력한 방법으로 구성할 수 있음

<br>

딕셔너리에 저장된 key를 입력받아 값을 출력하고, 키에 없다면 추가하는 코드
 ```python
 birthdays = {'Alice' : 'Apr 1', 'Bob' : 'Dec 12', 'jason' : 'may 30'}

while True :
    print('Enter a name: (black to quit)')
    name = input()
    if name == '':
        break

    if name in birthdays :
        print(birthdays[name] + ' is the birthday of ' + name)
    else :
        print('I do not have birthday information for ' + name)
        print('What is their birthday?')
        bday = input()
        birthdays[name] = bday
        print('birthday database updated.')
```

<br>

#### keys(), values(), items()
- 사전의 키, 값, 키와 값 모두를 돌려주는 메소드
- items() 메소드가 돌려주는 값은 키와 튜플이라는 점 유의
- 위 메소드로 리스트 값을 얻고 싶다면 list()함수에 전달
    - ex) list(birthdays.keys())


<br>

#### The get()
- 키와 값을 사용할때 사전에 키가 존재하는지 여부를 확인
- get(가져올 값의 키, 키가 존재하지 않을 때 돌려줄 값)

```python
items = {'apple' : 5, 'banana' : 7}
print('I am bringing ' + str(items.get('apple', 0)) + ' apple.')
>>> I am bringing 5 apple.
print('I am bringing ' + str(items.get('tomato', 0)) + ' tomato.')
>>> I am bringing 0 tomato.
```

- get()을 사용하지않으면 에러가 발생한다.

<br>

#### The setdefault()
- 딕셔너리 안의 어떤 특정한 키에 이미 값이 존재하지않는 경우만 그 키에 값을 설정할때가 종종있다.
- setdefault(검사할 키, 키가 존재하지 않을 때 해당키에 설정할 수 있는 값)
- 딕셔너리에 어떤 키가 존재하도록 보장할 수 있는 좋은 방법

```python
infomation = {'name' : 'boka', 'age': 25}
infomation.setdefault('like' , 'beef')
>>> 'beef'

infomation
>>> {'name': 'boka', 'age': 25, 'like': 'beef'}

infomation.setdefault('like' , 'fish')
>>> 'beef'
```
- 이미 infomation은 like라는 키를 가지고있으므로 키에 대한 값은 fish로 바뀌지 않는다.


<br>

#### 각 문자가 나타나는 개수를 세는 프로그램

- msg 변수 안에 있는 각 글자를 차례대로 되풀이 하면서 각 문자가 몇 번이나 나오는지 계산
- setdefault()는 count 사전에 키가 있음을 보장하므로(없으면 기본값 0을 추가) count[character] = count[character] + 1이 실행될 때 프로그램은 KeyError를 일으키지 않는다.

```python
msg = 'It was a bright cold day in April, and the clocks were striking thirteen. '
count = {}

for character in msg:
    count.setdefault(character, 0)
    count[character] = count[character] + 1

print(count)

>>> {'I': 1, 't': 6, ' ': 14, 'w': 2, 'a': 4, 's': 3, 'b': 1, 'r': 5, 'i': 6, 'g': 2, 'h': 3, 'c': 3, 'o': 2, 'l': 3, 'd': 3, 'y': 1, 'n': 4, 'A': 1, 'p': 1, ',': 1, 'e': 5, 'k': 2, '.': 1}
```


- 프로그램에 pprint 모듈을 가져오면 사전의 값들을 보기좋게 출력할 수 있다.
- 위 코드에 import pprint를 추가한뒤, print(count) -> pprint.pprint(count)로 바꾼뒤 실행
- 화면에 표시하는 대신 문자열값으로 얻고싶다면 pprint.pformat() 호출
    - pprint.pprint(count) == print(pprint.pformat(count))

```python
{' ': 14,
 ',': 1,
 '.': 1,
 'A': 1,
 'I': 1,
 'a': 4,
 'b': 1,
 'c': 3,
 'd': 3,
 'e': 5,
 'g': 2,
 'h': 3,
 'i': 6,
 'k': 2,
 'l': 3,
 'n': 4,
 'o': 2,
 'p': 1,
 'r': 5,
 's': 3,
 't': 6,
 'w': 2,
 'y': 1}
```

<br>








---------------

참고
- [파이썬 프로그래밍으로 지루한 작업 자동화하기](https://g.co/kgs/uScDFN)