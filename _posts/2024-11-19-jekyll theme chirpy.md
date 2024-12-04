---
title: jekyll theme chirpy - github build error
date: 2024-11-19 20:00:00 +0900
categories: [tech, web]
tags: [jekyll, chirpy, github build error, jekyll-theme-chirpy.scss, scss]
description: chirpy 테마를 사용하여 github blog 를 만들때 발생하는 github build error
---

대부분의 사람들이 github blog 를 만들어 보자고 마음을 먹으면, 가장 먼저 jekyll theme 를 살펴보는 것 같습니다.
저 또한 jekyll theme 적용에 대해서 알아보았고, 제일 눈이 가는 jekyll theme 는 chirpy 였습니다. 
알고 보니 많은 분들께서 선택하는 theme 더군요.

> 글을 작성하는 시점 기준으로 jekyll theme chirpy 의 버전은 7.1.1 입니다.
{: .prompt-info }

jekyll-theme-chirpy 를 설치하는 방법은 구글링을 해보면 굉장히 많습니다.
다만 저의 경우, 아래에서 서술할 github build error 를 경험하게 되었고 이를 해결하는 방법을 첫 포스팅으로 남겨봅니다.

## 1. error 발생 시 blog 첫 화면
구글링으로 찾아본 글들을 보면서 따라하다 보면, github 에 push 하고 아무런 오류를 확인하지 못합니다.
: (github Actions 를 확인 하기 전까진)
모든 코드를 commit 하고 push 한 뒤, github blog 에 방문해보면 아래와 같이 한 줄만 표현되고 나머지는 텅 빈 화면을 볼 수 있습니다.

```--- layout: home # Index page ---```

뭔가 layout 에 문제가 생겼다는 걸(?) 직감할 수 있습니다...
그리고 파일들을 하나둘씩 확인하다 보면 repo 가장 최상단의 index.html 의 소스 원문이 그냥 그대로 표현되는 것을 알게 됩니다.

이때부터 살펴본 포스팅들에 대한 신뢰감이 떨어지기 시작하고 또 다른 포스팅을 참고하며 git repo 를 지웠다 생성하기를 수도 없이 반복하게 됩니다. commit/push 도 수도 없이...

## 2. 원인 분석
여러 번에 걸친 소스코드 업로드, repo 생성&삭제 과정을 거치면서 더이상 소스는 문제가 아니고 github pages 의 어떠한 과정(?)에서 문제가 있겠구나 라는 생각이 들기 시작했습니다.

![alt text](/assets/img/configure jekyll.jpg)
_configure jekyll_

검색된 여러 포스팅들을 살펴보면 github blog 를 완성하는 데에 Settings > Pages 에서 Source 를 Actions 으로 변경하는 방식이 권장되고, Jekyll Configure 를 하여 jekyll.yml 을 추가하는 과정이 필수임을 알 수 있었습니다.

위와 같은 설정을 한 뒤에는 일반적인 소스코드를 push 하는 것과 다르게 Actions 탭에서 build > deploy 과정을 거치게 된다는 것을 알 수 있었고, 그리고 그 빌드 과정에서 오류가 발생하였음을 알게 되었습니다.


## 3. github build Error string
```Error: Can't find stylesheet to import.```

```
Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/jekyll-theme-chirpy.scss': 
                Can't find stylesheet to import.
```
![alt text](/assets/img/chirpy build error.png)
_github build error message_

## 4. 해결 방안
사실 본질적인 문제가 무엇이고 아래 서술한 해결방안이 어떻게 해결이 되는 것인지 저는 정확히는 아직 알지 못한 상태입니다.

다만 위 build error 를 검색해보면 `npm run build` 를 해야 한다는 얘기들을 많이 볼 수 있으며, 이는 local 에서가 아닌 github build 과정에서 수행되어야 한다는 것임을 알게 되었습니다.

github build 과정은 Settings > Pages 에서 추가한 `jekyll.yml(.github/workflows/jekyll.yml)` 에 workflow 가 정의되어 있고, 거기에 아래와 같이 npm build 과정을 추가해야 합니다.

npm build 과정을 추가하게 되면, 오류 없이 빌드/배포가 잘 수행되고 theme 가 올바르게 적용된 blog를 보실 수 있습니다.

[npm build / jekyll.yml](https://github.com/koredge/koredge.github.io/blob/b31e2f6ab39b2749af84234211ba47014b893e15/.github/workflows/jekyll.yml#L42)

![alt text](/assets/img/npm run build insert.jpg)
_npm build 과정 삽입_