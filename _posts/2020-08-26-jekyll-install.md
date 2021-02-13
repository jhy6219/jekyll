---
layout: post
title: 윈도우 환경 지킬 설치 - Jekyll on Windows 10
excerpt: 윈도우 환경 지킬 설치, 루비 설치, 지킬 블로그 테스트까지 Jekyll on Windows 10
categories: [jekyll]
tags: [jekyll, 설치]
last_modified_at: 2020-08-26
---

# 윈도우 환경 지킬 설치 - Jekyll on Windows 10

지킬 기반의 블로그를 운영하고 싶다면, 일단 로컬 컴퓨터에서 지킬을 실행할 수 있는 환경을 설정해 두는 것이 좋다. 매번 GitHub 에 올려서 업데이트를 확인하려면 시간도 걸리고, 매번 커밋을 수행해야 하니 커밋 숫자가 엄청 증가하게 된다.

윈도우 환경에서 지킬 블로그를 확인하기 위한 과정은 다음과 같다.

1. 루비 설치
2. 지킬 설치
3. 지킬 블로그 테마 선택 및 실행

----------

## 루비 설치 - Ruby for Windows

여기로 접속해서, 프로그램을 다운로드 한다.
<https://rubyinstaller.org/downloads/>
나는 Ruby Devkit 2.6.6-1 버전을 다운로드 했다.

![Ruby installer for Windows](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598413537762_image.png)


설치할 때 다 기본으로 하되, 그래도 옵션은 잘 보고, 왠만한 것 체크를 해버려~~~~

![루비 설치 경로 추가](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598413758662_image.png)


루비 설치가 완료 되었는지 확인해 보자. 먼저 터미널을 실행 시켜서

![](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598414222833_image.png)


설치된 루비와 gem 버전을 확인해 보면 된다.

![](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598414353806_image.png)


완료!

----------
## 지킬 설치 - Jekyll on Windows

아까 실행해둔 터미널에서 아래 gem 명령어를 수행한다. 지킬과 필수 패키지라고 하네요.

    gem install jekyll
    gem install minima
    gem install bundler
    gem install jekyll-feed
    gem install tzinfo-data

지킬 설치가 잘 되었는지 확인해 보자.

![](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598414983025_image.png)

----------
## 지킬 블로그 테마 선택 및 실행

**Clean 테마**

- 소스 페이지 - https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll
- 소개 페이지 - https://startbootstrap.com/themes/clean-blog-jekyll/

**다운로드**
그냥 다운로드 해온다. GitHub Repo 에서 Download ZIP 해서 로컬 PC에 저장한다.
각자 원하는 폴더에 두면 된다. 현재 예제는 D:\Jekyll\cloudhome 에 저장했다.

![](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598415594488_image.png)


**Jekyll 실행**
jekyll serve 로 실행해 본다. 해당 폴더로 이동해야 한다.
아래와 같이 에러가 나면 에러메시지를 보고 적당히 대응한다. 머 아래 그림처럼 필요한 것 설치를 더 해주거나, 
*참고) 여기 예제의 경우 아래 3가지 패키지를 더 설치했다.*

    gem install jekyll-paginate
    gem install jekyll-sitemap
    gem install wdm
![](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598416115758_image.png)


짠짠!

> Jekyll serve 성공!!
![jekyll serve](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598416300318_image.png)


그럼 해당 페이지로 접속해 볼까?
아래 처럼 떡 하니 블로그가 하나 만들어 졌다. 

![지킬 블로그 완성](https://paper-attachments.dropbox.com/s_1711116CDEC3CFDBA7FD2E2FD7E1DADD3AB29854C4019A9AC4D5614AF8ADE76F_1598416242080_image.png)


이젠, 각자의 취향에 맞게 테마를 수정하고, GitHub 에 올려서 공개하는 일만 남았다.


----------

참고 블로그 글들 - 이것도 정보니깐 잘 기록해 두자 매번 검색에 투자하는 시간이 쩝~~

- <http://error404.co.kr/dev/2018/04/13/jekyll-for-windows/>
- <https://shryu8902.github.io/jekyll/jekyll-on-windows/>
- <https://dev-yakuza.github.io/ko/jekyll/theme/>

