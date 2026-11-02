> [!NOTE]
> **This skill lives in the main collection: [milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills/tree/main/skills/ui-taste)**. Please ⭐ star it there; that's where updates land first.
> Docs: **https://milad-ahmd.github.io/agent-skills/skills/ui-taste/** · Claude Code: `/plugin install all-skills --marketplace milad-ahmd/agent-skills`

<div align="center">

# 💅 ui-taste

**Scores your CSS and Tailwind for one-off sizes, near-duplicate colours and off-grid spacing, then consolidates them into tokens. An Agent Skill for Claude Code, Cline, Cursor, Codex and other AI coding agents.**

[![License: MIT](https://img.shields.io/github/license/milad-ahmd/ui-taste)](LICENSE)
[![Stars](https://img.shields.io/github/stars/milad-ahmd/ui-taste?style=social)](https://github.com/milad-ahmd/ui-taste)
![Category](https://img.shields.io/badge/category-Frontend-blue)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cline%20%7C%20Cursor%20%7C%20Codex-8A2BE2)

[Install](#-install) · [Usage](#-usage) · [How it works](skills/ui-taste/SKILL.md) · [All skills](https://github.com/milad-ahmd/agent-skills)

</div>

> Part of **[agent-skills](https://github.com/milad-ahmd/agent-skills)**, a growing collection of practical skills for AI coding agents.

## 📦 Install

**One command (installs the whole collection):**

```bash
curl -fsSL https://raw.githubusercontent.com/milad-ahmd/agent-skills/main/install.sh | bash -s -- ui-taste
```

**Manually (Claude Code):**

```bash
git clone https://github.com/milad-ahmd/ui-taste /tmp/ui-taste
mkdir -p ~/.claude/skills && cp -r /tmp/ui-taste/skills/ui-taste ~/.claude/skills/
```

**Per project:** copy `skills/ui-taste` into `<project>/.claude/skills/`.
**Any other agent:** paste [`SKILL.md`](skills/ui-taste/SKILL.md) into your rules or system prompt.

## 💬 Usage

Just ask your agent:

```text
Our app looks amateur, fonts and spacing are all over the place
This UI screams AI-generated, make it look less generic
```

The full workflow, rules and output format are in [`SKILL.md`](skills/ui-taste/SKILL.md).

## 🔎 Sample output

`ui_lint.py` is plain Python 3 with no dependencies. Real output on the deliberately messy fixture that ships with it (the clean one scores 99):

```text
$ python3 ui_lint.py fixtures/messy --top 2

ui-lint: 1 css, 2 markup files, 83 declarations, 30 Tailwind utilities
skipped: 1 ignored folder, 2 minified

Score: 21/100

  fonts              4.0/10  4 families (target <= 2)
  type scale        12.5/15  10 distinct sizes (target <= 8)
  colours            0.0/20  27 distinct, 5 near-duplicate groups, 8 hue groups (azure, blue, orange, red, rose, spring green, violet, yellow)
  spacing            0.0/15  21 of 24 values off the 4px grid (88%)
  radii/shadows      3.3/10  9 radii, 7 shadows (target <= 4 each)
  contrast           0.0/10  9 of 9 same-rule pairs below WCAG AA
  overrides          1.5/8   4 !important (3.5 per 100 declarations), 3 z-index > 1000, 5 distinct z-index
  arbitrary values   0.0/7   11 design-token arbitrary values in 30 utilities
  generic look       0.0/5   purple/blue gradient, 5 emoji in markup, 11 of 11 text-align settings centred

Top issues (biggest point loss first)
  colours (-20.0)
    near-duplicates, likely meant to be the same: #3b82f6 (2) ~ #3a80f5 (1)  [dE <= 1.09]  src/styles.css:33, src/styles.css:40
    near-duplicates, likely meant to be the same: #323232 (1) ~ #333333 (1) ~ #343434 (1)  [dE <= 0.92]  src/styles.css:11, src/styles.css:4, src/styles.css:8
    mixed neutral families: gray, slate (pick one grey)
  spacing (-15.0)
    18px x4  src/Pricing.jsx:6
    13px x2  src/Pricing.jsx:5
  contrast (-10.0)
    #555555 on #666666 = 1.30:1 (needs 4.5)  src/index.html:11
    #bbbbbb on #ffffff = 1.92:1 (needs 4.5)  src/index.html:7
…
```

`--baseline before.json` prints the score change per category after a cleanup, and `--fail-below N` gates CI. Exit codes: `0` ok, `1` below the floor, `2` nothing to scan.

## 🧩 More skills

See the full collection: **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 🤝 Contributing

This repo is a read-only mirror. Please open issues and PRs in **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 📄 License

[MIT](LICENSE) © Milad Ahmadi

<div align="center">

**If this skill saved you time, a ⭐ helps others find it.**

</div>
