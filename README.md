# Awesome Jev Use Cases

> LLMs write essays. **Jev makes the call.** This is the community's living index of what people are actually shipping with TypeSafe AI's System One decision model — real repos, real measurements, and the patterns that already work.

[![Jev Launch](https://img.shields.io/badge/Jev-launched%2015%20Sep%202026-blue)](https://typesafe.ai)
[![System One](https://img.shields.io/badge/System%20One-Decision%20Model-orange)](https://typesafe.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/anandi1989/awesome-jev-usecases)
[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey.svg)](./LICENSE)

**Jev** is TypeSafe AI's first System One model — a decision engine that returns typed, calibrated judgments (Choice / Score / Noul) instead of free-form prose. It runs in 70–500 ms at ~$0.042 per million input tokens, and output tokens are free. In other words: fast enough to sit inside a game loop, cheap enough to run over millions of rows, and constrained enough that your code can branch on the answer without parsing JSON.

Every entry below links to a public repo or a documented result. No star-count theater — the star column was dropped on purpose, because launch-week stars track attention, not rigor.

---

## Why This Exists

Within 72 hours of launch, the community shipped the kind of things that used to need a frontier LLM and a prayer:

- A browser agent that books a Zürich → London flight in **7.1 seconds for $0.0039**
- Trading bots placing a buy/sell decision every **~300 ms**
- Computer-use agents deciding for **$0.0002 per step** — vs Opus 5 at $0.032
- Agent guardrails, code reviewers, drones, games, and bulk classifiers

Most of it is still experimental. This index exists so you can find the projects worth reading — and steal the patterns that already work.

---

## The 60-Second Version

You send Jev a **state** (a string, JSON object, or list of text) plus **typed questions**. It returns **typed answers with probabilities** — no invented fields, no malformed JSON, no off-schema values. Your code owns the control flow, the thresholds, and the side effects.

| Primitive | You declare | Jev returns |
|-----------|-------------|-------------|
| **Choice** | A list of options (up to 255) | The chosen option + probability per option + confidence |
| **Score** | An ordered rubric (2–10 levels) | A probability-weighted score + confidence |
| **Noul** | A yes/no statement | A single probability from 0 to 1 |

Three primitives is the whole API — and that's the point. Questions in one request are evaluated **in parallel and in isolation** against the same state, so asking ten questions costs roughly the time of one. That single property unlocks speculative fan-out, confidence-gated routing, and every pattern on this list.

**The economics (vendor-reported):** $0.042 / million input tokens, output free, 70–500 ms end-to-end. On TypeSafe's own four-workflow eval, Jev lands at 67.8% agreement with a frontier-model consensus at $0.0004 per case — essentially tied with GPT-5.6 Terra (67.9%) at ~1/76th the cost. Treat the multipliers as directional, not gospel: the honest independent numbers are lower.

---

## Flagship Projects (Highest Signal)

| Project | What it does | Headline result |
|---------|--------------|-----------------|
| [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | Browser agent with a dynamic indexed action space; a small LLM writes text only when a step needs it | Zürich → London Google Flights in **7.1 s / $0.0039** |
| [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | Market maker on Monad/Kuru — one buy/sell decision per block | **81 ms** model latency per block |
| [awlevin/typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) | macOS computer use via OCR + Jev action choice | **$0.0002 / decision** vs Opus 5 at $0.032 |
| [DevMortimer/pi-warden](https://github.com/DevMortimer/pi-warden) | Agent guardrails that steer instead of interrupt | **6 rule breaks → 0** across 150 paired runs |
| [AnshChoudhary/typesafe-ai-firewall](https://github.com/AnshChoudhary/typesafe-ai-firewall) | Pre-execution firewall for agent tool calls — one Noul per hazard | **0%** hard negatives blocked vs **39.2%** with a single "is this dangerous?" prompt |
| [Gaurav-Gosain/jev-sec-bench](https://github.com/Gaurav-Gosain/jev-sec-bench) | Blind prompt-injection & vulnerable-code benchmarks | **96.5%** injection accuracy, ECE 0.0588 |
| [TokenTrim/jev-agent-failure-benchmark](https://github.com/TokenTrim/jev-agent-failure-benchmark) | Can a decision model diagnose what broke an agent? | Beat GPT-5.4 on **every axis** across 6,257 traces for **$1.28** |
| [realZachi/pg-jev](https://github.com/realZachi/pg-jev) | Natural-language `WHERE` clauses for PostgreSQL — no embeddings, no vector column | 129 rows in **~1 s for ~$0.0009** |
| [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | Claude Code compaction → Jev keep/delete | Content stays **verbatim** |
| [TheoLeeCJ/openjev](https://github.com/TheoLeeCJ/openjev) | Open re-implementation on a frozen 4B model by reading option logits | Runs in the browser, no waitlist |
| [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | Super Mario from emulator RAM as object-centric JSON | No screenshots sent to the model |
| [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | Staged code reviewer + local dashboard | Risk matrix → evidence → severity → routing |
| [thruwire/foreman](https://github.com/thruwire/foreman) | Supervisor over Codex workers | Architecture experiment for software factories |
| [RomanSlack/jev-drone](https://github.com/RomanSlack/jev-drone) | Camera-only quadrotor in MuJoCo | Advisory at ~2.5 Hz; safety stays in code |

**Evidence note:** every headline result above is self-reported by the project author — launch-week artifacts, not independent audits. Treat them as proof-of-concept signal, not production case studies.

---

## Use-Case Catalog

### 1. Smart Workflow Decisions ("intelligent if-statements")

The fuzzy middle between brittle rules and expensive chat models — classify, route, score, and branch inside ordinary software.

- Support triage: department, urgency, frustration, refund intent, policy fit
- Model & skill routing in agent harnesses — send simple work to the fast tier, hard work to the strong tier
- Email fraud detection, résumé–job scoring, lead/ICP qualification
- Natural-language Postgres `WHERE` clauses → [realZachi/pg-jev](https://github.com/realZachi/pg-jev)
- Semantic spreadsheet formatting, Home Assistant automations → [AboveColin/HA-Jev](https://github.com/AboveColin/HA-Jev)

### 2. Bulk Map-Reduce Classification

Cheap judgment over giant corpora — the economics that make "run it on everything" rational.

- 1,018 papers → 24 topics for **~$0.08** (median ~256 ms)
- 98,000 listing classifications in ten minutes; YouTube comments, reviews, ad labeling, CMS tagging, log clustering
- 50 M-row scoring enters the ~$20 range
- Semantic features for classical ML — e.g. 2,000 wine notes → CatBoost numeric features at 1.77 RMSE

### 3. Real-Time Loops & Games

Action selection at game, UI, and market clock rates — perception and safety stay in code, Jev picks the move.

- Official: Doom (~10 Hz, ~$7/hr), Wikiracing over high-cardinality link frontiers
- Community: Subway Surfers ×50 parallel, StarCraft ([phyous/tsai-sc](https://github.com/phyous/tsai-sc)), Snake, Tetris, Pac-Man, 2048, stealth games
- Live conversation-state sensors; trolley-problem and moral-dilemma loops

### 4. Browser / Desktop / Mobile Agents

Screens become actions — Jev chooses the operation, a small writing model fills in only the free text.

- [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) (flagship), plus [Ying-Kai-Liao/jev-browser](https://github.com/Ying-Kai-Liao/jev-browser), jkudish, tontoko, vlad-terin
- Android UI agent: Uber route demo in ~21 s / 9 actions → [droidrun/mobile-jev](https://github.com/droidrun/mobile-jev)
- macOS computer-use via OCR → [awlevin/typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use)
- Voice → action: spoken "go back" mapped to a click in **~300 ms**

### 5. Agent Harness Engineering & Guardrails

Make the agent loop cheaper, safer, and composable — Jev as the load balancer above models, tools, and humans.

- Tool-call firewalls → [AnshChoudhary/typesafe-ai-firewall](https://github.com/AnshChoudhary/typesafe-ai-firewall)
- Steering agents instead of interrupting → [DevMortimer/pi-warden](https://github.com/DevMortimer/pi-warden), [AbdelStark/bicameral](https://github.com/AbdelStark/bicameral)
- Compaction, claim verification, prompt-injection screening, agent-failure diagnosis
- MCP servers → [jkudish/jev-mcp](https://github.com/jkudish/jev-mcp), [itsmostafa/typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp)

### 6. Search, Reranking & RAG

Relevance without embeddings — score each candidate with a Noul and sort by the probability.

- Rerank benchmarks vs Cohere / ZeroEntropy → [anessbelbati/jev-rerank-bench](https://github.com/anessbelbati/jev-rerank-bench) (nDCG@10 0.692 vs 0.691 — a tie)
- Citation grounding: does the quoted context support, contradict, or stay silent on the claim?
- Candidate selection for context windows; knowledge-graph entity alignment

### 7. Security, Moderation & Safety

Score, judge, and gate prompts, traces, tool calls, and claims — at a fraction of the LLM call you're protecting.

- Prompt-injection & vulnerable-code benchmarks → [Gaurav-Gosain/jev-sec-bench](https://github.com/Gaurav-Gosain/jev-sec-bench)
- Moderation pipelines — notably strong on non-English (Japanese: 36 misses vs OpenAI's 292 on 826 harmful texts)
- Pre-execution shell / tool safety checks; jailbreak screening on inbound and outbound messages

### 8. Open Re-implementations & Research

Reproducing the *interface*, not the weights — proof that the decision-layer idea travels.

- [TheoLeeCJ/openjev](https://github.com/TheoLeeCJ/openjev) and friends (logit reading, constrained parallel decoding)
- Local / browser / Apple Silicon / vLLM / SGLang experiments; calibration research and playgrounds
- Independent evals worth reading: Every's 777 judgments in <0.7 s (~25× faster than Claude, 6-of-7 defects caught); Near Here's 96% listing moderation; Archer Hume's 84.6% MMLU-Pro probe (third-party, not TypeSafe)

---

## Official Resources & SDKs

- [TypeSafe AI](https://typesafe.ai) · [Introducing System One Models & Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) · [Docs](https://docs.typesafe.ai/introduction) · [Console](https://console.typesafe.ai)
- **Official SDKs:** [typesafe-sdk-python](https://github.com/typesafe-ai/typesafe-sdk-python) · [typesafe-sdk-js](https://github.com/typesafe-ai/typesafe-sdk-js) · [system-one-adapter-python](https://github.com/typesafe-ai/system-one-adapter-python) (benchmark LLMs on the same interface)
- **Bypass the waitlist:** the [Vercel AI Gateway route](https://vercel.com/ai-gateway/models/jev) (`typesafe-ai/jev`)
- **Community clients:** Elixir, Ruby, Rust, .NET, PHP/Laravel, Go, Scala/ZIO — see the ecosystem on GitHub

---

## Contributing

This is a community index. PRs are welcome for:

1. New measured use cases (include cost / latency / accuracy when possible)
2. Missing high-signal repos — link the public source, not a description
3. Corrections or better categorization
4. Patterns that have proven reliable

Keep entries factual and link to source. Separate TypeSafe-reported numbers from your own measurements.

---

## License

MIT — for the index itself. Individual projects retain their own licenses.

---

**Last updated:** 18 September 2026
Jev is only a few days old. Expect this list to grow fast.
