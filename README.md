# blog-kr — 한국증시 레시피

한국 증시 일일 보고서·주간 분석·투자 상식을 다루는 정적 블로그(Hugo + GitHub Pages).
서버의 `report-service`(Claude Code 구독, $0)가 Markdown 포스트를 생성·push하면
GitHub Actions가 Hugo로 빌드해 Pages에 배포한다.

- 사이트: https://m-been.github.io/blog-kr/
- 테마: [PaperMod](https://github.com/adityatelange/hugo-PaperMod) (git submodule, `themes/PaperMod`)
- 빌드/배포: `.github/workflows/publish.yml` (push → Hugo build → Pages, **빌드 전용**)

## 구조

```
hugo.toml                     사이트 설정(메뉴/탁소노미/AdSense client 등)
content/
  about.md  privacy.md  contact.md   신뢰 3페이지(AdSense 필수)
  posts/                              글(일일보고서/주간레시피/투자상식 카테고리)
layouts/partials/
  extend_head.html                   AdSense 스크립트(adsenseClient 설정 시)
  extend_footer.html                 posts 글 하단 면책문 자동 삽입
  disclaimer.html                    면책문 본문
static/ads.txt                       AdSense 승인 후 게시자 ID 입력
```

## 로컬 미리보기 (Hugo extended 필요)

```bash
git submodule update --init --recursive
hugo server -D
```

## 발행 흐름

- **일일 보고서**: 컴플라이언스 통과 시 `main` 직접 push → 자동 빌드·배포
- **주간/에버그린**: draft 브랜치 → 초안 PR → 사람 머지 → 빌드·배포

## 배포 전 체크리스트

- [ ] `content/contact.md` 의 이메일을 실제 주소로 교체
- [ ] AdSense 승인 후 `hugo.toml` 의 `adsenseClient` + `static/ads.txt` 게시자 ID 입력
- [ ] GitHub repo Settings → Pages → Source = "GitHub Actions"
