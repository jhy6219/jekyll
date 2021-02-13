---
layout: post
title: 지킬 블로그 사이트맵 피드 설정 - Jekyll sitemap feed
excerpt: 지킬 블로그 사이트맵 피드 설정하고 글 목록과 최근 글이 잘 되는지 확인해보자 sitemap.xml feed.xml
categories: [jekyll]
tags: [jekyll, blog, 사이트맵, 피드]
last_modified_at: 2020-08-28
---

자기 블로그의 사이트맵과 피드를 제공하는 것은 검색이 되기위해서 가장 중요하다고 볼 수 있다.

[파워블로그 테크스톡님이 잘 정리하신 글](https://techstock.biz/Jekyll-Blog/Gemfile-analyize/){:target="_blank"} 에 보면,

> *From: Jekyll-Blog 지킬 블로그 Gemfile 분석*
> 
> sitemap이 잘 작동하는지의 테스트는 블로그URL/sitemap.xml 쳐본다
> 
> RSS Feed가 잘 작동하는지의 테스트는 블로그URL/feed.xml 쳐본다


이렇게 적혀있다.

물론, _config.yml 에 아래 플러그인을 명기해 줘야 할 듯 하다. (GitHub Pages 에서는 기본으로 제공하고 있는지 잘 모르겠다.)

```
plugins:
  - jekyll-feed
  - jekyll-sitemap
```

나의 사이트맵과 피드는 잘 나오고 있다.

- <https://note.devbj.com/feed.xml>

![feed.xml](https://paper-attachments.dropbox.com/s_96F9B500837B678523FF321850961A0C418D530CC9A3617547DBCB19FE0630C2_1598579049857_image.png)

- <https://note.devbj.com/sitemap.xml>

![sitemap.xml](https://paper-attachments.dropbox.com/s_96F9B500837B678523FF321850961A0C418D530CC9A3617547DBCB19FE0630C2_1598579085389_image.png)


---
레퍼런스
- [Jekyll-Blog 지킬 블로그 Gemfile 분석](https://techstock.biz/Jekyll-Blog/Gemfile-analyize/){:target="_blank"} 