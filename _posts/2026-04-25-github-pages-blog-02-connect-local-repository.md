---
title: "GitHub Pages 블로그 만들기 2. 로컬 폴더와 저장소 연결하기"
date: 2026-04-25 17:21:00 +0900
categories: [github-pages, jekyll, blog]
tags: [git, github, remote, push]
---

# GitHub Pages 블로그 만들기 2. 로컬 폴더와 저장소 연결하기

저장소를 만들었다면 다음은 로컬 작업 폴더를 그 저장소와 연결할 차례다.  
이 단계가 끝나야 Jekyll 설정 파일과 테마 파일을 실제로 관리할 수 있다.

이번 글에서는 Git 저장소 초기화, 원격 저장소 연결, 첫 커밋과 푸시 흐름까지 정리한다.

## 작업 폴더 준비

먼저 블로그 작업용 폴더를 만든다.

예를 들면 이런 식이다.

```bash
mkdir blog-20260425
cd blog-20260425
```

이 폴더 안에서 앞으로 블로그 관련 파일을 관리하게 된다.

## Git 저장소 초기화

이제 현재 폴더를 Git 저장소로 만든다.

```bash
git init
```

그러면 내부에 `.git` 폴더가 생기고, 이 디렉터리는 Git으로 관리되는 작업 공간이 된다.

필요하다면 기본 브랜치 이름도 함께 정리해준다.

```bash
git branch -M main
```

## 원격 저장소 연결

GitHub에서 만든 저장소 주소를 `origin`으로 등록한다.

```bash
git remote add origin https://github.com/unisong114/blog-20260425.git
```

잘 연결됐는지 확인하고 싶다면 아래 명령어를 사용할 수 있다.

```bash
git remote -v
```

출력 결과에 fetch와 push 주소가 모두 보이면 정상이다.

## 첫 파일을 추가하고 커밋하기

아직 본격적인 Jekyll 설정을 넣기 전이라면 간단한 `README.md`부터 만들어도 된다.

```bash
git add .
git commit -m "Initial commit"
```

이 커밋은 "이 저장소의 첫 상태"를 남기는 역할을 한다.  
나중에 블로그 구조가 커져도 첫 출발점을 다시 확인하기 쉽다.

## 원격 저장소로 푸시하기

이제 로컬 커밋을 GitHub에 올린다.

```bash
git push -u origin main
```

처음 푸시할 때 `-u` 옵션을 주면 이후에는 `git push`만으로도 같은 원격 브랜치에 올릴 수 있다.

## 이 단계에서 자주 만나는 문제

초기 연결 단계에서는 아래 같은 문제를 자주 만나게 된다.

### 1. 원격 저장소가 이미 설정된 경우

```bash
error: remote origin already exists.
```

이 경우에는 기존 원격을 확인하고, 필요하면 수정하면 된다.

```bash
git remote -v
git remote set-url origin https://github.com/unisong114/blog-20260425.git
```

### 2. 작성자 정보가 없는 경우

커밋 시 아래와 비슷한 메시지가 나올 수 있다.

```bash
Author identity unknown
```

그럴 때는 Git 사용자 정보를 먼저 설정한다.

```bash
git config user.name "your-name"
git config user.email "your-email@example.com"
```

### 3. 인증 문제로 푸시가 안 되는 경우

GitHub는 보안 정책상 비밀번호 대신 토큰이나 로그인된 인증 수단을 요구하는 경우가 많다.  
이 부분은 사용하는 환경에 따라 조금씩 다르니, 현재 로그인 방식이나 Git Credential Manager 설정을 확인하면 좋다.

## 여기까지 끝나면 무엇이 준비되나

이 단계를 마치면 적어도 아래 상태가 된다.

- 로컬 폴더가 Git 저장소가 된다.
- GitHub 원격 저장소와 연결된다.
- 첫 커밋이 만들어진다.
- 원격 `main` 브랜치에 푸시할 수 있다.

즉, 이제부터는 단순한 폴더가 아니라 "배포 가능한 블로그 프로젝트"의 기본 틀이 갖춰진 것이다.

## 마무리

저장소 생성보다 실제로 더 중요한 건 이 연결 단계일 수 있다.  
이 과정을 지나야 이후의 테마 설정, 페이지 구성, 배포 자동화가 모두 자연스럽게 이어지기 때문이다.

다음 글에서는 Jekyll 테마를 고르고, 그중 `Just the Docs`를 블로그에 적용하는 흐름을 정리해보겠다.
