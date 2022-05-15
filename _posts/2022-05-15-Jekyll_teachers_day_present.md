---
layout: post
title: 시각화 - ggplot2로 움직이는 꽃 그리기 
excerpt: 스승의 날을 맞아 교수님께 꽃을 선물드려보아요! 🌺
categories: [jekyll]
tags: #[jekyll, blog, 꿀팁]
last_modified_at: 2022-05-15
comments: true
---
아래는 내가 석사시절 스승의 날에 지도 교수님께 선물로 드린 그림(!?)이다.

> 실제 드린 원본은 태양에 교수님 사진이 들어가고, 꽃에는 랩실 사람들 5명의 얼굴이 들어간다. 교수님의 가르침을 받고, 지도 학생들이 무럭무럭 자란다는 의미를 담았다.🌱 

![present](https://user-images.githubusercontent.com/47768004/168471008-a88d2fa6-4517-4241-8a86-822505abd6e7.gif)

> TMI : 당시 지도 교수님께서는 학생에게 물건 선물을 받지 않으셔서, 감사의 마음을 어떻게 표현할지 고민되었다. 마침 해당 학기에 교수님께서 데이터 시각화 강의를 하셨는데, 수업에서 배우는 ggplot2 패키지를 이용해서 무언가를 만들어드리면 의미있을 것 같았다. 그래서 스승의 날 전날 밤을 새서 교수님께 그림 선물을 드렸던 기억이 있다. (교수님께서는 받고 어떤 마음이 드셨을까...)

선물을 준비하면서 아래 3가지 지점을 얻을 수 있었다. 그리고 이 작업이 나에겐 충분히 의미가 있다고 생각되어서 블로그에 남기려고 한다. 

- ggplot2에 대한 이해도 증가 
> 진짜 별게 다 되네.. 헤들리 위컴(ggplot2 개발자) 당신은 도덕책.. 
- 시각화의 생각 확장 
> "ggplot2으로 산점도, 선, 막대 그래프 말고 이런것도 할 수 있다고?"를 깨닫고, 이후에 ggplot2로 데이터를 표현하는데 적합한 새로운 그래프들을 그려나가는데도 도움이 되었다. 
- 오랜만에 수학 공부하니 뇌가 활성화되는 느낌 
> 원의 방정식이 얼마만이야..

그림은 크게 5가지 부분으로 구성되고, 하나씩 자세히 작성해보겠다. 
1. 꽃 
2. 줄기 
3. 잎사귀
4. 기타 배경 

우선, 아래 4개의 패키지를 사용한다. 
``` R
library(animation)
library(ggplot2)
library(tidyverse)
library(ggimage)
```

## 0. 애니메이션 

본격적인 그림 설명에 앞서 애니메이션을 그리는 법부터 정리해보자. animation 패키지에 있는 함수`saveGIF()`를 이용해서 애니메이션을 만들 수 있다. 여러개의 그림을 연결해서 애니메이션을 생성하고 gif파일 형식으로 저장된다. 아래 코드에서는 n개의 그림이 각각 dt초씩 재생되어 1개의 gif파일이 저장된다.

```R
saveGIF({
  for (i in 1:n){
    p1=ggplot()+
        ...
    print(p1)
  }
},interval = dt, ani.width = 400, ani.height = 400, movie.name = {파일저장경로/파일명.gif})
```

## 1. 꽃 

아래 코드를 바탕으로 아래와 같은 학생 꽃을 그릴 수 있다! 
2차원 등고선을 그리는 함수 `stat_density_2d()`를 이용해서 꽃을 그렸다. (꽃이라고 우겨본다.) 거기에 이미지를 추가하는 함수 `geom_image()`를 이용해서 꽃의 중심에 학생 사진을 추가했다. 
```R
geom_flower <- function(xcore, # 꽃의 중심 위치 
                        ycore,
                        n=1000, # 꽃 만들때 난수 생성 수  
                        image_path,# 이미지 경로 
                        image_size,
                        ...){
  # 등고선으로 꽃 만들고, 꽃 모양이 변하면 안되니까 시드 고정 
  set.seed(1234) 
  mean=c(0,0)
  # 난수 2쌍 생성
  .x <- mvtnorm::rmvnorm(n, mean) 
  df1 <- tibble(x = .x[, 1], y = .x[, 2])
  
  df=tibble(x = .x[, 1]+xcore, y = .x[, 2]+ycore)
  list(
    stat_density_2d(
      aes(x = x, y = y, fill = stat(level)), data = df, 
      geom = "polygon", show.legend = FALSE, color = "grey80"),
    geom_image(mapping=aes(xcore,ycore),image=image_path, size=image_size),
    scale_fill_gradient2(...)
  )
}

## 꽃 그리기 
ggplot()+
  geom_flower(xcore=0,
              ycore=0,
              image_path=paste0(path,"/image/student5.png"),
              image_size=0.5,
              low = "palevioletred1", 
              mid = "firebrick2", 
              high = "lightpink1",
              midpoint = 0.075
              )+
  theme_minimal()
```

<img width="350" alt="flower_plot" src="https://user-images.githubusercontent.com/47768004/168469861-a1311ff9-f6f3-40eb-af13-d5833e02dee0.png"> 

꽃은 아래와 같은 반원을 왔다갔다 하는 형태로 만들고 싶었다. (2->3->2->1->2...를 반복하는 형태로)

![스크린샷 2022-05-15 오후 9 04 55](https://user-images.githubusercontent.com/47768004/168471848-39fa43dc-88b0-4749-aac0-e54fd463abca.png)

따라서 아래와 같은 수식을 바탕으로 꽃이 움직이게 설정했다. 

> x = asin(wt)

> y = hcos(2πx/2a)

> a=0.5, h=0.5, t=c(0.1,0.2,..,2.9,3)

<img width="500" alt="flower_change" src="https://user-images.githubusercontent.com/47768004/168471444-a08c6549-9cf5-4772-b6fd-d58de0083d3b.png"> 

아래와 같이 잔망스럽게 움직이는 것을 볼 수 있다. 

<img width="500" alt="flower_move" src="https://user-images.githubusercontent.com/47768004/168472158-03ef49c0-9177-433e-8d4f-b328da2660c2.gif"> 


## 2. 줄기 

곡선을 그리는 함수 `geom_curve()`를 이용해서 아래와 같이 줄기를 그렸다. 줄기 시작과 끝(꽃 위치와 동일) 부분과 곡률만 설정해주면 되기 때문에 간단하다. 

```R
geom_stem <- function(x=0, # 뿌리 위치 
                      y=0, 
                      xend, # 줄기 끝 위치  
                      yend,
                      curvature, # 곡률 
                      color="olivedrab3"
                    ){
  list(
    geom_curve(aes(x = x, y = y, xend = xend, yend = yend), 
               ncp = 1000, curvature = curvature, size = 6, 
               color = color)
      )
}
```
<img width="400" alt="stem_move" src="https://user-images.githubusercontent.com/47768004/168473242-de879fe0-a853-40bd-9081-dbbec2660491.gif"> 

꽃이 움직이기 때문에 줄기도 자연스럽게 바람에 흔들리는 것처럼 휘어지는 것으로 연출하고 싶었다. 따라서 아래와 같은 수식을 바탕으로 곡률이 변하도록 설정했다. 해당 수식은 꽃의 움직임과 주기를 2π로 동일하게 맞췄다. 

> curvature = bcos(2πt)

> b=-0.1, t=c(0.1,0.2,..,2.9,3)

<img width="500" alt="curvature" src="https://user-images.githubusercontent.com/47768004/168473426-01b1d86b-ca82-4f8c-a2d6-38ade8ffdb67.png"> 


## 3. 잎사귀

점을 순서대로 연결하고, 닫힌 부분은 채워주는 `geom_polygon()`함수를 사용해서 잎사귀를 그릴 수 있다. 

``` R
geom_leaf <- function(x=0, # 잎과 잎사귀와의 간격 
                      xend=2, # xend-x : 잎사귀 길이 
                      xoffset = 0, # 잎사귀 위치  
                      yoffset = 0, 
                      xflip = 1, # 잎사귀 방향 
                      yflip = 1,      
                      fill = "olivedrab3", 
                      color = "palegreen4"
                    ){
  
  # 잎사귀의 곡선 함수
  f <- function(x) x^2 / 2 
  
  .x <- seq(x, xend, length.out = 100)
  .y <- f(.x)
  
  df <- tibble(x = c(.x, .y), y = c(.y, .x))
  df$x <- xflip * df$x + xoffset
  df$y <- yflip * df$y + yoffset
  
  geom_polygon(data = df, 
               aes(x = x, y = y),
               fill = fill, 
               color = color)
}

## 잎사귀 그리기 
ggplot()+
  geom_leaf(0, 2, 0, 0, -0.5, fill = "olivedrab3", color = "palegreen4")
```

<img width="350" alt="leaf" src="https://user-images.githubusercontent.com/47768004/168474650-6b2c8fcb-5723-406b-aeea-80e2df9968ab.png"> 

잎사귀의 밑 부분은 f(x)로, 윗 부분은 f(x)의 역함수로 구성했다. 좁은 간격으로 점을 여러개를 찍고, 그 점을 순서대로 연결하는 형태이다. (아래 그래프에서 색상에 해당하는 z가 점의 순서이다. 점이 진할수록 앞 순서이다.) 잎사귀 밑부분 (0,0)->...->(2,0) 그리고 잎사귀 윗 부분 (0,0)->...->(2,0)에 대해 촘촘하게 순서대로 점을 생성하고 이를 연결해서 자연스러운 곡선으로 보이게 했다. 

> f(x) = x²/2 

<img width="450" alt="leaf_frame" src="https://user-images.githubusercontent.com/47768004/168474648-6e4778f8-e1b5-47fd-b678-bb289ee22da5.png"> 


그리고 이제 이 잎사귀를 줄기에 붙여야한다. 줄기가 움직이기 때문에, 잎사귀의 위치도 시간에 따라 변한다. 아래 함수를 바탕으로 잎사귀의 위치를 구할 수 있다. 

```R
leaf_loc <- function(xend, # 꽃 위치 
                     yend,
                     p, # 위치(0~1 ->줄기 중심 기준 -100%~100%)
                     curvature # 줄기 곡률 
                     ){
  d <- sqrt(xend^2+yend^2)
  beta <- atan2(yend,xend)
  k = abs(curvature)
  
  sx = (2*p-1)
  virtual.x = d/2*sx
  virtual.y = -sign(curvature)*d/2*(sqrt(1/k^2-(sx)^2)-sqrt(1/k^2-1))

  cb = cos(beta)
  sb = sin(beta)
  
  leaf.x = cb*virtual.x -sb*virtual.y + d/2*cb
  leaf.y = sb*virtual.x +cb*virtual.y + d/2*sb
  
  return(c(leaf.x, leaf.y))
}
```

예를 들어 잎사귀를 줄기의 2/3지점에 위치 시킨다고 하자. (곡률에 따라 줄기의 길이가 달라지기 때문에 x, y 값이 계속 변한다.)
줄기의 좌표와 줄기의 곡률을 알고 있기 때문에, 이를 바탕으로 잎사귀의 위치를 알 수 있다. 아래의 이미지에서 빨간 점의 위치를 알고 싶다면, Or 좌표계에서 Ov 좌표계로 넘어가서, 원의 방정식을 기반으로 vir.x, vir.y를 구할 수 있다. (그림2 참고)
여기서 구한 vir.x, vir.y를 Ov -> Or 좌표계로 변경시키려면 회전 행렬을 이용하면 된다. 

![스크린샷 2022-05-15 오후 11 13 38](https://user-images.githubusercontent.com/47768004/168477229-2c10d523-141f-4042-abd3-a67c1c3d2219.png)



꽃, 줄기, 잎사귀, 잎사귀 위치 함수를 종합해서 다음과 같이 함수를 생성했고, 움직이는 꽃 한송이를 그려보았다. 잎사귀가 잘 붙어있는 것을 볼 수 있다. 

```R
dancing_flower<-function(flower_xcore, # flower 만의 좌표 
                         flower_ycode,
                         flower_ox, # 전체 이미지 좌표로 볼때
                         flower_oy=9,
                         flower_image_path,
                         flower_image_size,
                         flower_low='red',
                         flower_mid='purple',
                         flower_high='pink',
                         stem_curvature
                         ){
  list(
    geom_stem(x=flower_ox,
              xend=flower_xcore+flower_ox,
              yend=flower_ycode+flower_oy,
              curvature=stem_curvature,
              ),
    geom_flower(xcore=flower_xcore+flower_ox, 
                ycore=flower_ycode+flower_oy,
                image_path=flower_image_path,
                image_size=flower_image_size,
                low = flower_low, 
                mid = flower_mid, 
                high = flower_high,
                midpoint = 0.075),
    geom_leaf(xoffset = leaf_loc(flower_xcore, flower_ycode+flower_oy,0.3,stem_curvature)[1]+flower_ox,  
              yoffset = leaf_loc(flower_xcore, flower_ycode++flower_oy-1,0.3,stem_curvature)[2], 
              xflip = 0.5),  
    geom_leaf(xoffset = leaf_loc(flower_xcore, flower_ycode+flower_oy,0.3,stem_curvature)[1]+flower_ox,  
              yoffset = leaf_loc(flower_xcore, flower_ycode+flower_oy-1,0.3,stem_curvature)[2], 
              xflip = -0.5) 
  )
}

## 움직이는 꽃 한송이 
saveGIF({
  for (i in 1:length(x)){
    p1=ggplot()+
      dancing_flower(flower_xcore=x[i],
                     flower_ycode=y[i],
                     flower_ox=0,
                     flower_image_path=paste0(path,"/image/student5.png"),
                     flower_image_size=0.2,
                     flower_low='palevioletred1',
                     flower_mid='firebrick2',
                     flower_high='lightpink1',
                     stem_curvature=mycurve[i])+
      coord_cartesian(xlim=c(-6,6),ylim=c(0,12))
    print(p1)
  }
},interval = dt, ani.width = 400, ani.height = 400,movie.name = paste0(path,"/plot/dancing_flower.gif"))
```
![dancing_flower](https://user-images.githubusercontent.com/47768004/168477357-0aa6a918-7591-4dd2-a0cb-cf6d10920745.gif)


## 4. 기타 배경 

기타 배경은 상대적으로 간단하다. 

### 하늘과 땅 

직사각형을 생성하는 `geom_rect()`함수로 간단히 하늘과 땅을 구분했다. 
```R
ggplot()+
      geom_rect(mapping=aes(xmin=-5, xmax=30, ymin=0, ymax=22), fill="lightskyblue2",alpha=0.2)+#하늘
      geom_rect(mapping=aes(xmin=-5, xmax=30, ymin=-5, ymax=0), fill="sienna4") # 땅 
```

### 태양 

태양은 ppt로 이미지를 그려서 붙여왔고, 시간에 따라 햇빛의 size를 달리하여 반짝반짝한 느낌을 주었다. 그리고 태양의 중심에는 교수님 이미지를 넣었다. 

```R
sunshine_size=seq(0.27,0.31,length=5)
# t의 length가 31개라서 길이 31로 맞춰줌
my_sunshine_size=c(rep(c(sunshine_size,rev(sunshine_size)),3),sunshine_size[1]) 

saveGIF({
  for (i in 1:length(x)){
    p1=ggplot()+
      geom_image(mapping=aes(-0.1,0.1),image=paste0(path,'/image/sun2.png'),size=0.5)+ # 해
      geom_image(mapping=aes(0,0),image=paste0(path,'/image/sun1.png'),size=my_sunshine_size[i]) + # 빛 
      geom_image(mapping=aes(0,0),image=paste0(path,'/image/prof.png'),size=0.4)+
      coord_cartesian(xlim=c(-3,3),ylim=c(-3,3))
    print(p1)
  }
},interval = dt, ani.width = 200, ani.height = 200,movie.name = paste0(path,"/plot/sun.gif"))
```

![sun](https://user-images.githubusercontent.com/47768004/168478212-5b6aaac7-60f0-475b-865f-0dee23a38949.gif)

### 글씨 

글씨도 이미지로 가져왔고, x,y축 값에 대해 난수생성을 하여 약간의 움직임을 주어 인터랙티브한 느낌을 주었다. 

```R
.x <- mvtnorm::rmvnorm(length(x), mean=c(0,0)) 
rnorm<- tibble(text_x = .x[, 1], text_y = .x[, 2])
saveGIF({
  for (i in 1:length(x)){
    p1=ggplot()+
      geom_image(mapping=aes(0+rnorm$text_x[i]/50,0+rnorm$text_y[i]/50),image=paste0(path,'/image/text.png'),size=1)+
      coord_cartesian(xlim=c(-2,2),ylim=c(-2,2))
    print(p1)
  }
},interval = dt, ani.width = 200, ani.height = 200,movie.name = paste0(path,"/plot/text.gif"))

```
![text](https://user-images.githubusercontent.com/47768004/168478456-648cc5bd-b305-4101-b1aa-3f323c719321.gif)


> 전체 애니메이션 코드는 추후에 덧붙이겠습니다! 