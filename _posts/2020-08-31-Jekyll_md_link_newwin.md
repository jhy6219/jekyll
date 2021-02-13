---
layout: post
title: 지킬 블로그 마크다운 링크 새창으로
excerpt: 지킬 블로그에 마크다운 작성글에 있는 링크를 새창으로 여는 방법을 소개한다.
categories: [jekyll]
tags: [markdown, jekyll, 꿀팁]
last_modified_at: 2020-08-31
---

## 지킬 블로그 마크다운 링크 새창으로

이전에 썼던 글중에 일부를 예제용으로 가져오면

### 참고 글 목록
- [jekyll 블로그 tag 기능 추가](https://min9nim.github.io/2018/08/jekyll-tags/){:target="_blank"} 
- [Github Page Jekyll 에 카테고리 추가하기](https://blog.devari.kr/2019/jekyll/jekyll-category-setting){:target="_blank"} 
- [블로그 카테고리와 태그 목록 구성하기](https://devinlife.com/howto%20github%20pages/category-tag/){:target="_blank"} 

여기 링크를 눌러보면 새창으로 해당 링크가 열리는 것을 볼 수 있다.
마크다운이 기본으로 같은 창에 링크를 열어 버려, 귀찮아서 찾아봤다.
방법도 사실 귀찮지만, 조금만 신경 써 주면 새창으로 링크를 보낼 수 있다.
아래 코드에서 링크 마지막에 **{:target="_blank"}** 를 추가하면 된다. 
실제 위의 예제 링크의 마크다운 문서는 아래와 같다.

```
### 참고 글 목록
- [jekyll 블로그 tag 기능 추가](https://min9nim.github.io/2018/08/jekyll-tags/){:target="_blank"} 
- [Github Page Jekyll 에 카테고리 추가하기](https://blog.devari.kr/2019/jekyll/jekyll-category-setting){:target="_blank"} 
- [블로그 카테고리와 태그 목록 구성하기](https://devinlife.com/howto%20github%20pages/category-tag/){:target="_blank"} 
```

---

## 참고 글 목록
- [마크다운에서 링크 새 창 띄우기](http://blog.devari.kr/2019/tip/markdown-new-window){:target="_blank"}
