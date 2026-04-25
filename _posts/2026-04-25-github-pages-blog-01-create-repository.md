---
title: "GitHub Pages 블로그 만들기 1. 저장소 만들기"
date: 2026-04-25 17:20:00 +0900
categories: [github-pages, jekyll, blog]
tags: [github, github-pages, repository, jekyll]
---

# GitHub Pages 블로그 만들기 1. 저장소 만들기

GitHub에 저장소를 만들고 Jekyll 테마를 연결해 블로그를 운영하는 방식은 생각보다 단순하다.  
핵심은 "저장소를 만든다", "정적 사이트를 올린다", "GitHub Pages로 배포한다"의 세 단계다.

이번 글에서는 그 출발점인 저장소 생성부터 정리해보려고 한다.

## 왜 GitHub Pages로 블로그를 만들까

GitHub Pages는 GitHub 저장소를 기반으로 정적 사이트를 배포할 수 있게 해준다.

이 방식의 장점은 꽤 분명하다.

- Git으로 글과 설정을 함께 관리할 수 있다.
- Markdown 중심으로 작성할 수 있다.
- 별도 서버 비용 없이 공개 블로그를 운영할 수 있다.
- 개발 기록, 문서, 기술 노트를 쌓기에 잘 맞는다.

특히 Jekyll 테마와 함께 쓰면 블로그의 외형까지 비교적 빠르게 갖출 수 있다.

## 사용자 페이지와 프로젝트 페이지

GitHub Pages에는 크게 두 가지 방식이 있다.

첫 번째는 사용자 페이지다.

- 저장소 이름이 `username.github.io`
- 배포 주소가 `https://username.github.io/`

두 번째는 프로젝트 페이지다.

- 저장소 이름이 자유롭다. 예: `blog-20260425`
- 배포 주소가 `https://username.github.io/repository-name/`

내 경우에는 블로그 실습용 저장소를 따로 만들었기 때문에 프로젝트 페이지 방식을 사용했다.

예를 들면 이런 형태다.

- 저장소: `blog-20260425`
- 주소: `https://unisong114.github.io/blog-20260425/`

## GitHub에서 새 저장소 만들기

GitHub에 로그인한 뒤 새 저장소를 만든다.

진행 순서는 아래와 같다.

1. GitHub 우측 상단의 `New repository`를 누른다.
2. 저장소 이름을 입력한다.
3. 공개 저장소 여부를 선택한다.
4. `Create repository`를 누른다.

기술 블로그라면 보통 `Public` 저장소가 편하다.  
GitHub Pages는 공개 콘텐츠를 배포하는 목적에 잘 맞고, 포트폴리오나 기록 용도로도 활용하기 좋다.

## 저장소 이름은 어떻게 정하면 좋을까

프로젝트 페이지로 운영할 때는 저장소 이름이 그대로 URL 일부가 된다.  
그래서 너무 길거나 의미가 불분명한 이름보다는, 나중에 봐도 알아보기 쉬운 이름이 좋다.

예를 들면 다음처럼 정할 수 있다.

- `tech-blog`
- `notes`
- `study-log`
- `blog-20260425`

이 이름은 나중에 Jekyll 설정 파일에서 `baseurl`과도 연결된다.  
그래서 저장소 이름을 초반에 정리해두는 것이 생각보다 중요하다.

## 저장소를 만든 뒤 바로 보게 되는 화면

저장소를 막 만들면 GitHub는 보통 아래 명령어 흐름을 안내해준다.

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/username/repository.git
git push -u origin main
```

이 명령어는 로컬 폴더를 방금 만든 원격 저장소와 연결하기 위한 기본 흐름이다.  
다음 글에서는 바로 이 부분을 이어서 다룰 예정이다.

## 이번 단계에서 확인할 것

저장소를 만든 뒤에는 최소한 아래 항목을 확인해두면 좋다.

- 저장소 주소가 맞는지
- 기본 브랜치가 `main`인지
- 공개 저장소인지
- 앞으로 블로그 URL이 어떤 형태가 될지

이 정도만 정리되면 Jekyll 테마를 올릴 준비의 절반은 끝난 셈이다.

## 마무리

GitHub Pages 블로그 만들기의 첫 단계는 사실 복잡하지 않다.  
중요한 건 저장소를 어떤 방식으로 운영할지 먼저 정하는 것이다.

사용자 페이지로 갈지, 프로젝트 페이지로 갈지에 따라 주소 구조와 설정 방식이 조금 달라지기 때문이다.

다음 글에서는 로컬 폴더를 이 저장소와 연결하고, 첫 커밋과 푸시까지 진행해보겠다.
