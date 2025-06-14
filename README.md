# June Kim's Wiki

이 저장소는 MkDocs를 사용하여 관리되는 개인 위키입니다.

## 문서 추가 방법

1. `docs/` 디렉토리에 새로운 마크다운(`.md`) 파일을 생성합니다.
2. `mkdocs.yml` 파일의 `nav` 항목에 새 파일을 추가하여 네비게이션에 반영합니다.

## 로컬에서 문서 확인

```bash
mkdocs serve
```

- 위 명령어를 실행하면 `http://127.0.0.1:8000`에서 문서를 미리 볼 수 있습니다.

## 문서 사이트 빌드

```bash
mkdocs build
```
- `site/` 디렉토리에 정적 파일이 생성됩니다.

## 변경사항을 GitHub Pages에 반영하기

```bash
mkdocs gh-deploy
```
- 위 명령어를 실행하면 변경된 문서가 GitHub Pages에 자동으로 배포됩니다.
- GitHub Pages 설정이 필요할 수 있습니다. ([공식 가이드](https://www.mkdocs.org/user-guide/deploying-your-docs/#github-pages) 참고)

자세한 내용은 [MkDocs 공식 문서](https://www.mkdocs.org/)를 참고하세요. 