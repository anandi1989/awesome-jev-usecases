# Awesome Jev Use Cases

> LLMs write essays. **Jev makes the call.** This is the community's living index of what people are actually shipping with TypeSafe AI's System One decision model: real repos, real measurements, and the patterns that already work.

[![Jev Launch](https://img.shields.io/badge/Jev-launched%2015%20Sep%202026-blue)](https://typesafe.ai)
[![System One](https://img.shields.io/badge/System%20One-Decision%20Model-orange)](https://typesafe.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/anandi1989/awesome-jev-usecases)
[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey.svg)](./LICENSE)

**Jev** is TypeSafe AI's first System One model: a decision engine that returns typed, calibrated judgments (Choice / Score / Noul) instead of free-form prose. It runs in 70–500 ms at ~$0.042 per million input tokens, and output tokens are free. Fast enough to sit inside a game loop, cheap enough to run over millions of rows, and constrained enough that your code can branch on the answer without parsing JSON.

Every listing links to a public source. Headline results are tagged `[self-reported]` or `[independent]`, and every link is scored against a written rubric before it lands here (see [CONTRIBUTING.md](./CONTRIBUTING.md)).

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

You send Jev a **state** (a string, JSON object, or list of text) plus **typed questions**. It returns **typed answers with probabilities**: no invented fields, no malformed JSON, no off-schema values. Your code owns the control flow, the thresholds, and the side effects.

| Primitive | You declare | Jev returns |
|-----------|-------------|-------------|
| **Choice** | A list of options (up to 255) | The chosen option + probability per option + confidence |
| **Score** | An ordered rubric (2–10 levels) | A probability-weighted score + confidence |
| **Noul** | A yes/no statement | A single probability from 0 to 1 |

Three primitives is the whole API. That's the point. Questions in one request are evaluated **in parallel and in isolation** against the same state, so asking ten questions costs roughly the time of one. That one property unlocks speculative fan-out, confidence-gated routing, and every pattern on this list.

**The economics (vendor-reported):** $0.042 / million input tokens, output free, 70–500 ms end-to-end. On TypeSafe's own four-workflow eval, Jev lands at 67.8% agreement with a frontier-model consensus at $0.0004 per case: essentially tied with GPT-5.6 Terra (67.9%) at ~1/76th the cost. Treat the multipliers as directional, not gospel: the honest independent numbers are lower.

---

## Official Resources

**TypeSafe (official):**
- [TypeSafe AI](https://typesafe.ai) · [Introducing System One Models & Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) (launch post)
- [Docs](https://docs.typesafe.ai/introduction) · [API reference](https://docs.typesafe.ai/api) · [Primitives](https://docs.typesafe.ai/primitives) · [Patterns](https://docs.typesafe.ai/patterns) · [Models & pricing](https://docs.typesafe.ai/models) · [Demos](https://docs.typesafe.ai/demos)
- [Playground](https://console.typesafe.ai/playground) · [Workflow evals](https://evals.typesafe.ai) · [Console](https://console.typesafe.ai)

**Official SDKs & tools:**
- [typesafe-sdk-python](https://github.com/typesafe-ai/typesafe-sdk-python) · [typesafe-sdk-js](https://github.com/typesafe-ai/typesafe-sdk-js) · [system-one-adapter-python](https://github.com/typesafe-ai/system-one-adapter-python) (run LLMs over the same interface) · [agent skill](https://github.com/typesafe-ai/skills)

**Bypass the waitlist:** the [Vercel AI Gateway route](https://vercel.com/ai-gateway/models/jev) (`typesafe-ai/jev`).

**Community clients:** [Elixir](https://github.com/nshkrdotcom/typesafe_sdk) · [Ruby](https://github.com/joshmn/typesafe-sdk) · [Rust](https://github.com/gilljon/typesafe-ai-rs) · [.NET](https://github.com/saibimajdi/typesafe-dotnet-sdk) · [Go](https://github.com/Gaurav-Gosain/jev-go) · [Scala/ZIO](https://github.com/jamesward/zio-typesafe-ai) · [PHP/Laravel](https://github.com/Butochnikov/typesafe-sdk-php) · [Python (jevclient)](https://github.com/AboveColin/jevclient) · [Rust (typesafe-rs)](https://github.com/AbdelStark/typesafe-rs) · [CLI (jev-cli)](https://github.com/jtsang4/jev-cli) · [Vercel AI SDK provider](https://ai-sdk.dev/providers/ai-sdk-providers/typesafe-ai)

---

## Top Use Cases

The use cases with the most traction since launch: ranked by popularity, not raw star counts (stars are a hidden ordering signal only; rigor does not track reach).

### 🔥 Top

| Project | What it does | Headline result |
|---------|--------------|-----------------|
| [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | Browser agent with a dynamic indexed action space; a small LLM writes text only when a step needs it | Zürich → London Google Flights in **7.1 s / $0.0039** |
| [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | Claude Code compaction → Jev keep/delete | Content stays **verbatim** |
| [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | Market maker on Monad/Kuru: one buy/sell decision per block | **81 ms** model latency per block |
| [awlevin/typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) | macOS computer use via OCR + Jev action choice | **$0.0002 / decision** vs Opus 5 at $0.032 |
| [thruwire/foreman](https://github.com/thruwire/foreman) | Supervisor over Codex workers | Architecture experiment for software factories |
| [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | Staged code reviewer + local dashboard | Risk matrix → evidence → severity → routing |
| [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | Super Mario from emulator RAM as object-centric JSON | No screenshots sent to the model |

### ⚡ Rising

The "few upcoming": high rubric score but below the popularity cutoff. This tier is where rigor beats reach: several of these have single-digit stars and the strongest measured results.

| Project | What it does | Headline result |
|---------|--------------|-----------------|
| [realZachi/pg-jev](https://github.com/realZachi/pg-jev) | Natural-language `WHERE` clauses for PostgreSQL: no embeddings, no vector column | 129 rows in **~1 s for ~$0.0009** |
| [droidrun/mobile-jev](https://github.com/droidrun/mobile-jev) | Android agent: Jev decides each tap | Uber route in **~21 s / 9 actions** |
| [DevMortimer/pi-warden](https://github.com/DevMortimer/pi-warden) | Agent guardrails that steer instead of interrupt | **6 rule breaks → 0** across 150 paired runs |
| [AnshChoudhary/typesafe-ai-firewall](https://github.com/AnshChoudhary/typesafe-ai-firewall) | Pre-execution firewall for agent tool calls: one Noul per hazard | **0%** hard negatives blocked vs **39.2%** with a single "is this dangerous?" prompt |

> Every headline result above is self-reported by the project author. Treat them as launch-week proof-of-concept signal, not production case studies.

---

## Community Builders

The long tail of unique use cases, grouped by decision shape. Each entry answers two questions: *what does it do*, and *why is it unique*.

### 01 Workflow

Smart if-statements inside ordinary software: the fuzzy middle between brittle rules and expensive chat models.

- [kylemclaren/jevql](https://github.com/kylemclaren/jevql): `WHERE jev(...)` filters, `jev_prob` sorts, and `jev_choice` groups on a vanilla Postgres with no extension, judged client-side. *Unique: SQL filtering without a plugin or embeddings.* [self-reported]
- [AboveColin/HA-Jev](https://github.com/AboveColin/HA-Jev): Home Assistant integration; typed questions over entity state become sensors and automation actions. *Unique: a decision layer for household automations.* [self-reported]
- [valentynkit/jev-commit](https://github.com/valentynkit/jev-commit): one Noul on whether a commit message matches the staged diff, plus debug-leftover and unmentioned-work checks. *Unique: pre-commit semantic lint instead of a full review.* [self-reported]
- [valentynkit/jev.nvim](https://github.com/valentynkit/jev.nvim): plain-language buffer search; Treesitter splits the file into functions, Jev scores each, results land in quickfix. *Unique: semantic editor search with no embeddings.* [self-reported]
- [DanRWilloughby/snifftest](https://github.com/DanRWilloughby/snifftest): prose linter that sniffs out AI-writing tells; countable regex rules run locally, judgment rules send one paragraph at a time to Jev. *Unique: one probability per rule, no general model, and it never rewrites your text.* [self-reported]
- [zephel01/Jev-sample](https://github.com/zephel01/Jev-sample): question-shape demo: a 4-option Choice scores 48.3%, but decomposing into four precondition Nouls reaches 98.3%. *Unique: quantifies the atomic-question decomposition payoff.* [self-reported]
- [mrnugget/jev-shell-history](https://github.com/mrnugget/jev-shell-history): Fish-style Zsh history autosuggestions ranked by Jev from the current input. *Unique: semantic shell-history ranking with no embeddings.* [self-reported]
- [wustep/jev-playground](https://github.com/wustep/jev-playground): Jev chooses bounded musical attributes (enums only) while deterministic code renders sheet, audio, and MIDI. *Unique: enum-bounded music steering — the decision layer, not the notes, is the model's job.* [self-reported]

### 02 Bulk

Cheap judgment over giant corpora: the economics that make "run it on everything" rational.

- [valentynkit/jev-skip](https://github.com/valentynkit/jev-skip): sponsor-segment probability on YouTube's seek bar, scored from the caption track alone. *Unique: crowd-free sponsor detection (77% of SponsorBlock's sponsor seconds, ~$0.0008/video).* [self-reported]
- [youkiti/tiab-review-plugin](https://github.com/youkiti/tiab-review-plugin): title/abstract screening for systematic reviews across labeled medical datasets. *Unique: evidence-synthesis triage at scale (95% recall @ 16,645 records).* [self-reported]
- [kitze/Unclutter](https://github.com/kitze/Unclutter): per-element DOM classifier — keep/ad/cookie/promotion/newsletter/social/uncertain. *Unique: browser decluttering as a shipped job; no other entry covers UI hygiene.* [self-reported]
- [dani1005/book-aurora](https://github.com/dani1005/book-aurora): scores a novel's passages across nine emotions plus overall intensity, visualized as an emotional aurora. *Unique: whole-book emotion scoring — every passage becomes a row of colour.* [self-reported]
- [Tatuck/jev-boe-demo](https://github.com/Tatuck/jev-boe-demo): screens Spain's official gazette (BOE) daily, scoring public impact, classifying topics, and selecting summary paragraphs. *Unique: daily legal-gazette screening with impact scoring.* [self-reported]
- Canonical examples: 1,018 papers → 24 topics for ~$0.08; 2,000 wine notes → CatBoost numeric features at 1.77 RMSE.

### 03 Realtime

Action selection at game, UI, and market clock rates: perception and safety stay in code, Jev picks the move.

- [phyous/tsai-sc](https://github.com/phyous/tsai-sc): StarCraft shareware harness with 421 structured decisions. *Unique: real-time strategy from structured game state.* [self-reported]
- [valentynkit/jev-plays-pokemon-red](https://github.com/valentynkit/jev-plays-pokemon-red): code owns the route, Jev picks only at branches, and predictions are scored by Brier against RAM. *Unique: calibrated in-game decision logging.* [self-reported]
- [RomanSlack/jev-drone](https://github.com/RomanSlack/jev-drone): camera-only quadrotor; Jev is advisory at ~2.5 Hz while safety stays in code at 50 Hz. *Unique: split-rate control (tactical vs safety loop).* [self-reported]
- [sorrycc/typesafe-snake](https://github.com/sorrycc/typesafe-snake): Snake where Jev picks each move from structured game state. *Unique: the first linked implementation of a canonical realtime example.* [self-reported]
- [Reisenbug/TerraBlind](https://github.com/Reisenbug/TerraBlind): a pre-launch Terraria tModLoader mod that added Jev to fight the bosses — one question every 200 ms, code turns the answer into keystrokes. *Unique: an established game mod adopting Jev as its boss-fight decision layer, plus a code-only fresh-world pipeline.* [self-reported]
- Canonical examples: Doom (~10 Hz), Wikiracing, Snake, Tetris, Pac-Man, Subway Surfers ×50.

### 04 Verify

Score, judge, and gate prompts, traces, tool calls, and claims: at a fraction of the LLM call you're protecting.

- [valentynkit/jev-belay](https://github.com/valentynkit/jev-belay): blocks an unverified "done" in a coding agent; spends one Jev call only when files changed with no passing check since, and fails open on every error path. *Unique: evidence-gated task-completion guardrail.* [self-reported]
- [kiarina/labs: safety judgment](https://github.com/kiarina/labs/tree/main/2026/09/17/typesafe-jev-safety-judgment): moderation plus shell-command safety checks. *Unique: strong non-English (Japanese) moderation: 36 misses vs OpenAI's 292 on 826 harmful texts.* [self-reported]
- [teyhouse/jev-secret-detection](https://github.com/teyhouse/jev-secret-detection): secret/credential scanning in code and text. *Unique: a dedicated secret-detection decision, distinct from shell-command safety and agent guardrails.* [self-reported]
- [Red5d/jev-cvss](https://github.com/Red5d/jev-cvss): extracts CVSS v3.0/v3.1/v4.0 metrics from vulnerability descriptions and scores deterministically. *Unique: structured CVSS extraction — Jev parses, code computes.* [self-reported]
- Canonical examples: citation grounding, jailbreak and prompt-injection screening, pre-execution shell checks.

### 05 Harness

Make the agent loop cheaper, safer, and composable: Jev as the load balancer above models, tools, and humans.

- [jkudish/jev-mcp](https://github.com/jkudish/jev-mcp): MCP server exposing claim verification, content screening, and semantic ranking to coding agents. *Unique: verification + injection screening over MCP.* [self-reported]
- [itsmostafa/typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp): single-binary Go MCP for Claude and Codex. *Unique: zero-dependency agent integration.* [self-reported]
- [AbdelStark/bicameral](https://github.com/AbdelStark/bicameral): Pi harness: the LLM writes, Jev supplies typed reflexes for policy, loop detection, and review. *Unique: a decision layer as the coding-harness reflex arc.* [self-reported]
- [jexp/neo4jev](https://github.com/jexp/neo4jev): navigates a Neo4j graph one relationship at a time via a classifier over neighbouring relationships. *Unique: graph traversal as a typed decision, hop by hop.* [self-reported]
- [xinyao27/jevonian](https://github.com/xinyao27/jevonian): Local OpenAI/Anthropic/Responses-compatible proxy where one Jev call answers both the model route and the thinking level for its `jevonian/auto` model, after code has filtered candidates by protocol, context window, effort floor, and spent quota windows; a pinned model or explicit route skips Jev entirely, and each turn is logged with the serving model, reason, token usage, and estimated cost. *Unique: the decision is a cost-and-cache one, not just a capability one, and it stays auditable.* [self-reported]
- Canonical examples: skill routing, context reduction, model routing.

### 06 Voice

Sub-second decisions on the audio path: the youngest pillar, still mostly conceptual.

- Spoken "go back" mapped to a click in **~300 ms** (voice → action)
- End-of-utterance and turn-taking detection via a Noul over the voice-activity signal
- Speak-up gates for wake-word-free assistants

No canonical repo has shipped yet; this is the pillar to watch.

---

## Benchmarks

Rigor over reach. Everything here is tagged independent or self-reported.

### Independent evaluations

- [Near Here: "Listing moderation on jev-1.13.0"]: 96% listing moderation vs Mistral Small 4 (84%) and Gemini Flash-Lite (86%). `[independent]`

- [largitdata: "Jev System One Model open-source benchmark"](https://www.largitdata.com/en/blog/jev-system-one-model-open-source-benchmark/): multi-turn RAG routing — Gemma 4 31B vs Jev vs open alternatives; latency advantage for Jev. `[independent]`

### Benchmark repos

- [Gaurav-Gosain/jev-sec-bench](https://github.com/Gaurav-Gosain/jev-sec-bench): blind prompt-injection & vulnerable-code detection: 96.5% accuracy, ECE 0.0588, 662 samples [self-reported]
- [TokenTrim/jev-agent-failure-benchmark](https://github.com/TokenTrim/jev-agent-failure-benchmark): beat GPT-5.4 on every axis across 6,257 traces for $1.28 [self-reported]
- [anessbelbati/jev-rerank-bench](https://github.com/anessbelbati/jev-rerank-bench): nDCG@10 0.692 vs Cohere 0.691 (a tie, 14 datasets) [self-reported]
- [anisselbd/jev-phishing-bench](https://github.com/anisselbd/jev-phishing-bench): 2,000 emails vs Claude Haiku 4.5 [self-reported]
- [iammrduncan/typesafe-ai-benchmark](https://github.com/iammrduncan/typesafe-ai-benchmark): Jev vs Qwen 3.8 27B on Cerebras [self-reported]
- [vinilana/jev-eval-agent](https://github.com/vinilana/jev-eval-agent): public eval harness [self-reported]
- [jmanhype/jev-dspy-lab](https://github.com/jmanhype/jev-dspy-lab): DSPy companion; calibration and confidence-gated abstention [self-reported]

### Open re-implementations

Reproducing the *interface*, not the weights: proof that the decision-layer idea travels.

- [TheoLeeCJ/SemIf](https://github.com/TheoLeeCJ/SemIf) (was "openjev"): frozen 4B model, reads option logits, runs in the browser
- [vinnylarouge/jevlike](https://github.com/vinnylarouge/jevlike): one-pass scorer; Doom, chess, and Wikispeedia demos
- [Mapika/decider](https://github.com/Mapika/decider): Qwen3.5-2B fine-tune that emits typed decisions
- [NullPo-jp/PocketJev](https://github.com/NullPo-jp/PocketJev): on-device iPhone decisions (MLX + Qwen3-VL)
- [Laya](https://huggingface.co/convaiinnovations/laya): Apache-2.0 open alternative, 3 checkpoints, runs on a free Colab T4 (~30 ms vs ~302 ms, 0.590 vs 0.974 accuracy)
- [com-kotobalabs/open-jev-deberta-v3-large](https://huggingface.co/com-kotobalabs/open-jev-deberta-v3-large): open reproduction on DeBERTa-v3-large (self-hostable)

**Watch:** the [Jev Reproductions Tracker](https://huggingface.co/spaces/multimodalart/jev-reproductions-tracker) on Hugging Face follows every open-weight reproduction attempt.

---

## Popular Blogs

The writing worth reading, ranked by writer popularity × content uniqueness. SEO recaps are excluded by design.

1. [Every: "TypeSafe's Jev Judged Everything I've Written in 0.7 Seconds"](https://every.to/also-true-for-humans/mini-vibe-check-typesafe-s-jev-judged-everything-i-ve-written-in-0-7-seconds): Mike Taylor. *The only independent hands-on measurement at launch.*
2. [TechCrunch: "A new kind of AI model from a ChatGPT inventor is thrilling developers"](https://techcrunch.com/2026/09/18/a-new-kind-of-ai-model-from-a-chatgpt-inventor-is-thrilling-developers/): *Mainstream validation with adoption quotes from Vercel and Bryo AI engineers.*
3. [Flavio Copes: "A deep dive into Jev"](https://flaviocopes.com/jev/): *The most thorough API/SDK walkthrough.*
4. [Archer Hume: "Jev's Architecture Unmasked"](https://archerhume.com/posts/jevs-architecture-unmasked/): *The only serious reverse-engineering attempt.*
5. [Latent Space: "AINews: Jev, a System One model"](https://www.latent.space/p/ainews-jev-a-system-one-model-that): Swyx. *The launch, placed in context.*
6. [The Register: "TypeSafe AI debuts model for machines that plays Doom"](https://www.theregister.com/ai-and-ml/2026/09/16/typesafe-ai-debuts-model-for-machines-that-plays-doom/5296711): Thomas Claburn. *The best independent news coverage.*
7. [ts2.tech: "TypeSafe AI Raises $40 Million for Jev, but Its 445× Cost Claim Is Still Self-Tested"](https://ts2.tech/en/typesafe-ai-raises-40-million-for-jev-but-its-445x-cost-claim-is-still-self-tested/): *The skeptical audit of self-tested benchmarks, plus funding verification.*
8. [Kingy AI: "Jev review: the AI model that doesn't generate text"](https://kingy.ai/blog/typesafe-jev-review-the-ai-model-that-doesnt-generate-text/): *The skeptical counterweight.*
9. [dev.to (Valyu AI): "How to Use Jev: A practical guide"](https://dev.to/valyuai/how-to-use-jev-a-practical-guide-to-typesafes-system-one-model-g5e): *A hands-on tutorial with code and real numbers.*
10. [OrcaRouter: "Jev / TypeSafe System One: what we know"](https://www.orcarouter.ai/blog/jev-typesafe-system-one-what-we-know): *The claim-vs-evidence audit (the 75× vs 193× discrepancy).*
11. [DataCamp: "System One Models: Jev"](https://www.datacamp.com/blog/system-one-models-jev): *The eval-table explainer.*
12. [agentjournal.dev: "One judge call, or twelve dimension scores?"](https://agentjournal.dev/blog/llm-judge-vs-feature-extraction/): *An independent methodology measurement.*
13. [LangChain: "Building a harness with Jev"](https://www.langchain.com/blog/building-a-harness-with-jev): *A first-party harness guide from a major framework vendor.*
14. X @CompleteSkeptic: "Jev launch announcement thread": Diogo Almeida. *Primary launch announcement (~25M views).*
15. [Hacker News: "TypeSafe AI launch discussion thread"](https://news.ycombinator.com/item?id=49717558): *The richest technical critique with named commenters.*

---

## Contributing

This is a community index. Each section has its own bar: see [CONTRIBUTING.md](./CONTRIBUTING.md) for the full rules and the rubric every link is scored against. The short version:

- **Official Resources**: fix or update links only.
- **Top Use Cases**: maintainer-curated via the popularity formula; PRs may nominate but won't self-merge.
- **Community Builders**: open; an entry must actually use Jev, be *unique*, and state *what it does* and *why it's unique*.
- **Benchmarks**: open; label every result `[self-reported]` or `[independent]`.
- **Popular Blogs**: maintainer-curated via writer popularity × content uniqueness; SEO recaps are rejected.

---

## Anything else?

Found something that doesn't fit any section, or just want to say hi?

- Open an [issue](https://github.com/anandi1989/awesome-jev-usecases/issues) on this repo
- Reach out on GitHub: [@anandi1989](https://github.com/anandi1989)

---

## License

MIT: for the index itself. Individual projects retain their own licenses.

---

**Last updated:** 22 September 2026

*Jev is only a few days old. Expect this list to grow fast!!!*
