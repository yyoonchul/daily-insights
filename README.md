# 📰 Daily Tech Digest

관심 있는 글의 링크를 모아두면, Claude Code가 읽고 요약하여 하루 1파일로 정리해주는 시스템.

## 사용법

### 1. 링크 모으기

`inbox.md`에 URL을 한 줄씩 추가한다.

```plaintext
https://techcrunch.com/2025/02/16/some-article
https://stripe.com/blog/api-update
https://news.ycombinator.com/item?id=xxxxx  # 요약만
```

### 2. 다이제스트 생성

Claude Code에서 `/digest` 실행.

```bash
claude
> /digest
```

### 3. 결과 확인

`content/YYYY/MM/DD.md`에 정리본이 생성된다.

## 구조

```plaintext
├── inbox.md                  # 링크를 넣는 곳
├── content/                  # 생성된 정리본
│   └── YYYY/MM/DD.md
├── .claude/skills/digest/    # Claude Code Skill
│   ├── SKILL.md
│   ├── prompt-summarize.md
│   └── template-daily.md
├── config/settings.yaml
└── README.md
```

## 출력 포맷

- **간단 요약**: 글별 불렛 3개씩 위에 쭉
- **상세 정리**: 글별 10\~20줄 분석 아래에 쭉 (같은 순서)

## 메모 기능

URL 뒤에 `#`으로 메모를 달 수 있다.

- `# 요약만` → 상세 정리 생략
- `# 중요` → 참고용 (처리에 영향 없음)