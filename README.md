# Daily Insights

Astro static site for bilingual daily tech digests.

## Site Routes

- List: `/` and `/daily-insights`
- Detail: `/daily-insights/YYYY/MM/DD/`

## Local Development

```bash
npm install
npm run dev
```

Build output is generated to `dist/`:

```bash
npm run build
```

## Digest Content Paths

Content is stored under `src/daily-insights/content/`:

- Inbox: `src/daily-insights/content/inbox.md`
- Index: `src/daily-insights/content/index.json`
- Daily file: `src/daily-insights/content/YYYY/MM/DD.md`

## Digest Skill Usage

Digest skills are located under `src/daily-insights/.codex/skills/digest` and
`src/daily-insights/.claude/skills/digest`.

Run from the `src/daily-insights` directory:

```bash
cd src/daily-insights
```

Then:

- Codex: `$digest`
- Claude Code: `/digest`

Workflow:

1. Read URLs from `content/inbox.md` (relative to `src/daily-insights`)
2. Generate `content/YYYY/MM/DD.md` (EN first, then KO)
3. Update `content/index.json`
4. Clear `content/inbox.md`

## Automation

For Codex/Claude launchd schedule setup and operations:

- `src/daily-insights/scripts/automation/GUIDE.md`
