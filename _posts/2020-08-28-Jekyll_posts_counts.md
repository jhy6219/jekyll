---
layout: post
title: 지킬 블로그 총 게시글의 수는? - Jekyll blog total number of posts
excerpt: 지킬 블로그 총 게시글의 수가 궁금하다면 이리저리 머리 굴릴 필요 없이 간단하게 구할 수 있다. Jekyll blog total number of posts
categories: [jekyll]
tags: [jekyll, blog, 꿀팁]
last_modified_at: 2020-08-28
---

지킬 블로그 총 게시글의 수가 궁금하다면??
for loop 을 돌려서 구해야 하나 고민 하는 순간 검색을 해보니...

정답이 너무 쉽다. 아래 글을 봐도 되고, 정답을 아래 적어둘 터니 여기서 바로 봐도 된다.
Jekyll blog total number of posts

- [Display the total number of posts in a site](https://blog.lakshmanbasnet.com/jekyll/jekyll-post-count/){:target="_blank"}

정답은

```
{{ "{{ site.posts | size "}} }}
```

혹은 이렇게 해도 된다.

```
{{ "{{ site.posts.size "}} }}
```

태그 페이지에 이것을 활용해 보았다.
글 숫자에 따라 태그 글자의 크기를 키우도록 하는 좋은 코드

아이디어를 참고한 글은 아래
- [jekyll 블로그 tag 기능 추가](https://min9nim.github.io/2018/08/jekyll-tags/){:target="_blank"}

``` html
{% raw %}
  <!-- font_size 변수 지정: 태그해당글숫자/전체글숫자 * 20 + 14 -->
  {% capture font_size %}
    {{tag_size | times: 20 | divided_by:site.posts.size | plus: 14 }}
  {% endcapture %}
  
  <li>
  <a href="#{{tag_name}}" style="font-size:{{font_size}}px">
    {{ tag_name }}<span>({{ tag_size }})</span>
  </a></li>
  {% endfor %}
{% endraw %}
```

이 결과는 아래 그림처럼 나온다. 글이 너무 작아서 4개 정도가 제일 크게 나오네요 ^^;;;

![](https://paper-attachments.dropbox.com/s_1DBBCA2B6F751C8D2CD9F45C3B2C1E9A662D9DDFDAA5E9D8700D5ECE5C2010B3_1598592847176_image.png)

하나 더 지킬 블로그에 카테고리 기능을 넣었다면,

개별 카테고리에 해당되는 글의 숫자도 알고 싶다. 진짜 알고 싶다면...정답확인!!

```
{{"{{ site.categories[카테고리이름].size "}}}}
```

---
레퍼런스 목록
- [Display the total number of posts in a site](https://blog.lakshmanbasnet.com/jekyll/jekyll-post-count/){:target="_blank"}
- [jekyll 블로그 tag 기능 추가](https://min9nim.github.io/2018/08/jekyll-tags/){:target="_blank"}
