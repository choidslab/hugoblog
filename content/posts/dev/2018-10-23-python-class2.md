---
layout: post
title: "[Python] class, get/set, property, private, name mangling"
subtitle: ""
date: 2018-10-23 20:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, class, getter, setter, name convention, private, name mangling, property, decorator, Introducing Python]
---

### 1. get/set 함수
  - Java, C++ 등 일부 언어에서는 클래스 멤버 변수에 직접 접근을 제어하는 `private` 속성을 지원
  - 이러한 private 변수에 접근하기 위해 setter/getter 함수를 이용
  - 하지만, Python에서는 모든 속성이 `public`
  - Python에서 클래스 멤버 변수에 접근하는 것을 제한하는 방식
    - setter/getter 함수
    - `property`
    - 멤버변수 앞에 `__` 더블 언더스코어 추가(private naming convention)

```python
# 1. getter/setter 함수를 이용하여 완벽하지 않은 private 구현
class Duck():
    def __init__(self, input_name):
        self.hidden_name = input_name
    def get_name(self):
        print("inside the getter")
        return self.hidden_name
    def set_name(self, input_name):
        print("inside the setter")
        self.hidden_name = input_name
    name = property(get_name, set_name)

if __name__ == "__main__":
    fowl = Duck("Howard")
    print(fowl.name)
    print(fowl.get_name())

    fowl.name = "Tim"
    print(fowl.name)
```

---

### 2. property 데커레이터를 이용한 변수 private 구현
  - 앞서 언급한 코드의 경우 get_name(), set_name() 함수를 직접 호출 할 수 있기 때문에 멤버 변수를 완벽히 private하게 할 수 없음
  - `property` 데커레이터를 통해 문제 해결  

```python
class Duck():
    def __init__(self, input_name):
        self.hidden_name = input_name

    @property # getter
    def name(self):
        print("inside the getter")
        return self.hidden_name

    @name.setter
    def name(self, input_name):
        print("inside the setter")
        self.hidden_name = input_name

if __name__ == "__main__":
    fowl = Duck("Howard")
    print(fowl.name)

    # 아래와 같은 접근은 불가능
    # print(fowl.get_name())

    fowl.name = "Tim"
    print(fowl.name)
```

  - 앞선 예제코드와 달리 직접 getter/setter 함수에 접근할 수 없음
  - property 데커레이터를 통해 name을 속성에 접근하듯 할 수 있음
  - 하지만, 코드를 호출하는 위치에서 hidden_name이라는 변수를 알고 있을 경우 여전히 직접 접근이 가능

---

### 3. 클래스 멤버 변수 접근제어를 위한 Name Mangling

  - 클래스 외부에서 멤버 변수를 볼 수 없도록 하는 변수 네이밍 컨벤션이 있음
  - 클래스 외부에서 감추고자 하는 변수 앞에 `__` 언더스코어를 2번 붙여주면 됨(Name Mangling)
  - 다음 예제코드에서는 앞선 예제의 `self.hidden_name`을 `self.__name`으로 수정
  - 멤버에 직접 접근할 경우(아래의 `dk.name` 부분) `AttributeError: 'Duck' object has no attribute '__name'` Error 발생

```python
class Duck():
    def __init__(self, input_name):
        # double underscore
        self.__name = input_name

    @property
    def name(self):
        print("inside getter")
        return self.__name

    @name.setter
    def name(self, input_name):
        print("inside setter")
        self.__name = input_name

if __name__ == "__main__":
    dk = Duck("DS")

    print(dk.name)
    print(dk.__name)
```

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용에 대한 요약 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 잘못된 내용이 있는 경우 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.180-186
