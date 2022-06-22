---
layout: post
title: "[Python] 입력된 정수만큼 숫자 입력 받기"
subtitle: "Python Code Snippet"
date: 2022-06-22 21:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, selenium, pytube, automation]
---

## 개요
코딩 테스트 연습? 훈련?을 하면서 자주 사용되거나 기록해두면 좋을 것 같은 코드 조각을 블로그에 남기기로 했다. 
오늘 첫 코드 조각은 입력된 정수만큼 숫자를 입력 받아 리스트에 저장하는 코드이다.

## Code Snippet 
```python
# 정수 입력
n = int(input())
# n번 반복하면서 숫자를 입력 받아 List에 저장
nums = [int(input()) for _ in range(n)]
print(nums)
```
