# Goedel-Prover-V2-8B on miniF2F: a reproducibility audit

This audit re-runs Goedel-Prover-V2-8B on miniF2F-test through the model's own released pipeline and asks whether it reproduces the paper's **pass@32 = 84.6%**. The repository holds the pre-registration, every script that was run, the result summaries and the hashes of the raw outputs, so each number below can be checked. The report is a draft and has not been peer reviewed.

| | pass@32 |
|---|---|
| Paper (arXiv 2508.03613, Tables 2 and 4) | 84.6% ± 0.6% |
| Model card | 83.0% |
| **This audit, repository dataset** | **82.38% (201/244)** |
| **This audit, paper's statements for 4 differing problems** | **82.79% (202/244)** |
| Goedel-LM/Goedel-Prover-V2#8 | 73.77% (180/244) |

- The audit is one full run of 244 problems × 32 attempts on an A100 in bf16. It used the repository's own `inference.py` and `compile.py` at commit `2e9036e1`, with the pinned Lean `v4.9.0-rc1` / Mathlib and the pinned vLLM 0.8.5.
- The repository's `dataset/minif2f.jsonl` differs from the paper's `AI-MO/minif2f_test` in four statements, and this run solved none of those four. Restoring the paper's statements adds one solved problem.
- Re-checking 380 timed-out attempts with a 1,200 s limit added no solved problems.
- About 4 problems of the gap to the paper remain unexplained.

[REPORT.md](REPORT.md) gives the full result, every departure from the official pipeline, the side findings, and a list of what the audit does *not* claim.

## Contents

| Path | What |
|---|---|
| `REPORT.md` | The audit report |
| `PLAN.md` | Pre-registration, written before each run; check the commit times |
| `PILOT_LOG.md`, `STATUS.md` | Running log |
| `scripts/` | Every script that was run, on GCP VMs |
| `pilot/` | L4 and A100 pilots (10 problems × 8), including the "does not fit a 24 GB GPU" log |
| `main/round1/`, `main/retry/` | Summaries, the official `summarize.py` output, and SHA-256 manifests of the raw files |
| `followup/` | Corrected-statement dataset and summary for the 4-problem follow-up |

The raw outputs are attached to the GitHub release and take about 0.5 GB uncompressed. They contain the model input, the model output and the checked Lean code for all 7,808 + 128 attempts, plus the Lean result for each attempt. You can verify them against the `SHA256SUMS` files in this repository.

## How this was made

I produced the runs, scripts and report with AI coding agents (Claude Code), and I directed and reviewed their work. AI review is not human review, and I am responsible for the claims.

## 中文摘要

這份稽核用 Goedel-Prover-V2 官方 repo 的推論與 Lean 檢查程式，重跑 Goedel-Prover-V2-8B 在 miniF2F-test 上的 pass@32，看能不能重現論文的數字。報告目前是草稿，尚未經過同儕審查。

- 使用 repo 附的資料檔，結果是 201/244 = 82.38%，論文則是 84.6%。
- repo 的資料檔與論文所用的版本有 4 題陳述不同。改用論文的版本後多解出 1 題，結果是 202/244。
- 以 1,200 秒重新檢查逾時的證明，沒有任何一次轉為通過。
- 與論文仍差約 4 題，原因尚未查明。

完整內容請見 [REPORT.md](REPORT.md)。

## License

The code and text written for this audit are released under the MIT license; see [LICENSE](LICENSE).

- `scripts/check_one.py` reproduces a short `handle()` function from Goedel-Prover-V2, which is licensed under Apache-2.0.
- The miniF2F statements and the model outputs in the data files come from their respective sources and keep those sources' licenses.
