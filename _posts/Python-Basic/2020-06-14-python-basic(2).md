---
layout: post
title: Python로 엑셀 다루기
subtitle: < openpyxl >
feature-img: "assets/img/sample_feature_img_2.png"
categories : [Python/Basic]
tags: [python, basic, 기초, 엑셀, openpyxl]
---

- openpyxl
    - get_sheet_by_name()
    - get_column_letter()
    - column_index_from_string()



<br>


### openpyxl
- 파이썬은 OpenPyXL을 내장하고 있지않으므로 따로 설치해줘야한다.

```python
pip install openpyxl
```

<br>

example.xlsx
![size_main]({{ site.baseurl }}/assets/img/example_xlsx.png)
- sheet2와 sheet3은 비어있다.


<br>

#### 엑셀 문서 열기
- 통합문서에 있는 모든 시트의 이름이 담긴 리스트는 get_sheet_names()를 이용하여 얻을 수 있다.

```python
# output은 >>>로 표시
import openpyxl

wb = openpyxl.load_workbook('example.xlsx')
wb.get_sheet_names()
>>> ['Sheet1', 'Sheet2', 'Sheet3']

sheet = wb.get_sheet_by_name('Sheet3')
sheet
>>> <Worksheet "Sheet3">

type(sheet)
>>> <class openpyxl.worksheet.worksheet.Worksheet>

anotherSheet = wb.active
anotherSheet
>>> <Worksheet "Sheet1">
```
- 각각의 시트는 Worksheet 객체에 대응된다.
- Workbook객체의 get_sheet_by_name()에 시트이름 문자열을 전달하면 시트를 가져올 수 있다.
- active를 호출하면 통합문서의 활성 시트를 얻을 수 있다.
    - 활성시트란 통합문서를 엑셀에서 열었을 때 가장 먼저 나타나는 시트
- Worksheet 개체를 얻고 나면 title 속성으로 이름을 얻을 수 있다.

<br>

#### 시트에서 셀 값 가져오기

```python
import openpyxl

wb = openpyxl.load_workbook('example.xlsx')
sheet = wb.get_sheet_by_name('Sheet1')
sheet['A1']
>>> <Cell 'Sheet1'.A1>

sheet['A1'].value
>>> datetime.datetime(2015, 4, 5, 13, 34, 2)

c = sheet['B1']
c.value
>>> 'Apples'

'Row %s, Column %s is %s' % (c.row, c.column, c.value)
>>> 'Row 1, Column 2 is Apples'

'Cell %s is %s' % (c.coordinate, c.value)
>>> 'Cell B1 is Apples'

sheet['C1'].value
>>> 73
```


- Cell 객체는 value 속성을 가지고 있으며, 그 셀에 저장된 값을 포함하고 있다.
- Cell 객체는 셀의 위치 정보를 제공하는 row(행), column(열), coordinate(좌표) 속성을 가지고 있다.
- openpyxl은 열A에 있는 날짜를 자동으로 해석해서 datetime(날짜시간)값으로 돌려준다.
- 프로그램에서 열을 글자로 지정하기 까다로울 수 있다.
    - Z 다음에는 열 이름이 두글자로 이루어지기 때문(AA, AB, AC ..)
    - 대안으로는 시트의 cell() 메소드를 사용할 때 row와 column 키워드 매개변수에 정수를 전달하여 셀을 얻을 수 있다.
    - 첫번째 행 또는 열은 정수 1이 아닌 0임을 유의

<br>

```python 
sheet.cell(row=1, column=2) # 정수2가 아닌 B가 전달되는 것 유의
>>> <Cell 'Sheet1'.B1>

sheet.cell(row=1, column=2).value 
>>> 'Apples'

for i in range(1, 8, 2) :
     print(i, sheet.cell(row= i, column=2).value)

>>> 1 Apples
    3 Pears
    5 Apples
    7 Strawberries
```
- 시트의 cell() 메소드를 사용하여 row=1과 column=2를 전달하면 셀 B1에 대한 Cell객체를 얻을 수 있다.
    - sheet['B1']으로 지정하는 것과 같은 결과
    - 그 후 cell() 메소드와 함께 키워드 매개변수를 사용하면 for루프를 사용하여 연속된 결과를 출력할 수 있다.
    - B열로 내려가 행 번호가 홀수인 모든 셀의 값을 출력
- for 루프의 i 변수는 cell() 메소드의 row 키워드에 전달되며, column 키워드 매개변수에는 항상 2가 전달된다.



```python
sheet.max_row
>>> 7
sheet.max_column
>>> 3
```

- Worksheet 객체의 max_row와 max_column로 시트의 크기를 판단할 수 있다.


<br>

#### 열 이름의 글자와 숫자 사이 변환
- 숫자를 글자로 변환하려면 openpyxl.utils.column_index_from_string()을 호출한다.
- 글자를 숫자로 변환하려면 openpyxl.utils.get_column_letter()을 호출한다.

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string

get_column_letter(1)
>>> 'A'

get_column_letter(2)
>>> 'B'

get_column_letter(27)
>>> 'AA'

get_column_letter(900)
>>> 'AHP'

wb = openpyxl.load_workbook('example.xlsx')
sheet = wb.get_sheet_by_name('Sheet1')
get_column_letter(sheet.max_column)
>>> 'C'

column_index_from_string('A')
>>> 1

column_index_from_string('AA')
>>> 27
```

- openpyxl.utils 모듈에서 두가지 함수를 가져온 뒤, get_column_letter()를 호출하고 27과 같은 정수를 전달하여 27번째 컬럼의 글자 이름이 무엇인지 알아낼 수 있다.
- 반대로 column_index_from_string()에 컬럼의 글자이름을 전달하면 함수는 그 열이 숫자로는 어떤 값인지 알려준다.

<br>

#### 시트에서 행과 열 얻기
- 특정한 행, 열 또는 사각형 영역 안에 있는 모든 cell 객체를 얻기 위해 Worksheet 객체를 조각낼 수 있다.
- 얻어낸 조각을 루프에 돌려서 그에 속해있는 모든 셀을 사용할 수 있다.

```python
import openpyxl

wb = openpyxl.load_workbook('example.xlsx')
sheet = wb.get_sheet_by_name('Sheet1')

tuple(sheet['A1' : 'C3'])
>>> ((<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.B1>, <Cell 'Sheet1'.C1>), (<Cell 'Sheet1'.A2>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.C2>), (<Cell 'Sheet1'.A3>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.C3>))
```

- A1에서 C3에 이르는 직사각형 영역안에 있는 Cell 객체를 필요로 한다고 지정
    - 이 영역 안에 있는 Cell 객체를 포함하는 Generator 객체를 얻게된다.
    - Generator 객체를 눈으로 확인하는데 도움이 되도록 tuple함수 사용
        - 위 튜플은 세 개의 튜플을 포함하고 있다.(각 행당 하나씩으로 지정된 영역의 가장 위쪽부터 가장 아래쪽까지 지정한 영역 안에 있는 한 행의 cell객체를 왼쪽에서 오른쪽 순으로 포함하고 있음)


```python
for rowOfCellObjects in sheet['A1':'C3']:
     for cellObj in rowOfCellObjects:
             print(cellObj.coordinate, cellObj.value)
     print('--- END OF ROW ---')
 
>>> A1 2015-04-05 13:34:02
    B1 Apples
    C1 73
    --- END OF ROW ---
    A2 2015-04-05 03:41:23
    B2 Cherries
    C2 85
    --- END OF ROW ---
    A3 2015-04-06 12:46:51
    B3 Pears
    C3 14
    --- END OF ROW ---
```

- 영역안에 있는 각 셀의 값을 출력하기 위해 for루프를 두 번 사용
- 바깥쪽 for 루프는 조각의 각 행을 차례대로 거쳐간다.
- 안쪽 for루프는 한 행의 각 셀을 차례대로 거쳐간다.
- 특정 행이나 열에 있는 셀의 값을 사용하려면 Worksheet 객체의 rowdhk column 속성을 사용할 수 있다.

```python
import openpyxl

wb = openpyxl.load_workbook('example.xlsx')
sheet = wb.active
list(sheet.columns)[1]
>>> (<Cell 'Sheet1'.B1>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.B4>, <Cell 'Sheet1'.B5>, <Cell 'Sheet1'.B6>, <Cell 'Sheet1'.B7>)

for cellObj in list(sheet.columns)[1]:
    print(cellObj.value)

>>> Apples
    Cherries
    Pears
    Oranges
    Apples
    Bananas
    Strawberries
```

- Worksheet 객체의 rows 속성을 사용하면 튜플의 튜플을 얻는다.(column도 동일)
    - 이들 각 내부 튜플은 각자 한 행을 나타내고, 그 행의 cell객체를 포함한다.
- example.xlsx 는 7행 3열로 이루어져있기 때문에 rows는 7개의 튜플(각각 3개의 cell객체를 포함)로 구성된 튜플이며, columns는 3개의 튜플(각각 7개의 cell객체를 포함)로 구성된 튜플
- 하나의 특정 튜플을 사용하려면 더 큰 튜플의 인덱스로 참조할 수 있다.(하나의 행이나 열을 나타내는 튜플을 얻은 후에는 루프로 그 안의 Cell객체를 차례대로 얻어서 출력할 수 있다.)
    - ex) 열 B를 나타내는 튜플을 얻으려면 sheet.columns[1]을 사용
    - ex) 열 A에 있는 Cell 객체가 포함된 튜플을 얻으려면 sheet.columns[0]을 사용

<br>

#### 엑셀 문서 만들기

```python
import openpyxl

wb = openpyxl.Workbook()
wb.get_sheet_names()
>>> ['Sheet']

sheet = wb.active
sheet.title
>>> 'Sheet'

sheet.title = 'create spread sheet'
wb.get_sheet_names()
>>> ['create spread sheet']
```

- openpyxl.Workbook() 함수를 호출하여 비어있는 새 Workbook 객체를 만든다.
- 통합 문서는 sheet라는 이름의 시트하나로 시작한다.
- attribute 속성에 새로운 문자열을 저장함으로 써 시트의 이름을 바꿀 수 있다.
- Workbook 객체 또는 그 안에 시트나 셀을 변경한다 해도 save() 통합 문서 메소드를 호출하기 전까지는 스프레드시트 파일에 기록되지 않는다.


<br>

#### 시트 만들고 없애기

```pthon
import openpyxl

wb = openpyxl.Workbook()
wb.get_sheet_names()
>>> ['Sheet']

wb.create_sheet()
>>> <Worksheet "Sheet1">

wb.get_sheet_names()
>>> ['Sheet', 'Sheet1']

wb.create_sheet(index=0, title ='First Sheet')
>>> <Worksheet "First Sheet">

wb.get_sheet_names()
>>> ['First Sheet', 'Sheet', 'Sheet1']

wb.remove_sheet(wb.get_sheet_by_name('Sheet1'))
wb.get_sheet_names()
>>> ['First Sheet', 'Sheet']
```

- create_sheet 메소드에 시트의 위치와 이름을 설정하여 만들 수 있다.
    - 아무것도 지정해주지 않으면 통합문서의 가장 마지막 시트로 설정된다.
- remove_sheet 메소드는 매개변수로 시트의 이름의 문자열이 아닌 Worksheet 객체를 받는다.
    - 제거하려는 시트의 이름만을 알고 있는 경우에는 get_sheet_by_name()을 호출하고 돌려받은 값을 remove_sheet()에 전달한다.

<br>

#### 셀에 값 쓰기

```python
import openpyxl

wb = openpyxl.Workbook()
sheet = wb.get_sheet_by_name('Sheet1')
sheet['A1'] = 'Hello world!'
sheet['A1'].value
>>> 'Hello world!'
```

- 셀에 값을 쓰는것은 사전에 키의 값을 쓰는 것과 비슷
- 셀의 좌표를 문자열로 가지고 있다면 Worksheet 객체 안에서 쓰고자 하는 셀을 지정하기 위해서 사전키처럼 사용할 수 있다.



<br>


#### 정리
- 스프레드시트 파일로부터 하나의 셀을 읽기까지에 관련된 모든 함수, 메소드 및 데이터 유형의 개요

1. openpyxl 모듈을 가져온다.
2. openpyxl.load_workbook() 함수를 호출한다.
3. Workbook 객체를 가져온다.
4. 통합 문서의 active 또는 sheetnames을 호출한다.
5. Worksheet 객체를 가져온다.
6. 인덱스를 사용하거나 cell() 시트 메소드를 row와 column 키워드 매개변수와 함께 사용한다.
7. Cell 객체를 가져온다.
8. Cell 객체의 value 속성을 읽어들인다.

<br>

---------------

참고
- [파이썬 프로그래밍으로 지루한 작업 자동화하기](https://g.co/kgs/uScDFN)