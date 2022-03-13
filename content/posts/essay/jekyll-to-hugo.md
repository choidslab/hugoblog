---
title: "Jekyll 블로그에서 Hugo 블로그로 이전 후기"
date: 2022-03-07T08:39:28+09:00
categories: [essay]
tags: [Hugo, 블로그, Netlify, 이전, 후기]
---

### 개요
지난 3월 초에 Hugo 블로그 구축을 완료했다. 세부적인 테마 설정, SEO, Google Analytics 등 몇 가지 추가 설정이 필요한 상황이지만 큰 틀에서 구축은 모두 완료한 상태이다. 내가 많은 분들의 도움을 받아 Hugo 블로그로 이전한 것 처럼 이 글을 보고 Hugo 블로그로 옮기려 하는 분들에게 도움이 될까하여 후기를 남긴다.

### Jekyll 블로그에서 Hugo 블로그로 이전
2018년 기술/학습 블로그의 필요성을 느껴 Jekyll, Github Page 기반의 블로그를 만들었다. 당시 유행?이었던 TIL(Today I Learned) 작성을 중심으로
블로그를 운영했다.([이전 블로그](tech.dslab.kr)) 블로그 내용은 부실했지만 기술/학습 블로그 운영이라는 노력을 좋게 봐준 한 스타트업에서 입사 제의 연락을 받았고, 취업도 할 수 있었다. 물론 취업을 하면서 흐지부지 글 작성을 오랜 기간 못하기도 했지만 어쨌든 블로그를 폐쇄하지 않고 운영은 계속했다.<br><br>
그렇게 시간이 흘러 2022년이 되었고, 새로운 마음으로 다시 기술/학습 블로그를 운영하고 싶은 마음과 함께 기존의 Jekyll에서 벗어나 다른 블로그 플랫폼으로 옮기고 싶다는 생각을 하게 되었고, 다음 이유들과 자료를 바탕으로 `Hugo`, `Netlify` 기반의 블로그로 이전하게 되었다.

### Hugo, Netlify 선택 이유

1. `카테고리 및 테마 관리의 편의성`
  - 개인적으로 Hugo가 Jekyll 보다 테마 관리와 카테고리 구성이 편리했다.
2. `속도`
  - Jekyll은 Ruby 언어 기반이고 Hugo는 Go 언어 기반이다. 다양한 자료를 검토한 결과 속도가 빠른 Hugo를 선택하게 되었다.
  - 글을 작성한 뒤, local에서 확인했을 때도 내용 바로 반영되어 작성하면서도 내용 확인을 빠르게 할 수 있었다. Flutter의 Hot reload 기능이 생각났다!
3. [Static Site Generator 비교 사이트](https://jamstack.org/generators/)
  - Static Site Generator 비교 사이트에서 자료를 보니 Hugo가 Jekyll 보다 Star 수도 높았다.
  - 단순히 Star가 높다고 좋은 것은 아니지만 1번과 2번 내용을 종합했을 때 최근에는 Jekyll 보다 Hugo가 더 인기 있는 것은 사실인 것 같다.
4. `Netlify` 호스팅 선택
  - Github Page 외에 호스팅 서비스를 무료로 제공하는 Netlify라는 것을 처음 알게 되었다.
  - Hugo를 Github Page로 호스팅할 경우 git submodule을 이용해야 하고, 결과적으로 [repository에 push를 각각 따로 2번 해줘야하는 번거로움](https://lena-chamna.netlify.app/post/how_to_make_hugo_blog_with_netlify/)이 있다는 사실을 알게 되었다.
  - 반면 Netlify는 Github Repository에 올려두고 해당 Repository 주소를 Netlify에 연결해주면 글을 작성하거나, 테마 설정파일을 수정할 경우 Repository 한 번만 push주면 바로 반영이 된다.

결과적으로 위와 같은 이유들로 `Hugo + Netlify`를 선택하게 되었다.

### Hugo 테마 선정
Jekyll에서 Hugo로 이전하면서 가장 먼저 한 작업은 Hugo 설치가 아니라 Hugo 테마를 선정하는 일이었다. 테마를 한 번 선택하면 다른 테마로 옮기는 일이 상당히 번거롭기 때문에 처음부터 마음에 딱 맞는 테마를 고르기 위해 시간 투자를 많이 했던 것 같다. 개인적으로 내가 테마를 선정한 기준은 다음과 같다.

1. 반응형일 것(모바일, 태블릿에서도 잘 보여야 하니까! 물론 Hugo 테마는 반응형 아닌 것이 없다.)
2. Dark Mode 지원
3. 카테고리 기능 지원

Hugo 테마는 [공식사이트](https://themes.gohugo.io/)에서 다양하게 찾아 볼 수 있다. 시간을 두고 이틀 정도 천천히 테마를 골라 보았고, 그 중 기준에 가장 적합한 `LoveIt` 테마를 선택하게 되었다.

### Hugo 설치
저는 `macOS 환경`에서 설치를 진행했습니다. Hugo 설치를 위해서는 다음 준비가 필요하며 설치는 공식 홈페이지를 참조하면 된다.

1. `Go 언어` 설치 - [Go 공식홈페이지](https://go.dev/doc/install)
2. `homebrew` 설치 - [homebrew 공식홈페이지](https://brew.sh/)  

Go, homebrew 설치가 완료되면 hugo 설치는 너무나 쉽습니다. 다음 명령어로 설치가 진행된다.
```
brew install hugo
```

hugo가 정상적으로 설치되었는지 확인하기 위해 다음 명령어를 입력하여 `hugo version`을 입력한다.
```
hugo version
```
저의 경우 2022.03.11 기준으로 `hugo v0.92.2+extended darwin/amd64 BuildDate=unknown`라는 결과가 출력된 것을 확인할 수 있었다.

### Hugo 블로그 사이트 설치
hugo 설치까지 완료되면 로컬에 hugo 블로그 사이트를 설치하는 것은 다음 명령어로 가능하다.
```
hugo new site <folder-name>
```
폴더이름은 나중에 Git Repository에 push 할 것을 감안하며 작명한다. 실행 후 `congratulations!...` 메시지가 출력되면 정상적으로 블로그가 생성된 것이다. Hugo 블로그의 기본 폴더 구조는 다음과 같다.
```
├── config.toml(Hugo 블로그 config 파일, 해당 파일에서 설정값 변경)
├── archetypes
├── content
├── data
├── layouts
├── resources
├── static
└── themes(테마 설치 위치)
```

### Hugo 테마 설치
테마 설치는 다음의 순서로 진행된다.
1. 블로그 사이트 생성 폴더로 경로 이동
2. `git init`으로 local repository 초기화
3. `git submodule add <theme git 다운로드 주소> <themes/theme-name>` 테마 설치
4. themes/theme-name 폴더에 있는 config.toml 파일을 복사, 기존에 생성된 config.toml 덮어쓰기
테마가 정상적으로 설치되었는지 확인하기 위해 터미널 창에서 `hugo server` 명령을 실행한 뒤, localhost 웹브라우저를 통해 확인한다.

### Hugo Github Repository에 올리기
Local Repository와 Remote Repository를 연결하는 작업이다.
대략적인 순서는 다음과 같다.
1. Github 접속 후, Hugo 블로그를 업로드할 Repository 생성
2. `git remote add origin <remote repository url>` 연결
3. `git commit -m "First Commit"`
4. `git push origin master`

큰 틀에서 위와 같은 스텝으로 진행하며, 필요에 따라 `.gitignore` 파일을 생성하여 불필요한 폴더들을 제외하면 된다. [참고: gitignore.io](https://gitignore.io/)

### 배포를 위한 Netlify(호스팅) 설정
Netlify는 처음 사용하는 것이었지만 생각보다 심플했다. Netlify에서 Hugo가 올라간 Github Repository를 연결해주면 끝!
간단하게 순서를 정리하면 다음과 같다.
1. Netlify 계정 생성
2. `Sites` > `Add new site` > `Import an existing project`
3. Connect to Git provider에서 Github 선택 > Github Authorized
4. Hugo 블로그가 업로드된 Repository 선택
  - `Branch to deploy`는 `master` 선택
5. Deploy Site

위의 단계를 거치면 배포가 완료된다. 배포된 Site를 선택하면 `Domain settings` 버튼을 눌러 주소를 확인할 수 있는데 Netlify에 배포된 사이트 주소는 기본적으로 `<customname>.netlify.app`으로 생성된다. Github page로 호스팅 할 경우 `<username>.github.io`와 같이 생성되는 것과 같다고 할 수 있다.

### 가비아(Gabia) 서브도메인(Subdomain) Netlify에 연결하기
netlify.app 도메인 주소 대신 개인 도메인을 연결하여 사용할 수 있다. 개인적으로 가비아를 통해 개인 도메인(dslabk.kr)을 구매해서 계속 사용해왔으며 Netfily 도메인 설정 기능을 통해 개인 도메인 연결이 가능했다. 나의 경우 서브도메인을 사용하여 이전 블로그(tech.dslab.kr)에 연결해서 사용하고 있었기에 이번에도 새로운 서브도메인을 생성하여 Hugo 블로그에 연결하기로 했다. 순서는 다음과 같다.

1. 가비아 > 등록 도메인 > DNS 관리 이동 및 설정
  - 타입: `CNAME`, 호스트: `서브도메인으로 사용할 이름`(나의 경우 `blog`로 입력)
  - 값/위치: `dschoi.netlify.app.`, TTL: `600`
2. Netlify > 생성된 Site > Domain settings > `Domain Management`
  - `Custom domains` 항목에서 `Add domain alias` 선택
  - `서브도메인 입력` > `Save` 선택(나의 경우 가비아 DNS 관리에서 호스트 값을 blog로 했기 때문에 서브도메인명은 blog.dslab.kr이 된다. 이 값을 입력하면 된다.)
3. 입력된 서브도메인 이름이 `Custom domains` 항목에 보여지게 되고, `Primary domain`이라 표시된다.

이 과정을 거치면 이제 netlify.app 주소뿐만 아니라 자신의 개인 서브도메인으로도 Hugo 블로그에 접속이 된다!

### 마무리하며
`Jekyll + Github Page` 블로그에서 `Hugo + Netlify` 블로그로 이전하는 과정에서 경험한 내용을 기록해보았다. 최대한 짧게 정리해보고 싶었고, 스크린샷도 첨부하여 누구나 보고 따라 할 수 있도록 내용을 정리하려고 했는데 시간 여건이 되지 않아 부득이 글로 굵직한 내용만 남겨보았다. <br><br>Hugo 블로그로 옮기며 Go언어를 몰라도 할 수 있을까 내심 걱정했지만 생각해보니 Jekyll 블로그를 만들 때도 Ruby를 전혀 몰랐고, Hugo로 옮긴 지금도 Go에 대해 잘 모른다. 즉, `누구나 다 Hugo 블로그를 만들 수 있다! :)` 테마도 마음에 들고, 배포도 정말 빨라서 Jekyll 블로그보다 만족도가 높다. 혹시 Hugo로 이전을 계획하고 계신분이 있다면 꼭 옮기시길 추천드린다. <br><br>

더 자세한 내용은 Hugo 공식 홈페이지와 아래의 참고 사이트를 통해 많은 도움을 받았으니 참고하면 좋을 듯 하다.

### 참고

[1] [Hugo Documents](https://gohugo.io/getting-started/quick-start/) <br>
[2] [Netlify 설정](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/#configure-a-subdomain)<br>
[3] [레나참나님 블로그](https://lena-chamna.netlify.app/post/how_to_make_hugo_blog_with_netlify/) <br>
[4] [한정수님 Github](https://github.com/Integerous/Integerous.github.io)  <br>
[5] [태태태님 블로그](https://taetaetae.github.io/) <br>
