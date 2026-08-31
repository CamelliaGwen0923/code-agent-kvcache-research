# Code Agent KV-Cache Research

面向 Code Agent 长上下文请求的 KV-cache 复用、分层存储与软硬件协同研究。

> 当前项目阶段：**0-3 阶段——调研成果版本管理与归档**  
> 本阶段仅固化文献、综述、指标口径与后续研究入口；尚未进入系统实现与性能结论阶段。

## 阶段状态

本阶段已经完成 Code Agent 研究边界、五类文献地图、结构化索引、独立 IEEE 调研报告、首轮硬件约束和 GitHub 归档入口。当前内容不代表已经取得真实 Trace 统计或 RTX 5090 性能结果，也不代表更高容量 HBM 服务器已经获批。

项目暂不自动进入下一技术阶段。完成优先研究问题、指标口径、首轮模型与推理框架、Trace 来源及单机/服务器实验边界评审后，再进入 **0-4 阶段——调研结论评审与研究问题收敛**。

## 当前成果

- [英文 IEEE 双栏调研报告](reports/Survey_KV_Cache_Reuse_and_Hierarchical_Memory_for_Code_Agents_IEEE_v1.pdf)
- [前期 Code Agent 工作负载英文报告](reports/Code_Agent_Workloads_and_KV_Cache_Reuse_IEEE_English.pdf)
- [论文 LaTeX 源码](survey/survey.tex)
- [76 篇文献目录及项目相关性说明](references/文献目录与项目相关性.md)
- [中文分层阅读路线](references/中文阅读路线.md)
- [BibTeX 文献库](references/references.bib)
- [CSV 文献索引](references/references.csv)
- [项目定义与技术指标确认表](project_docs/Code_Agent_KVCache_Project_Definition_Metrics_Confirmation_v1.docx)
- [Code Agent Trace 字段模板](project_docs/Code_Agent_Trace_Field_Template_v1.xlsx)
- [Code Agent 工作负载与 KVCache 复用场景分析](project_docs/Code_Agent_KVCache_Workload_Analysis_v1.docx)

## 调研覆盖范围

1. Code Agent 工作负载、仓库级任务与长时程交互；
2. 精确前缀缓存、Radix/Chunk 索引与位置相关性；
3. HBM、DRAM、NVMe 及远端 KV-cache 分层；
4. Prefill/Decode 解耦、KV 传输与收益感知调度；
5. KV-cache 量化、压缩、淘汰及模型架构兼容；
6. 正确性、延迟、成本、隔离与侧信道安全。

## 语料规模

| 内容 | 数量 |
|---|---:|
| 论文记录 | 76 |
| 可离线阅读的开放获取 PDF | 39 篇，约 913 页 |
| 仅保留官方论文入口 | 37 |
| 官方技术文档入口 | 18 |
| IEEE 调研报告参考文献 | 88 |

论文 PDF 未直接写入 Git 历史。完整离线资源集中在 ZIP 归档中，避免许可证混淆和仓库体积持续膨胀。

## 完整调研资料包

文件：`Code_Agent_KVCache_Comprehensive_Research_Pack_v2.zip`

- 大小：84,017,532 bytes（约 80.1 MiB）
- SHA-256：`0e2752786c9e484de41c5858a90d783e115cbf5a673a9aca408a1351a8bb9b7a`

完整 ZIP 在本项目的交付对话中提供下载；上传 GitHub 后，统一作为 Release `v0.3-research-survey` 的附件，不写入 Git 历史。在 Ubuntu 中可执行：

```bash
sha256sum Code_Agent_KVCache_Comprehensive_Research_Pack_v2.zip
```

输出应与上面的 SHA-256 完全一致。ZIP 没有直接写入 Git 历史，因为它包含大量论文 PDF，约 80 MiB。

## 当前研究判断

- Code Agent 的稳定系统提示词、工具定义、仓库规则及追加式轨迹，为精确前缀复用提供了天然机会。
- 文本相同不等于 KV 状态可直接复用；前置上下文、Token 位置、模型版本和位置编码均属于正确性条件。
- 逻辑命中只有在查询、传输和恢复开销低于重新 Prefill 时，才构成有效命中。
- 项目提出的 70%/95% 命中率、90% TTFT 降幅和 10% 成本比目前均为**待验证目标**，不是既有实验结论。

## 计划实验环境

- 操作系统：Ubuntu
- GPU：NVIDIA GeForce RTX 5090，32 GB GDDR7
- 系统内存：64 GB
- 更高容量 HBM/服务器环境：申请暂定，尚未锁定

## 编译 IEEE 报告

源码位于 `survey/`：

- `survey.tex`：IEEEtran 双栏正文，图形使用 TikZ 内嵌生成；
- `references.bib`：论文使用的参考文献库；
- `IEEEtran.cls`：归档构建所使用的类文件。

Ubuntu 安装完整 TeX Live 后，在 `survey/` 中运行：

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error survey.tex
```

`reports/` 中的 PDF 是已完成逐页视觉检查的交付版本。

## 仓库结构

```text
.
├── README.md
├── reports/                 # 独立 IEEE PDF
├── survey/                  # LaTeX 源码、IEEEtran 与引用库
├── references/              # CSV/BibTeX/JSON/Markdown 索引
├── project_docs/            # 前期可编辑项目材料
├── archive/                 # 版本号和完整包内文件校验清单
└── release/                 # 阶段发布说明
```

## 使用与再分发边界

本仓库当前用于内部研究归档。各论文及第三方材料的版权归原作者与出版方所有：

- 完整包中的离线论文仅收录来源页面明确标注开放许可的版本，具体许可入口见来源清单；
- 对无法确认可再分发的论文，仅保留官方入口，不复制全文；
- 官方网页会持续更新，本项目不把网页快照作为长期权威规范；
- 引用、改编和再次分发时，仍须遵守每篇论文自己的许可与署名条件。

项目自身的报告、索引和说明材料在确定对外开源许可证前，默认不授予额外使用许可。
