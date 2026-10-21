# 🔥 Creative Spark

**The creative director skill for Claude Code — turns "bikinin konsep" into a shippable campaign in one message.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-5A32FB)](https://docs.claude.com/en/docs/claude-code/skills)
[![Version](https://img.shields.io/badge/version-2.0-orange)](CHANGELOG.md)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

Stop getting "here are 5 generic ideas" out of your AI. **Creative Spark** is a single Claude Code skill that turns any creative brief — a one-line idea or a full campaign — into distinct concepts, a real production plan, tool-ready prompts, and finished deliverables, for **18 mediums** from TikTok ads to game trailers to packaging design.

No API keys. No extra install. Drop one folder in and your Claude Code sessions think like a creative director.

---

## Table of Contents

- [Why this exists](#why-this-exists)
- [What it actually does](#what-it-actually-does)
- [Install in 30 seconds](#install-in-30-seconds)
- [See it work](#see-it-work)
- [Everything inside](#everything-inside)
- [The 18 mediums it covers](#the-18-mediums-it-covers)
- [New in v2.0: built for reach](#new-in-v20-built-for-reach)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## Why this exists

Ask most LLMs for "a creative idea" and you get three bullet points that are secretly the same idea wearing different adjectives — steam rising off coffee, a sunrise, a laptop in a café. Safe, forgettable, and indistinguishable from what a competitor's AI would also produce.

Creative Spark fixes this by giving Claude an actual creative *process*, not a vibe:

- A **Cliché Radar** that names the three obvious ideas first — so the real concepts have to beat them, not accidentally be them.
- A **Distinctness Test** — if two concepts could swap titles and nobody would notice, one gets cut.
- A **Deliverable Ladder** that tells you honestly whether you got a finished asset, a production-ready spec, or just a concept — never dressed up as more than it is.
- Depth that scales to the ask: a caption idea gets one sharp direction, not a 14-section production bible nobody asked for.

## What it actually does

| You say | Creative Spark delivers |
|---|---|
| "prompt gambar kucing astronot yang estetik" | One tool-ready prompt + a keyword version + 2 meaningful variations, in under a minute |
| "30s TikTok ad for my coffee shop" | 3 genuinely distinct concepts (not 3 colors of the same idea) → a recommendation → full shot list with timecodes → ready-to-paste video-gen prompts |
| "launch campaign, eco sneaker brand, 2 weeks, small budget" | Full **Creative DNA** (the single source of truth every asset obeys) → an asset matrix across platforms → a Lean version that fits the real budget |
| "give me 10 hook variations to test" | A **Variant Matrix** that crosses real axes (hook type × tone × format) instead of 10 near-duplicates, each tagged Safe-bet / Test-first / Wildcard |
| "bikin konten biar bisa viral" | The optional **Virality & Shareability Lens**: hook taxonomy, shareability triggers, platform literacy — with zero fake-virality promises |

## Install in 30 seconds

**Option A — project skill (recommended, scoped to one repo):**
```bash
git clone https://github.com/verycoolapps/creative-spark-skill.git
mkdir -p .claude/skills
cp -r creative-spark-skill/creative-spark .claude/skills/creative-spark
```

**Option B — personal skill (available in every Claude Code session):**
```bash
mkdir -p ~/.claude/skills
cp -r creative-spark-skill/creative-spark ~/.claude/skills/creative-spark
```

**Option C — packaged `.skill` file:** grab [`creative-spark.skill`](creative-spark.skill) from this repo and install it the way your Claude Code setup installs packaged skills.

That's it — no dependencies, no build step, no API key. Open Claude Code and ask for anything creative; the skill activates automatically on phrasing like *"ide kreatif," "bikin prompt gambar," "give me a concept," "make it go viral,"* or any brief that's creative-shaped even without those exact words.

## See it work

> **Prompt:** `Launch campaign for an eco sneaker brand: 30s film, 5 social posts, landing page hero, 2 weeks, small budget`

Creative Spark reads this as a **Campaign Spark** (multi-asset, multi-platform) and delivers, in one structured reply:

1. **The read** — objective, audience, the one insight that matters.
2. **3 distinct concepts**, each scored against the Cliché Radar baseline (forests, recycled-bottle reveals, slow-mo running — all named and avoided or deliberately subverted), tagged Anchor / Edge / Leap, with one recommended.
3. **Creative DNA** for the winner — palette, tone of voice, motion language, the "locks" every later asset must respect.
4. **Full production plan** — shot list with timecodes, asset register, a **Lean version** that fits a 2-week budget.
5. **A tool-adapted prompt pack** with continuity locks, so the shoe looks like the same shoe across every generated shot.
6. **Honest status** on every piece — Generated, Specified, or Proposed — never claiming a render exists if it doesn't.

## Everything inside

```
creative-spark/
├── SKILL.md                         # the core skill — laws, process, 18 sections
└── references/
    ├── medium-playbooks.md          # deep workflow per medium (18 mediums)
    └── prompt-adapters.md           # how to write prompts per generator tool type
```

- **396-line core skill** — intent decoding, concept generation, creative direction, prompt engineering, production planning, a 12-criterion quality gate, safety/rights/ethics, failure recovery.
- **18 medium-specific deep playbooks** — each with its own workflow, spec template, quality gates, and named failure modes.
- **10-section prompt-adapter reference** — because a Midjourney-style keyword chain and a natural-language video model read prompts completely differently, and a confident wrong syntax wastes your generation budget.

## The 18 mediums it covers

Video/ads/reels · Image & photography · Illustration · Motion graphics & animation · Audio & music · Storytelling & copy · Branding & identity · Advertising & campaigns · Presentations & decks · Web & interactive · 3D & creative coding · Emerging/hybrid (AR, installations) · **UGC & creator-style content** · **AI avatars & faceless channels** · **Game trailers & cinematics** · **Podcast covers/trailers/audiograms** · **Merch & print-on-demand** · **Out-of-home, packaging & retail**

## New in v2.0: built for reach

Four optional modules layer on top of the core skill whenever the brief actually calls for them — they never hijack a brief that isn't about reach:

- **Virality & Shareability Lens** — a named taxonomy of shareability triggers (surprise, identity signal, save-worthy, emotional peak, participation hook...) and hook types for the first 1–3 seconds, plus directional platform literacy. Explicitly refuses to promise guaranteed virality — this raises odds, it doesn't fake them.
- **Rapid Variant & Batch Generation** — a Variant Matrix method so "give me 10 hooks" produces 10 *actually different* bets instead of 10 rewordings, each tagged Safe-bet / Test-first / Wildcard.
- **Localization & Cross-Market Deep Dive** — goes past caption translation into idiom transfer, color/symbol meaning shifts, script/layout direction, and explicit Indonesian/SEA-market defaults.
- **Post-Launch Signal Reading** — maps real metrics (hook retention, save rate, CTR-vs-conversion gap) to the exact thing to fix next, so "the ad didn't convert" doesn't get misdiagnosed as a creative problem when it's actually an offer problem.

See [`CHANGELOG.md`](CHANGELOG.md) for the full diff from v1.

## FAQ

**Does this call any image/video/music generation API?**
No. It's pure prompt engineering for Claude Code — it writes the brief, the plan, and the prompts; you run the prompts in whatever generator you already use (or let Claude build what it can build directly: copy, SVG, HTML/CSS/JS, p5.js/three.js).

**Will it actually make my content go viral?**
No skill can promise that, and this one is built to refuse that promise explicitly (see §15.5 Trend-Jacking Ethics in `SKILL.md`). What it does is make sure you're not accidentally skipping the things that correlate with reach — a real hook, a real reason to share, a participation mechanic — instead of shipping a technically-fine asset with none of them.

**Does it work in Bahasa Indonesia?**
Yes — it replies in the user's language by default and includes explicit Indonesian/SEA-market localization defaults (§17).

**Can I use this for client work / commercial projects?**
Yes — MIT licensed, see [`LICENSE`](LICENSE).

## Contributing

Found a medium that deserves its own playbook? A tool-adapter pattern that's gone stale? Open an issue or a PR — `references/medium-playbooks.md` and `references/prompt-adapters.md` are designed to grow section by section without touching the core `SKILL.md`.

## License

[MIT](LICENSE) — use it, fork it, ship it.
