# MkDocs에 Google AdSense 연동하기

MkDocs 사이트에 Google AdSense 광고를 추가하는 방법을 설명합니다.

## 사전 준비사항

- Google AdSense 계정
- 승인된 웹사이트
- AdSense 광고 코드

## 방법 1: extra_javascript를 사용한 전역 설정

### 1. AdSense 스크립트 파일 생성

`docs/js/adsense.js` 파일을 생성합니다:

```bash
mkdir -p docs/js
```

```javascript
// docs/js/adsense.js
// Google AdSense 자동 광고 코드
(adsbygoogle = window.adsbygoogle || []).push({
    google_ad_client: "ca-pub-YOUR-PUBLISHER-ID",
    enable_page_level_ads: true
});
```

### 2. mkdocs.yml 설정

```yaml
site_name: My Wiki

extra_javascript:
  - https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-YOUR-PUBLISHER-ID
  - js/adsense.js

extra:
  analytics:
    gtag: G-YOUR-TRACKING-ID  # Google Analytics (선택사항)
```

## 방법 2: HTML 템플릿 오버라이드

### 1. 커스텀 템플릿 디렉토리 생성

```bash
mkdir -p overrides
```

### 2. mkdocs.yml에 custom_dir 추가

```yaml
theme:
  name: material
  custom_dir: overrides
```

### 3. 메인 템플릿 오버라이드

`overrides/main.html` 파일 생성:

```html
{% extends "base.html" %}

{% block extrahead %}
  {{ super() }}
  <!-- Google AdSense -->
  <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-YOUR-PUBLISHER-ID"
     crossorigin="anonymous"></script>
{% endblock %}

{% block content %}
  {{ super() }}
  
  <!-- 콘텐츠 하단 광고 -->
  <div class="admonition adsense">
    <ins class="adsbygoogle"
         style="display:block"
         data-ad-client="ca-pub-YOUR-PUBLISHER-ID"
         data-ad-slot="YOUR-AD-SLOT-ID"
         data-ad-format="auto"
         data-full-width-responsive="true"></ins>
    <script>
         (adsbygoogle = window.adsbygoogle || []).push({});
    </script>
  </div>
{% endblock %}
```

## 방법 3: 특정 페이지에만 광고 추가

### 1. 페이지 템플릿 생성

`overrides/partials/adsense.html`:

```html
<div class="adsense-container" style="margin: 2rem 0;">
    <ins class="adsbygoogle"
         style="display:block"
         data-ad-client="ca-pub-YOUR-PUBLISHER-ID"
         data-ad-slot="YOUR-AD-SLOT-ID"
         data-ad-format="auto"
         data-full-width-responsive="true"></ins>
    <script>
         (adsbygoogle = window.adsbygoogle || []).push({});
    </script>
</div>
```

### 2. 마크다운 파일에서 광고 삽입

```markdown
# 페이지 제목

일부 콘텐츠...

!!! adsense ""
    <ins class="adsbygoogle"
         style="display:block"
         data-ad-client="ca-pub-YOUR-PUBLISHER-ID"
         data-ad-slot="YOUR-AD-SLOT-ID"
         data-ad-format="auto"></ins>
    <script>
         (adsbygoogle = window.adsbygoogle || []).push({});
    </script>

더 많은 콘텐츠...
```

## 광고 스타일링

커스텀 CSS 추가 (`docs/css/adsense.css`):

```css
/* AdSense 광고 컨테이너 스타일 */
.adsense-container {
    margin: 2rem auto;
    padding: 1rem;
    background-color: #f5f5f5;
    border-radius: 8px;
    text-align: center;
}

/* 광고 레이블 */
.adsense-container::before {
    content: "Advertisement";
    display: block;
    font-size: 0.8rem;
    color: #666;
    margin-bottom: 0.5rem;
}

/* 반응형 광고 */
@media (max-width: 768px) {
    .adsense-container {
        margin: 1rem 0;
        padding: 0.5rem;
    }
}
```

mkdocs.yml에 CSS 추가:

```yaml
extra_css:
  - css/extra.css
  - css/adsense.css
```

## 중요 고려사항

### 1. AdSense 정책 준수

- 과도한 광고 배치 피하기
- 콘텐츠와 광고의 명확한 구분
- 사용자 경험 우선 고려

### 2. 성능 최적화

```javascript
// 지연 로딩 구현
document.addEventListener('DOMContentLoaded', function() {
    // 스크롤 시 광고 로드
    let adsLoaded = false;
    window.addEventListener('scroll', function() {
        if (!adsLoaded && window.scrollY > 100) {
            loadAdsense();
            adsLoaded = true;
        }
    });
});

function loadAdsense() {
    const script = document.createElement('script');
    script.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-YOUR-PUBLISHER-ID';
    script.async = true;
    script.crossOrigin = 'anonymous';
    document.head.appendChild(script);
}
```

### 3. 광고 위치 추천

- **헤더 하단**: 네비게이션 바로 아래
- **사이드바**: 목차 옆 공간 활용
- **콘텐츠 중간**: 긴 글의 중간 섹션
- **푸터 상단**: 페이지 하단 콘텐츠 끝

## 테스트 및 디버깅

1. **로컬 테스트**:
   ```bash
   mkdocs serve
   ```

2. **광고 표시 확인**:
   - 개발자 도구에서 광고 요청 확인
   - AdSense 대시보드에서 노출 수 확인

3. **일반적인 문제**:
   - 광고가 표시되지 않음: AdSense 승인 상태 확인
   - 레이아웃 깨짐: CSS 충돌 검사
   - 느린 로딩: 지연 로딩 구현 고려

## 참고 자료

- [Google AdSense 도움말](https://support.google.com/adsense/)
- [MkDocs 템플릿 커스터마이징](https://www.mkdocs.org/user-guide/customizing-your-theme/)
- [Material for MkDocs 커스터마이징](https://squidfunk.github.io/mkdocs-material/customization/)