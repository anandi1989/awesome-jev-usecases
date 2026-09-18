# Awesome Jev Use Cases

> **Evidence-backed index of real-world Jev (TypeSafe AI System One) use cases, repos, patterns, and measured results since launch (15 Sep 2026).**

[![Jev Launch](https://img.shields.io/badge/Jev-launched%2015%20Sep%202026-blue)](https://typesafe.ai)
[![System One](https://img.shields.io/badge/System%20One-Decision%20Model-orange)](https://typesafe.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com)

**Jev** is TypeSafe AI’s first System One model — a frontier decision engine optimized for fast, typed, calibrated judgments (Choice / Score / Noul) instead of free-form text generation.  
Typical latency 70–500 ms · ~$0.042 / M input tokens · output tokens free.

This repository is a living, searchable index of what the community has actually shipped in the first days after launch.  
Every entry is grounded in public repos, measured results, or documented experiments.

---

## Quick Start

```bash
# Clone
git clone https://github.com/YOUR_USER/awesome-jev-usecases.git
cd awesome-jev-usecases

# Browse
open README.md          # or just read below
```

No installation required. This is a curated knowledge index + links to working code.

---

## Why This Exists

Within 72 hours of launch the community produced:
- Browser agents that book flights in ~7 s for < $0.004
- Trading bots making decisions every ~300 ms
- Computer-use agents at $0.0002 per step
- Agent guardrails, code reviewers, drones, games, bulk classifiers, and more

Most of these projects are still experimental. This index helps you find the ones worth reading and the patterns that already work.

---

## Flagship Projects (Highest Signal)

| Project | What it does | Headline result | Stars (approx) |
|---------|--------------|-----------------|----------------|
| [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | Browser agent with dynamic indexed action space | Zürich → London Google Flights in **7.1 s / $0.0039** | ~2.3k |
| [TheoLeeCJ/openjev](https://github.com/TheoLeeCJ/openjev) | Open re-implementation on frozen 4B model (logit reading) | Runs in browser, no waitlist | ~850 |
| [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | Claude Code compaction → Jev keep/delete | Content stays **verbatim** | ~850 |
| [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | Market maker on Monad/Kuru | **81 ms** model latency per block | ~530 |
| [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | Super Mario from emulator RAM (no screenshots) | Object-centric JSON → controller actions | ~220 |
| [awlevin/typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) | macOS computer use via OCR + Jev | **$0.0002 / decision** vs Opus 5 $0.032 | ~170 |
| [thruwire/foreman](https://github.com/thruwire/foreman) | Supervisor over Codex workers | Architecture experiment for software factories | — |
| [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | Staged code reviewer + dashboard | Risk matrix → evidence → severity → routing | — |
| [RomanSlack/jev-drone](https://github.com/RomanSlack/jev-drone) | Drone control in MuJoCo | Advisory at ~2.5 Hz | ~50+ |

---

## Use-Case Catalog

### 1. Smart Workflow Decisions (“Intelligent if-statements”)
Fuzzy classify / route / score / branch inside ordinary software.

- Support triage (dept, urgency, frustration, refund, policy fit)
- Model / skill routing in agent harnesses
- Email fraud detection, résumé–job scoring
- Natural-language Postgres WHERE clauses → [realZachi/pg-jev](https://github.com/realZachi/pg-jev)

### 2. Bulk Map-Reduce Classification
Cheap judgment over large corpora.

- 1,018 papers → 24 topics (~$0.08 for classifications)
- YouTube comments, product reviews, ad labeling, CMS tagging, log clustering
- Economics: 50 M-row table scoring becomes practical (~$20 range)

### 3. Real-Time Loops & Games
Decisions inside tight control loops.

- Official: Doom (~10 Hz, ~$7/hr), Wikiracing (high-cardinality links)
- Community: Subway Surfers ×50, StarCraft, Snake, 2048, Tetris, stealth games
- Live conversation state sensors

### 4. Browser / Desktop / Mobile Agents
- [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) (flagship)
- Additional browser agents (jkudish, Ying-Kai-Liao, tontoko, vlad-terin)
- Android UI agent (Uber route demo ~21 s / 9 actions)
- macOS computer-use with OCR

### 5. Agent Harness Engineering & Guardrails
- Tool-call firewalls ([AnshChoudhary/typesafe-ai-firewall](https://github.com/AnshChoudhary/typesafe-ai-firewall))
- Steering agents instead of interrupting ([DevMortimer/pi-warden](https://github.com/DevMortimer/pi-warden))
- Compaction, claim verification, prompt-injection screening
- MCP servers ([jkudish/jev-mcp](https://github.com/jkudish/jev-mcp) and others)

### 6. Search, Reranking & RAG
- Relevance scoring without embeddings
- Candidate selection for context windows
- Rerank benchmarks vs Cohere / ZeroEntropy

### 7. Security, Moderation & Safety
- Prompt injection & vulnerable-code benchmarks
- Moderation pipelines (notably strong on non-English in some tests)
- Pre-execution shell / tool safety checks

### 8. Open Re-implementations & Research
- Multiple “OpenJev” variants (logit reading, constrained parallel decoding)
- Local / browser / Apple Silicon / vLLM / SGLang experiments
- Calibration research and playgrounds

---

## Other High-Quality Indexes

| Resource | Focus |
|----------|-------|
| [aliaihub/awesome-jev-usecases](https://github.com/aliaihub/awesome-jev-usecases) | Deepest evidence-backed catalog + measured results |
| [Anil-matcha/awesome-jev-by-typesafe](https://github.com/Anil-matcha/awesome-jev-by-typesafe) | Patterns, prompts, starter code |
| [AnotiaWang/awesome-jev](https://github.com/AnotiaWang/awesome-jev) | Applications, SDKs, demos & games |
| [galigutta.github.io/jev-use-cases](https://galigutta.github.io/jev-use-cases/) | Independent MECE taxonomy (6 pillars) |
| [classify.st](https://classify.st/) | Public catalogue of shipped jobs with cost/latency |

---

## Official Resources

- [TypeSafe AI](https://typesafe.ai)
- [Introducing System One Models & Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) (launch post)
- [Jev docs / console](https://console.typesafe.ai) (early access)

---

## Contributing

This is a community index. PRs are welcome for:

1. New measured use cases (include cost / latency / accuracy when possible)
2. Missing high-signal repos
3. Corrections or better categorization
4. Patterns that have proven reliable

Please keep entries factual and link to source.

---

## Naming Note

Directory / repo name chosen for search discoverability around:
- “Jev use cases”
- “TypeSafe Jev”
- “System One model”
- “Jev decision model”
- “awesome Jev”

---

## License

MIT (for the index itself). Individual projects retain their own licenses.

---

**Last updated:** 18 September 2026  
Jev is only a few days old. Expect this list to grow rapidly.
