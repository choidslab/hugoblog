---
layout: post
title: "[Python] class, 상속, 함수 Override, super()"
subtitle: ""
date: 2018-10-15 23:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, class, inheritance, override, Introducing Python]
---

### 1. 객체(object)와 클래스(class)
  - Python에서는 모든 것이 `객체`
  - 숫자, 문자, 문자열 등...
  - 객체는 데이터(변수 또는 속성)와 코드(함수 또는 메소드)를 포함한다.
  - 객체는 `class`에 의해 생성

```python
class Person():
    # 객체 초기화를 위한 __init__ 함수
    def __init__(self, name):
        self.name = name

if __name__ == "__main__":
    someone = Person("nick")
    print(someone.name)

# 실행결과
# nick
```
  - class는 객체를 만드는 틀, class를 통해 여러개의 객체를 생성
  - 객체의 초기화를 위해 class 내부에 `__init__`함수 선언
  - `__init__` 함수의 첫 번째 매개변수는 `self`, self는 특정 객체 자신을 의미
  - 위의 예제코드 동작 순서
    - Person 클래스의 정의를 찾음
    - 새로운 객체를 메모리에 생성
    - 객체의 `__init__` 함수를 호출, 새로 생성된 객체를 self에 전달하고, 다음으로 초기화 문자열 `"nick"`을 전달
    - `self.name`을 전달된 문자열로 초기화
    - 새로운 객체를 반환
    - someone 객체를 연결

---

### 2. 상속(Inheritance), 오버라이드(Override)
  - 기존의 클래스에 새로운 기능을 추가하거나 변경하여 코드의 재사용성을 높이는 객체지향언어의 개념
  - 기존 클래스의 함수는 상속된 클래스에서 재정의(오버라이드) 할 수 있음
  - 상위 클래스: 부모 클래스, 상위 클래스, 슈퍼(Super) 클래스, 베이스(Base) 클래스
  - 하위 클래스: 자식 클래스, 하위 클래스, 서브(Sub) 클래스, 파생된(Derived) 클래스

```python
class Car():
    def exclaim(self):
        print("I'm a Car")

class Yugo(Car):
    # 함수 오버라이드
    def exclaim(self):
        print("I'm a Yugo! Much like a Car, but more Yugo-ish.")

give_me_a_car = Car()
give_me_a_yugo = Yugo()

give_me_a_car.exclaim()
give_me_a_yugo.exclaim()
```

  - 상위 클래스 Car()로부터 상속된 Yugo() 클래스의 exclaim() 함수는 상위 클래스와 다른 동작을 하고 있음
  - 이와 같이 상속받은 함수를 하위 클래스에서 재정의 하는 것을 오버라이드(Override)라고 함
  - 또한, 다음 예제코드와 같이 상위 클래스에는 없는 함수를 하위 클래스에 추가로 정의할 수 있음

```python
class Car():
    def exclaim(self):
        print("I'm a Car")

class Yugo(Car):
    # 함수 오버라이드
    def exclaim(self):
        print("I'm a Yugo! Much like a Car, but more Yugo-ish.")
    # 하위 클래스에서 추가된 함수
    def need_a_push(selfs):
        print("A little help here?")

give_me_a_car = Car()
give_me_a_yugo = Yugo()

give_me_a_car.exclaim()
give_me_a_yugo.exclaim()
give_me_a_yugo.need_a_push() # 하위 클래스에 추가된 함수 호출
```

---

### 3. super() 함수
  - 하위 클래스에서 상위 클래스의 함수를 호출하는 방법
  - `super()` 함수
  - 다음 예제코드는 하위 클래스에서 super()함수를 이용하여 상위 클래스의 __init__() 함수를 명시적으로 호출하여 name 값을 초기화 하는 것을 보여준다.

```python
class Person():
    def __init__(self, name):
        self.name = name

# Person 클래스를 상속
class EmailPerson(Person):
    def __init__(self, name, email):
        # 상위 클래스 Person의 __init__함수를 이용하여 name 값을 초기화
        super().__init__(name)
        self.email = email

if __name__ == "__main__":
    p1 = EmailPerson("Kim", "Kim@kim.com")
    print(p1.name + ' & ' + p1.email)
# 실행결과
# Kim & Kim@kim.com
```


<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용에 대한 요약 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 잘못된 내용이 있는 경우 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.171-180
