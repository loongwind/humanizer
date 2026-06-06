# AGENTS.md

Guidance for AI coding agents (Claude Code, Codex, Warp, OpenCode, etc.) working in this repository.

## What this repo is

This repository is a **Claude Code / OpenCode skill** implemented entirely as Markdown.

The runtime artifact is `SKILL.md`: the agent reads its YAML frontmatter followed by the editor prompt. There is no build step and no code to run. Claude Code uses fields such as `allowed-tools`; OpenCode recognizes a smaller field set and ignores unknown frontmatter fields.

This fork has been adapted for **Chinese AI-writing humanization**. It is not a literal translation of the English upstream. The prompt is rewritten for Chinese writing habits and common Chinese LLM artifacts.

## Key files

- `SKILL.md` — the skill itself. YAML frontmatter (`name`, `version`, `description`, `allowed-tools`) followed by the canonical, numbered pattern list with before/after examples. **This is the source of truth.** Note: `allowed-tools` is primarily a Claude Code field; OpenCode may ignore unknown fields.
- `README.md` — for humans: installation, usage, a summary table of the patterns, examples, and version history.
- `LICENSE` — MIT license inherited from upstream.

## The maintenance contract

`SKILL.md` and `README.md` must stay in sync. When you change behavior or content:

- **Patterns:** the skill currently defines **30 numbered Chinese AI-writing patterns**. If you add, remove, rename, or renumber any pattern, update:
  - the README pattern tables,
  - the “30 类中文 AI 写作痕迹” wording,
  - cross-references in `SKILL.md`,
  - the version history.
- **Version:** `SKILL.md` frontmatter has a `version:` field and `README.md` has a “版本历史” section. Bump both together.
- **Chinese-first behavior:** do not reintroduce English-only heuristics unless they are clearly useful for Chinese text. For example, title case and English curly quotes are not core Chinese patterns.
- **Non-obvious fixes:** if you change the prompt to handle a tricky failure mode, add a short note to README’s version history explaining what changed and why.

## Editing `SKILL.md`

- Preserve valid YAML frontmatter formatting and indentation.
- File tools in `allowed-tools` are for cases where the user explicitly asks the skill to read or rewrite files. For pasted text, the skill should normally return the rewrite in the conversation rather than writing files.
- The prompt below the frontmatter is the product. Edit it like a careful instruction document, not code.
- Keep examples in idiomatic Chinese.
- Prefer concrete before/after examples over abstract advice.
- Do not add rules that encourage inventing facts, data, citations, names, institutions, or examples not present in the source text.
- When adding a rule, include:
  1. a short pattern name,
  2. warning words or structures,
  3. why it sounds AI-generated,
  4. before/after examples.

## Style expectations for this fork

The skill should push Chinese text toward:

- concrete facts over abstract value claims,
- clear subjects and actions,
- fewer slogans and four-character phrase piles,
- fewer “赋能 / 助力 / 打造 / 生态 / 闭环” style placeholders,
- fewer formulaic “背景 → 价值 → 展望” paragraphs,
- natural rhythm rather than perfectly symmetrical paragraphs,
- no fabrication of facts.

## No build step

There are no tests, package scripts, or build artifacts. Verification consists of:

1. checking Markdown readability,
2. checking YAML frontmatter validity by inspection,
3. ensuring `SKILL.md` and `README.md` describe the same pattern count and version,
4. optionally trying `/humanizer` locally in Claude Code or OpenCode.
