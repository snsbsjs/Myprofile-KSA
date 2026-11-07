# Profile-KSA

전북대학교 컴퓨터인공지능학부 2학년 김수아의 개인 포트폴리오 사이트입니다.
2026학년도 초급프로젝트 과제 1로, Hugo 테마 **Hextra**를 사용해 만들고 GitHub Actions로 GitHub Pages에 자동 배포합니다.

- **사이트**: <https://snsbsjs.github.io/Myprofile-KSA/>
- **저장소**: <https://github.com/snsbsjs/Myprofile-KSA>

## 사이트 구성

| 메뉴 | 주소 | 내용 |
|---|---|---|
| 홈 | `/` | 이름과 짧은 소개, 소개·대표 활동 카드, GitHub 버튼 |
| 소개 | `/about/` | 관심 분야, 학습 목표와 실행 계획, 사용하는 기술과 도구 |
| 활동 | `/projects/` | 대표 활동: 동아리 정기모임 신청 사이트 |

## 폴더 구조

실제 사이트는 `site/` 폴더 안에 있습니다. 저장소 최상위의 나머지 파일(`layouts/`, `docs/` 등)은 처음 내려받은 Hextra 원본 ZIP의 파일이며, 빌드에는 `site/` 폴더만 사용합니다.

| 경로 | 역할 |
|---|---|
| `site/hugo.yaml` | 사이트 설정 (사이트 이름, 메뉴, 언어 등) |
| `site/pages.json` | GitHub Pages용 배포 주소(baseURL) 설정. 준비 스크립트가 생성 |
| `site/content/_index.md` | 홈 화면 |
| `site/content/about/index.md` | 소개 페이지 |
| `site/content/projects/index.md` | 활동 페이지 |
| `site/themes/template/` | Hextra 테마 파일 |
| `.github/workflows/hugo-pages.yml` | GitHub Actions 자동 빌드·배포 설정 |
| `.github/pages_build.py` | Actions에서 실행하는 빌드 스크립트 (수업 제공 `prepare_github_pages.py`의 사본) |

## 필요한 도구와 버전

GitHub Actions의 자동 배포에서는 아래 버전을 사용합니다. (`.github/workflows/hugo-pages.yml`에 지정)

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo (extended) | 0.167.0 | 사이트 빌드 |
| Go | 1.27.1 | Hugo 모듈로 테마 불러오기 |
| Dart Sass | 1.105.0 | 스타일 처리 |
| Node.js | 24 | 빌드 보조 도구 설치 |
| Python | 3.12 | 빌드 스크립트 실행 |

내 컴퓨터에서 미리 보려면 **Hugo extended**와 **Go**만 있으면 됩니다. 테마가 검색 기능용 스크립트를 인터넷(CDN)에서 받아오므로 인터넷 연결이 필요합니다.

## 설치 (Windows)

~~~powershell
winget install Hugo.Hugo.Extended
winget install GoLang.Go
~~~

설치 후 PowerShell을 다시 열고 버전을 확인합니다.

~~~powershell
hugo version
go version
~~~

## 빌드와 미리보기

모든 명령은 `site` 폴더에서 실행합니다.

~~~powershell
cd site
~~~

**미리보기 서버** (파일을 저장하면 자동으로 새로고침됩니다)

~~~powershell
hugo server --config hugo.yaml,pages.json --theme template --themesDir themes
~~~

브라우저에서 <http://localhost:1313/Myprofile-KSA/> 를 엽니다. 끝내려면 `Ctrl + C`를 누릅니다.

**빌드만 하기** (결과는 `site/public/` 폴더에 생성)

~~~powershell
hugo --config hugo.yaml,pages.json --theme template --themesDir themes
~~~

## 내용 수정하기

| 바꾸고 싶은 것 | 수정할 파일 |
|---|---|
| 홈 화면 문구·카드·GitHub 버튼 | `site/content/_index.md` |
| 소개 페이지 | `site/content/about/index.md` |
| 활동 페이지 | `site/content/projects/index.md` |
| 사이트 이름, 상단 메뉴, 사이트 설명 | `site/hugo.yaml` |

페이지 내용은 마크다운(Markdown)으로 작성합니다. `##`는 소제목, `-`는 목록, `**글자**`는 굵은 글씨입니다.

## 재배포와 확인

`main` 브랜치에 push하면 GitHub Actions가 자동으로 빌드하고 GitHub Pages에 배포합니다.

1. 파일을 수정하고 저장합니다.
2. 바뀐 파일을 커밋하고 push합니다.

~~~powershell
git status
git add 수정한파일경로
git commit -m "무엇을 바꿨는지 설명하는 메시지"
git push
~~~

3. 저장소의 **Actions** 탭에서 방금 push한 커밋으로 실행이 시작되었는지 확인합니다.
4. 실행 안의 **build**와 **deploy**가 모두 초록색 체크가 될 때까지 기다립니다. (보통 1~3분)
5. 시크릿 창에서 <https://snsbsjs.github.io/Myprofile-KSA/> 를 열어 바뀐 내용을 확인합니다. 예전 화면이 보이면 `Ctrl + F5`로 새로고침합니다.

**실패했을 때**: 빨간 X가 뜬 실행을 눌러 실패한 단계의 로그를 확인합니다.
- `REF_NOT_FOUND`처럼 `ERROR`가 있으면 내용·설정 문제이므로 파일을 고쳐 다시 push합니다.
- deploy 단계의 `Timeout reached`처럼 일시적인 문제면 **Re-run failed jobs**로 다시 실행합니다.


## 출처와 라이선스

| 자료 | 사용 위치 | 구분 | 출처 | 이용 조건 |
|---|---|---|---|---|
| Hextra 테마 | `site/themes/template/`, 저장소 최상위의 원본 파일 | 외부 자료 | <https://github.com/imfing/hextra> | MIT License, Copyright (c) 2023 Xin. 원문은 [`LICENSE`](./LICENSE)에 그대로 유지 |
| 배포 준비 스크립트와 워크플로 | `.github/pages_build.py`, `.github/workflows/hugo-pages.yml`, `site/pages.json` | 외부 자료 (수업 제공) | 수업 제공 `prepare_github_pages.py` 3.1 | 수업 자료 |
| 사이트 문구 (홈·소개·활동) | `site/content/` | 직접 제작 + AI 도움 | 본인 경험과 내용을 바탕으로 작성 | 아래 AI 활용 범위 참고 |
| 사이트 설정 수정 | `site/hugo.yaml`, `site/content/_index.md` | 직접 제작 + AI 도움 | 본인 판단으로 적용 | 아래 AI 활용 범위 참고 |
| 관리자 설정 화면 캡처 | `site/content/projects/admin-settings.png` | 직접 제작 | 본인이 운영 중인 동아리 신청 사이트를 직접 캡처 | 부원 이름 등 개인정보가 보이지 않는 화면으로 촬영 |

사이트 아래쪽의 "Powered by Hextra" 표시는 테마 출처 고지로 그대로 두었습니다.

### AI 활용 범위

- **사용 도구**: Claude (claude.ai)
- **사이트 문구**: 활동 내용, 관심 분야, 목표 등 모든 사실은 본인이 제공했고, AI가 문장을 정리한 초안을 본인이 검토·수정해 반영했습니다.
- **설정과 오류 해결**: 데모 콘텐츠 정리 방법, 메뉴·카드·이미지 펼침 상자 설정, 빌드 실패 원인 분석에 AI의 제안을 참고했고, 적용 여부는 본인이 판단하고 Actions 결과와 공개 사이트에서 직접 확인했습니다.
