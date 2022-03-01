---
layout: post
title: "[Python] class, class method, static method, named tuple"
subtitle: ""
date: 2018-10-23 22:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, class, classmethod, staticmethod, namedtuple, Introducing Python]
---

### 1. class method
  - 일반적으로 클래스 안에 정의된 함수는 `self`를 인자로 받는 인스턴스 함수(Instance Method)
  - `@classmethod` 데커레이터가 함수에 정의되어 있다면 이는 클래스 함수(Class Method)로 클래스 전체에 영향을 줌
  - 클래스 함수는 생성된 모든 객체에 영향을 줌
  - Python에서는 클래스 함수의 매개변수로 `cls`를 사용
  - 다음 예제코드는 클래스 함수를 통해 해당 클래스로부터 생성된 객체의 수를 확인할 수 있음

```python
# ex) class method
class A():
    count = 0

    def __init__(self):
        A.count += 1

    def exclaim(self):
        print("I'm an A!")

    @classmethod
    def kids(cls):
        print("A has", cls.count, "little objects.")

if __name__ == "__main__":
    easy_a = A()
    breezy_a = A()
    wheezy_a = A()
    A.kids()
```

---

### 2. static method
  - 정적 함수는 클래스나 객체에 영향을 미치지 않음, 편의를 위한 함수
  - `@staticmethod` 데커레이터가 함수에 정의 되어 있으면 이는 정적 함수를 의미
  - 전달인자로 `self`나 `cls`가 없음
  - 정적 함수의 경우 객체 생성 없이 해당 함수의 호출이 가능!

```python
# ex) static method
class CoyoteWeapon():
    @staticmethod
    def commercial():
        print("This CoyoteWeapon has been brought to you by Acme")

CoyoteWeapon.commercial()
```

---

### 3. 네임드 튜플(Named Tuple)
  - 클래스 선언 없이 객체를 생성하는 방법
  - tuple 성질을 가지면서 각 요소에 변수 이름으로 접근이 가능
  - 값이 불변(immutable)하는 객체
  - 일반 객체 선언보다 공간/시간 효율성이 좋음
  - Python 자체에서 지원되지 않으므로 `from collections import namedtuple` import 필요
  - 딕셔너리에서 key, value 값을 추출하여 `keyword argument` 형태로 값을 전달할 수 있음

```python
from collections import namedtuple

Bird = namedtuple('Bird', 'bill tail')
duck = Bird('wide orange', 'long')
print(duck)
print(duck.bill)
print(duck.tail)

#parts 딕셔너리에서 key, value 값을 각각 추출하여 Duck클래스에 인자로 전달
parts = {'bill': 'wide orange', 'tail': 'long'}
duck2 = Bird(**parts) # keyword argument
print(duck2)
```

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용에 대한 요약 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 잘못된 내용이 있는 경우 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.186-195
