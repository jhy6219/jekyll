---
layout: post
title: 지킬 블로그 페이지 설정 - Jekyll pagination
excerpt: 지킬 블로그 페이지 나누기 기능을 부트스트랩을 활용하여 모양을 바꿔보자 - Jekyll pagination
categories: [jekyll]
tags: [jekyll, blog, 페이지, 부트스트랩]
last_modified_at: 2020-08-28
---

지킬 플러그인에서 jekyll-paginate 를 사용하면 거의 자동으로 페이지 이동 기능을 이용할 수 있다.
아래 링크를 참고하면, 기본 코드의 틀을 가져올 수 있다.

- [Jekyll pagination, https://jekyllrb.com/docs/pagination/](https://jekyllrb.com/docs/pagination/){:target="_blank"}
- [지킬 페이지 나누기, https://jekyllrb-ko.github.io/docs/pagination/](https://jekyllrb-ko.github.io/docs/pagination/){:target="_blank"}


문제는 어떻게 보여지는 것인지 인데…
일단, 부트스트랩 사이트로 가보자.

- [부트스트램, https://getbootstrap.com/docs/4.0/components/pagination/](https://getbootstrap.com/docs/4.0/components/pagination/){:target="_blank"}

여기에 보면 기본적인 페이지 네비게이션 모양들이 있다.
이중에 이렇게 생긴놈으로 하나 골랐다. 코드를 가져와서 지킬 페이지 기능과 유기적으로 결합시켜 보자.

![](https://paper-attachments.dropbox.com/s_603F93C6C3AC8460FB1869CA7717C0B5C9ED9711793509404E01466E2B9744C5_1598572405756_image.png)


코드는 아래 gist code 를 사용하면 된다. 아래 gits 창 하단에 view raw 를 누르면 깔끔하게 다운로드 할 수 있다.

<script src="https://gist.github.com/bjnhur/5512866a8cd49fc70341262524eb041f.js"></script>

먼저, 변경되기전의 Clean 테마에서는 아래 그림처럼 페이지 기능이 구현되어 있었다.

![](https://paper-attachments.dropbox.com/s_603F93C6C3AC8460FB1869CA7717C0B5C9ED9711793509404E01466E2B9744C5_1598572592987_image.png)


결과적으로 나의 블로그에 적용된 모양은 아래와 같다.

![](https://paper-attachments.dropbox.com/s_603F93C6C3AC8460FB1869CA7717C0B5C9ED9711793509404E01466E2B9744C5_1598572497065_image.png)


흠 그럴듯 하게 변경되었다.. ^0^

