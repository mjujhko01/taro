# 타로카드 — Design Guide
> 한밤의 점집 — 조용한 남색 밤하늘 위에 금빛 한 점

**Theme:** dark only (라이트 모드 없음)
**Platform:** 모바일 웹 우선 (기준 폭 375px, 최대 폭 480px)
**참고:** Linear 디자인 가이드를 타로 서비스에 맞게 바꾼 문서. 기획 문서 `TARO_01~04`와 Tailwind v4 · shadcn 규칙을 따른다.

타로 서비스의 디자인은 **카드 한 장이 주인공**이 되도록 나머지를 조용하게 둔다. 바탕은 푸른빛이 도는 거의 검은 남색(#0a0a14)이고, 글자는 흰색 계열이며, 금빛(#f0c76a) 하나만 "지금 누를 것"을 알린다. 장식은 최소로 하고, 카드 그림과 해석 문장이 화면의 유일한 볼거리가 된다. 입력 화면은 가볍고 안심되게, 결과 화면은 한 장의 이미지처럼 완결되게 만든다.

Linear에서 가져온 것: 어두운 면 위계, 헤어라인 테두리, 한 화면 한 개의 강조색, 작은 반경 어휘.
타로에서 바꾼 것: 강조색(산성 라임 → 달빛 금색), 서체(Inter → 한글 서체 Pretendard), 모바일 터치 크기, 카드 뒤집기 모션, 개인정보 안내 컴포넌트.

---

## 1. 원칙

1. **카드가 주인공**: 결과 화면에서 카드 그림이 가장 크고 밝다. 다른 요소는 카드보다 눈에 띄지 않는다.
2. **금색은 한 화면에 한 번**: 금색 채움은 그 화면의 핵심 버튼 하나(시작 · 카드 뽑기)에만. 장식 · 보조 버튼 · 링크에 쓰지 않는다.
3. **안심이 먼저**: 개인정보 안내(🔒)는 입력칸 바로 아래와 결과 화면에 항상 보이고, 읽기 쉬운 대비를 지킨다. 작아도 흐리게 만들지 않는다.
4. **짧고 또렷하게**: 해석은 3줄. 줄 사이를 넉넉히 띄우고 한 줄에 한 문장.
5. **오락용임을 숨기지 않기**: "오락용 타로 해석입니다"는 결과 화면 · 저장 이미지 · 공유 글에 같은 문구로 들어간다.
6. **엄지로 누른다**: 모든 누르는 요소는 높이 44px 이상. 중요한 버튼은 화면 아래쪽에 둔다.

---

## 2. 색 (Colors)

### 팔레트

| 이름 | 값 | 토큰 | 용도 |
|---|---|---|---|
| Void | `#0a0a14` | `--color-void` | 페이지 바탕 |
| Carbon | `#12121f` | `--color-carbon` | 카드 · 입력창 바탕 |
| Obsidian | `#1a1a2b` | `--color-obsidian` | 한 단계 올라온 면 (선택된 칩, 팝업) |
| Graphite | `#2a2a40` | `--color-graphite` | 구분선 · 헤어라인 테두리 (장식용) |
| Smoke | `#3d3d57` | `--color-smoke` | 입력창 · 칩 테두리 (눈에 보여야 하는 경계) |
| Ash | `#8a8aa6` | `--color-ash` | 보조 글자 · 비활성 아이콘 |
| Fog | `#a3a3bd` | `--color-fog` | 안내문 · 입력 라벨 |
| Mist | `#d6d6e6` | `--color-mist` | 본문 글자 |
| Paper | `#ffffff` | `--color-paper` | 제목 · 해석 문장 · 강조 글자 |
| Moon Gold | `#f0c76a` | `--color-gold` | **핵심 버튼 · 선택 표시 · 포커스 링** (유일한 강조색) |
| Iris | `#a99cff` | `--color-iris` | 별자리 · 카드 번호 등 작은 장식 글자 (버튼 금지) |
| Coral | `#f27d7d` | `--color-coral` | 오류 메시지 (생년월일 오류 등) |
| Mint | `#5ed08a` | `--color-mint` | 성공 안내 (저장 · 복사 완료) |

### 대비 (WCAG 계산값)

| 글자 | 바탕 | 대비 | 판정 |
|---|---|---|---|
| Paper | Void | 19.7 : 1 | 통과 |
| Mist | Void / Carbon | 13.7 / 12.9 : 1 | 통과 |
| Fog | Void / Carbon | 8.0 / 7.5 : 1 | 통과 |
| Ash | Void / Carbon / Obsidian | 5.9 / 5.5 / 5.1 : 1 | 통과 (본문 4.5 이상) |
| Void 글자 | Moon Gold 버튼 | 12.3 : 1 | 통과 |
| Gold | Void | 12.3 : 1 | 통과 |
| Coral · Mint · Iris | Void | 7.5 · 10.2 · 8.3 : 1 | 통과 |

- 테두리: Graphite는 Void 위에서 1.4:1로 거의 안 보이는 **장식용**이다. 입력창 · 칩처럼 "여기가 눌린다"는 경계는 Smoke(1.9:1)와 배경 차이를 함께 써서 알린다.
- 오류 · 성공은 **색만으로 알리지 않는다.** 아이콘 또는 문구를 반드시 함께 둔다.

### shadcn 변수 매핑

shadcn 컴포넌트는 `bg-primary`처럼 의미 이름만 쓴다. 아래처럼 연결한다.

| shadcn 변수 | 값 |
|---|---|
| `--background` | Void |
| `--foreground` | Paper |
| `--card` / `--popover` | Carbon |
| `--card-foreground` / `--popover-foreground` | Paper |
| `--primary` | Moon Gold |
| `--primary-foreground` | Void |
| `--secondary` | Obsidian |
| `--secondary-foreground` | Mist |
| `--muted` | Carbon |
| `--muted-foreground` | Ash |
| `--accent` | Obsidian |
| `--accent-foreground` | Paper |
| `--destructive` | Coral |
| `--border` | Graphite |
| `--input` | Smoke |
| `--ring` | Moon Gold |

---

## 3. 글씨 (Typography)

### 서체

| 역할 | 서체 | 대체 |
|---|---|---|
| 기본 (UI · 본문 · 제목) | **Pretendard Variable** | `system-ui`, `Apple SD Gothic Neo`, `Noto Sans KR` |
| 카드 이름 (선택) | **Noto Serif KR** 500 | `serif` |
| 숫자 · 로마 숫자 (XIX 등) | Pretendard, `font-variant-numeric: tabular-nums` | — |

- Inter는 한글 글리프가 없어 쓰지 않는다.
- 카드 이름에만 명조 계열을 쓰면 타로다운 분위기가 나온다. 다른 곳에는 쓰지 않는다.

### 크기 (모바일 기준)

| 역할 | 크기 | 굵기 | 줄 높이 | 자간 | 토큰 | 쓰는 곳 |
|---|---|---|---|---|---|---|
| display | 32px | 600 | 1.25 | -0.02em | `--text-display` | 시작 화면 제목 |
| title | 24px | 600 | 1.3 | -0.015em | `--text-title` | 화면 제목 · 결과 상단 "지민님의 타로" |
| card-name | 22px | 500 (serif) | 1.3 | 0 | `--text-card-name` | 카드 이름 |
| body-lg | 18px | 500 | 1.6 | -0.01em | `--text-body-lg` | **해석 3줄** |
| body | 16px | 400 | 1.6 | -0.01em | `--text-body` | 본문 · 입력 값 |
| label | 14px | 500 | 1.4 | -0.005em | `--text-label` | 입력 라벨 · 버튼 글자 |
| caption | 13px | 400 | 1.5 | 0 | `--text-caption` | 개인정보 안내 · 오락용 안내 |

### 규칙

- **입력창 글자는 16px 이상.** 그보다 작으면 iOS에서 입력할 때 화면이 확대된다.
- 굵기는 **400 · 500 · 600**만 쓴다. 700 이상 금지.
- 한글은 줄 높이 1.5~1.6을 지키고, `word-break: keep-all`로 단어 중간에서 끊기지 않게 한다. `text-wrap: balance`를 제목에 쓴다.
- 영문 대문자 변환(uppercase) · 넓은 자간 금지.
- 해석 문장은 `text-body-lg` + Paper 색. 한 줄에 한 문장.

---

## 4. 간격 · 모양 (Spacing & Shapes)

**기준 단위:** 4px · **밀도:** 여유 있음 (모바일 터치 우선)

### 간격

| 이름 | 값 | 쓰는 곳 |
|---|---|---|
| `gap-1` | 4px | 아이콘과 글자 사이 |
| `gap-2` | 8px | 칩 사이 · 버튼 사이 |
| `gap-3` | 12px | 라벨과 입력창 |
| `gap-4` | 16px | 입력 항목 사이 · 카드 안 간격 |
| `gap-6` | 24px | 섹션 사이 · 카드 안쪽 여백 |
| `gap-8` | 32px | 화면 큰 덩어리 사이 |
| `gap-12` | 48px | 시작 화면 위아래 여백 |

- 화면 좌우 여백 **20px**. 아래 버튼 영역은 `padding-bottom: max(20px, env(safe-area-inset-bottom))`로 홈 바를 피한다.
- 간격은 `flex` + `gap-*`으로 만든다. `space-x-*` · `space-y-*` 금지 (shadcn 규칙).
- 너비와 높이가 같으면 `size-*`를 쓴다 (`size-11`).

### 모서리 반경

| 요소 | 값 | 토큰 |
|---|---|---|
| 입력창 · 버튼 | 10px | `--radius-md` |
| 칩 (주제 선택) | 10px | `--radius-md` |
| 카드 컨테이너 · 결과 카드 | 16px | `--radius-xl` |
| **타로 카드 그림** | 12px | `--radius-card` |
| 배지 · 작은 태그 | 6px | `--radius-sm` |
| 알약 (토스트) | 9999px | `--radius-full` |

- 반경 어휘는 이 다섯 가지만. 임의 값(`rounded-[13px]`) 금지.

### 그림자 · 입체감

- 면 구분은 **면 색 단계 + 1px 테두리**로 한다. 큰 그림자 금지.
- 허용 그림자는 둘뿐이다.
  - 결과 카드 은은한 후광: `0 0 40px -8px rgba(240, 199, 106, 0.18)` (금빛이 아주 옅게 번짐. 결과 카드 한 곳에만)
  - 팝업 · 토스트: `0 4px 24px rgba(0, 0, 0, 0.5)`

### 면의 위계

| 단계 | 이름 | 값 | 용도 |
|---|---|---|---|
| 0 | Void | `#0a0a14` | 화면 바탕 |
| 1 | Carbon | `#12121f` | 입력창 · 결과 카드 |
| 2 | Obsidian | `#1a1a2b` | 선택된 칩 · 팝업 · 눌렀을 때 |

---

## 5. 컴포넌트 규칙

shadcn/ui 컴포넌트를 먼저 쓰고, 없을 때만 직접 만든다. 색은 의미 이름(`bg-primary`, `text-muted-foreground`)만 쓴다.

### 5-1. 버튼 (Button)

| 변형 | 모양 | 쓰는 곳 | 한 화면 수 |
|---|---|---|---|
| **primary** | 배경 Gold · 글자 Void · 높이 52px · 가로 가득 · 반경 10px · 14~16px / 600 | [타로 시작] · [카드 한 장 뽑기] | 1개 |
| **secondary** | 배경 Obsidian · 글자 Paper · 높이 48px | [이미지 저장] · [결과 공유] | 2개 |
| **outline** | 투명 · 1px Smoke 테두리 · 글자 Mist · 높이 48px | [다시 뽑기] | 1개 |
| **ghost** | 투명 · 글자 Fog · 높이 44px | [처음으로] · 뒤로 가기 | 자유 |

- 상태: hover는 밝기 +6%, **pressed는 `scale-[0.98]`**, **focus-visible은 2px Gold 링 + 2px 간격**, disabled는 불투명도 40% + `cursor-not-allowed`.
- **비활성 primary**는 [카드 한 장 뽑기] 조건 미충족 때 쓴다. 왜 비활성인지 알 수 있게 입력칸 안내를 같이 보여 준다.
- 아이콘은 `data-icon="inline-start"`로 넣고, 아이콘에 크기 클래스를 주지 않는다.
- 로딩 상태는 `Spinner` + `disabled`를 조합한다 (`isLoading` 속성 없음). 이미지 만드는 동안 [이미지 저장]에 쓴다.
- 결과 화면 버튼 배치: 2×2 그리드, `gap-2`. 윗줄 [이미지 저장] [결과 공유] / 아랫줄 [다시 뽑기] [처음으로].

### 5-2. 입력 (Field · Input)

- `FieldGroup` + `Field` + `FieldLabel`로 만든다. `div` + `space-y-*` 금지.
- 입력창: 높이 52px · 배경 Carbon · 1px Smoke 테두리 · 글자 Paper 16px · 자리 표시 글자 Ash · 반경 10px · 좌우 안쪽 여백 16px.
- 포커스: 테두리 Gold + 2px Gold 링 (옅게 40%).
- **오류**: `Field`에 `data-invalid`, 입력창에 `aria-invalid`. 테두리 Coral + 아래에 Coral 문구와 ⚠ 아이콘 ("날짜를 다시 확인해 주세요").
- 이름: `maxLength=10`, 오른쪽에 `3/10` 글자 수 (caption · Ash).
- 생년월일: 숫자 키패드(`inputmode="numeric"`), 연 · 월 · 일 3칸 또는 한 칸 자동 구분. 오류는 입력 확정(blur) 때 보여 준다.
- 전공은 라벨 옆에 `선택` 배지를 붙인다 (Badge secondary).

### 5-3. 주제 선택 (ToggleGroup)

주제 6개는 선택지 2~7개이므로 **`ToggleGroup`** (단일 선택)을 쓴다. 버튼을 반복해 직접 선택 상태를 만들지 않는다.

- 3열 × 2행 그리드, `gap-2`. 칩 높이 56px · 이모지(💼 💰 💕 🌿 📚 ✨) 위, 글자 아래 (또는 한 줄).
- 기본: 배경 Carbon · 1px Smoke 테두리 · 글자 Mist.
- 선택: 배경 Obsidian · **1px Gold 테두리** · 글자 Paper · 오른쪽 위 작은 ✓. (**색만으로 구분하지 않기 위해 ✓를 함께 둔다.**)
- 이모지는 장식이다 (`aria-hidden`). 칩 글자가 이름이다.

### 5-4. 카드 (Card)

`Card` · `CardHeader` · `CardTitle` · `CardContent` · `CardFooter`를 쓴다. 한 `CardContent`에 몰아넣지 않는다.

| 종류 | 모양 | 쓰는 곳 |
|---|---|---|
| **기본 카드** | 배경 Carbon · 1px Graphite 테두리 · 반경 16px · 안쪽 여백 24px · 그림자 없음 | 입력 영역 묶음 |
| **결과 카드** | 기본 카드 + 금빛 후광 · 안쪽 여백 24px · 폭 가득 | 저장 이미지가 되는 영역 |

결과 카드 안쪽 순서(위에서 아래로):
1. `지민님의 타로 · 커리어` (title 24px, Paper) + 주제 배지
2. 타로 카드 그림 (아래 5-5)
3. `XIX 태양 · ♌ 사자자리` (카드 번호 Iris · 카드 이름 serif Paper · 별자리 Iris)
4. 해석 3줄 (body-lg Paper, 줄 간격 12px)
5. `※ 오락용 타로 해석입니다` (caption Fog)

### 5-5. 타로 카드 그림 (TarotCard)

| 항목 | 값 |
|---|---|
| 비율 | **2 : 3** (예: 폭 200px · 높이 300px). 결과 카드 안에서 폭의 약 55% |
| 모서리 | 12px |
| 테두리 | 1px Gold (불투명도 60%) |
| 뒷면 | Obsidian 바탕 + Gold 헤어라인 별 문양 (직접 만든 그림) |
| 앞면 | 카드 그림 (출처가 분명한 그림만, PRD 리스크) |

**뒤집기 모션** (F-3)
- `rotateY(0 → 180deg)`, 길이 **0.8초** (1초 이내 조건), `cubic-bezier(0.2, 0.8, 0.2, 1)`, `transform-style: preserve-3d`.
- 뒤집는 동안 카드가 살짝 떠오른다 (`translateY(-8px)` → 0).
- `prefers-reduced-motion: reduce`이면 뒤집기 없이 **0.2초 페이드**로 바꾼다.
- 뒤집기가 끝나면 해석 3줄이 위에서 아래로 순서대로 나타난다 (줄마다 80ms 간격, 페이드 + `translateY(6px)`).

### 5-6. 개인정보 안내 (PrivacyNote)

입력 화면 · 결과 화면 공통. 기능명세의 안내문을 그대로 쓴다.

- `Alert` 컴포넌트로 만든다 (직접 만든 `div` 금지). 배경 Carbon · 1px Graphite 테두리 · 반경 10px · 안쪽 여백 12px 16px.
- 🔒 아이콘 + caption 13px · 글자 Fog. 줄 높이 1.5.
- 위치: 입력 화면은 **입력칸 바로 아래** (PRD 리스크 대응), 결과 화면은 버튼 아래.
- 흐리게 만들지 않는다. 불투명도 낮추기 금지.

### 5-7. 배지 (Badge)

- 기본: 배경 `rgba(255,255,255,0.06)` · 글자 Fog · 반경 6px · 높이 22px · 12px / 500.
- "선택" 표시 · 주제 표시에 쓴다. `span`에 색을 직접 입히지 않는다.

### 5-8. 안내 · 토스트

| 상황 | 종류 | 아이콘 | 색 |
|---|---|---|---|
| 이미지 저장 성공 · 복사 성공 | 토스트 (알약, 아래 중앙, 2.5초) | ✓ | Mint |
| 생년월일 오류 | 입력칸 아래 문구 | ⚠ | Coral |
| 이미지 저장 안 됨 | 화면 안 이미지 표시 + `Alert` ("길게 눌러 저장해 주세요") | ⓘ | Fog |
| 복사 실패 | 글 상자 표시 + `Alert` ("길게 눌러 복사해 주세요") | ⓘ | Fog |

- 토스트는 프로젝트가 쓰는 base에 맞는 `toast` / `sonner`를 쓴다. 직접 `z-index`를 주지 않는다.
- 문구는 `TARO_04` 안내 문구표를 그대로 쓴다.

### 5-9. 이미지 만들기용 카드 (저장 · 공유 이미지, 1080×1350)

저장 이미지는 화면 컴포넌트를 그대로 크게 그린 것이다. 따로 디자인하지 않는다.

- 크기 1080×1350 (4:5). 바탕 Void + 중앙에 은은한 금빛 방사형 빛(불투명도 8%, 한 번만).
- 안전 여백 80px. 카드 그림 폭 440px (2:3 → 높이 660px).
- 글자 크기는 화면의 약 3배로 쓴다: 제목 64px · 해석 40px(줄 높이 1.6) · 오락용 안내 28px.
- 하단 중앙에 서비스 이름 "🔮 오늘의 타로" (28px · Ash).
- 넣지 않는 것: **생년월일 · 전공 원문** (원칙 2).
- 서체는 이미지를 만들기 전에 불러와 둔다 (Pretendard · Noto Serif KR). 불러오지 못하면 `system-ui`로 대체해 글자가 깨지지 않게 한다.

### 5-10. 화면 구조

| 화면 | 구성 |
|---|---|
| S-01 시작 | 세로 중앙 정렬 · 카드 뒷면(폭 160px) → 제목 display → 설명 body → [타로 시작] primary → 오락용 안내 caption |
| S-02 내 정보 | 상단 바(← 제목) → `FieldGroup`(이름 · 생년월일 · 전공) → 주제 `ToggleGroup` → PrivacyNote → 하단 고정 [카드 한 장 뽑기] |
| S-03 결과 | 결과 카드 → 버튼 2×2 → PrivacyNote |

- 하단 고정 버튼 영역: 배경 Void + 위쪽에 Void → 투명 그라데이션 24px(내용이 버튼 뒤로 살짝 사라지는 용도. 이 그라데이션 외에 그라데이션 금지).
- 상단 바 높이 56px · 뒤로 가기는 ghost 아이콘 버튼 `size-11`.
- 최대 폭 480px로 가운데 정렬. 그보다 넓은 화면은 양옆을 Void로 채운다.

---

## 6. 모션

| 이름 | 길이 | 곡선 | 쓰는 곳 |
|---|---|---|---|
| fast | 150ms | ease-out | 버튼 눌림 · 칩 선택 |
| base | 200ms | ease-out | 화면 전환 페이드 · 토스트 등장 |
| flip | 800ms | `cubic-bezier(0.2, 0.8, 0.2, 1)` | 카드 뒤집기 |
| reveal | 줄당 80ms 지연 | ease-out | 해석 3줄 순서대로 등장 |

- `@keyframes`는 `@theme`의 `--animate-*`로 정의한다.
- `prefers-reduced-motion: reduce`이면 뒤집기 · 이동 모션을 끄고 페이드만 쓴다.
- 반짝이는 별 · 파티클 등 무한 반복 장식 모션은 쓰지 않는다 (집중과 배터리).

---

## 7. 접근성

- 모든 누르는 요소 **44×44px 이상**.
- 포커스 링은 항상 보인다 (Gold 2px). 제거 금지.
- 화면 읽기: 카드 그림에는 `alt="XIX 태양 카드"`처럼 카드 이름을 쓴다. 이모지는 `aria-hidden`.
- 오류 · 성공은 색 + 아이콘 + 문구 세 가지로 알린다.
- 토스트는 `role="status"`, 오류 문구는 `role="alert"`.
- 본문 대비 4.5:1 이상 (2장 표 참고).
- 확대 허용 (`user-scalable=no` 금지).

---

## 8. Tailwind v4 시작 코드

```css
@import "tailwindcss";

@custom-variant dark (&:where(.dark, .dark *));

@theme {
  /* 팔레트 */
  --color-void: #0a0a14;
  --color-carbon: #12121f;
  --color-obsidian: #1a1a2b;
  --color-graphite: #2a2a40;
  --color-smoke: #3d3d57;
  --color-ash: #8a8aa6;
  --color-fog: #a3a3bd;
  --color-mist: #d6d6e6;
  --color-paper: #ffffff;
  --color-gold: #f0c76a;
  --color-iris: #a99cff;
  --color-coral: #f27d7d;
  --color-mint: #5ed08a;

  /* shadcn 의미 이름 */
  --color-background: var(--color-void);
  --color-foreground: var(--color-paper);
  --color-card: var(--color-carbon);
  --color-card-foreground: var(--color-paper);
  --color-popover: var(--color-carbon);
  --color-popover-foreground: var(--color-paper);
  --color-primary: var(--color-gold);
  --color-primary-foreground: var(--color-void);
  --color-secondary: var(--color-obsidian);
  --color-secondary-foreground: var(--color-mist);
  --color-muted: var(--color-carbon);
  --color-muted-foreground: var(--color-ash);
  --color-accent: var(--color-obsidian);
  --color-accent-foreground: var(--color-paper);
  --color-destructive: var(--color-coral);
  --color-border: var(--color-graphite);
  --color-input: var(--color-smoke);
  --color-ring: var(--color-gold);

  /* 서체 */
  --font-sans: "Pretendard Variable", Pretendard, system-ui, "Apple SD Gothic Neo", "Noto Sans KR", sans-serif;
  --font-serif: "Noto Serif KR", serif;

  /* 글자 크기 */
  --text-display: 32px;
  --text-display--line-height: 1.25;
  --text-display--letter-spacing: -0.02em;
  --text-title: 24px;
  --text-title--line-height: 1.3;
  --text-title--letter-spacing: -0.015em;
  --text-card-name: 22px;
  --text-card-name--line-height: 1.3;
  --text-body-lg: 18px;
  --text-body-lg--line-height: 1.6;
  --text-body-lg--letter-spacing: -0.01em;
  --text-body: 16px;
  --text-body--line-height: 1.6;
  --text-label: 14px;
  --text-label--line-height: 1.4;
  --text-caption: 13px;
  --text-caption--line-height: 1.5;

  /* 반경 */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-xl: 16px;
  --radius-card: 12px;

  /* 그림자 */
  --shadow-glow: 0 0 40px -8px rgb(240 199 106 / 0.18);
  --shadow-pop: 0 4px 24px rgb(0 0 0 / 0.5);

  /* 모션 */
  --ease-flip: cubic-bezier(0.2, 0.8, 0.2, 1);
  --animate-fade-in: fade-in 0.2s ease-out;
  --animate-reveal: reveal 0.3s ease-out both;

  @keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  @keyframes reveal {
    from { opacity: 0; transform: translateY(6px); }
    to { opacity: 1; transform: translateY(0); }
  }
}

@layer base {
  html { color-scheme: dark; }
  body {
    @apply bg-background text-foreground antialiased font-sans;
    word-break: keep-all;
  }
}
```

- 이 서비스는 어두운 테마 하나뿐이므로 `<html class="dark">`로 고정하고, 컴포넌트에서 `dark:` 색 덮어쓰기는 하지 않는다 (shadcn 규칙).

---

## 9. Do · Don't

### Do
- 금색은 한 화면에 핵심 버튼 하나에만 쓴다.
- 해석 문장은 Paper 색 + 18px + 줄 높이 1.6으로 크게 보여 준다.
- 선택 상태는 테두리 색 + ✓ 아이콘으로 함께 알린다.
- 개인정보 안내는 입력칸 바로 아래에 읽히는 대비(Fog 이상)로 둔다.
- 간격은 `gap-*`, 정사각형은 `size-*`, 조건부 클래스는 `cn()`을 쓴다.
- shadcn 컴포넌트(`Field`, `ToggleGroup`, `Card`, `Alert`, `Badge`, `Spinner`)를 먼저 쓴다.
- 입력창 글자는 16px 이상.

### Don't
- 굵기 700 이상을 쓰지 않는다.
- 금색을 보조 버튼 · 링크 · 장식 · 본문 글자에 쓰지 않는다.
- Iris · Coral · Mint를 버튼 바탕이나 장식 채움에 쓰지 않는다 (글자 · 아이콘 · 작은 표시 전용).
- 큰 그림자 · 네온 번짐 · 무지개 그라데이션을 쓰지 않는다 (결과 카드 후광과 하단 버튼 영역 그라데이션만 예외).
- `rounded-[임의값]`, `bg-blue-500` 같은 원색 직접 지정 금지. 토큰만 쓴다.
- 개인정보 안내를 불투명도 낮추거나 아주 작게 만들지 않는다.
- 색만으로 상태를 알리지 않는다.
- 저장 이미지 · 공유 글에 생년월일 · 전공 원문을 넣지 않는다.
- 계속 반짝이는 장식 모션을 넣지 않는다.

---

## 10. 구현 전에 정할 것

| 항목 | 상태 |
|---|---|
| 카드 그림 22장 출처 · 스타일 (직접 제작 또는 허가된 그림) | PRD 미정. 그림 스타일에 따라 Gold 테두리 · 후광 강도를 다시 맞춘다 |
| Pretendard · Noto Serif KR 불러오기 방식 (자체 호스팅 권장 — 외부 CDN에 방문 기록이 가지 않게) | 미정 |
| 카드 뒷면 문양 | 미정 |
| 실제 기기(작은 화면 320px, 인앱 브라우저)에서 확인 | 구현 후 |
