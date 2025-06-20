# MkDocs와 GitHub Pages로 위키 사이트 만들기

MkDocs와 GitHub Pages를 활용하면 간단하게 위키 사이트를 만들고 무료로 호스팅할 수 있습니다.

## 사전 준비사항

- Python 설치
- Git 설치
- GitHub 계정

## 프로젝트 환경 설정

### 1. 프로젝트 디렉토리 생성

```bash
mkdir my-wiki
cd my-wiki
```

### 2. Python 가상환경 설정

pyenv를 사용하는 경우
```bash
pyenv local 3.12.2
python -m venv .venv
source .venv/bin/activate  # Mac/Linux
# Windows: .venv\Scripts\activate
```

### 3. MkDocs 설치

```bash
pip install mkdocs mkdocs-material
```

### 4. MkDocs 프로젝트 초기화

```bash
mkdocs new .
```

이 명령어는 다음과 같은 구조를 생성합니다.
```
my-wiki/
├── docs/
│   └── index.md
└── mkdocs.yml
```

## GitHub 리포지토리 설정

### 1. Git 초기화

```bash
git init
```

### 2. .gitignore 파일 생성

```bash
echo ".venv/" > .gitignore
echo "site/" >> .gitignore
```

### 3. GitHub에서 새 리포지토리 생성

GitHub에서 새 리포지토리를 생성합니다 (예: `my-wiki`)

### 4. 리모트 저장소 연결 및 푸시

```bash
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:<username>/my-wiki.git
git push -u origin main
```

## 사이트 배포

### 1. GitHub Pages로 배포

```bash
mkdocs gh-deploy
```

이 명령어는

- 사이트를 빌드하고
- `gh-pages` 브랜치를 생성하여
- 빌드된 파일을 푸시합니다

### 2. 사이트 확인

배포가 완료되면 다음 주소에서 사이트를 확인할 수 있습니다.
```
https://<username>.github.io/<repo-name>/
```

## 위키 문서 추가

### 1. 새 문서 생성

`docs` 폴더에 마크다운 파일을 추가합니다.

```bash
# 예: MkDocs 가이드 문서 생성
echo "# MkDocs 가이드" > docs/mkdocs-guide.md
```

### 2. 네비게이션 설정

`mkdocs.yml` 파일을 수정하여 네비게이션을 구성합니다.

```yaml
site_name: My Wiki

nav:
  - Home: index.md
  - MkDocs 가이드: mkdocs-guide.md
```

### 3. 로컬에서 미리보기

```bash
mkdocs serve
```

브라우저에서 `http://127.0.0.1:8000`으로 접속하여 확인할 수 있습니다.

### 4. 변경사항 배포

```bash
git add .
git commit -m "Add MkDocs guide"
git push
mkdocs gh-deploy
```

## Material 테마 적용 (선택사항)

더 현대적인 디자인을 원한다면 Material 테마를 적용할 수 있습니다.

```yaml
site_name: My Wiki

theme:
  name: material
  language: ko
  features:
    - navigation.tabs
    - navigation.sections
    - toc.integrate

nav:
  - Home: index.md
  - MkDocs 가이드: mkdocs-guide.md
```

## 팁

- **자동 배포**: GitHub Actions를 설정하면 main 브랜치에 푸시할 때마다 자동으로 배포할 수 있습니다
- **커스텀 도메인**: GitHub Pages 설정에서 커스텀 도메인을 연결할 수 있습니다
- **플러그인**: MkDocs는 다양한 플러그인을 지원합니다 (검색, PDF 내보내기 등)
- **마크다운 확장**: pymdown-extensions를 설치하면 더 많은 마크다운 기능을 사용할 수 있습니다

## 참고 자료

- [MkDocs 공식 문서](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages 문서](https://docs.github.com/en/pages)