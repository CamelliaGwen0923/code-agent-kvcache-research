# English Reading Guide

**English** | [简体中文](中文阅读路线.md)

Build the project model from the Code Agent workload first, then study correctness and safety boundaries, and only then move to caching systems, tiering, and compression. Do not start with quantization papers.

## 0. Read the project artifacts first

1. [Repository overview](../README.md): current status, frozen scope, and confidentiality boundary.
2. [Stage 0 artifact index](../reports/stage-0/README.md): the complete 0-4 and 0-5 archive.
3. [Stage 0-5 Experimental Predesign - English PDF](../reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_EN.pdf): RQ/G/H, workloads, baselines, M0-M8, metrics, correctness, statistics, and Stage 1 admission.
4. [Stage 0-4 Research Problem Convergence](../reports/stage-0/Code_Agent_KVCache_Stage_0-4_Research_Problem_Convergence_v1.pdf) and [Evidence-Gap Matrix](../reports/stage-0/Code_Agent_KVCache_Stage_0-4_Evidence_Gap_Matrix_v1.xlsx): why the final direction was selected.
5. [English IEEE Survey](../reports/Survey_KV_Cache_Reuse_and_Hierarchical_Memory_for_Code_Agents_IEEE_v1.pdf) and [earlier workload report](../reports/Code_Agent_Workloads_and_KV_Cache_Reuse_IEEE_English.pdf): the broader literature map.

For machine-readable references, use [references.csv](references.csv) and [references.bib](references.bib). The detailed 76-paper annotations are currently in the [Chinese annotated catalog](文献目录与项目相关性.md).

## First pass: establish the research object

- **SWE-bench: Can Language Models Resolve Real-World GitHub Issues?** - benchmark for real repository-level issues and long-context requirements.
- **SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering** - tool-loop and Agent-computer-interface baseline.
- **OpenHands: An Open Platform for AI Software Developers as Generalist Agents** - general software-development Agent platform and trajectory structure.
- **Agentless: Demystifying LLM-based Software Engineering Agents** - non-Agent localization, repair, and validation comparison.
- **SWE-bench Goes Live!** - continuously updated repository-level evaluation and contamination control.
- **Multi-SWE-bench: A Multilingual Benchmark for Issue Resolving** - multilingual repository tasks and Agent comparison.
- **Training Software Engineering Agents and Verifiers with SWE-Gym** - training environment and trajectory data for software-engineering Agents.
- **ContextBench: A Benchmark for Context Retrieval in Coding Agents** - diagnosis of context retrieval in coding-agent trajectories.

## Second pass: establish reproducible systems baselines

- **Efficient Memory Management for Large Language Model Serving with PagedAttention** - baseline for PagedAttention and GPU KV memory management.
- **SGLang: Efficient Execution of Structured Language Model Programs** - baseline for RadixAttention and reuse in structured generation.
- **Prompt Cache: Modular Attention Reuse for Low-Latency Inference** - modular prompt caching and position handling.
- **ChunkAttention: Efficient Self-Attention with Prefix-Aware KV Cache and Two-Phase Partition** - prefix-aware sharing and attention kernels.
- **CacheBlend: Fast Large Language Model Serving for RAG with Cached Knowledge Fusion** - non-prefix cache fusion and selective recomputation.
- **EPIC: Efficient Position-Independent Caching for Serving Large Language Models** - position-independent caching and linear-boundary repair.
- **Irminsul: MLA-Native Position-Independent Caching for Agentic LLM Serving** - MLA-native position-independent caching for Agents.
- **Compute Or Load KV Cache? Why Not Both?** - benefit boundary for parallel cache loading and recomputation.
- **MemServe: Context Caching for Disaggregated LLM Serving with Elastic Memory Pool** - distributed elastic memory pools and cross-instance caching.
- **DistServe: Disaggregating Prefill and Decoding for Goodput-optimized Large Language Model Serving** - prefill/decode disaggregation baseline.
- **CacheGen: KV Cache Compression and Streaming for Fast Large Language Model Serving** - KV compression, streaming, and bandwidth adaptation.
- **LMCache: An Efficient KV Cache Layer for Enterprise-Scale LLM Inference** - cross-engine, cross-request KV cache layer.

## Third pass: capacity, quality, and security

- **KIVI: A Tuning-Free Asymmetric 2bit Quantization for KV Cache** - asymmetric 2-bit KV quantization baseline.
- **KVQuant: Towards 10 Million Context Length LLM Inference with KV Cache Quantization** - KV quantization for extremely long context.
- **H2O: Heavy-Hitter Oracle for Efficient Generative Inference of Large Language Models** - heavy-hitter-driven KV eviction.
- **Scissorhands: Exploiting the Persistence of Importance Hypothesis for LLM KV Cache Compression at Test Time** - persistent importance under fixed cache budgets.
- **Efficient Streaming Language Models with Attention Sinks** - attention sinks and streaming long context.
- **SnapKV: LLM Knows What You are Looking for Before Generation** - pre-generation important-token selection.
- **PyramidKV: Dynamic KV Cache Compression based on Pyramidal Information Funneling** - pyramidal layer-wise cache budgets.
- **MiniCache: KV Cache Compression in Depth Dimension for Large Language Models** - depth-wise cross-layer KV merging.
- **DeepSeek-V2: A Strong, Economical, and Efficient Mixture-of-Experts Language Model** - MLA structure and changed KV representation.
- **DeepSeek-V3 Technical Report** - DeepSeek-V3 architecture and MLA implementation context.
- **GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints** - GQA structure and shared KV heads.
- **LongBench: A Bilingual, Multitask Benchmark for Long Context Understanding** - bilingual, multitask long-context evaluation.

## Reading discipline

- Treat the Stage 0-5 report as the frozen protocol, not as a result report.
- Keep Pilot data separate from Core results.
- Record negative and failed results instead of deleting them.
- For online documentation, record the access date and version; use the [official resource list](official_docs.md) as the maintained entry point.

