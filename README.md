# blog-20260425

`Just the Docs` 테마를 사용하는 GitHub Pages 블로그 저장소입니다.

## 로컬 실행

1. Ruby와 Bundler를 설치합니다.
2. 프로젝트 루트에서 `bundle install`
3. `bundle exec jekyll serve`
4. 브라우저에서 `http://localhost:4000/blog-20260425/` 확인

## 배포

이 저장소는 GitHub Actions로 GitHub Pages에 배포되도록 설정되어 있습니다.

GitHub에서 아래만 확인하면 됩니다.

1. `Settings`
2. `Pages`
3. `Build and deployment`
4. `Source`를 `GitHub Actions`로 선택

배포 주소:

- <https://unisong114.github.io/blog-20260425/>

## 이미지 넣는 위치

포스트에 넣을 이미지는 아래 경로에 두면 됩니다.

- 공용 이미지: `assets/images/`
- 글별 이미지: `assets/images/posts/`

예시:

- `assets/images/posts/github-pages-flow.png`
- `assets/images/posts/jekyll-theme-settings.png`

Markdown에서는 이렇게 사용할 수 있습니다.

```md
![설명]({{ '/assets/images/posts/github-pages-flow.png' | relative_url }})
```

프로젝트 페이지는 `baseurl`이 붙기 때문에, 가능하면 위처럼 `relative_url` 필터를 사용하는 편이 안전합니다.
