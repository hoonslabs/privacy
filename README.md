# hoonslabs — Privacy Policies

GitHub Pages로 호스팅되는 hoonslabs 앱 개인정보 처리방침 저장소.

**Live URL:** https://hoonslabs.github.io/privacy/

---

## 구조

```
privacy/
  index.html          ← 앱 목록 허브 페이지
  .nojekyll           ← Jekyll 비활성화 (순수 HTML)
  virmina/
    index.html        ← Virmina 개인정보 처리방침
  <appname>/
    index.html        ← 새 앱 추가 시 동일 구조
```

## URL 구조

| 앱 | URL |
|---|---|
| 허브 | `https://hoonslabs.github.io/privacy/` |
| Virmina | `https://hoonslabs.github.io/privacy/virmina/?lang=ko` |
| 새 앱 | `https://hoonslabs.github.io/privacy/<appname>/?lang=ko` |

`?lang=ko` / `?lang=en` 파라미터로 언어 선택. 미지정 시 브라우저 언어 자동 감지.

---

## GitHub Pages 설정 (최초 1회)

1. 저장소 → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / Folder: `/ (root)`
4. **Save**
5. 약 1분 후 `https://hoonslabs.github.io/privacy/` 접근 가능

---

## 새 앱 개인정보 처리방침 추가

### 1. 폴더 생성 및 파일 복사

```bash
cp -r virmina/ <new-app-name>/
```

### 2. 복사한 `index.html` 수정

| 항목 | 위치 |
|---|---|
| `<title>` | `<title>Privacy Policy — <AppName></title>` |
| 앱 이름 | `<h1>` 태그 내 서비스명 |
| 로고 이모지 | `.logo-mark` 내 이모지 |
| 유효일 | `최종 업데이트:` 날짜 |
| 이메일 | `privacy@<domain>` |
| 앱 설명 | 1번 섹션 개요 문단 |

### 3. 허브 페이지(`index.html`) 업데이트

`coming-soon` 카드 블록을 복사하여 실제 앱 카드로 변경:

```html
<a class="app-card" href="./<appname>/">
  <div class="app-card-left">
    <div class="app-icon" style="background: linear-gradient(135deg, #색상1, #색상2);">🎯</div>
    <div>
      <div class="app-name">앱 이름</div>
      <div class="app-desc">앱 설명</div>
    </div>
  </div>
  <span class="chevron">›</span>
</a>
```

### 4. 앱 코드에서 URL 연결

**iOS** (`SafariView.swift`):
```swift
// URL.privacyPolicy 와 동일한 방식으로 앱별 상수 추가
static var newAppPrivacyPolicy: URL {
    let lang = Locale.current.language.languageCode?.identifier == "ko" ? "ko" : "en"
    var c = URLComponents(string: "https://hoonslabs.github.io/privacy/<appname>/")!
    c.queryItems = [URLQueryItem(name: "lang", value: lang)]
    return c.url!
}
```

**Android** (`PrivacyPolicyLauncher.kt`):
```kotlin
private const val PRIVACY_POLICY_BASE_URL = "https://hoonslabs.github.io/privacy/<appname>/"
```

### 5. 커밋 & 푸시

```bash
git add .
git commit -m "feat: add <appname> privacy policy"
git push
```

푸시 후 약 30초~1분 내에 GitHub Pages에 반영됩니다.

---

## 개인정보 처리방침 내용 수정

```bash
# 내용 수정 후
git add virmina/index.html
git commit -m "docs(virmina): update privacy policy - 유효일 갱신"
git push
```

> 앱 코드 업데이트나 앱스토어 심사 없이 즉시 반영됩니다.

---

## 유효일 갱신 규칙

다음 변경 사항 발생 시 각 파일 상단 유효일을 갱신합니다.

- Google AdMob 정책 변경
- 새로운 데이터 수집 항목 추가
- 제3자 서비스 추가/제거
- 법률(GDPR, CCPA, PIPA) 개정 대응

---

## 앱별 링크 현황

| 앱 | 플랫폼 | 개인정보 처리방침 URL |
|---|---|---|
| Virmina | iOS / Android | `https://hoonslabs.github.io/privacy/virmina/` |
