# Code Agent KVCache 研究项目

[English](README.md) | **简体中文**

面向 Code Agent 长上下文请求的 KVCache 安全复用、分层保留与软硬件协同研究。

> **项目状态：** Stage 0 的研究问题、研究目标、可证伪假设、工作负载、基线、实验矩阵、主指标、正确性门槛与复现规则均已冻结。研究与设计成果已经完成归档。Stage 1 尚未开始。
>
> **证据边界：** 本仓库保存的是研究与实验设计，不包含已经完成的性能结果。候选目标不得写成实测结论。

## 建议从这里开始

1. 阅读 [中文阅读路线](references/中文阅读路线.md) 或 [English Reading Guide](references/Reading_Guide_EN.md)。
2. 查看 [Stage 0 成果索引](reports/stage-0/README.md)。
3. 阅读 Stage 0-5 实验预设计报告：[中文 DOCX](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_ZH.docx)、[英文 PDF](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_EN.pdf) 或 [英文 DOCX](reports/stage-0/Code_Agent_KVCache_Stage_0-5_Experimental_Predesign_Report_v1_EN.docx)。
4. 使用 [Stage 0-4 证据空白矩阵](reports/stage-0/Code_Agent_KVCache_Stage_0-4_Evidence_Gap_Matrix_v1.xlsx) 与 [研究问题收敛报告](reports/stage-0/Code_Agent_KVCache_Stage_0-4_Research_Problem_Convergence_v1.pdf) 查看冻结研究方向的依据。

## 已冻结的研究方向

项目聚焦暂停-恢复型、追加式 Code Agent 会话，主技术路线为：

> **精确前缀复用 + GPU/DRAM/NVMe/重计算联合决策 + 任务级价值评测**

完整证据链为：

> 为什么复用 -> 哪些内容能安全复用 -> 从哪里恢复 -> 恢复是否比重算更快 -> 输出是否正确 -> 任务是否成功 -> 结论能否复现。

| 冻结对象 | 范围 |
|---|---|
| 研究问题 | RQ1-RQ5；RQ1-RQ4 为核心，RQ5 为长期泛化 |
| 研究目标 | G1-G8 |
| 可证伪假设 | H1-H8 |
| 工作负载 | W1 公开真实轨迹、W2 自采集 SWE-bench Agent 轨迹、W3 合成轨迹 |
| 回放方式 | R1 结构回放、R2 Token 精确回放、R3 端到端 Agent |
| 基线 | B0-B6 |
| 实验组 | M0-M8 |
| 主指标 | 正确性、有效 Token 命中率、P95 TTFT、会话完成时间、每个成功任务成本 |

高风险的非前缀复用 G6 只能在精确前缀主线通过全部正确性门槛后启动；跨模型、架构与硬件泛化 G8 属于后续扩展。

## Stage 0 成果

- [Stage 0 成果索引](reports/stage-0/README.md)
- [英文 IEEE 调研报告](reports/Survey_KV_Cache_Reuse_and_Hierarchical_Memory_for_Code_Agents_IEEE_v1.pdf)
- [前期 Code Agent 工作负载英文报告](reports/Code_Agent_Workloads_and_KV_Cache_Reuse_IEEE_English.pdf)
- [IEEE 调研报告 LaTeX 源码](survey/survey.tex)
- [76 篇文献目录与项目相关性说明](references/文献目录与项目相关性.md)
- [BibTeX 文献库](references/references.bib) 与 [CSV 文献索引](references/references.csv)
- [官方技术资料入口 / Official Technical Resources](references/official_docs.md)
- [项目定义与技术指标确认表](project_docs/Code_Agent_KVCache_Project_Definition_Metrics_Confirmation_v1.docx)
- [Code Agent Trace 字段模板](project_docs/Code_Agent_Trace_Field_Template_v1.xlsx)
- [工作负载与 KVCache 复用场景分析](project_docs/Code_Agent_KVCache_Workload_Analysis_v1.docx)

## 候选目标不是实验结果

此前提出的 70%/95% 命中率、90% TTFT 降幅和 10% 成本比，仍然只是需要在 Stage 1 验证的候选目标，不能作为已经取得的成果引用。

## 首期计划环境

- Ubuntu
- NVIDIA GeForce RTX 5090，32 GB GDDR7
- 64 GB 系统内存
- 本地 NVMe

精确模型 Revision、CUDA/PyTorch/vLLM 版本、缓存容量、Block Size、并发量、重复次数与超时，均须由 Stage 1 环境审计或 Pilot 决定。

## Stage 1 准入规则

Stage 1 首先只进行 Ubuntu、NVIDIA 驱动、CUDA、Python、GPU 与内存健康、Swap、NVMe、Docker、现有环境和项目隔离要求的只读盘点。在审计完成前，不安装软件、不升级驱动、不修改现有 Python 环境，也不运行正式性能实验。

Stage 1 的实验代码与结果将存放在独立私有仓库 `code-agent-kvcache-experiments`。大型 KV 文件、模型权重、密钥、私人 Prompt、未脱敏 Trace 和未脱敏日志不得进入 Git。

## 仓库结构

```text
.
├── README.md / README.zh-CN.md
├── reports/
│   ├── stage-0/             # Stage 0-4 与 0-5 冻结成果
│   └── *.pdf                # IEEE 报告
├── survey/                  # LaTeX 源码、IEEEtran 与引用库
├── references/              # 双语导引、索引与官方入口
├── project_docs/            # 前期可编辑项目材料
├── archive/                 # 资料包版本与校验清单
└── release/                 # 双语发布说明
```

## 使用、保密与再分发边界

本私有仓库用于内部研究归档。论文与第三方材料版权归原作者和出版方所有；独立调研资料包中的开放获取 PDF 受各自来源许可约束，无法确认再分发权限的材料只保留官方入口。

分享任何副本前，必须移除未发表 Prompt、私人 Trace、凭据与密钥、模型权重、大型 KV 文件和未脱敏日志。在仓库明确采用许可证之前，项目自身报告、索引与说明材料不额外授予使用许可。

