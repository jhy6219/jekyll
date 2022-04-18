---
layout: post
title: 지킬2 블로그 총 게시글의 수는? - Jekyll blog total number of posts
excerpt: 지킬 블로그2 총 게시글의 수가 궁금하다면 이리저리 머리 굴릴 필요 없이 간단하게 구할 수 있다. Jekyll blog total number of posts
categories: [jekyll]
tags: #[jekyll, blog, 꿀팁]
last_modified_at: 2020-08-28
---


시계열 데이터란 시간을 기반으로 순서가 매겨진 데이터이다. 시계열 데이터는 날짜/시각 정보가 반드시 포함된다. 따라서 시계열 데이터를 다룰 때에 날짜/시각를 문자형이나 수치형이 아닌 날짜형으로 변환하면 전처리/ 시각화/ 모델링에 편리하게 사용할 수 있다. 

해당 포스트에서는 시계열 데이터 분석/추출할 때 사용하는 프로그램인 R, Python, SQL에서의 날짜/시각 처리에 대해 정리했다. 

### R에서의 날짜/시각 처리 

R에서는 lubridate라는 패키지만 있으면, 편하게 시계열 데이터를 다룰 수 있다. (사실 lubridate말고도 다양한 날짜 처리 패키지가 있지만, 개인적인 경험으로는 lubridate가 제일 간편하다! 더 좋은게 있다면 추천 부탁드려요!!)

```R
# install.packages("lubridate") # install이 안되어있다면 install부터 하기.
library(lubridate)


```