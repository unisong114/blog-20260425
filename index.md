---
title: Home
nav_order: 1
description: GitHub Pages blog home
---

# Unisong Blog

이 사이트는 GitHub Pages 위에서 `Just the Docs` 테마로 운영되는 블로그입니다.

## 시작하기

- 새 글은 [`_posts/`](_posts/) 아래에 Markdown 파일로 추가합니다.
- 상단 네비게이션에 고정할 페이지는 루트에 `.md` 파일을 만들고 `title`, `nav_order`를 넣으면 됩니다.
- 사이트 설정은 [`_config.yml`](_config.yml)에서 바꿀 수 있습니다.

## 최근 글

{% assign latest_posts = site.posts | slice: 0, 5 %}
{% if latest_posts.size > 0 %}
{% for post in latest_posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}
{% else %}
- 아직 게시된 글이 없습니다. 첫 글을 작성해 보세요.
{% endif %}
