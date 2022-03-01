---
layout: post
title: "[Python] import, module, package"
subtitle: ""
date: 2018-09-17 16:20:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, module, import, package , Introducing Python]
---

### 1. 모듈과 import 문
  - 모듈: 파이썬 코드로 작성된 하나의 파일을 의미
  - `import` 문을 이용하여 모듈을 추가할 수 있음

```python
# report.py
def get_description():
    """Return random weather, just like the pros"""
    from random import choice
    possibilities = ['rain', 'snow', 'sleet', 'fog', 'sun', 'who knows']
    return choice(possibilities)

# weatherman.py
# import 방식에 따른 코드 비교
# import 방식 1번
import report
description = report.get_description()
print("Today's weather: ", description)

# import 방식 2번
import report as wr
description = wr.get_description()
print("Today's weather: ", description)

# import 방식 3번
from report import get_description as do_it
description = do_it()
print("Today's weather: ", description)

# 실행결과
Today's weather:  snow
Today's weather:  sun
Today's weather:  fog
```
위의 예제 코드를 살펴보면 메인 프로그램 weather.py에서 모듈 report.py를 3가지 형태로 import하여 사용하는 방법을 보여준다.

첫 번째 방식의 경우 report 모듈 전체를 import하였다. get_description함수 앞에 report.을 붙여 메인 프로그램에서 사용하고 있음을 보여주고 있으며 모듈 이름으로 한정함으로써 다른 모듈과의 네이밍 충돌을 방지할 수 있다.

두 번째 방식의 경우 alias를 이용하였다. 원래 report라는 모듈의 이름을 메인 프로그램에서는 `wr`로 사용하겠다고 `as`문을 이용하여 새로운 이름을 붙여주었다. as문을 통해 이름이 충돌되는 것을 막을 수 있고, 모듈 이름이 길 경우 이를 간소화하여 사용할 수 있는 방법을 제공한다.

세 번째 방식의 경우 필요한 모듈만 import를 하였다. report 모듈의 get_description 함수만을 사용하도록 포함하였다. 이 방식 또한 alias를 이용할 수 있음을 예시 코드를 통해 확인할 수 있다.

---

#### 2. 모듈 검색 경로
파이썬은 모듈 경로(Path)를 어떻게 찾아서 import 하게 되는 것일까? 파이썬은 리스트 형태로 저장된 디렉터리 경로명과 표준 sys 모듈에 저장되어 있는 ZIP 아카이브 파일을 참조하여 모듈을 찾게 된다. 그러나 기본적으로 모듈을 검색할 때는 해당 .py이 저장된 현재 디렉터리를 먼저 검사하여 import 할 파일을 찾게 된다.

아래의 예시는 sys 모듈에 저장된 path 정보를 보여주는 코드와 결과이다.
```python
# 코드
import sys
for place in sys.path:
    print(place)

# 실행결과
/Users/dooseop/PycharmProjects/IntroducingPython
/Users/dooseop/PycharmProjects/IntroducingPython
/Library/Frameworks/Python.framework/Versions/3.7/lib/python37.zip
/Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7
/Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/lib-dynload
/Users/dooseop/PycharmProjects/IntroducingPython/venv/lib/python3.7/site-packages
/Users/dooseop/PycharmProjects/IntroducingPython/venv/lib/python3.7/site-packages/setuptools-39.1.0-py3.7.egg
/Users/dooseop/PycharmProjects/IntroducingPython/venv/lib/python3.7/site-packages/pip-10.0.1-py3.7.egg
/Applications/PyCharm.app/Contents/helpers/pycharm_matplotlib_backend
```

---

### 3. 패키지
  - 패키지는 앞서 설명한 모듈 파일들이 한데 모아 둔 계층구조의 폴더라 할 수 있다.
  - 파이썬은 \_\_init\_\_.py 파일을 포함하는 디렉터리를 패키지로 간주한다. (내용은 없어도 무관)

---

### 4. 파이썬 표준 라이브러리
  - 해당 내용은 향후 프로그램을 구현할 때 참조하면 되기 때문에 포스팅 내용 요약에서 생략

---

### 5. 다른 파이썬 코드 가져오기
표준 라이브러리에서 원하는 모듈이 없거나 사용하고자 하는 모듈이 정상적으로 동작하지 않을 때가 있다. 이러한 경우 3rd-party 오픈소스를 통해 원하는 모듈을 가져와 사용할 수 있다.
  - PyPI
  - github
  - readthedocs
  - activestate

<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용에 대한 요약 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 잘못된 내용이 있는 경우 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.145-151
