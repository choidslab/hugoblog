---
layout: post
title: "[Python] datetime, time 모듈"
subtitle: ""
date: 2018-10-30 18:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, datetime, time]
---

### 1. datetime 모듈  

```python
>>> from datetime import date
>>> halloween = date(2015,10,31) # halloween 객체 생성
>>> halloween
datetime.date(2015, 10, 31)
>>> halloween.day # day, month, year 속성을 통해 값에 접근
31
>>> halloween.month
10
>>> halloween.year
2015
>>> date.today() # 오늘 날짜 출력
datetime.date(2018, 10, 30)
```

  - `datetime` 모듈은 4개의 주요 객체를 갖는다.
    - `date`: 년/월/일
    - `time`: 시/분/초/마이크로초
    - `datetime`: 날짜/시간
    - `timedelta`: 날짜 또는 시간 간격
  - `date.today()`를 통해 오늘 날짜 정보를 확인할 수 있음

```python
>> from datetime import time
>> noon = time(12,0,0)
>> noon
datetime.time(12, 0)
>> noon.hour
12
>> noon.minute
0
>> noon.second
0
>> noon.microsecond
0
```

  - datetime 모듈의 `time` 객체는 시간 정보를 표현하는데 사용된다.
  - `hour`, `minute`, `second`, `microsecond` 속성을 통해 각각 시간/분/초/마이크로초 정보를 표현할 수 있다.

---

### 2. time 모듈

```python
>>> import time
>>> now = time.time()
>>> now
1540890403.521025 # epoch 값으로 표현된 시간 정보
```

  - 파이썬에는 datetime 모듈의 time 객체와 별도로 `time` 모듈이 존재한다. time 모듈에는 `time()` 함수가 있다.
  - 시간을 나타내는 한 가지 방법에는 어떤 시작점을 기준으로 시간의 초를 세는 에포(epoch) 방식이 있다. 예를 들면 유닉스에서는 1970.01.01 자정을 기준으로 시간을 계산한다. 이러한 epoch 방식은 시스템 간 날짜와 시간 정보를 교환하는 방법으로 쓰인다.
  - time 모듈의 time() 함수는 현재 시간을 epoch 값으로 반환한다.

```python
>>> import time
>>> now = time.time()
>>> time.ctime(now)
'Tue Oct 30 18:06:43 2018' # ctime() 함수를 이용하여 epoch 값을 문자열로 변환한 결과
>>> time.localtime(now)
time.struct_time(tm_year=2018, tm_mon=10, tm_mday=30, tm_hour=18, tm_min=6, tm_sec=43, tm_wday=1, tm_yday=303, tm_isdst=0)
>>> from datetime import date
>>> some_day = date(2015, 12, 12)
>>> fmt = "It's %B %d, %Y, local time: %I:%M:%S%p"
>>> some_day.strftime(fmt)
"It's December 12, 2015, local time: 12:00:00AM"
```

  - epoch 값은 `ctime()` 함수를 이용하여 문자열로 변환이 가능하다.
  - 날짜, 시간 정보를 얻기 위해 time 모듈의 `struct_time` 객체를 사용한다.
  - `localtime()` 함수는 시간을 시스템 표쥰시간 정보로 표현하며, `gmtime()` 함수는 UTC 기준의 시간정보를 제공한다.
  - `strftime()` 함수를 이용하여 날짜와 시간을 문자열로 변환할 수 있다. strftime()은 문자열 출력 포맷 지정이 가능하다.
    - `%Y: 년(1900~)`
    - `%m: 월(01~12)`
    - `%B: 월 이름(January, ...)`, `%b: 월 축약 이름(Jan, ...)`
    - `%d: 월의 일자(01~31)`
    - `%A: 요일 이름(Sunday, ...)`, `%a: 요일 축약 이름(Sun, ...)`
    - `%H: 24시간 표현(00~23)`, `%I: 12시간 표현(01~12)`
    - `%p: 오전/오후(AM,PM)`
    - `%M: 분(00~59)`
    - `%S: 초(00~59)`

---


<br>

>본 포스팅 내용은 `처음시작하는 파이썬(Introducing Python)`을 학습한 내용에 대한 요약 글입니다. 코드에 문제가 있을 수 있으며 다소 부정확한 내용이 있을 수 있으니 참고하시기 바랍니다. 잘못된 내용이 있는 경우 덧글로 남겨주시면 내용을 반영하여 수정하도록 하겠습니다. 감사합니다.

<br>

---

#### [Reference]

[1] 처음시작하는 파이썬(Introducing Python), p.330-339
