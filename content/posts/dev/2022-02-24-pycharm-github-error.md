---
layout: post
title: "Pycharm Github 'Request response: Bad credentials'"
subtitle: ""
date: 2022-02-24 08:00:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, pycharm, ide, github, error]
---

### Pycharm Github 연결 에러

Python 프로그래밍 시 Pycharm을 주로 사용하고 있다.
그리고 macOS 기준 `Pycharm > Preferences > Version Control >  Github`를 통해 Github Repository와 연결하여 사용 중이다.
그런데 갑자기 아래와 같이 `Request response: Bad credentials`라는 오류 메시지와 함께 Github 연결에 문제가 발생하였다.
<br>
![]({{site.url}}/assets/post_img/python/pycharm_github1.png)

해결 방법은 생각보다 간단했다. 연결된 Github 계정을 삭제한 뒤,
다시 연결해주면 다음과 같이 문제 없이 정상적으로 Pycharm, Github 연결이 완료되는 것을 확인할 수 있었다.
![]({{site.url}}/assets/post_img/python/pycharm_github2.png)

요약하면 Pycharm과 Github 연결 시 `Request response: Bad credentials`에러가 발생하면 계정을 다시 연결해주면 해결된다.
