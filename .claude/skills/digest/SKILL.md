---

## name: digest description: &gt; inbox.md에 쌓인 링크들을 읽고, 각 글의 본문을 수집·요약하여 날짜별 정리본 마크다운 파일을 생성합니다. "다이제스트 만들어줘", "오늘 링크 정리해줘" 같은 요청 시 사용합니다. disable-model-invocation: true allowed-tools: Bash, Read, Write, Glob, Grep

# Daily Digest 생성

inbox.md의 링크들을 수집·요약하여 `content/YYYY/MM/DD.md` 정리본을 생성합니다.

## 실행 단계

### 1. 인박스 읽기

- 프로젝트 루트의 `inbox.md` 파일을 읽는다.
- 각 줄을 파싱한다:
  - 빈 줄 → 무시
  - `#`으로만 시작하는 줄 (URL 없이) → 무시 (코멘트)
  - URL이 포함된 줄 → URL 추출. URL 뒤에 `#` 이후 텍스트가 있으면 메모로 분리.
- URL이 하나도 없으면 "📭 인박스가 비어있습니다."를 출력하고 **중단**.
- 중복 URL은 자동 제거 (정규화 후 비교).

### 2. 본문 수집

각 URL에 대해:

- 웹페이지를 fetch하여 본문을 읽는다.
- 메타데이터를 추출한다: 제목, 출처(도메인명 기반), 게시일.
- 수집 실패 시 (페이월, 404, 타임아웃 등):
  - 해당 글을 `⚠️ 수집 실패`로 표기.
  - 제목과 링크는 유지하되, 요약은 생략.

### 3. 요약 생성

수집된 본문을 기반으로 각 글마다 아래 항목을 생성한다. 요약 프롬프트 상세 지침은 [prompt-summarize.md](prompt-summarize.md)를 참조.

| 항목 | 규격 |
| --- | --- |
| 카테고리 | AI, DevTools, Cloud, Security, Frontend, Backend, Business, Open Source, HN, Misc 중 택 1 |
| 간단 요약 | 핵심 포인트 불렛 3개 (각 1줄) |
| 상세 정리 | 20\~30줄 분량의 상세 분석 |

- 메모에 "요약만"이 포함되어 있으면 해당 글의 상세 정리를 생략한다.

### 4. 정리본 생성

출력 포맷은 [template-daily.md](template-daily.md)를 참조.

- 파일 경로: `content/YYYY/MM/DD.md` (오늘 날짜 기준)
- 디렉토리가 없으면 자동 생성.
- 같은 날짜 파일이 이미 존재하면 기존 내용에 append.
  - 이미 있는 글(URL 기준)은 스킵.

### 5. 인박스 클리어

- `inbox.md` 파일 내용을 비운다 (파일은 유지, 내용만 클리어).

### 6. 완료 보고

아래 내용을 출력한다:

- ✅ 처리된 글 수
- 📄 생성된 파일 경로
- ⚠️ 실패한 URL 목록 (있는 경우)