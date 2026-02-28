# Translation Policy (Agent Guide v3.0)

## 0) 목적
- 결과물은 “번역문”이 아니라 **한국어로 처음부터 쓰인 글**처럼 읽혀야 합니다.
- 의미(사실/제약/의도)를 보존하되, 문장 구조·리듬·수사는 한국어 관습에 맞게 재작성합니다.
- 문체는 고정값이 아니라 **문서 스타일 시트(Style Sheet)의 선택 결과**입니다.
- 품질 하한을 보장하기 위해 **하드 게이트(통과/탈락)**를 둡니다.

---

## 1) 기본 방향
- Source: English
- Target: Korean

---

## 2) 우선순위 (Strict)
1) 자연스러운 한국어 가독성/리듬 (번역투 제거)
2) 의미 충실도 (의도/제약/사실 보존)
3) 용어 일관성 (글로서리 우선)
4) 수사/톤 재현 (한국어식 등가치환)

---

## 3) 4패스 작업 절차 (필수)
모든 작업은 반드시 아래 순서로 수행하고, 산출물을 저장합니다.

### Pass 0. Style Sheet 생성(내부 계약)
- 저장: `out/_meta/<same-filename>.style.json`
- 포함 필드(필수):
  - genre: (essay/op-ed/report/manual/interview/etc.)
  - stance: (monologue / addressing_reader / neutral_report)
  - default_register: (한다체 / 합니다체 / 해요체)
  - pov_base: (나는 / 저는 / 우리는)
  - reader_address: (none / 여러분 / 당신 / 독자)
  - permitted_shifts:
    - quote_blocks: true/false
    - emphasis_blocks: true/false
    - reader_address_blocks: true/false
    - scope: paragraph_only (fixed)
  - html_mode: true/false
  - html_scope:
    - translate_only_visible_text: true
    - include_tags: [article]
    - include_selectors: [p,h1,h2,h3,li,blockquote]
    - exclude_selectors: [head,title,meta,script,style,pre,code,.sf-hidden,nav,footer,form]
  - forbidden:
    - noun_only_sentences
    - random_register_mixing
    - html_tag_attr_changes
    - punctuation_spacing_loss
  - notes: short

### Pass 1. 1차 번역(의미 보존)
- 저장: `out/_draft/<same-filename>.ko.draft`
- 사실/수치/제약/범위를 정확히 옮깁니다.
- 어색함은 허용합니다(리라이트에서 해결).

### Pass 2. 2차 리라이트(한국어 원고화)
- 저장: `out/<same-filename>`
- 한국어 호흡으로 재구성합니다.
- 번역투 제거, 수사 등가치환, 단락 리듬 설계를 수행합니다.
- Style Sheet에서 허용한 전환만 “단락 단위”로 사용합니다.

### Pass 3. QA 게이트(통과 전 출력 금지)
- 저장: `out/_meta/<same-filename>.qa.md`
- 하드 게이트 실패 시 Pass 2 재실행 후 QA 재검사(최대 2회)

---

## 4) HTML 번역 규칙 (하드 룰)
HTML은 텍스트와 구조가 섞여 있으므로 번역 범위를 강제합니다.

### 4.1 번역 대상
- `article` 내부의 **가시 텍스트**(예: p/h1/h2/h3/li/blockquote)

### 4.2 번역 금지
- `head`, `title`, `meta`, `script`, `style`, `pre`, `code`, JSON-LD(schema)
- 태그명/속성명/클래스명/데이터 속성값
- 링크 URL, 이미지 src, data-* 값
- 숨김 텍스트(`.sf-hidden` 등 UI 숨김 카피)
- 폼 placeholder/버튼 UI 카피(기본 제외)

### 4.3 링크 처리
- URL은 그대로 유지
- 앵커 텍스트(사람이 읽는 문구)만 번역

---

## 5) 리라이트 규칙(전문 번역가 수준 핵심)

### 5.1 출력 파손/파편화 금지
- 명사만 단독으로 남는 문장 금지.
- 병렬 수사(Like A. Like B.)는 한국어에서 서술문으로 통합.

### 5.2 장문/나열 재구성
- 나열 3개 이상이면 문장 분해(2문장 이상).
- 쉼표 2개 이상이면 분해를 우선 검토.
- 결론 선제시 → 근거/조건 후술.

### 5.3 번역투 트리거 제한
- `~라고 할 수 있습니다`, `~처럼 들립니다`는 원문에 동일한 완곡이 있을 때만.
- 기본은 단정형/지시형/설명형.

### 5.4 수사/비유 등가치환
- 단어가 아니라 효과를 번역.
- 직역이 어색하면 관용 치환 → 이미지 재구성 → 설명형(효과 유지 시) 순.

---

## 6) QA 게이트

### 6.1 하드 게이트(FAIL이면 출력 금지)
1) **문장 공백 붕괴**
- 본문에 아래 패턴이 남아있으면 FAIL:
  - `([.?!])([가-힣A-Za-z0-9"'])`
  - 의미: 마침표/물음표/느낌표 뒤에 공백 없이 바로 글자가 붙음

2) **문체 무작위 혼용**
- 본문(인용 블록 제외)에서 아래가 공존하면 FAIL:
  - `나는` AND `저는`
  - `다/이다` 계열 종결 AND `습니다/입니다` 계열 종결
  - 독자 호칭(당신/여러분/귀하/독자) 중 2개 이상

3) **명사 단독문/파편 문장**
- “명사 + 마침표” 형태가 의미 단위 없이 연속되는 경우 FAIL

4) **HTML 구조 훼손**
- 태그/속성/스크립트/스타일 변경 또는 번역 금지 영역 번역 시 FAIL

5) **보존 요소 훼손**
- 숫자/단위/버전/코드블록/식별자 변형 시 FAIL

### 6.2 소프트 스코어(0–100) 루브릭
- A 의미/사실 충실도 (25)
- B 한국어 문장력/자연스러움 (25)
- C 담화 설계/장르 적합성 (15)
- D 화자/독자 관계·문체 운용 (15)
- E 용어/표기 정확성 (10)
- F 편집 품질/검수 통과 가능성 (10)

QA 로그에는 반드시 포함:
- 하드 게이트 체크리스트 PASS/FAIL + 근거 스니펫
- 소프트 스코어: 항목별 점수 + 총점
- 최우선 수정 3개

---

## 7) 보존 규칙(절대)
- Markdown 구조, 링크, 파일명/경로, 인라인 코드, 식별자
- 단위/숫자/버전 표기
- 코드 블록(``` ... ```) 번역 금지

---

## 8) [역주] 규칙
- 원문만으로 의미가 확정되지 않을 때만 최소로 사용.
- 새로운 사실 추가 금지.

---

## 9) 출력 규칙
- 최종 출력은 번역문만.
- 중간 과정은 파일로만 저장하고 출력하지 않음.
