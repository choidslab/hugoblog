---
layout: post
title: "[Python] 함수(Function)"
subtitle: ""
date: 2018-09-10 13:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, function, Introducing Python]
---

### 1. 함수(Function)
함수는 코드의 재사용성을 높여준다. 함수는 크게 정의(Define)와 호출(Call)에 의해 동작되며 다음과 같은 일을 수행한다.
  - 값의 입력, 전달(argument, parameter)
  - 함수 내부 구조에 의한 값 처리
  - 값 반환(return)

함수의 호출 부분에서 처리할 값을 전달하는데 이 때 전달해주는 값을 전달인자(argument)라 하고, 전달인자의 값이 복사되어 실제 함수가 정의된 부분에 선언된 매개변수(parameter)로 값이 전달 된다.

파이썬에서 함수의 정의는 `def` 키워드를 통해 정의되며 마지막에는 콜론(:)을 붙여준다. 함수의 기본 구조는 다음과 같다.

```python
def do_something(parameter):
    statement
```

함수에 반드시 매배견수가 필요한 것은 아니다. 함수에의 매개변수 값을 생략해도 동작하는 함수도 존재한다. 아래의 함수는 `True` 값을 반환하는 매개변수 없는 함수의 예시를 보여준다.

```python
def agree():
    return True
```

---

### 2. 위치 인자(Positional Arguments)
파이썬은 함수의 인자를 유연하게 처리할 수 있다. 값을 순서대로 상응하는 매개변수에 복사하는 위치 인자를 지원한다. 다음 함수는 위치 인자로 딕셔너리를 만들어 반환한다. 함수 호출 부분에 순서대로 입력된 인자 값이 함수의 정의된 위치에 순서대로 전달된 것을 결과 값을 통해 확인할 수 있다. 위치 인자를 정확히 활용하기 위해서는 각 위치별 인자 값의 의미를 알고 있어야 한다.
```python
>>> def menu(wine, entree, dessert):
>>>     return {'wine':wine, 'entree':entree, 'dessert':dessert}
>>> menu('chardonnay','chicken','cake')
{'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'cake'}
```

---

### 3. 키워드 인자(Keyword Arguments)
키워드 인자는 앞서 설명한 위치 인자의 위치 의미를 알아야만 하는 단점을 보완할 수 있게 해준다. 즉, 매개변수에 상응하는 이름을 지정하여 위치에 상관 없이 이름을 통해 매개변수의 위치에 관계 없이 정확히 값을 전달해 줄 수 있다. 아래는 키워드 인자를 사용한 예시이다.(키워드 인자와 위치 인자는 함께 사용할 수 있다.)
```python
# 키워드 인자를 사용한 예제
>>> menu(entree='beef', dessert='bagel', wine='bordeaux')
{'wine': 'bordeaux', 'entree': 'beef', 'dessert': 'bagel'}

# 위치 인자, 키워드 인자를 함께 사용한 예제
>>> menu('frontenac', dessert='flan', entree='fish')
{'wine': 'frontenac', 'entree': 'fish', 'dessert': 'flan'}
```

---

### 4. 기본 매개변수 값 지정하기(Default Parameter)
함수의 매개변수에 기본값을 지정하여 사용할 수 있다. 함수를 호출하는 위치에서 매개변수에 대응하는 전달인자 값을 제공하지 않을 경우, 기본 매개변수 값을 사용하게 된다. 다음은 예제 코드이다.

```python
# Default parameter 지정 (dessert='pudding')
>>> def menu(wine, entree, dessert='pudding'):
	return {'wine':wine, 'entree':entree, 'dessert':dessert}
# dessert 값을 지정하지 않고 함수를 호출한 경우
>>> menu('chardonnay', 'chicken')
{'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'pudding'}
# dessert 값에 'doughnut' 값을 전달하여 함수를 호출한 경우
>>> menu('dunkelfelder','duck','doughnut')
{'wine': 'dunkelfelder', 'entree': 'duck', 'dessert': 'doughnut'}

```
<br>

#### 5. 위치 인자 모으기: `* (Asterisk)`
함수의 매개변수에 애스터리스크를 사용할 때, 매개변수에서 위치 인자 변수들을 튜플로 묶어준다. 다음의 예제를 살펴보자.
```python
# 가변인자 *args
>>> def print_args(*args):
        print('Positional argument tuple:', args)
# 함수 호출 시 값을 전달하지 않았을 경우 결과        
>>> print_args()
Positional argument tuple: ()
# 함수 호출 시 여러 값을 전달한 경우 결과
>>> print_args(1, 2, 'test')
Positional argument tuple: (1, 2, 'test')
```
애스터리스크를 통해 전달된 인자를 모두 취할 수 있게 한다. `*`를 사용할 때 가변 인자의 이름으로 `args`를 관용적으로 사용한다.

<br>

#### 6. 키워드 인자 모으기: `**`
키워드 인자를 딕셔너리로 묶기 위해 2개의 애스터리스크를 사용한다. 인자의 이름은 key 값이 되고, 값은 딕셔너리 key의 값이 된다. 다음 예시 코드를 통해 키워드 인자가 어떻게 딕셔너리를 표현되는지 확인할 수 있다.
```python
>>> def print_kwargs(**kwargs):
        print('Keyword arguments:', kwargs)
>>> print_kwargs(wine='melot', entree='mutton',dessert='marcaroon')
Keyword arguments: {'wine': 'melot', 'entree': 'mutton', 'dessert': 'marcaroon'}
```
`**kwargs`에 전달된 키워드는 딕셔너리에서 key 값으로, 키워드의 값은 딕셔너리 key 값에 대응되는 값으로 저장된 것을 확인할 수 있다.

#### 7. 내부 함수
파이썬은 함수 안에 또 다른 함수를 정의할 수 있다.

```python
>>> def outer(a, b):
        def inner(c, d):
            return c + d
        return inner(a, b)
>>>outer(4, 7)
11
```
내부(Inner) 함수는 루프(Loop)나 코드 중복을 피하기 위해 또 다른 함수 내에 복잡한 작업을 한 번 이상 수행할 때 유용하게 사용된다.

#### 8. 익명 함수: lambda()
파이썬의 람다 함수(Lambda Function)는 단일문으로 표현되는 익명 함수(Anonymous Function)이다. 다음은 예시 코드이다.

```python
# 람다 함수를 사용하지 않고, 일반 함수를 활용하여 출력한 결과
>>> def edit_story(words, func):
        for word in words:
            print(func(word))
>>> stairs = ['thud','meow','thud','hiss']
>>> def enliven(word):
        return word.capitalize() + '!'
>>> edit_story(stairs, enliven)
Thud!
Meow!
Thud!
Hiss!

# 다음은 람다 함수를 활용한 출력 결과
>>> edit_story(stairs, lambda word: word.capitalize() + '!')
Thud!
Meow!
Thud!
Hiss!
```
람다 함수를 통해 enliven()함수를 단일문으로 간단하게 처리할 수 있음을 확인할 수 있다. 대부분의 경우에는 enliven()과 같이 실제 함수를 정의하여 사용하는 것이 훨씬 명확하다. 람다 함수는 많은 작은 함수를 정의하고, 이를 호출하여 얻은 결과값을 저장하는 경우 유용하게 사용될 수 있다.

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용을 요약한 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 또한, 잘못된 내용이나 모호한 내용이 있는 경우 전문가분들께서 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 읽어주셔서 감사합니다.


<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.126-140
