# Contributing

Every link in this repo is scored against a written rubric before it is listed. The rubric lives in `.internal_docs/rubrics.md` (maintainers only). This file is the contributor-facing version.

## The short version

- Keep the diff small — one entry or one short paragraph, in the closest matching section.
- Link the public source (repo or specific file), not a description.
- State *what it does* and *why it's unique*.
- Label every result `[self-reported]` or `[independent]`.
- No unverified performance numbers. Disclose affiliation if it's your project.

## Section rules

| Section | Who adds | Requirements |
|---|---|---|
| **Official Resources** | maintainers | Fix or update links only. Closed set. |
| **Top Use Cases** (🔥/⚡) | maintainers | Ranked by popularity + rubric score. PRs may nominate but won't self-merge. |
| **Community Builders** | anyone | Must (1) actually use Jev, (2) be **unique** (same decision-shape + domain = duplicate), (3) state *what it does* + *why it's unique*, (4) link a public source. |
| **Benchmarks** | anyone | Label `[self-reported]`/`[independent]`; link raw outputs where they exist. |
| **Popular Blogs** | maintainers | Ranked by writer popularity × content uniqueness. SEO recaps auto-rejected. |

## Entry format (Community Builders & Benchmarks)

```
- [owner/repo](link) — <what it does, one line>. <why it's unique, one line>. [self-reported|independent]
```

## Eligible sources

Repos, benchmarks, and writing from Substack, Medium, X.com, Reddit, dev.to, daily.dev, lobster.rs, and HackerNews are all eligible. Discussions and posts qualify only if they carry primary information (a measured result, a first-hand demo, or an original claim) **with a link** — commentary or reposts do not. Aggregators (daily.dev and similar) are never linked directly; follow through to the original source and score that.

## Uniqueness gate

Before adding, check the section for an existing entry with the same decision shape and domain. If one exists, your entry must explain what genuinely differs — otherwise it is a duplicate. Contributor-authored repos are protected: if a duplicate arises, the original contributor's repo stays.

## Hard rules

- No raw star counts on the page.
- One placement per link (Top XOR Community XOR Benchmarks XOR Blogs).
- Keep arithmetic, dates, and thresholds in the *code* you describe, not in the claim.
