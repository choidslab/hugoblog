---
layout: post
title: "[Python] 예외처리, try/except"
subtitle: ""
date: 2018-09-10 17:50:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, try, except , Introducing Python]
---

### 1. 예외처리
  - 어떤 상황에서 실패할 수 있는 코드를 실행했을 때 잠재적인 에러를 방지하기 위해 `예외처리`가 필요하다.
  - 파이썬에서는 `try/except` 구문 사용
  - 에러가 예상되는 코드에 `try`문 사용, 에러 처리를 위해서는 `except`문 사용

```python
>>> short_list = [1, 2, 3]
>>> position = 5
>>> try:
       short_list[position]
>>> except:
       print('Need a position between 0 and', len(short_list)-1, ' but got', position)

Need a position between 0 and 2  but got 5
```
try 블록 안의 코드를 실행할 때 에러가 발생하며 예외가 발생한다. 예외가 발생하면 except 블록에 구현된 코드가 실행된다. 만약 try 블록 내의 코드에서 에러가 발생하지 않을 경우에는 except 안의 코드는 실행되지 않고 건넌뛰게 된다. 위의 예시코드와 같이 except에 어떠한 인자도 없는 경우 모든 예외 타입을 잡는다는 것(Catch)을 의미한다. 따라서 특정 에러에 대한 예외 처리를 해주기 위해서는 다음과 같이 코드를 작성해야 한다.

`except 예외 타입 as 이름`

다음 예시코드는 IndexError에 대해 보여준다.
```python
short_list = [1, 2, 3]
while True:
    value = input('Position [q to quit]?')
    if value == 'q':
        break
    try:
        position = int(value)
        print(short_list[position])
    except IndexError as err:
        print('Bad index:', position)
    except Exception as other:
        print('Something else broke:', other)

# 실행 결과
Position [q to quit]?1
2
Position [q to quit]?0
1
Position [q to quit]?2
3
Position [q to quit]?3
Bad index: 3
Position [q to quit]?two
Something else broke: invalid literal for int() with base 10: 'two'
Position [q to quit]?q
```
3을 입력하면 IndexError가 발생한다. 그리고 two를 입력하면 모든 예외를 처리하는 두 번째 예외 코드에서 int() 함수에 대한 예외가 발생하는 것을 확인할 수 있다.

---

### 2. 예외 만들기
모든 예외는 파이썬 표준 라이브러리에 이미 정의되어 있다. 따라서 필요한 예외 처리를 선택해서 활용할 수 있다. 프로그래머는 예외를 만들어 사용할 수 있는데 이 때 예외의 타입을 정의하기 위해 클래스(Class)를 활용한다. (클래스의 자세한 내용은 6장에서 학습) 예외는 클래스이고, `Exception 클래스`를 상속하여 정의할 수 있다. (Exception 클래스의 하위 클래스) 다음의 예시코드는 words 문자열에 대문자가 있을 경우 예외를 발생시키는 UppercaseException 예외를 만든 것이다. 예외는 `raise` 키워드를 통해 발생시킬 수 있다.

```python
class UppercaseException(Exception):
    pass

words = ['eeenie', 'meenine', 'NO', 'miny']

for word in words:
    if word.isupper():
        raise UppercaseException(word)

#실행 결과 (에러 발생)
Traceback (most recent call last):
  File "/Users/dooseop/PycharmProjects/IntroducingPython/chapter4.py", line 32, in <module>
    raise UppercaseException(word)
__main__.UppercaseException: NO
```


<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용을 요약한 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 또한, 잘못된 내용이나 모호한 내용이 있는 경우 전문가분들께서 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 읽어주셔서 감사합니다.



<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.145-151
