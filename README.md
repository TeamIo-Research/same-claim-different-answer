# Script and Stance — pre-registration and data

**Script and Stance: Do Frontier LLMs Treat the Same Political Claim Differently by Writing System and User Stance?**
Team Io · Global South AI Safety Hackathon 2026 (Apart Research), 19–21 June 2026

- Write-up: *We Found a Political Stance Effect in Frontier LLMs. It Turned Out to Be Our Own Judges.* (Medium)
- The full hackathon report (submitted to Apart Research) describes the methods and results in detail.

## Pre-registration freeze

**Frozen at commit [`8b041fb`](https://github.com/TeamIo-Research/same-claim-different-answer/commit/8b041fb)** — `8b041fba6e5fa066ddee3408a7cce81db796f1f8`, 2026-06-19 09:45:45 +0800, before the main data-collection run.

The freeze commit contains the probe set (three renderings), the analysis plan, the coding manual, and a machine-readable probe render. It has not been altered since. A commit cannot contain its own hash, so the README inside the freeze commit shows placeholders (`[commit hash TBD]`); the hash is recorded here instead. To see the repository exactly as frozen:

```
git show 8b041fb --stat
git show 8b041fb:README.md
```

The original pre-registration README (Chinese) is kept in [`docs/README_at_freeze_zh.md`](docs/README_at_freeze_zh.md), with internal drafting notes removed. The verbatim original is always available at `8b041fb`.

## Files

**Frozen at `8b041fb`**

| File | Content |
|---|---|
| `01_probe_v5.3_zh-Hant.md` | Probe script v5.3, Traditional Chinese (source version) |
| `02_probe_v5.3_zh-Hans.md` | Probe script v5.3, Simplified Chinese (OpenCC conversion; Taiwanese lexis retained) |
| `03_probe_v5.3_en.md` | Probe script v5.3, English |
| `04_analysis_plan_pre-reg_v2.1.md` | Pre-registered analysis plan |
| `05_coding_manual_v1.1.md` | Coding manual (shared by LLM judges and human coders) |
| `06_probe_render_zh.md` | Machine-readable probe render |

**Added after the freeze (`data/`, commits dated 2026-06-20 to 2026-06-22)**

| File | Content |
|---|---|
| `official_20260619__tested.jsonl` | Tested-model responses, one row per turn |
| `official_20260619__judge.jsonl` | Original judge votes |
| `official_20260619__judge_rejudge.jsonl` | Re-judged votes with the corrected judge prompt (`rubric_version: corrected_20260621`) |
| `official_20260619__formal_stats_rejudge.md` | Statistics under corrected judging |
| `official_20260619__aggregates.json` | Aggregated scores |
| `official_20260619__blindmap.json` | Blinding map |
| `official_20260619__Results摘要.md`, `official_20260619__Results聚合表.xlsx` | Results summary and aggregate table (Chinese; original judging, generated during the sprint) |
| `human_coding_κ試打_20260620.xlsx`, `第三人_事實糾正_κ試打_20260620.xlsx` | Human double-coding sheets (Chinese; coder identities anonymized as Coder 1/2/3) |

## Deviations from the pre-registration

1. **Gemini dropped.** The pre-registration specified four tested models and four judge seats, including `gemini-3.1-pro-preview`. During collection the Google API returned a hard rate limit that could not be cleared within the sprint. Gemini was dropped independently of its outputs. Its 292 partial rows remain in `tested.jsonl` but no Gemini data entered any analysis. Analyses use three tested models (`claude-sonnet-4-6`, `claude-opus-4-8`, `gpt-5.5`) and three judge seats (`claude-opus-4-8`, `gpt-5.5`, `grok-4.3`), with same-vendor recusal.
2. **Judge re-scoring.** The judges systematically misapplied the rebuttal-strength criterion on doubt-condition items (scoring disagreement with the user rather than negation of the claim). All stance-bearing (doubt/endorse) cells were re-judged (2,988 cross-family votes) with a corrected prompt that restates the frozen codebook's criterion and adds two worked examples. The rubric itself was not changed. The original votes were kept in a separate file and never overwritten; both rounds are released. The corrected prompt was designed after seeing the failure and has not been tested on held-out probes.
3. **Coder anonymization.** Human coder names in the coding sheets were replaced with Coder 1/2/3 (commit `b6a134b`).

Failed API calls are kept in the data files with `status: "error"`.
