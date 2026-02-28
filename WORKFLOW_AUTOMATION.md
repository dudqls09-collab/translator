# 번역 워크플로우 자동화 제안

현재 방식(수동 단일 HTML 다운로드 → 업로드 → `git pull` → 번역 요청)은 안정적이지만, 반복 비용이 큽니다. 아래처럼 **3단계 파이프라인**으로 바꾸면 효율이 크게 올라갑니다.

## 1) 수집 단계 자동화 (브라우저 측)

- 브라우저 확장(또는 userscript)에서 현재 페이지를 단일 HTML로 저장할 때,
  - 파일명 규칙을 고정합니다: `YYYYMMDD-HHMMSS__domain__slug.html`
  - 저장 직후 지정된 동기화 폴더(예: Dropbox/iCloud/GDrive 로컬 폴더)로 자동 이동합니다.
- 가능하면 메타데이터를 HTML 주석으로 삽입합니다.
  - 예: 원본 URL, 저장 시각, 언어 감지값

효과:
- 파일명 충돌 감소
- 입력 이력 추적 단순화

## 2) 리포 반입/정리 자동화 (로컬 스크립트)

리포 루트에 `scripts/intake.sh`를 두고 1회 명령으로 처리합니다.

권장 동작:
1. 리모트 최신화: `git pull --rebase`
2. 동기화 폴더에서 신규 HTML 스캔
3. 중복 검사(파일 해시 기준)
4. 신규 파일만 `/inbox`로 복사
5. `/inbox/index.csv`(선택) 갱신: `filename,url,imported_at,status`
6. 변경사항 자동 커밋(선택)

예시 명령:

```bash
bash scripts/intake.sh ~/Sync/translation_html
```

## 3) 번역 요청 자동화 (프롬프트 생성)

이미 있는 `prompts/TRANSLATE_TASK_TEMPLATE.md`를 기반으로, 대상 파일 목록을 넣은 요청문을 자동 생성합니다.

- `scripts/make_translate_request.sh`에서
  - `/inbox`의 미처리 파일을 찾고
  - 템플릿에 파일 목록을 주입한 뒤
  - 클립보드 복사 또는 `requests/`에 저장

효과:
- 매번 수동으로 파일명 복붙하지 않아도 됨
- 누락/중복 요청 감소

---

## 추천 운영 모델

- **Daily intake**: 하루 1~2회 `intake.sh` 실행
- **Batch translate**: 누적된 파일을 한 번에 번역 요청
- **Post-check**: `/out` 생성 확인 후 `STATUS.md` 업데이트

작업 상태를 명확히 하려면 `STATUS.md`에 아래 상태 태그를 통일합니다.

- `imported`
- `requested`
- `translated`
- `reviewed`

## 최소 구현 순서 (빠르게 시작)

1. 파일명 규칙 고정
2. `scripts/intake.sh` 추가
3. `scripts/make_translate_request.sh` 추가
4. 주 1회 회고: 누락/중복 케이스 점검

이 순서로 가면 기존 방식을 거의 유지하면서도 반복 작업을 크게 줄일 수 있습니다.
