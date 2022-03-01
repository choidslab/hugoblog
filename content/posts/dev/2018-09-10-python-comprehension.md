---
layout: post
title: "[Python] 컴프리헨션(Comprehension)"
subtitle: ""
date: 2018-09-10 12:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, comprehension, Introducing Python]
---

### 컴프리헨션(Comprehension)
  - 컴프리헨션은 함축을 의미한다. 하나 이상의 Iterator로부터 파이썬 자료구조를 만드는 방법이다. 간편한 구문으로 반복문과 조건 테스트를 결합할 수 있게 해준다.
  - 컴프리헨션을 사용하는 것은 초급 이상의 단계에서 파이썬을 어느 정도 알고 있다는 것을 의미한다. 즉, 더 파이써닉하게 사용한다는 것을 의미한다.  

---

### 1. list 컴프리헨션

리스트 컴프리헨션을 활용한 정수 리스트 생성

`[표현식 for 항목 in 순회 가능 객체]`

```python
>>> number_list = [number for number in range(1, 6)]
>>> number_list
[1, 2, 3, 4, 5]
```
또 다른 예제로 홀수 정수만을 갖는 리스트를 컴프리헨션으로 표현하면 다음과 같다.

`[표현식 for 항목 in 순회 가능 객체 if 조건]`
```python
>>> oddnumber_list = [number for number in range(1, 10) if number % 2 == 1]
>>> oddnumber_list
[1, 3, 5, 7, 9]
```

---

### 2. 딕셔너리(Dictionary) 컴프리헨션

딕셔너리도 컴프리헨션 표현이 가능하다.

`{key_표현식 : value_표현식 for 표현식 in 순회 가능 객체}`

```python
>>> word = 'letters'
>>> letter_counts = {letter: word.count(letter) for letter in word}
>>> letter_counts
{'l': 1, 'e': 2, 't': 2, 'r': 1, 's': 1}
```

---

### 3. Set 컴프리헨션

Set 컴프리헨션 표현도 가능하다.

`{표현식 for 표현식 in 순회 가능 객체}`

if테스트와 다중 for절이 있는 형식에서 Set 컴프리헨션 사용이 가능하다.

```python
>>> a_set = {number for number in range(1, 6) if number % 3 == 1}
>>> a_set
{1, 4}
```

---

### 4. Generator 컴프리헨션

튜플(tuple)은 컴프리헨션 표현이 없다. ()괄호를 사용할 경우 Generator 컴프리헨션이 된다.
```python
>>> number_thing = (number for number in range(1,6))
>>> type(number_thing)
<class generator>
```
type() 실행 결과를 통해 볼 수 있듯이 Generator 컴프리헨션은 Generator 객체를 반환한다. 따라서 for문을 통해 Generator 객체를 순환할 수 있다.

```python
>>> for number in number_thing:
...     print(number)
...
1
2
3
4
5
```

```
Generator는 한 번만 실행될 수 있다.
값을 처리한 뒤 이를 기억하고 있지 않으므로 다시 시작하거나 백업할 수 없다.
```
<br>

컴프리헨션 표현을 자주 사용하지 않아 익숙하지 않은데 앞으로 반복해서 사용하여 pythonic하게 코딩을 할 수 있도록 노력해봐야겠다.
컴프리헨션 요약은 여기까지...

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용을 요약한 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 또한, 잘못된 내용이나 모호한 내용이 있는 경우 전문가분들께서 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 읽어주셔서 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.121-126
