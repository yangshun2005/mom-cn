> **[中文化] MoM**
>
> 此项目是 [MemTensor/MoM](https://github.com/MemTensor/MoM) 的中文翻译版本。
> 代码与上游保持一致，未做功能改动。
> - 原项目 Stars: 44
> - 主语言: Python
> - 许可证: Apache-2.0
> - 整理日期: 2026-10-09
> - 原始 README: [README_en.md](README_en.md)
>
> 著作权归上游作者所有。功能改动请提到上游仓库。

---
## 这是什么

MoM（Mixtures of Scenario-Aware Document Memories）是一个面向 RAG 系统的文档记忆框架。它把 RAG 里的文本处理从被动分块改成主动记忆抽取：先像领域专家那样整体理解文档，再构造结构化的文档记忆。目标读者包括 NLP 与信息检索研究者、LLM 应用开发者，以及关注小模型（SLM）认知能力的研究者。

## 核心能力

- **主动记忆抽取**：把 RAG 里的文本处理从被动文本分块（chunk）改为主动记忆抽取。
- **结构化文档记忆**：把文档记忆定义为由宏观逻辑大纲、高度浓缩的核心内容和语义连贯的原子块组成的三元组。
- **MoM 框架与 CoM**：MoM 通过多路径采样和多维评估机制生成高质量记忆；再用反向推理策略构造 CoM（Chain of Memory extraction），把复杂认知能力迁移给 SLM。
- **三层检索机制**：覆盖逻辑大纲、核心内容和原文的文档记忆检索；上游从概率建模角度证明，该策略相比检索前融合能更有效地减少信息损失。
- **MemReader 模型**：在 Hugging Face 上提供 1.5B、3B、7B 三档 MemReader 模型。
- **多领域实验**：在新闻、金融等不同领域的三个 QA 数据集上做实验，并提出用于评估记忆块质量的记忆评测指标。

## 快速开始

安装依赖：

```bash
pip install -r requirements.txt
```

启动 milvus-lite 向量数据库服务：

```bash
milvus-server --data /Storage/path/of/the/database
```

下载模型到对应目录，按需修改配置，然后运行 `chunk_*.py` 和 `mom_*.py` 完成领域文档的文本分块；随后执行 `quick_start.py` 和 `retrieval.py` 进行检索与问答。例如：

```bash
CUDA_VISIBLE_DEVICES=0 nohup python chunk_gpt.py >> multifiled/qwen3_14B_set.log 2>&1 &
```

```bash
CUDA_VISIBLE_DEVICES=1 nohup python quick_start.py 
--docs_path 'crud_qwen3_14B_set.json' 
--collection_name 'crud_qwen3_14B_set' 
--retrieve_top_k 8 
--task 'quest_answer' 
--construct_index 
>> log/mom_crud_qwen3_14B_set.log 2>&1 &
```

另外可以打开并运行 `chunk.ipynb`，对不同分块策略的结果做质量评估。

## 与上游的差异

本仓库不做功能改动，只补充中文文档。如需提交功能改动，请提到上游仓库 [MemTensor/MoM](https://github.com/MemTensor/MoM)。

## 许可证

上游项目使用 Apache License 2.0。本仓库的代码部分沿用上游同一许可证。
