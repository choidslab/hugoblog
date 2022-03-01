---
layout: post
title: "[Python] Generator, Decorator, enumerate"
subtitle: ""
date: 2018-09-10 17:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, generator, decorator, enumerate, Introducing Python]
---

### 1. 제너레이터(Generator)
제너레이터는 파이썬에서 어떤 시퀀스를 생성하는 객체를 의미한다. 특히, 제너레이터는 이터레이터(Iterator)의 소스롤 자주 활용된다. 대표적인 제너레이터로는 `range()` 함수가 있다. 제너레이터는 제너레이터 함수로 함수 형태로 쓰일 수도 있는데 이 때 일반 함수와 달리 return이 아닌 `yield`문으로 값을 반환하게 된다. yield문은 간단히 말해 제너레이터 객체로 반환을 한다는 의미이다. 다음은 제너레이터의 예시 코드이다.

```python
# yield문을 통해 제너레이터 함수를 작성한 예시코드
>>> def my_range(first=0, last=10, step=1):
        number = first
        while number < last:
            yield number
            number += step
>>> my_range
<function my_range at 0x10d80be18>
# my_range()함수를 호출한 결과, 제너레이터 객체가 반환된 것을 확인할 수 있다.
>>> ranger = my_range(1, 5)
>>> ranger
<generator object my_range at 0x10d7dba98>
# 제너레이터 객체는 이터레이터의 소스가 되기 때문에 for문을 통해 순회하면서 제너레이터 객체가 갖고 있는 값을 출력할 수 있다.
>>> for x in ranger:
        print(x)
1
2
3
4

```

---

### 2. 데코레이터(Decorator)
미리 선언된 함수의 소스코드를 바꾸지 않고 함수의 기능을 수정하고 싶을 때 활용할 수 있는 기능이 데코레이터이다. 일반적인 예는 함수에 전달된 인자를 보기 위해 디버깅 문을 추가하는 것이다. 즉, `데코레이터는 하나의 함수를 취해 또 다른 함수를 반환하는 함수`이다. 이를 위해 다음 3가지를 활용한다.
  - *args와 **kwargs
  - 내부 함수
  - 함수 인자

다음의 document_it() 함수는 데코레이터를 설명하기 위한 함수이다. 해당 함수는 다음과 같이 데코레이터를 정의한다.
  - 함수 이름과 인자값 출력
  - 인자로 함수를 실행
  - 결과 출력
  - 수정된 함수를 사용할 수 있도록 반환

```python
# 데코레이터 함수 정의
>>> def document_it(func):
      def new_function(*args, **kwargs):
            print('Running function:', func.__name__)
            print('Positional arguments:', args)
            print('Keyword arguments:', kwargs)
            result = func(*args, **kwargs)
            print('Result:', result)
            return result
      return new_function
```
document_it() 함수는 어떤 func ㅎ마수 이름을 전달해도 new_function()이라는 새로운 함수를 얻게 된다. 다음은 데코레이터의 사용 방법을 보여준다. 사용방법은 수동으로 할당하는 방식과 자동으로 할당하는 방식이 있다.

```python
# 두 정수를 더하는 함수
>>> def add_ints(a, b):
        return a + b
>>> add_ints(3, 5)
8
# 데코레이터에 add_ints()함수를 수동으로 할당하는 방법, 반환된 새로운 함수는 cooler_add_ints에 저장
# document_it()에 정의된 새로운 형태의 함수를 통해 결과 값이 출력되는 것을 확인할 수 있음
>>> cooler_add_ints = document_it(add_ints)
>>> cooler_add_ints(3, 5)
Running function: add_ints
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 8
8

# 다음은 자동으로 데코레이터를 할당하는 방법은 '@데코레이터_이름'을 추가하면 된다.
>>> @document_it
def add_ints(a, b):
    return a + b
>>> add_ints(3, 5)
Running function: add_ints
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 8
8
```

---

### 3. enumerate
```python
for i, name in enumerate(['Tom', 'Choi', 'Steve']):
  print(i, name)

# 실행결과
0 Tom
1 Choi
2 Steve
```

  - `enumerate`는 순서가 있는 type(리스트, 튜플, 문자열)을 입력으로 받아 각 요소의 인덱스와 값을 함께 출력해주는 기능을 한다.
  - `enumerate(순환가능한 자료형, 시작값)` 첫 번째 인자로 순환가능한(iterable) 값을 전달하고, 두 번째 인자로 인덱스 시작 값을 지정할 수 있다. 예를 들어 1로 지정한다면 인덱스의 시작은 원래 0부터지만 0이 아닌 1로 계산하여 위의 실행결과에서 `0 Tom --> 1 Tom`으로 바뀌어 출력된다.
  - 인덱스 시작을 0이 아닌 1로 시작하는 것이지 두 번째 요소부터 출력되는 것이 아님에 주의하자.

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용을 요약한 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 또한, 잘못된 내용이나 모호한 내용이 있는 경우 전문가분들께서 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 읽어주셔서 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.141-145
