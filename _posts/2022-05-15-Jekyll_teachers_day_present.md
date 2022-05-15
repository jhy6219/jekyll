---
layout: post
title: 시각화 - ggplot2로 움직이는 꽃 그리기 
excerpt: 스승의 날을 맞아 교수님께 꽃을 선물드려보아요! 🌺
categories: [jekyll]
tags: #[jekyll, blog, 꿀팁]
last_modified_at: 2022-05-15
---
아래는 내가 석사시절 스승의 날에 지도 교수님께 선물로 드린 그림(?)이다!
(원본은 해에 교수님 사진이 들어가고, 꽃은 랩실 사람들 5명의 얼굴이 들어감. 교수님의 가르침을 받고 무럭무럭 자란다는 의미를 담았다.🌱)
![present](https://user-images.githubusercontent.com/47768004/168469324-8cc6e17e-b0ae-4647-bd85-2c06e142715b.gif)

TMI : 지도 교수님께서는 학생으로부터 물건 선물을 받지 않으셔서, 존경의 마음을 어떻게 표현할지 고민되었다. 마침 해당 학기에 교수님께서 데이터 시각화 강의를 하셨는데, 수업에서 배우는 ggplot2 패키지를 이용해서 무언가를 만들어가면 의미있을 것 같았다. 그래서 스승의 날 전날 밤을 새서 선물을 드렸던 기억이 있다. (교수님께서는 받고 어떤 마음이 드셨을까...)

그림을 그리면서 아래 3가지 지점을 얻을 수 있었고, 의미가 있다고 생각되어서 블로그에 남기려고 한다. 

- ggplot2에 대한 이해도 증가 
- 시각화의 생각 확장 // ggplot2으로 산점도, 선, 막대 그래프 말고 이런것도 할 수 있다고?를 깨닫고, 이후에 ggplot2로 데이터를 표현하는데 적합한 새로운 그래프들을 그려나가는데도 도움이 됨.
- 오랜만에 수학 공부하니 뇌가 활성화되는 느낌 

그림은 크게 4가지 부분으로 구성되고, 하나씩 자세히 작성해보겠다. 
1. 꽃 
2. 줄기 
3. 잎사귀
4. 기타 배경 

## 1. 꽃 

아래 함수를 바탕으로 아래와 같은 꽃을 그릴 수 있다! 
```R
geom_flower <- function(xcore, #꽃의 중심 위치 
                        ycore,
                        n=1000, #꽃 만들때 난수 생성 수  
                        image_path,#이미지 경로 
                        image_size,
                        ...){
  #등고선으로 꽃 만들고, 꽃 모양이 변하면 안되니까 시드 고정 
  set.seed(1234) 
  mean=c(0,0)
  #난수 2쌍 생성
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
![only_flower](https://user-images.githubusercontent.com/47768004/168469859-fd3e0217-6e74-4493-803d-7c684fa757f5.png)

![flower_plot](https://user-images.githubusercontent.com/47768004/168469861-a1311ff9-f6f3-40eb-af13-d5833e02dee0.png)



