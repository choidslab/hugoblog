---
layout: post
title: "[Python] Youtube 영상 다운로드(with youtube_dl)"
subtitle: ""
date: 2019-09-10 21:30:00 +0900
comments: true
author: DSLab
background: '/img/bg-index.jpg'
categories: [dev]
tags: [python, youtube_dl]
---

### youtube-dl 라이브러리  
  - youtube-dl은 CLI 기반의 유투브 영상 다운로드 프로그램이다.
  - 설치 후, 터미널 환경에서 명령어 형태로 실행이 가능하며 Python 코드로도 실행 가능하다.
  - youtube-dl의 장점은 다양한 `options`을 통해 자막, Thumbnail 이미지, 원하는 화질의 영상 선택 등이 가능하다는 점과 현재까지 꾸준히 코드가 업데이트 되고 있다는 점이다.
  - youtube 영상을 다운로드 받을 수 있는 또 다른 Python 패키지로 `pytube`가 있으나 github 업데이트가 중단된지 오래되었다.

### 예제 코드
```python
import os
import youtube_dl

VIDEO_DOWNLOAD_PATH = './'  # 다운로드 경로

def download_video_and_subtitle(output_dir, youtube_video_list):

    download_path = os.path.join(output_dir, '%(id)s-%(title)s.%(ext)s')

    for video_url in youtube_video_list:

        # youtube_dl options
        ydl_opts = {
            'format': 'best/best',  # 가장 좋은 화질로 선택(화질을 선택하여 다운로드 가능)
            'outtmpl': download_path, # 다운로드 경로 설정
            'writesubtitles': 'best', # 자막 다운로드(자막이 없는 경우 다운로드 X)
            'writethumbnail': 'best',  # 영상 thumbnail 다운로드
            'writeautomaticsub': True, # 자동 생성된 자막 다운로드
            'subtitleslangs': 'en'  # 자막 언어가 영어인 경우(다른 언어로 변경 가능)
        }

        try:
            with youtube_dl.YoutubeDL(ydl_opts) as ydl:
                ydl.download([video_url])
        except Exception as e:
            print('error', e)


if __name__ == '__main__':

    youtube_url_list = [  # 유투브에서 다운로드 하려는 영상의 주소 리스트(아래는 Sample Video 리스트)
        "https://www.youtube.com/watch?v=dP15zlyra3c",
        "https://www.youtube.com/watch?v=0EiV-ERKRRs",
        "https://www.youtube.com/watch?v=-CoApUAZFf8",
        "https://www.youtube.com/watch?v=M25AP_KPwlI"
    ]
    download_video_and_subtitle(VIDEO_DOWNLOAD_PATH, youtube_url_list)
    print('Complete download!')
```
youtube_dl을 활용하여 영상과 자막, Thumbnail을 다운로드 받는 간단한 예제 코드를 작성해보았다. 유투브 영상의 Video ID값이 포함된 주소 리스트를 넘겨주면 option에 설정된 조건에 맞는 데이터(영상, 자막, 이미지)를 다운로드 받게 된다.
youtube_dl 사용법은 굉장히 간단하지만, options 값을 어떻게 설정해주어야 하는지 다소 어려움이 있었다. youtube_dl 도큐먼트와 구글 검색을 통해 필요한 options 값을 넣어주면 원하는 조건의 데이터를 다운로드 받을 수 있다.
굉장히 간단한 코드이지만 향후 원하는 영상을 손쉽게 다운로드 받을 수 있는 영상 크롤러로 코드를 확장할 계획이다. 또한, PyQT5를 활용하여 GUI 형태로도 구현해보고자 한다.

### format options(영상 화질선택 옵션)
  - format key에 넣는 값에 따라 각각 다른 화질의 영상을 선택적으로 다운로드 할 수 있다.
  - 지원되는 화질 중 가장 좋은 화질로 받으려면 앞서 언급한 예제 코드와 같이 `'format': 'best/best'`로 설정하면 된다.

```
format code extension resolution  note
140         m4a       audio only  DASH audio , audio@128k (worst)
160         mp4       144p        DASH video , video only
133         mp4       240p        DASH video , video only
134         mp4       360p        DASH video , video only
135         mp4       480p        DASH video , video only
136         mp4       720p        DASH video , video only
17          3gp       176x144     
36          3gp       320x240     
5           flv       400x240     
43          webm      640x360     
18          mp4       640x360     
22          mp4       1280x720    (best)
```

---

#### [Reference]

[1] [youtube-dl](https://ytdl-org.github.io/youtube-dl/index.html)  
[2] https://github.com/choidslab/youtube-video-downloader
