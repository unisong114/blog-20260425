---
title: "GitHub Pages 블로그 만들기 3. Jekyll 테마 적용하기"
date: 2026-04-25 17:22:00 +0900
categories: [github-pages, jekyll, blog]
tags: [jekyll, theme, just-the-docs, config]
---

# GitHub Pages 블로그 만들기 3. Jekyll 테마 적용하기

저장소를 만들고 로컬 환경과 연결했다면 이제 블로그의 외형을 정할 차례다.  
Jekyll 블로그에서 이 역할을 담당하는 것이 바로 테마다.

이번 글에서는 `Just the Docs` 테마를 예시로 사용해, Jekyll 테마를 어떻게 연결하는지 정리해보겠다.

## 왜 Just the Docs를 골랐는가

`Just the Docs`는 원래 문서 사이트에 강한 테마지만, 정리형 블로그나 개발 노트에도 꽤 잘 맞는다.

선택 이유는 단순하다.

- 구조가 깔끔하다.
- 검색과 내비게이션 구성이 좋다.
- Markdown 문서가 많아질수록 장점이 커진다.
- GitHub Pages와 함께 쓰기 좋은 사례가 많다.

화려한 블로그 테마보다는, 오래 써도 질리지 않는 정돈된 구조를 원할 때 적합하다.

## 기본적으로 필요한 파일

테마를 연결하려면 최소한 아래 파일이 필요하다.

- `Gemfile`
- `_config.yml`

`Gemfile`은 사용할 Ruby gem을 정의하고, `_config.yml`은 Jekyll 사이트 설정을 담는다.

## Gemfile 작성

예시는 아래와 같다.

```ruby
source "https://rubygems.org"

gem "jekyll", "~> 4.4"
gem "just-the-docs", "~> 0.10.1"

group :jekyll_plugins do
  gem "jekyll-seo-tag"
end
```

여기서 핵심은 `just-the-docs`를 의존성에 추가하는 것이다.  
이 설정을 기준으로 로컬 빌드와 GitHub Actions 빌드가 진행된다.

## _config.yml에서 테마 연결

Jekyll의 핵심 설정 파일인 `_config.yml`에는 테마와 사이트 정보를 넣는다.

예시는 아래처럼 시작할 수 있다.

```yml
title: Unisong Blog
description: Notes, posts, and docs powered by Just the Docs on GitHub Pages.
theme: just-the-docs

url: https://unisong114.github.io
baseurl: /blog-20260425
```

여기서 특히 중요한 항목은 `url`과 `baseurl`이다.

## url과 baseurl이 중요한 이유

프로젝트 페이지 방식의 GitHub Pages는 저장소 이름이 주소 뒤에 붙는다.

예를 들면 실제 주소가 다음과 같을 수 있다.

```text
https://unisong114.github.io/blog-20260425/
```

이 경우:

- `url`: `https://unisong114.github.io`
- `baseurl`: `/blog-20260425`

이 설정이 틀리면 CSS가 깨지거나 링크가 잘못 연결되기 쉽다.  
초기에 가장 자주 실수하는 부분 중 하나다.

## 내비게이션과 검색 설정

`Just the Docs`는 문서형 탐색에 강점이 있어 관련 설정도 함께 켜두면 좋다.

예를 들면 다음과 같다.

```yml
nav_enabled: true
search_enabled: true
heading_anchors: true
color_scheme: light
```

이 정도만 있어도 기본 사용성은 충분히 좋아진다.

## 포스트 컬렉션도 함께 설정하기

블로그처럼 글을 발행하려면 `_posts`를 자연스럽게 다룰 수 있도록 컬렉션 설정을 넣어두는 것이 편하다.

```yml
collections:
  posts:
    permalink: "/:collection/:year-:month-:day-:title/"
    output: true
```

그리고 기본 레이아웃도 함께 지정해둘 수 있다.

```yml
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: post
```

이렇게 해두면 글이 많아졌을 때도 구조를 관리하기 쉽다.

## 테마 적용 단계에서 꼭 체크할 것

테마 연결 직후에는 아래 항목을 확인하는 것이 좋다.

- `Gemfile`에 테마가 들어갔는지
- `_config.yml`의 `theme` 값이 맞는지
- `url`, `baseurl`이 저장소 구조와 맞는지
- 글과 페이지의 기본 레이아웃 설정이 필요한지

이 네 가지만 맞아도 초반 시행착오를 꽤 줄일 수 있다.

## 마무리

Jekyll 테마를 붙이는 과정은 단순히 "디자인을 입힌다"기보다, 사이트의 구조와 동작 방식을 정하는 작업에 가깝다.

특히 GitHub Pages 프로젝트 페이지라면 `baseurl` 설정까지 함께 생각해야 한다.  
다음 글에서는 실제 블로그에 필요한 파일 구조를 만들고, 홈과 소개 페이지, 첫 포스트까지 어떻게 구성하는지 정리해보겠다.
