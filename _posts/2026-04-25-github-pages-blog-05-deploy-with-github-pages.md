---
title: "GitHub Pages 블로그 만들기 5. GitHub Actions로 배포하기"
date: 2026-04-25 17:24:00 +0900
categories: [github-pages, jekyll, blog]
tags: [github-pages, github-actions, deploy, workflow]
---

# GitHub Pages 블로그 만들기 5. GitHub Actions로 배포하기

저장소와 테마, 기본 파일 구조까지 준비했다면 이제 실제 배포를 연결할 차례다.  
이 단계가 끝나야 저장소에 푸시한 변경 내용이 웹사이트에 반영된다.

이번 글에서는 GitHub Pages와 GitHub Actions를 이용해 Jekyll 블로그를 배포하는 흐름을 정리한다.

## 왜 GitHub Actions 방식으로 배포할까

예전에는 GitHub Pages가 특정 브랜치의 정적 파일을 바로 배포하는 방식으로 많이 쓰였다.  
지금은 Actions 기반 배포가 더 유연하고, Jekyll 빌드 과정을 명확하게 관리하기 좋다.

장점은 아래와 같다.

- 빌드와 배포 과정을 코드로 관리할 수 있다.
- 워크플로 로그를 통해 오류를 추적하기 쉽다.
- 테마와 의존성 관리가 명확하다.

## Pages 설정에서 먼저 확인할 것

GitHub 저장소에서 아래 메뉴를 확인한다.

1. `Settings`
2. `Pages`
3. `Build and deployment`
4. `Source`

여기서 `GitHub Actions`를 선택해야 커스텀 워크플로가 정상 동작한다.

이 설정이 빠져 있으면 워크플로가 실행되더라도 Pages 사이트 정보를 찾지 못하거나, 배포가 이어지지 않는 경우가 있다.

## 워크플로 파일 만들기

보통 워크플로는 아래 경로에 둔다.

```text
.github/workflows/pages.yml
```

예시는 다음과 같다.

```yml
name: Deploy Jekyll site to Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v5

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: "3.3"
          bundler-cache: true

      - name: Build with Jekyll
        run: bundle exec jekyll build
        env:
          JEKYLL_ENV: production

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v4
        with:
          path: ./_site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

이 워크플로는 `main` 브랜치에 푸시가 발생하면 Jekyll 사이트를 빌드하고 Pages에 배포한다.

## 워크플로에서 눈여겨볼 부분

### permissions

아래 권한은 Pages 배포에 필요하다.

```yml
permissions:
  contents: read
  pages: write
  id-token: write
```

권한이 부족하면 배포 단계에서 실패할 수 있다.

### build와 deploy 분리

워크플로를 `build`와 `deploy`로 나누면 어디에서 문제가 났는지 파악하기 쉽다.

- `build`: 사이트 생성
- `deploy`: 생성된 결과 업로드 및 반영

이 분리는 나중에 오류를 볼 때 꽤 유용하다.

## 배포 후 확인하는 방법

워크플로 파일을 커밋하고 푸시했다면, GitHub의 `Actions` 탭에서 실행 상태를 볼 수 있다.

확인할 것은 다음 정도다.

- `build`가 성공했는지
- `deploy`가 성공했는지
- 최종 배포 URL이 표시되는지

정상이라면 프로젝트 페이지 주소는 아래처럼 열린다.

```text
https://unisong114.github.io/blog-20260425/
```

## 자주 만나는 배포 오류

### 1. Pages가 활성화되지 않은 경우

`Settings > Pages > Source`가 `GitHub Actions`로 되어 있지 않으면 배포가 정상적으로 이어지지 않을 수 있다.

### 2. baseurl 설정 오류

프로젝트 페이지인데 `baseurl`이 빠져 있거나 잘못되면 CSS, 링크, 이미지 경로가 깨질 수 있다.

### 3. 액션 버전 경고

오래된 액션 버전을 사용하면 Node 런타임 경고가 뜰 수 있다.  
가능하면 최신 메이저 버전을 확인하고 반영하는 편이 안전하다.

## 마무리

GitHub Pages 배포는 처음에는 복잡해 보이지만, 실제로는 "Pages 설정"과 "워크플로 파일" 두 축만 맞으면 꽤 안정적으로 작동한다.

이 단계까지 끝내면 블로그는 이제 단순한 파일 모음이 아니라, 푸시만으로 공개되는 사이트가 된다.  
다음 글에서는 첫 글 작성, 메뉴 정리, 그리고 세팅 중 자주 만나는 오류들을 함께 정리해보겠다.
