# Awesome Jev Use Cases

> LLMs write essays. **Jev makes the call.** This is the community's living index of what people are actually shipping with TypeSafe AI's System One decision model — real repos, real measurements, and the patterns that already work.

[![Jev Launch](https://img.shields.io/badge/Jev-launched%2015%20Sep%202026-blue)](https://typesafe.ai)
[![System One](https://img.shields.io/badge/System%20One-Decision%20Model-orange)](https://typesafe.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/anandi1989/awesome-jev-usecases)
[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey.svg)](./LICENSE)

**Jev** is TypeSafe AI's first System One model — a decision engine that returns typed, calibrated judgments (Choice / Score / Noul) instead of free-form prose. It runs in 70–500 ms at ~$0.042 per million input tokens, and output tokens are free. Fast enough to sit inside a game loop, cheap enough to run over millions of rows, and constrained enough that your code can branch on the answer without parsing JSON.

Every listing links to a public source. Headline results are tagged `[self-reported]` or `[independent]` — and every link is scored against a written rubric before it lands here (see [CONTRIBUTING.md](./CONTRIBUTING.md)).

---

## Contents

- [What is Jev](#what-is-jev)
- [Official Resources](#official-resources)
- [Top Use Cases](#top-use-cases)
- [Community Builders](#community-builders)
  - [01 Workflow](#01-workflow) · [02 Bulk](#02-bulk) · [03 Realtime](#03-realtime) · [04 Verify](#04-verify) · [05 Harness](#05-harness) · [06 Voice](#06-voice)
- [Benchmarks](#benchmarks)
- [Popular Blogs](#popular-blogs)
- [Contributing](#contributing)
- [License](#license)

---

## What is Jev

You send Jev a **state** (a string, JSON object, or list of text) plus **typed questions**. It returns **typed answers with probabilities** — no invented fields, no malformed JSON, no off-schema values. Your code owns the control flow, the thresholds, and the side effects.

| Primitive | You declare | Jev returns |
|-----------|-------------|-------------|
| **Choice** | A list of options (up to 255) | The chosen option + probability per option + confidence |
| **Score** | An ordered rubric (2–10 levels) | A probability-weighted score + confidence |
| **Noul** | A yes/no statement | A single probability from 0 to 1 |

Three primitives is the whole API — and that's the point. Questions in one request are evaluated **in parallel and in isolation** against the same state, so asking ten questions costs roughly the time of one. That one property unlocks speculative fan-out, confidence-gated routing, and every pattern on this list.

**The economics (vendor-reported):** $0.042 / million input tokens, output free, 70–500 ms end-to-end. On TypeSafe's own four-workflow eval, Jev lands at 67.8% agreement with a frontier-model consensus at $0.0004 per case — essentially tied with GPT-5.6 Terra (67.9%) at ~1/76th the cost. Treat the multipliers as directional, not gospel: the honest independent numbers are lower.

---

## Official Resources

**TypeSafe (official):**
- [TypeSafe AI](https://typesafe.ai) · [Introducing System One Models & Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) (launch post)
- [Docs](https://docs.typesafe.ai/introduction) · [API reference](https://docs.typesafe.ai/api) · [Primitives](https://docs.typesafe.ai/primitives) · [Patterns](https://docs.typesafe.ai/patterns) · [Models & pricing](https://docs.typesafe.ai/models)
- [Playground](https://console.typesafe.ai/playground) · [Workflow evals](https://evals.typesafe.ai) · [Console](https://console.typesafe.ai)

**Official SDKs & tools:**
- [typesafe-sdk-python](https://github.com/typesafe-ai/typesafe-sdk-python) · [typesafe-sdk-js](https://github.com/typesafe-ai/typesafe-sdk-js) · [system-one-adapter-python](https://github.com/typesafe-ai/system-one-adapter-python) (run LLMs over the same interface) · [agent skill](https://github.com/typesafe-ai/skills)

**Bypass the waitlist:** the [Vercel AI Gateway route](https://vercel.com/ai-gateway/models/jev) (`typesafe-ai/jev`).

**Community clients:** [Elixir](https://github.com/nshkrdotcom/typesafe_sdk) · [Ruby](https://github.com/joshmn/typesafe-sdk) · [Rust](https://github.com/gilljon/typesafe-ai-rs) · [.NET](https://github.com/saibimajdi/typesafe-dotnet-sdk) · [Go](https://github.com/Gaurav-Gosain/jev-go) · [Scala/ZIO](https://github.com/jamesward/zio-typesafe-ai) · [PHP/Laravel](https://github.com/Butochnikov/typesafe-sdk-php)

---

## Top Use Cases

The use cases with the most traction since launch — ranked by popularity, not raw star counts (stars are a hidden ordering signal only; rigor does not track reach).

### 🔥 Top

| Project | What it does | Headline result |
|---------|--------------|-----------------|
| [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | Browser agent with a dynamic indexed action space; a small LLM writes text only when a step needs it | Zürich → London Google Flights in **7.1 s / $0.0039** |
| [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | Claude Code compaction → Jev keep/delete | Content stays **verbatim** |
| [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | Market maker on Monad/Kuru — one buy/sell decision per block | **81 ms** model latency per block |
| [awlevin/typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) | macOS computer use via OCR + Jev action choice | **$0.0002 / decision** vs Opus 5 at $0.032 |
| [thruwire/foreman](https://github.com/thruwire/foreman) | Supervisor over Codex workers | Architecture experiment for software factories |
| [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | Staged code reviewer + local dashboard | Risk matrix → evidence → severity → routing |
| [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | Super Mario from emulator RAM as object-centric JSON | No screenshots sent to the model |

### ⚡ Rising

The "few upcoming" — high rubric score but below the popularity cutoff. This tier is where rigor beats reach: several of these have single-digit stars and the strongest measured results.

| Project | What it does | Headline result |
|---------|--------------|-----------------|
| [realZachi/pg-jev](https://github.com/realZachi/pg-jev) | Natural-language `WHERE` clauses for PostgreSQL — no embeddings, no vector column | 129 rows in **~1 s for ~$0.0009** |
| [droidrun/mobile-jev](https://github.com/droidrun/mobile-jev) | Android agent — Jev decides each tap | Uber route in **~21 s / 9 actions** |
| [DevMortimer/pi-warden](https://github.com/DevMortimer/pi-warden) | Agent guardrails that steer instead of interrupt | **6 rule breaks → 0** across 150 paired runs |
| [AnshChoudhary/typesafe-ai-firewall](https://github.com/AnshChoudhary/typesafe-ai-firewall) | Pre-execution firewall for agent tool calls — one Noul per hazard | **0%** hard negatives blocked vs **39.2%** with a single "is this dangerous?" prompt |

> Every headline result above is self-reported by the project author. Treat them as launch-week proof-of-concept signal, not production case studies.

---

## Community Builders

The long tail of unique use cases, grouped by decision shape. Each entry answers two questions: *what does it do*, and *why is it unique*.

### 01 Workflow

Smart if-statements inside ordinary software — the fuzzy middle between brittle rules and expensive chat models.

- [kylemclaren/jevql](https://github.com/kylemclaren/jevql) — `WHERE jev(...)` filters, `jev_prob` sorts, and `jev_choice` groups on a vanilla Postgres with no extension, judged client-side. *Unique: SQL filtering without a plugin or embeddings.*
- [AboveColin/HA-Jev](https://github.com/AboveColin/HA-Jev) — Home Assistant integration; typed questions over entity state become sensors and automation actions. *Unique: a decision layer for household automations.*
- [valentynkit/jev-commit](https://github.com/valentynkit/jev-commit) — one Noul on whether a commit message matches the staged diff, plus debug-leftover and unmentioned-work checks. *Unique: pre-commit semantic lint instead of a full review.*
- [valentynkit/jev.nvim](https://github.com/valentynkit/jev.nvim) — plain-language buffer search; Treesitter splits the file into functions, Jev scores each, results land in quickfix. *Unique: semantic editor search with no embeddings.*

### 02 Bulk

Cheap judgment over giant corpora — the economics that make "run it on everything" rational.

- [valentynkit/jev-skip](https://github.com/valentynkit/jev-skip) — sponsor-segment probability on YouTube's seek bar, scored from the caption track alone. *Unique: crowd-free sponsor detection (77% of SponsorBlock's sponsor seconds, ~$0.0008/video).*
- [youkiti/tiab-review-plugin](https://github.com/youkiti/tiab-review-plugin) — title/abstract screening for systematic reviews across labeled medical datasets. *Unique: evidence-synthesis triage at scale (95% recall @ 16,645 records).*
- Canonical examples: 1,018 papers → 24 topics for ~$0.08; 2,000 wine notes → CatBoost numeric features at 1.77 RMSE.

### 03 Realtime

Action selection at game, UI, and market clock rates — perception and safety stay in code, Jev picks the move.

- [phyous/tsai-sc](https://github.com/phyous/tsai-sc) — StarCraft shareware harness with 421 structured decisions. *Unique: real-time strategy from structured game state.*
- [valentynkit/jev-plays-pokemon-red](https://github.com/valentynkit/jev-plays-pokemon-red) — code owns the route, Jev picks only at branches, and predictions are scored by Brier against RAM. *Unique: calibrated in-game decision logging.*
- [RomanSlack/jev-drone](https://github.com/RomanSlack/jev-drone) — camera-only quadrotor; Jev is advisory at ~2.5 Hz while safety stays in code at 50 Hz. *Unique: split-rate control (tactical vs safety loop).*
- Canonical examples: Doom (~10 Hz), Wikiracing, Snake, Tetris, Pac-Man, Subway Surfers ×50.

### 04 Verify

Score, judge, and gate prompts, traces, tool calls, and claims — at a fraction of the LLM call you're protecting.

- [valentynkit/jev-belay](https://github.com/valentynkit/jev-belay) — blocks an unverified "done" in a coding agent; spends one Jev call only when files changed with no passing check since, and fails open on every error path. *Unique: evidence-gated task-completion guardrail.*
- [kiarina/labs — safety judgment](https://github.com/kiarina/labs/tree/main/2026/09/17/typesafe-jev-safety-judgment) — moderation plus shell-command safety checks. *Unique: strong non-English (Japanese) moderation — 36 misses vs OpenAI's 292 on 826 harmful texts.*
- Canonical examples: citation grounding, jailbreak and prompt-injection screening, pre-execution shell checks.

### 05 Harness

Make the agent loop cheaper, safer, and composable — Jev as the load balancer above models, tools, and humans.

- [jkudish/jev-mcp](https://github.com/jkudish/jev-mcp) — MCP server exposing claim verification, content screening, and semantic ranking to coding agents. *Unique: verification + injection screening over MCP.*
- [itsmostafa/typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) — single-binary Go MCP for Claude and Codex. *Unique: zero-dependency agent integration.*
- [AbdelStark/bicameral](https://github.com/AbdelStark/bicameral) — Pi harness: the LLM writes, Jev supplies typed reflexes for policy, loop detection, and review. *Unique: a decision layer as the coding-harness reflex arc.*
- Canonical examples: skill routing, context reduction, model routing.

### 06 Voice

Sub-second decisions on the audio path — the youngest pillar, still mostly conceptual.

- Spoken "go back" mapped to a click in **~300 ms** (voice → action)
- End-of-utterance and turn-taking detection via a Noul over the voice-activity signal
- Speak-up gates for wake-word-free assistants

No canonical repo has shipped yet — this is the pillar to watch.

---

## Benchmarks

Rigor over reach. Everything here is tagged independent or self-reported.

### Independent evaluations

- [Every — "Mini-Vibe Check"](https://every.to/also-true-for-humans/mini-vibe-check-typesafe-s-jev-judged-everything-i-ve-written-in-0-7-seconds) (Mike Taylor) — 777 judgments in <0.7 s (~$0.0032 each), 6-of-7 planted defects caught, ~25× faster than Claude Fable 5.1. `[independent]`
- Near Here (UK events company) — 96% listing moderation vs Mistral Small 4 (84%) and Gemini Flash-Lite (86%). Community-reported. `[independent]`
- [Archer Hume — "Architecture Unmasked"](https://archerhume.com/posts/jevs-architecture-unmasked/) — 84.6% MMLU-Pro, ECE 0.0313. Third-party probe, not a TypeSafe figure. `[independent]`

### Benchmark repos

- [Gaurav-Gosain/jev-sec-bench](https://github.com/Gaurav-Gosain/jev-sec-bench) — blind prompt-injection & vulnerable-code detection: 96.5% accuracy, ECE 0.0588, 662 samples
- [TokenTrim/jev-agent-failure-benchmark](https://github.com/TokenTrim/jev-agent-failure-benchmark) — beat GPT-5.4 on every axis across 6,257 traces for $1.28
- [anessbelbati/jev-rerank-bench](https://github.com/anessbelbati/jev-rerank-bench) — nDCG@10 0.692 vs Cohere 0.691 (a tie, 14 datasets)
- [anisselbd/jev-phishing-bench](https://github.com/anisselbd/jev-phishing-bench) — 2,000 emails vs Claude Haiku 4.5
- [iammrduncan/typesafe-ai-benchmark](https://github.com/iammrduncan/typesafe-ai-benchmark) — Jev vs Qwen 3.8 27B on Cerebras
- [vinilana/jev-eval-agent](https://github.com/vinilana/jev-eval-agent) — public eval harness
- [jmanhype/jev-dspy-lab](https://github.com/jmanhype/jev-dspy-lab) — DSPy companion; calibration and confidence-gated abstention

### Open re-implementations

Reproducing the *interface*, not the weights — proof that the decision-layer idea travels.

- [TheoLeeCJ/SemIf](https://github.com/TheoLeeCJ/SemIf) (was "openjev") — frozen 4B model, reads option logits, runs in the browser
- [vinnylarouge/jevlike](https://github.com/vinnylarouge/jevlike) — one-pass scorer; Doom, chess, and Wikispeedia demos
- [Mapika/decider](https://github.com/Mapika/decider) — Qwen3.5-2B fine-tune that emits typed decisions
- [NullPo-jp/PocketJev](https://github.com/NullPo-jp/PocketJev) — on-device iPhone decisions (MLX + Qwen3-VL)

---

## Popular Blogs

The writing worth reading, ranked by writer popularity × content uniqueness. SEO recaps are excluded by design.

1. [Every — "TypeSafe's Jev Judged Everything I've Written in 0.7 Seconds"](https://every.to/also-true-for-humans/mini-vibe-check-typesafe-s-jev-judged-everything-i-ve-written-in-0-7-seconds) — Mike Taylor. *The only independent hands-on measurement at launch.*
2. [Flavio Copes — "A deep dive into Jev"](https://flaviocopes.com/jev/) — *The most thorough API/SDK walkthrough.*
3. [Archer Hume — "Jev's Architecture Unmasked"](https://archerhume.com/posts/jevs-architecture-unmasked/) — *The only serious reverse-engineering attempt.*
4. [Latent Space — "AINews: Jev, a System One model"](https://www.latent.space/p/ainews-jev-a-system-one-model-that) — Swyx. *The launch, placed in context.*
5. [The Register — "TypeSafe AI debuts model for machines that plays Doom"](https://www.theregister.com/ai-and-ml/2026/09/16/typesafe-ai-debuts-model-for-machines-that-plays-doom/5296711) — Thomas Claburn. *The best independent news coverage.*
6. [Kingy AI — "Jev review: the AI model that doesn't generate text"](https://kingy.ai/blog/typesafe-jev-review-the-ai-model-that-doesnt-generate-text/) — *The skeptical counterweight.*
7. [OrcaRouter — "Jev / TypeSafe System One: what we know"](https://www.orcarouter.ai/blog/jev-typesafe-system-one-what-we-know) — *The claim-vs-evidence audit (the 75× vs 193× discrepancy).*
8. [DataCamp — "System One Models: Jev"](https://www.datacamp.com/blog/system-one-models-jev) — *The eval-table explainer.*
9. [agentjournal.dev — "One judge call, or twelve dimension scores?"](https://agentjournal.dev/blog/llm-judge-vs-feature-extraction/) — *An independent methodology measurement.*

---

## Contributing

This is a community index. Each section has its own bar — see [CONTRIBUTING.md](./CONTRIBUTING.md) for the full rules and the rubric every link is scored against. The short version:

- **Official Resources** — fix or update links only.
- **Top Use Cases** — maintainer-curated via the popularity formula; PRs may nominate but won't self-merge.
- **Community Builders** — open; an entry must actually use Jev, be *unique*, and state *what it does* and *why it's unique*.
- **Benchmarks** — open; label every result `[self-reported]` or `[independent]`.
- **Popular Blogs** — maintainer-curated via writer popularity × content uniqueness; SEO recaps are rejected.

---

## License

MIT — for the index itself. Individual projects retain their own licenses.

---

**Last updated:** 19 September 2026

*Jev is only a few days old. Expect this list to grow fast.*
