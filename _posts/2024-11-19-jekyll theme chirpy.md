---
title: jekyll theme chirpy - github build error
date: 2024-11-19 20:00:00 +0900
categories: [tech, web]
tags: [jekyll, chirpy, github build error, jekyll-theme-chirpy.scss, scss]
description: chirpy 테마를 사용하여 github blog 를 만들때 발생하는 github build error
---

대부분의 사람들이 github blog 를 만들어 보자고 마음을 먹으면, 가장 먼저 jekyll theme 를 살펴보는것 같습니다.
저 또한 jekyll theme 적용에 대해서 알아보았고, 제일 눈이 가는 jekyll theme 는 chirpy 였습니다. 

알고 보니 많은 분들께서 선택하는 theme 더군요.

> 글을 작성하는 시점 기준으로 jekyll theme chirpy 의 버전은 7.1.1 입니다.
{: .prompt-info }

jekyll-theme-chirpy 를 설치하는 방법은 구글링을 해보면 굉장히 많습니다.
다만 저의 경우, 아래에서 서술할 github build error 를 경험하게 되었고 이를 해결하는 방법을 첫 포스팅으로 남겨봅니다.


--- layout: home # Index page ---

Error: Can't find stylesheet to import.

Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/jekyll-theme-chirpy.scss':
                    Can't find stylesheet to import.

![alt text](/assets/img/chirpy build error.png)
_github build error message_