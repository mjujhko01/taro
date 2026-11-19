# 타로카드 — Design Guide
> 한밤의 점집 — 어두운 남색 바탕 위에 연두 한 점

**Theme:** dark only (라이트 모드 없음)
**Platform:** 모바일 웹 우선 (기준 폭 375px, 최대 폭 480px)
**기준 자료:** 기획 문서 `TARO_01~04` + 선배가 준 「명지대학교 타로 디자인 팩」(이하 **디자인 팩**) + Tailwind v4 · shadcn 규칙

## 0. 이 문서가 디자인 팩과 맞춘 것 · 다르게 한 것

디자인 팩은 **라이트 테마**(연회색 바탕 + 흰 카드 + 연두 강조) 한 벌이다. 이 프로젝트는 **다크로 통일**하기로 했으므로, 팩에서 **구조는 그대로** 가져오고 **색 값만 다크용으로 바꿨다.**

| 구분 | 내용 |
|---|---|
| 팩 그대로 | 색 **역할 이름**(14개 토큰), 서체(Noto Sans KR), 글자 스타일 8개(크기 · 줄 높이 · 자간 -2%), 컴포넌트 구성 · 크기 · 모서리 반경, 아이콘 7개, 카드 그림(Rider-Waite-Smith 1909), 카드 뽑기 모션, 저장 · 공유 안내 흐름 |
| 다크용으로 바꿈 | 색 **값**. 바탕 · 면 · 글자 · 테두리를 어두운 남색 계열로 새로 정했다. **팩에 없는 값이므로 이 문서가 기준**이다 (2장) |
| 팩 + 결정 | 강조색은 팩의 연두 `#00D959`를 그대로 쓴다. 기존 금색은 폐기. Primary 버튼 글자는 다크 통일에 맞춰 **어두운 글자**(`on-accent`)로 한다 (흰 글자는 대비 1.9:1이라 쓰지 않는다) |
| 팩에서 달라진 점 | 주제 칩은 **글자만**(이모지 없음). 카드 이름은 명조가 아니라 Headline(Noto Sans KR Bold). 금빛 후광 · 명조 서체 폐기 |

> 팩의 `TARO_04 와이어프레임`은 이모지 칩(💼 💰 …)이 들어 있다. 이 문서는 팩을 따라 칩에서 이모지를 뺐으므로, 와이어프레임 문서와 달라진다. 와이어프레임 갱신 여부는 별도로 정한다.

---

## 1. 원칙

1. **카드가 주인공**: 결과 화면에서 카드 그림(Rider-Waite-Smith)이 가장 크고 눈에 띈다. 나머지는 조용하게.
2. **연두는 "지금 누를 것"**: 강조색 채움은 그 화면의 핵심 버튼 하나(타로 시작 · 카드 한 장 뽑기, 결과 화면은 [결과 공유])에만. 선택 표시(칩 · 포커스)에는 테두리로 쓴다.
3. **안심이 먼저**: 개인정보 안내(🔒)는 입력칸 바로 아래와 결과 화면에 항상 보이고, 읽을 수 있는 대비를 지킨다.
4. **짧고 또렷하게**: 해석은 3줄 · 90자 이내. 가운데 정렬.
5. **오락용임을 숨기지 않기**: "오락용 타로 해석입니다"는 결과 화면 · 저장 이미지 · 공유 글에 같은 문구로.
6. **엄지로 누른다**: 누르는 요소는 높이 44px 이상. 중요한 버튼은 화면 아래.

---

## 2. 색 (Colors)

토큰 이름은 디자인 팩과 같다. 값은 다크용이다. (Figma 변수 컬렉션 `Taro`, 모드 `Dark`)

| 토큰 | 다크 값 | 팩(라이트) 값 | 용도 |
|---|---|---|---|
| `color/bg` | `#0A0A14` | `#F3F3F5` | 화면 바탕 |
| `color/surface` | `#12121F` | `#FFFFFF` | 카드 · 입력창 · 칩 바탕 |
| `color/surface-sub` | `#1A1A2B` | `#F6F6F8` | 한 단계 올라온 면 (개인정보 안내, 눌렀을 때) |
| `color/text/primary` | `#FFFFFF` | `#000000` | 제목 · 해석 · 입력 값 |
| `color/text/secondary` | `#A3A3BD` | `#4D4D4E` | 설명 · 입력 라벨 · 칩 기본 글자 |
| `color/text/tertiary` | `#8A8AA6` | `#979F9B` | 안내 · 오락용 문구 · 자리 표시 |
| `color/text/on-accent` | `#0A0A14` | `#FFFFFF` | 강조색 · inverse 위의 글자 (**다크 통일에서 어두운 글자로 바꿈**) |
| `color/border` | `#3D3D57` | `#DCDCDD` | 입력창 · 보조 버튼 · 칩 테두리 |
| `color/accent` | `#00D959` | `#00D959` | Primary 버튼 · 선택 테두리 · 포커스 (**팩 그대로**) |
| `color/accent-soft` | `#0D2B1C` | `#E6FAEF` | 선택된 칩 바탕 · 카드 뒷면 장식 |
| `color/accent-strong` | `#00D959` | `#00D959` | 강조 글자 (선택된 칩 글자 · 카드 메타) |
| `color/disabled` | `#2A2A40` | `#D7D7D7` | 비활성 버튼 바탕 |
| `color/danger` | `#F27D7D` | `#E5484D` | 오류 테두리 · 오류 문구 |
| `color/inverse` | `#F3F3F5` | `#232427` | 토스트 바탕 (**다크에서는 밝은 면**) |
| `color/accent-illust` | `#00DE00` | `#00DE00` | 일러스트 · 스와이프 안내 글자 (**팩 그대로**) |

### 대비 (WCAG 계산값, 다크 값 기준)

| 글자 | 바탕 | 대비 | 판정 |
|---|---|---|---|
| text/primary | bg | 19.7 : 1 | 통과 |
| text/secondary | bg / surface / surface-sub | 8.0 / 7.5 / 7.0 : 1 | 통과 |
| text/tertiary | bg / surface / surface-sub | 5.9 / 5.5 / 5.1 : 1 | 통과 (4.5 이상) |
| on-accent | accent | 10.4 : 1 | 통과 |
| on-accent | inverse | 17.8 : 1 | 통과 |
| accent / accent-strong | bg / surface | 10.4 / 9.8 : 1 | 통과 |
| accent-strong | accent-soft | 8.0 : 1 | 통과 |
| danger | bg / surface | 7.5 / 7.1 : 1 | 통과 |
| text/tertiary | disabled | 4.2 : 1 | 비활성 요소라 예외 |
| 흰 글자 | accent (팩 원래 조합) | 1.9 : 1 | **쓰지 않음** |

- `color/border`는 bg 위에서 1.9:1이라 경계가 겨우 보인다. 입력창 · 칩은 **테두리 + 면 색 차이**를 함께 쓴다.
- 오류 · 성공은 **색만으로 알리지 않는다.** 문구(+ 아이콘)를 같이 둔다.

### shadcn 변수 매핑

| shadcn 변수 | 팩 토큰 |
|---|---|
| `--background` | `color/bg` |
| `--foreground` | `color/text/primary` |
| `--card` · `--popover` | `color/surface` |
| `--card-foreground` · `--popover-foreground` | `color/text/primary` |
| `--primary` | `color/accent` |
| `--primary-foreground` | `color/text/on-accent` |
| `--secondary` | `color/surface-sub` |
| `--secondary-foreground` | `color/text/secondary` |
| `--muted` | `color/surface` |
| `--muted-foreground` | `color/text/tertiary` |
| `--accent` | `color/accent-soft` |
| `--accent-foreground` | `color/accent-strong` |
| `--destructive` | `color/danger` |
| `--border` · `--input` | `color/border` |
| `--ring` | `color/accent` |

---

## 3. 글씨 (Typography)

서체는 **Noto Sans KR** 하나. 모든 스타일 자간 **-2%**. (Figma 글자 스타일 `Taro/…`)

| 스타일 | 굵기 | 크기 / 줄 높이 | 쓰는 곳 |
|---|---|---|---|
| `Taro/Display` | Bold | 28 / 38 | 시작 화면 제목 |
| `Taro/Title` | Bold | 22 / 32 | 화면 질문 ("어떤 주제가 궁금한가요?", 결과 상단 이름) |
| `Taro/Headline` | Bold | 18 / 26 | 카드 이름 · 앱 바 제목 |
| `Taro/Body` | Regular | 16 / 26 | **해석 본문** (가운데 정렬, 3줄) |
| `Taro/Body Bold` | Bold | 16 / 24 | L 버튼 글자 |
| `Taro/Label` | Medium | 15 / 22 | M 버튼 · 칩 · 토스트 |
| `Taro/Caption` | Regular | 13 / 19 | 안내 · 보조 · 오락용 문구 |
| `Taro/Caption Bold` | Bold | 13 / 19 | 입력 라벨 |

규칙
- 굵기는 Regular · Medium · Bold만 쓴다 (Noto Sans KR에 SemiBold 없음).
- 입력창 글자는 **16px 이상**(Body). 그보다 작으면 iOS에서 입력 때 화면이 확대된다.
- `word-break: keep-all`로 단어 중간에서 줄이 끊기지 않게 한다. 제목에는 `text-wrap: balance`.
- 영문 대문자 변환 · 넓은 자간 금지.

---

## 4. 간격 · 모양

**기준 단위:** 4px

### 간격

| 값 | 쓰는 곳 |
|---|---|
| 4 | 아이콘 미세 간격 |
| 6 | 버튼 아이콘과 라벨 사이 |
| 8 | 칩 사이 · 입력 라벨과 입력창 · 버튼 사이 |
| 10 | 개인정보 안내 아이콘과 글자 사이 |
| 12 | 하단 고정 버튼 영역 위쪽 여백 |
| 16 | 입력 항목 사이 · 결과 카드 안 간격 |
| 20 | **화면 좌우 여백** |
| 24 | 시작 화면 요소 사이 · 결과 카드 좌우 안쪽 여백 |
| 44 | 화면 맨 위 (상태 표시줄 영역) |

- 간격은 `flex` + `gap-*`으로. `space-x-*` · `space-y-*` 금지 (shadcn 규칙).
- 너비와 높이가 같으면 `size-*`.
- 하단 버튼 영역: `padding-bottom: max(34px, env(safe-area-inset-bottom))`.

### 모서리 반경 (팩 그대로)

| 요소 | 값 | 변수 |
|---|---|---|
| 화면 틀(디자인 파일용) | 32 | `radius/screen` |
| 결과 카드 | 24 | `radius/xl` |
| 칩 (알약) | 22 | `radius/pill` |
| L 버튼 | 16 | `radius/lg` |
| M 버튼 | 14 | `radius/md` |
| 입력창 · 개인정보 안내 · 토스트 · 카드 뒷면 | 12 | `radius/sm` |
| 카드 앞면(그림) | 10 | `radius/card` |

### 그림자 · 입체감

- 면 구분은 **면 색 단계 + 1px 테두리**로 한다.
- 카드 앞면(그림)만 그림자: `0 6px 16px rgba(0,0,0,0.12)` — 팩 값이며 다크에서는 약해 보이니 구현 때 `0.4`로 올려 쓴다. 선택된 카드는 `0 10px 28px`.
- 토스트 · 팝업은 그림자 없이 `inverse` 면의 대비로 구분한다.

### 면의 위계

| 단계 | 토큰 | 용도 |
|---|---|---|
| 0 | `color/bg` | 화면 바탕 |
| 1 | `color/surface` | 결과 카드 · 입력창 · 칩 |
| 2 | `color/surface-sub` | 개인정보 안내 · 눌렀을 때 |

---

## 5. 컴포넌트 규칙 (크기는 팩 그대로)

shadcn/ui 컴포넌트를 먼저 쓰고, 없을 때만 직접 만든다. 색은 의미 이름(`bg-primary` 등)만 쓴다.

### 5-1. 아이콘

20×20 · 선 두께 1.8 · 둥근 끝. 색은 붙는 글자 색을 따른다.

`chevron-left`(뒤로) · `download`(이미지 저장) · `share`(결과 공유) · `refresh`(다시 뽑기) · `home`(처음으로) · `lock`(개인정보) · `copy`(복사)

- 이모지 아이콘은 쓰지 않는다 (팩: 구현 시 SVG로 교체).
- 버튼 안 아이콘은 `data-icon="inline-start"`, 아이콘에 크기 클래스를 주지 않는다 (shadcn).

### 5-2. 버튼 (Button)

| 변형 | 크기 | 모양 | 글자 |
|---|---|---|---|
| **Primary L** | 335×56 · 반경 16 | 바탕 `accent` | `Body Bold` · `on-accent` |
| **Primary M** | 162×48 · 반경 14 | 바탕 `accent` | `Label` · `on-accent` |
| **Secondary L / M** | 335×56 / 162×48 | 바탕 `surface` · 1px `border` | `Body Bold` / `Label` · `text/primary` |
| **Disabled L / M** | 335×56 / 162×48 | 바탕 `disabled` | `text/tertiary` |

- 아이콘 20px, 아이콘과 라벨 간격 6px. 가운데 정렬.
- **화면당 Primary는 1개.** 결과 화면은 [결과 공유]만 Primary M, 나머지(이미지 저장 · 다시 뽑기 · 처음으로)는 Secondary M.
- L은 화면당 주요 행동(타로 시작 · 카드 한 장 뽑기), M은 결과 화면 2×2 버튼.
- Disabled: 이름 · 생년월일 · 주제 중 하나라도 비면. 이유가 보이게 입력칸 안내를 같이 둔다.
- 눌림 `scale-[0.98]`, 포커스 `focus-visible` 2px `accent` 링 + 2px 간격.
- 로딩은 `Spinner` + `disabled` 조합 (`isLoading` 없음).

### 5-3. 입력 (Field · Input)

`FieldGroup` + `Field` + `FieldLabel`로 만든다.

| 부분 | 값 |
|---|---|
| 라벨 | `Caption Bold` · `text/secondary` (예: "이름 (닉네임 OK)") |
| 입력창 | 335×52 · 반경 12 · 바탕 `surface` · 1px `border` · 좌우 16 |
| 라벨-입력창 간격 | 8 |
| 값 글자 | `Body` — 입력 전 `text/tertiary`, 입력 후 `text/primary` |
| 도움말 | `Caption` · `danger` (오류 때만) |

상태
- **Default**: 위 기본.
- **Filled**: 값 `text/primary`.
- **Focused**: 테두리 2px `accent`.
- **Error**: 테두리 1.5px `danger` + 아래 `danger` 문구 "날짜를 다시 확인해 주세요". 오류는 `Field`에 `data-invalid`, 입력창에 `aria-invalid`.

규칙: 이름 최대 10자 · 생년월일은 숫자 키패드(`inputmode="numeric"`)이고 실제 날짜만 허용 · 전공은 선택(라벨에 "선택" 표시) · 이름은 닉네임 권장(이미지 · 공유에 들어감).

### 5-4. 주제 칩 (Topic Chip, `ToggleGroup`)

선택지 2~7개이므로 `ToggleGroup`(단일 선택). 버튼을 반복해 선택 상태를 직접 만들지 않는다.

| 상태 | 모양 |
|---|---|
| Default | 105×44 · 반경 22(알약) · 바탕 `surface` · 1px `border` · `Label` `text/secondary` |
| Selected | 바탕 `accent-soft` · **1.5px `accent` 테두리** · 글자 15 Bold `accent-strong` |

- 3열 × 2행, 간격 8. 글자만(이모지 없음).
- 선택은 테두리 + 굵은 글자로 알린다 (색만으로 구분하지 않음).

### 5-5. 개인정보 안내 (Privacy Notice, `Alert`)

- 335 폭 · 반경 12 · 바탕 `surface-sub` · 좌우 16 / 상하 14 · lock 아이콘 20 + `Caption`(12~13) `text/secondary` · 간격 10.
- 입력 화면은 **입력칸 바로 아래**, 결과 화면은 버튼 아래. 같은 컴포넌트를 쓴다.
- 문구(입력 화면): "입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요."
- 불투명도를 낮추지 않는다.

### 5-6. 토스트 (Toast)

- 반경 12 · 바탕 `inverse`(밝은 면) · 좌우 20 / 상하 14 · `Label` `on-accent`(어두운 글자).
- 저장 성공 "이미지를 저장했어요" · 복사 성공 "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요".
- 프로젝트 base에 맞는 `toast` / `sonner`를 쓰고 직접 `z-index`를 주지 않는다. `role="status"`.

### 5-7. 앱 바 (App Bar)

- 375×56 · 좌우 16 · 간격 8. 왼쪽 뒤로(chevron-left 20) · 가운데 제목 `Headline` · 오른쪽 같은 크기 빈칸(제목을 가운데에 두기 위함).
- 속성: Title(글자), Show Back(켜기/끄기).

### 5-8. 타로 카드 (Tarot Card)

**그림**: Rider-Waite-Smith(1909) 메이저 아르카나 22장. 파일: 78 Tarot Cards. 직접 만든 그림이 아니므로 출처를 화면 · 저장소에 남긴다.

| 항목 | 값 |
|---|---|
| 앞면 | 160×268 · 반경 10 · 그림이 꽉 차게(FILL) · 그림자 |
| 뒷면 | 120×200 · 반경 12 · 바탕 `surface` · 2px `accent` 테두리 · 안쪽 8px 들여 1px `accent` 사각형(반경 8) · 가운데 64px 원(`accent-soft` + 1px `accent`) 안에 별 36 · 점 2개 |
| 크기 변형 | 결과 카드 160×268, 공개 화면 208×348, 시작 화면 부채꼴 128×214 |

**뒤집기 · 뽑기 모션** (F-3)
- 카드 뒷면 22장을 부채꼴(반지름 430, 간격 8°)로 펼치고 좌우 스와이프로 넘긴다. 탭한 카드가 가운데로 올라오며(0.5초, 크기 1.7배) 뒤집힌다(rotateY 180° 0.6초). 앞면은 22장 중 무작위, 정방향.
- 진입은 카드가 아래→위로 0.02초 간격(stagger). 결과 자리로 이동(FLIP 0.5초) 뒤 해석 줄이 0.08초 간격으로 나타난다.
- `transform` · `opacity`만 애니메이션한다. `prefers-reduced-motion: reduce`이면 4배 빠르게(거의 즉시).

### 5-9. 결과 카드 (Result Card)

335 폭 · 반경 24 · 바탕 `surface` · 좌우 24 / 상하 28 · 간격 16 · 가운데 정렬. 이 영역이 그대로 저장 이미지가 된다.

위에서 아래로
1. 제목 `지민님의 타로 · 커리어` (`Title`, `text/secondary`)
2. 카드 앞면 160×268
3. 메타 `XIX 태양 · 사자자리` (`Headline`, `accent-strong`)
4. 해석 3줄 (`Body`, `text/primary`, 가운데, 줄 간격 2) — 줄1 카드×주제 기본 문장(이름 포함), 줄2 별자리, 줄3 전공 계열
5. `※ 오락용 타로 해석입니다` (`Caption`, `text/tertiary`)

속성: Title · Meta · Line 1~3(글자), **Show Major Line**(켜기/끄기 — 전공 미입력 시 3줄째 끔).

### 5-10. 저장 이미지 (1080×1350 PNG)

결과 카드 영역 그대로. 이름 · 주제 · 카드 · 별자리 · 해석 3줄 · 오락용 안내 · 서비스 이름. **생년월일 · 전공 원문은 넣지 않는다.**

- 바탕 `bg`, 안전 여백 80, 간격 24. 카드 그림 폭 380(높이 약 637). 제목 48 · 메타 40 · 해석 36(줄 높이 1.5) · 오락용 28 · 서비스 이름 28. (Figma 파일의 저장 이미지 시안 기준)
- 서체는 이미지를 만들기 전에 불러와 둔다. 못 불러오면 `system-ui`로 대체.

### 5-11. 저장 · 공유 피드백 (F-5 · F-6)

| 상황 | 모양 |
|---|---|
| 저장 성공 | 토스트 "이미지를 저장했어요" |
| 자동 복사 성공 | 토스트(2줄) |
| 저장 안 됨 (인앱 브라우저) | 어두운 가림막(`inverse`를 쓰지 않고 `bg` 80%) 위 아래 시트: "이미지를 길게 눌러 저장해 주세요" + 이미지 160×200 + 버튼 |
| 복사 실패 | 시트: "아래 글을 길게 눌러 복사해 주세요" + 메시지 글 상자 + 버튼 |

- 시트 바탕은 `surface`, 반경 24(위쪽), 좌우 20 / 위 24.
- 공유 메시지 템플릿은 `TARO_04`와 같다. 생년월일 · 전공 원문 없음.

### 5-12. 화면 구조

| 화면 | 구성 |
|---|---|
| S-01 시작 | 세로 가운데 · 제목 Display · 카드 뒷면(부채꼴) · 설명 `Body` `text/secondary` · [타로 시작] Primary L · 오락용 안내 `Caption` |
| S-02 내 정보 | 앱 바 → `FieldGroup`(이름 · 생년월일 · 전공) → 주제 칩 → 개인정보 안내 → 하단 고정 [카드 한 장 뽑기] Primary L |
| S-03 결과 | 앱 바 → 결과 카드 → 버튼 2×2 → 개인정보 안내 |

- 좌우 여백 20, 간격 16, 상단 44(상태 표시줄), 하단 고정 영역 위 12 · 아래 34.
- 최대 폭 480으로 가운데. 그보다 넓으면 양옆을 `bg`로 채운다.

---

## 6. 모션

| 이름 | 길이 | 쓰는 곳 |
|---|---|---|
| fast | 150ms | 버튼 눌림 · 칩 선택 |
| base | 200ms | 화면 전환 페이드 · 토스트 등장 |
| pick | 500ms | 선택한 카드가 가운데로 |
| flip | 600ms | 카드 뒤집기 |
| reveal | 줄당 80ms 지연 | 해석 3줄 순서대로 등장 |

`@keyframes`는 `@theme`의 `--animate-*`로 정의. `prefers-reduced-motion`이면 이동 · 회전을 끄고 페이드만. 무한 반복 장식 모션 금지.

---

## 7. 접근성

- 누르는 요소 **44×44px 이상** (칩 높이 44, 버튼 48~56).
- 포커스 링은 항상 보인다 (2px `accent`).
- 카드 그림 `alt="XIX 태양 카드"`처럼 카드 이름.
- 오류 · 성공은 색 + 문구(+ 아이콘). 토스트 `role="status"`, 오류 문구 `role="alert"`.
- 본문 대비 4.5:1 이상 (2장 표). 확대 허용 (`user-scalable=no` 금지).

---

## 8. Tailwind v4 시작 코드

```css
@import "tailwindcss";

@custom-variant dark (&:where(.dark, .dark *));

@theme {
  /* 팩 토큰 이름 + 다크 값 */
  --color-bg: #0a0a14;
  --color-surface: #12121f;
  --color-surface-sub: #1a1a2b;
  --color-text-primary: #ffffff;
  --color-text-secondary: #a3a3bd;
  --color-text-tertiary: #8a8aa6;
  --color-on-accent: #0a0a14;
  --color-border: #3d3d57;
  --color-accent: #00d959;
  --color-accent-soft: #0d2b1c;
  --color-accent-strong: #00d959;
  --color-disabled: #2a2a40;
  --color-danger: #f27d7d;
  --color-inverse: #f3f3f5;
  --color-accent-illust: #00de00;

  /* shadcn 의미 이름 */
  --color-background: var(--color-bg);
  --color-foreground: var(--color-text-primary);
  --color-card: var(--color-surface);
  --color-card-foreground: var(--color-text-primary);
  --color-popover: var(--color-surface);
  --color-popover-foreground: var(--color-text-primary);
  --color-primary: var(--color-accent);
  --color-primary-foreground: var(--color-on-accent);
  --color-secondary: var(--color-surface-sub);
  --color-secondary-foreground: var(--color-text-secondary);
  --color-muted: var(--color-surface);
  --color-muted-foreground: var(--color-text-tertiary);
  --color-accent-foreground: var(--color-accent-strong);
  --color-destructive: var(--color-danger);
  --color-input: var(--color-border);
  --color-ring: var(--color-accent);

  /* 서체 · 글자 스타일 (자간 -2%) */
  --font-sans: "Noto Sans KR", system-ui, "Apple SD Gothic Neo", sans-serif;
  --tracking-taro: -0.02em;
  --text-display: 28px;      --text-display--line-height: 38px;
  --text-title: 22px;        --text-title--line-height: 32px;
  --text-headline: 18px;     --text-headline--line-height: 26px;
  --text-body: 16px;         --text-body--line-height: 26px;
  --text-label: 15px;        --text-label--line-height: 22px;
  --text-caption: 13px;      --text-caption--line-height: 19px;

  /* 반경 */
  --radius-card: 10px;
  --radius-sm: 12px;
  --radius-md: 14px;
  --radius-lg: 16px;
  --radius-pill: 22px;
  --radius-xl: 24px;

  /* 그림자 */
  --shadow-card: 0 6px 16px rgb(0 0 0 / 0.4);
  --shadow-card-picked: 0 10px 28px rgb(0 0 0 / 0.5);

  /* 모션 */
  --animate-fade-in: fade-in 0.2s ease-out;
  --animate-reveal: reveal 0.3s ease-out both;
  @keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
  @keyframes reveal {
    from { opacity: 0; transform: translateY(6px); }
    to { opacity: 1; transform: translateY(0); }
  }
}

@layer base {
  html { color-scheme: dark; }
  body {
    @apply bg-background text-foreground antialiased font-sans;
    letter-spacing: var(--tracking-taro);
    word-break: keep-all;
  }
}
```

`<html class="dark">`로 고정하고, 컴포넌트에서 `dark:` 색 덮어쓰기는 하지 않는다.

---

## 9. Do · Don't

### Do
- 팩의 토큰 이름 · 글자 스타일 이름 · 컴포넌트 크기를 그대로 쓴다.
- 강조색 채움은 한 화면에 Primary 버튼 하나.
- 연두 위 글자는 어두운 글자(`on-accent`).
- 해석은 `Body` + `text/primary` + 가운데 정렬 + 3줄.
- 선택 상태는 테두리 + 굵은 글자로, 오류는 문구와 함께.
- shadcn 컴포넌트(`Field`, `ToggleGroup`, `Alert`, `Badge`, `Spinner`)를 먼저 쓴다.

### Don't
- 흰 글자를 연두 바탕에 쓰지 않는다 (1.9:1).
- 이전 금색 · 명조 서체 · 금빛 후광을 쓰지 않는다.
- 팩에 없는 색 · 반경(`rounded-[13px]`) · 원색(`bg-blue-500`)을 임의로 쓰지 않는다.
- 굵기 SemiBold 이하/ExtraBold 이상을 쓰지 않는다 (Regular · Medium · Bold만).
- 개인정보 안내의 불투명도를 낮추거나 숨기지 않는다.
- 저장 이미지 · 공유 글에 생년월일 · 전공 원문을 넣지 않는다.
- 칩 · 아이콘에 이모지를 쓰지 않는다.

---

## 10. 남은 결정 · 확인 필요

| 항목 | 상태 |
|---|---|
| 다크 색 값 (`bg` ~ `inverse`) | 팩에 없는 값을 이 문서에서 정했다. 선배에게 다크 버전이 있는지 확인 |
| 카드 그림 22장 중 Figma 파일에는 태양 카드만 올림 | 나머지 21장은 구현 시 연결 |
| 카드 그림 출처 표기 위치 (화면 하단 · 설정 · 저장소 README) | 미정. Rider-Waite-Smith(1909) 공개 도메인 여부는 구현 전 재확인 |
| 와이어프레임(`TARO_04`)의 이모지 칩 | 팩은 글자만. 와이어프레임 문서 갱신 여부 미정 |
| 팩의 카드 고르기(스와이프) 화면 | 이 프로젝트 Figma 파일에는 아직 반영하지 않음 (기존 화면 유지) |
| 폰트 불러오기 방식 (Noto Sans KR 자체 호스팅 권장) | 미정 |
| 실제 기기(320px, 인앱 브라우저) 확인 | 구현 후 |
