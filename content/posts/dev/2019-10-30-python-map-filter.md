---
layout: post
title: "[Python] lambda, map, filter"
subtitle: ""
date: 2019-10-30 22:30:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, lambda, map, filter]
---

### lambda
---
  - `lambda` 함수는 복잡하지 않은 짧고, 간결한 형태의 함수를 구현할 때 쓰임
  - def 키워드를 사용하지 않고 함수 선언

```python
pow = lambda num1, num2: num1 ** num2
result = pow(2, 10)
```
<br>

### map
---
  - `map`은 첫 번째 argument로 `함수이름` 전달, 두 번째 argument로 `iteratable`타입의 데이터 전달
  - map은 전달된 iteratable 데이터의 각 요소를 하나씩 첫 번째 인자로 입력된 함수에 전달하여 처리 후 결과를 반환

```python
# map을 이용하여 리스트 데이터의 각 요소 값을 +1씩 증가시키기
def increment(x):
    return x + 1

list(map(increment, [1, 2, 3, 4]))
```
<br>

### filter
---
  - `filter`는 단어 뜻 그대로 데이터를 걸러내는 기능을 하는 파이썬 내장함수
  - lambda 함수와 결합하여 많이 사용
  - 첫 번째 argument로 `함수이름` 전달, 두 번째 argument로 `iteratable`타입의 데이터 전달

```python
# 리스트 데이터 중 양수인 값만 새로운 리스트로 추가
# def 함수 사용
def positive():
    return x > 0
print(list(filter(positive, [-1, 0, 10, -3, 8, -7])))

# lambda 함수 사용
print(list(filter(lambda x: x>0, [-1, 0, 10, -3, 8, -7]))
```

---

#### [Reference]

[1] [점프 투 파이썬](https://wikidocs.net/32)  
