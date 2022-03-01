---
layout: post
title: "Page build failed: Symlink does not exist"
subtitle: ""
date: 2018-08-28 12:10:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [github, Symlink]
---

### [Problem]

github 블로그를 만들 때 'git push' 후, 아래와 같은 에러가 발생하였다.

>The page build failed for the master branch with the following error: The symbolic link `/vendor/bundle/gems/ffi-1.9.25/ext/ffi_c/libffi-i386/include/ffitarget.h` targets a file which does not exist within your site's repository. For more information, see https://help.github.com/articles/page-build-failed-symlink-does-not-exist-within-your-site-s-repository/

해당 문제 발생 후, Github 블로그 페이지가 정상적으로 Load 되지 않거나, 수정된 내용이 블로그 페이지에 반영되지 않음을 확인했다.

### [Solution]

구글 검색을 통해 해당 문제가 발생하는 원인은 github 블로그 페이지와 관련된 vendor 디렉터리 내용을 commit했기 때문임을 알 수 있었다. 해당 문제는 '.gitignore'에 vendor 디렉터리를 추가함으로써 해결이 가능하다.

1. `.gitignore` 파일을 열어 `vendor/\*\*`를 추가하고, 저장.
2. git으로 versioning 되고 있는 vendor/를 삭제하기 위해 다음 명령을 실행
  * `git rm --cached -r vendor/`
3. git add, git commit, git push를 수행한다.
* `git add . *`
* `git commit -m 'remove vendor from versioning'`
* `git push origin master**`

위의 과정을 수행한 뒤, github -> Settings -> GitHub Pages에서 `Your site is published at https://dslab0915.github.io/`와 같이 활성화 되면 정상적으로 github 블로그 페이지가 로드되는 것을 확인할 수 있다.

### [Reference]

[1] https://stackoverflow.com/questions/49867220/jekyll-website-wont-load
