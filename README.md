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
