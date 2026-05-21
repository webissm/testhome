# Vibe Coding 랜딩페이지

> AI 업무 자동화 교육 홍보용 랜딩페이지

---

## 파일 구조

```
project1/
├── landing.html   # 페이지 구조 + 스크립트
└── landing.css    # 전체 스타일
```

---

## 페이지 섹션 구성

| 순서 | 섹션 | 주요 내용 |
|------|------|-----------|
| 1 | **Hero** | 메인 헤드라인 + 이메일 신청 폼 |
| 2 | **대상** | 추천 대상 3가지 카드 |
| 3 | **결과물** | 랜딩페이지 / 업무자동화 / 챗봇 |
| 4 | **커리큘럼** | STEP 01~05 카드 + 신청 폼 |
| 5 | **FAQ** | 자주 묻는 질문 아코디언 |
| 6 | **Footer** | 교육명, 링크, 카피라이트 |

---

## 디자인 시스템

### 컬러 (CSS 변수)

| 변수 | 값 | 용도 |
|------|----|------|
| `--primary` | `#7C3AED` | 보라 — 주요 강조 |
| `--secondary` | `#60A5FA` | 네온 블루 — 보조 강조 |
| `--gradient` | 보라 → 블루 | 버튼, 로고 |
| `--gradient-text` | 라이트 보라 → 블루 | h1 텍스트 |

### 다크 / 라이트 모드

`data-theme` 속성으로 전환. `:root`(다크)와 `[data-theme="light"]`(라이트) 두 세트의 변수로 관리.

| 변수 | 다크 | 라이트 |
|------|------|--------|
| `--bg` | `#0A0A0F` | `#F4F4FF` |
| `--bg-card` | `#13131A` | `#FFFFFF` |
| `--text-1` | `#F0F0FF` | `#12122A` |
| `--text-2` | `#9090A8` | `#50507A` |

### 타이포그래피

| 변수 | 크기 | 용도 |
|------|------|------|
| `--fs-hero` | `clamp(2.8rem, 7vw, 5.5rem)` | h1 |
| `--fs-h2` | `clamp(1.9rem, 4vw, 3rem)` | 섹션 제목 |
| `--fs-sub` | `clamp(1rem, 2.5vw, 1.35rem)` | 히어로 서브 |
| `--fs-body` | `0.95rem` | 본문 |

---

## 인터랙션 & UX

### 스크롤 fade-in
`IntersectionObserver`로 `.reveal` 클래스 요소를 감지하여 `.is-visible` 클래스 부여.

```js
const io = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
        if (entry.isIntersecting) {
            setTimeout(() => entry.target.classList.add('is-visible'), i * 90);
            io.unobserve(entry.target);
        }
    });
}, { threshold: 0.12 });
```

### 이메일 신청
"지금 신청하기" 클릭 시 `mailto:smjcreate@naver.com`으로 메일 클라이언트 실행.

```js
window.location.href = 'mailto:smjcreate@naver.com?subject=...&body=...';
```

### FAQ 아코디언
`.faq-item`에 `.is-open` 토글 + `max-height` 트랜지션으로 슬라이드 효과. 한 번에 하나만 열림.

### 다크/라이트 모드 토글
`localStorage`에 선택값 저장하여 페이지 재방문 시 유지.

---

## 반응형 (모바일 퍼스트)

| 구분 | 브레이크포인트 | 주요 변화 |
|------|---------------|-----------|
| 모바일 | `< 768px` | 햄버거 메뉴, 하단 고정 CTA 버튼, 1열 그리드 |
| 데스크톱 | `≥ 768px` | 상단 네비게이션, 하단 CTA 숨김, 3열 그리드 |

### 모바일 전용 UI
- **하단 고정 CTA 바** — 스크롤해도 항상 화면 하단에 표시
- **햄버거 메뉴** — 드로어 형태로 전체 화면 펼침

---

## 커리큘럼 내용

| STEP | 제목 | 결과 |
|------|------|------|
| 01 | 바이브 코딩의 이해 | AI와 함께 코딩하는 패러다임 이해 |
| 02 | Claude Code 가이드 | 자연어로 코드 작성, AI 협업 개발 환경 구축 |
| 03 | 파일정리 자동화 | 자동화 스크립트로 수작업 제거 |
| 04 | 랜딩 페이지 제작 | AI와 함께 전문 홍보 페이지 제작 |
| 05 | AI 에이전트 만들기 | OpenAI API 기반 챗봇·에이전트 개발 |

---

## 기술 스펙

- **언어**: HTML5 / CSS3 / JavaScript (ES6+, 외부 라이브러리 없음)
- **시맨틱 태그**: `header`, `main`, `section`, `article`, `footer`
- **접근성**: ARIA 레이블, `aria-expanded`, `aria-live`, `role` 속성 적용
- **CSS 설계**: `:root` 변수 기반, 모바일 퍼스트 반응형
- **JS 패턴**: IIFE(`(function(){})()`)로 전역 스코프 오염 방지

---

## 수정 가이드

### 연락 이메일 변경
`landing.html` 내 `mailto:` 주소 수정:
```js
window.location.href = 'mailto:변경할이메일@도메인.com?subject=...';
```

### 컬러 변경
`landing.css` 상단 `:root` 변수 수정:
```css
:root {
    --primary: #7C3AED;   /* 메인 컬러 */
    --secondary: #60A5FA; /* 보조 컬러 */
}
```

### 커리큘럼 STEP 추가/수정
`landing.html`의 `#curriculum` 섹션 내 `.step-grid` 안에 `<article class="step-card reveal">` 블록 추가.
