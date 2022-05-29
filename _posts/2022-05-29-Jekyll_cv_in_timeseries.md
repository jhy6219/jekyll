---
layout: post
title: 시계열 - non dependent cross validation
excerpt: 시계열 데이터에서의 특징을 반영한 non dependent cross validation에 대해 알아보자
categories: [시계열]
tags: #[jekyll, blog, 꿀팁]
last_modified_at: 2022-05-29
comments: true
use_math: true
---

시계열 예측 모델을 만들 때에도 cross validation을 할 수 있는데, 시간의 순서로 정렬되어있다는 데이터의 특성을 고려해야한다. 따라서 비시계열 데이터와 달리 적용 형상이 약간 다르고, non dependent cross validation라는 형태의 교차검증 방식도 있다. 시계열의 다른 cross validation을 소개하면서, 해당 방식도 정리해보고자 한다. 

## Hold-out Cross-Validation

Hold-out Cross-Validation은 아래와 이미지와 같이 특정 비율로 학습/ 테스트 데이터를 1회 분할하는 방법론이다. 

보통 예측 모델을 평가/검증할 때 아래와 같이 데이터를 `학습 : 테스트 = 8:2`로 나누고 학습 데이터로 모델을 학습하고, 테스트 데이터로 모델을 평가한다. 사실 비율은 자기 마음인데, 테스트 데이터의 비율이 너무 늘어나면 그만큼 학습 데이터가 부족할까봐 8:2 정도로 많이 나누는 것 같다.

> t=1~15인 데이터가 있고, 모델의 input 기간이 2, output 기간이 1일 때 train 데이터를 기반으로 a ~ k 데이터셋을 바탕으로 모델을 학습한다. 그리고 ㅣ ~ m 데이터셋을 바탕으로 모델을 평가한다. 

<img width="450" alt="스크린샷 2022-05-29 오후 10 24 40" src="https://user-images.githubusercontent.com/47768004/170871123-058507d8-5203-4924-b6a0-77e2782a10bf.png">

하지만! 아래 경우에는 교차 검증을 실시한다. 하지만 모든 것에는 trade off가 있는 법.. 그만큼 모델 학습/평가 소요 시간이 증가한다. 
- 8:2로 나눠도 학습 데이터가 부족한 것 같을 때 (전반적으로 데이터가 많이 부족할 때 )
- 20%의 테스트 데이터에 과적합이 될까 두려울 때

## K-Fold Cross-Validation

K-Fold Cross-Validation은 아래와 같이 데이터를 K등분해서, 1개의 fold를 테스트 데이터로, K-1개의 fold를 학습 데이터로 돌아가면서 K번 반복하는 방법론이다. 학습 데이터와 테스트 데이터가 계속 교차하면서, 모든 데이터가 한번씩은 테스트 데이터가 되어보기 때문에, 과적합이 될 우려가 적다. 또한 전체 데이터를 학습 데이터로 사용할 수 있다는 점도 장점이다. K개의 모델을 앙상블해서 예측 결과를 낼 수 있다. (연속해서 학습을 할 수 있는 뉴럴 네트워크 모델에서는 순차적으로 K번에 걸쳐 학습하는 방법도 있는 것으로 보인다.)

<img width="350" alt="스크린샷 2022-05-29 오후 10 48 27" src="https://user-images.githubusercontent.com/47768004/170872333-fa6fbc49-743f-4ef0-9e81-8c21ddae1817.png">

<img width="600" alt="스크린샷 2022-05-29 오후 10 49 36" src="https://user-images.githubusercontent.com/47768004/170872388-4122f5d1-8ace-4670-ab16-dc6ef919c2e4.png">
