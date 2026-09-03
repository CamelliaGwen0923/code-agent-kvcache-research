# Code Agent KVCache Research

**English** | [简体中文](README.zh-CN.md)

Research on safe KVCache reuse, tiered retention, and hardware-software co-design for long-context Code Agents.

> **Project status:** Stage 0-5.7 was approved on September 2, 2026. The Stage 0 research questions, hypotheses, workloads, baselines, experiment matrix, primary metrics, correctness gates, and reproducibility rules are frozen. The research/design archive is complete; formal Stage 0 closure still requires the `stage-0-complete` tag. Stage 1 has not started.
>
> **Evidence boundary:** this repository contains research and experimental design, not completed performance results. Candidate targets must not be presented as measured outcomes.

## Start here

1. Read the [English reading guide](references/Reading_Guide_EN.md) or [中文阅读路线](references/中文阅读路线.md).
2. Review the [Stage 0 artifact index](reports/stage-0/README.md).
3. Read the Stage 0-5 experimental predesign report in [English PDF](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_EN.pdf), [English DOCX](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_EN.docx), or [Chinese DOCX](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_ZH.docx).
4. Use the [Stage 0-4 evidence-gap matrix](reports/stage-0/Code_Agent_KVCache_Stage_0-4_Evidence_Gap_Matrix_v1.xlsx) and [problem-convergence report](reports/stage-0/Code_Agent_KVCache_Stage_0-4_Research_Problem_Convergence_v1.pdf) for the evidence behind the frozen direction.

## Frozen research direction

The project studies pause-resume, append-only Code Agent sessions. Its main line is:

> **Exact-prefix reuse + joint GPU/DRAM/NVMe/recomputation decisions + task-level value evaluation**

The evidence chain is:

> Why reuse -> what can be reused safely -> where to restore it from -> whether restoration is faster than recomputation -> whether output is correct -> whether the task succeeds -> whether the conclusion is reproducible.

| Frozen object | Scope |
|---|---|
| Research questions | RQ1-RQ5; RQ1-RQ4 are core and RQ5 is long-term generalization |
| Goals | G1-G8 |
| Falsifiable hypotheses | H1-H8 |
| Workloads | W1 public traces, W2 self-collected SWE-bench Agent traces, W3 synthetic traces |
| Replay modes | R1 structural, R2 token-exact, R3 end-to-end Agent |
| Baselines | B0-B6 |
| Experiment groups | M0-M8 |
| Primary metrics | correctness, effective token hit rate, P95 TTFT, session completion time, cost per successful task |

High-risk non-prefix reuse (G6) begins only after the exact-prefix main line passes every correctness gate. Cross-model, architecture, and hardware generalization (G8) is a later extension.

## Stage 0 outputs

- [Stage 0 artifact index](reports/stage-0/README.md)
- [English IEEE survey](reports/Survey_KV_Cache_Reuse_and_Hierarchical_Memory_for_Code_Agents_IEEE_v1.pdf)
- [Earlier English workload report](reports/Code_Agent_Workloads_and_KV_Cache_Reuse_IEEE_English.pdf)
- [IEEE survey LaTeX source](survey/survey.tex)
- [76-paper Chinese annotated catalog](references/文献目录与项目相关性.md)
- [BibTeX library](references/references.bib) and [CSV index](references/references.csv)
- [Official technical resources / 官方技术资料](references/official_docs.md)
- [Project definition and metric confirmation](project_docs/Code_Agent_KVCache_Project_Definition_Metrics_Confirmation_v1.docx)
- [Code Agent trace field template](project_docs/Code_Agent_Trace_Field_Template_v1.xlsx)
- [Workload and KVCache reuse analysis](project_docs/Code_Agent_KVCache_Workload_Analysis_v1.docx)

## Candidate targets are not results

The earlier figures of 70%/95% hit rate, 90% TTFT reduction, and 10% cost ratio remain candidate targets for Stage 1 experiments. They are not achieved results and must not be cited as such.

## Planned initial environment

- Ubuntu
- NVIDIA GeForce RTX 5090, 32 GB GDDR7
- 64 GB system memory
- Local NVMe

Exact model revision, CUDA/PyTorch/vLLM versions, cache budgets, block size, concurrency, repetitions, and timeouts remain undecided until the Stage 1 environment audit and Pilot.

## Stage 1 admission rule

Stage 1 starts with a read-only inventory of Ubuntu, NVIDIA driver, CUDA, Python, GPU and memory health, swap, NVMe, Docker, existing environments, and isolation requirements. Until that audit is complete, the project does not authorize software installation, driver upgrades, changes to existing Python environments, or formal performance experiments.

Stage 1 experiment code and results will live in a separate private repository, `code-agent-kvcache-experiments`. Large KV files, model weights, secrets, private prompts, unsanitized traces, and unsanitized logs must not enter Git.

## Repository structure

```text
.
├── README.md / README.zh-CN.md
├── reports/
│   ├── stage-0/             # Stage 0-4 and 0-5 frozen artifacts
│   └── *.pdf                # IEEE reports
├── survey/                  # LaTeX source, IEEEtran, and bibliography
├── references/              # bilingual guides, indexes, and official links
├── project_docs/            # editable early-stage project materials
├── archive/                 # package version and checksum inventory
└── release/                 # bilingual release notes
```

## Use, confidentiality, and redistribution

This private repository is an internal research archive. Copyright in papers and third-party materials remains with their authors and publishers. Open-access PDFs in the separate research package follow their source licenses; uncertain items are represented by official links only.

Before sharing any copy, remove unpublished prompts, private traces, credentials, keys, model weights, large KV artifacts, and unsanitized logs. Project-authored reports, indexes, and notes grant no additional reuse license until an explicit repository license is adopted.

