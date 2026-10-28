# 苏剑林《科学空间》学习笔记

系统学习苏剑林（Kimi 研究员，RoPE 提出者）博客《科学空间》（kexue.fm）的个人笔记仓库。

**定位**：只写自己的概括、推导脉络梳理与思考，附原文链接；不搬运原文全文。原文版权归苏剑林所有，遵循其站点的署名-非商业-保持一致协议。

## 站点盘点（2026-10-27）

《科学空间》自 2009 年连载至今约 1600 篇（文章 ID 已至 11848）。与大模型研究最相关的核心主线：

| 主线 | 规模 | 说明 |
|---|---|---|
| A. Transformer 升级之路 + 位置编码 | 编号 21 篇（2021–2025） | 从 Sinusoidal 溯源、RoPE、长度外推到 MLA，博客的招牌系列 |
| B. 注意力变体与 KV Cache | 约 15 篇 | MHA/MQA/GQA/MLA 之争、线性注意力简史、DeltaNet/GDN/KDA、Kimi Linear |
| C. MoE 环游记 | 编号 9 篇（2025–2026） | 从几何意义重构 MoE，负载均衡（Aux Loss / Loss-Free / QB）为核心议题 |
| D. 优化器与训练科学 | 50+ 篇 | Muon 全家桶（赏析/续集/msign/流形最速下降 7 篇/流式幂迭代 5 篇）、Adam 理论、学习率与 Batch Size 4 篇、MuP 系列、「让炼丹更科学」系列 |
| E. 生成模型 | 扩散漫谈编号 31 篇（2022–2025） | DDPM 出发，经 ODE/SDE 统一框架到流匹配与一致性模型；另有 VAE 系列 8+ 篇 |
| F. 线性注意力与 SSM | 约 15 篇 | 重温 SSM 4 篇、线性 Attention 探索、DeltaNet 系列 |
| G. Kimi 工程报告解读 | 约 6 篇 | Moonlight（Muon 可扩展性）、Kimi Linear 技术报告、K3 架构复盘、QK-Clip |
| H. 数学基础散篇 | 100+ 篇 | 低秩近似之路 5 篇、矩阵求导、概率不等式、JL 引理、渐近估计等，多为 A–G 的弹药库 |
| I. 早期 NLP | 数十篇（2019–2022） | bert4keras、GlobalPointer、CoSENT、SimBERT 等，本仓库暂不覆盖 |

## 第一批基石笔记（10 篇）

| # | 笔记 | 主线 | 原文 | 一句话主题 |
|---|---|---|---|---|
| 01 | [Sinusoidal 位置编码追根溯源](notes/01-sinusoidal-origin.md) | A | [kexue.fm/archives/8231](https://kexue.fm/archives/8231) | 用泰勒展开 + 相对位置约束反推出 Sinusoidal 编码的必然形式 |
| 02 | [博采众长的旋转式位置编码 RoPE](notes/02-rope.md) | A | [kexue.fm/archives/8265](https://kexue.fm/archives/8265) | 解函数方程得到 RoPE：以绝对位置编码之形，行相对位置编码之实 |
| 03 | [缓存与效果的极致平衡：从 MHA、MQA、GQA 到 MLA](notes/03-mha-to-mla-cache.md) | B | [kexue.fm/archives/10091](https://kexue.fm/archives/10091) | KV Cache 压缩的演化史；MLA 的本质是低秩投影之后换上通用线性变换 |
| 04 | [MLA 为什么如此之好？（上）](notes/04-mla-why-so-good-1.md) | A/B | [kexue.fm/archives/10907](https://kexue.fm/archives/10907) | 受控实验拆解 MLA 的优势来源：head_dim 最大，其次 Partial RoPE 与 KV 共享 |
| 05 | [MoE 环游记 1：从几何意义出发](notes/05-moe-geometry.md) | C | [kexue.fm/archives/10699](https://kexue.fm/archives/10699) | 把 FFN 写成专家向量之和，MoE 即「按范数 Top-k 近似稠密模型」 |
| 06 | [MoE 环游记 2：不患寡而患不均](notes/06-moe-load-balance.md) | C | [kexue.fm/archives/10735](https://kexue.fm/archives/10735) | 用 STE 从第一性原理推导负载均衡 Aux Loss，并指出它并非真正的 loss |
| 07 | [简单谈谈 K3 的 MoE 和 Attention](notes/07-k3-moe-attention.md) | G | [kexue.fm/archives/11848](https://kexue.fm/archives/11848) | K3 = KDA + MLA + Stable LatentMoE + AttnRes；SiTU、QB 与 NoPE 的取舍 |
| 08 | [Muon 续集：为什么我们选择尝试 Muon？](notes/08-muon-sequel.md) | D | [kexue.fm/archives/10739](https://kexue.fm/archives/10739) | 谱范数约束下的最速下降 = Muon；Update RMS 对齐实现 Adam 超参平移 |
| 09 | [为什么 Adam 的 Update RMS 是 0.2？](notes/09-adam-update-rms.md) | D | [kexue.fm/archives/11267](https://kexue.fm/archives/11267) | 平均场近似给出闭式：纯噪声极限下 RMS 只由 $\beta_1$ 决定 |
| 10 | [生成扩散模型漫谈（一）：DDPM = 拆迁 + 建房](notes/10-diffusion-ddpm.md) | E | [kexue.fm/archives/9119](https://kexue.fm/archives/9119) | 先学会逐步加噪「拆迁」，再逐项反演「建房」，训练目标化为预测噪声 |

## Backlog（待续规模）

- A 线：升级之路其余 19 篇（长度外推专题 6–18 占大头）+ 第 21 篇（MLA 下）
- B 线：线性注意力简史、DeltaNet 的 L2 Normalize、Kimi Linear 解读等约 12 篇
- C 线：环游记其余 7 篇（均匀分布之思、动态激活、均衡最优分配 = QB 出处、门控归一化之争等）
- D 线：Muon 赏析、流形最速下降 7 篇、学习率与 Batch Size 其余 3 篇、MuP 系列等约 40 篇
- E 线：扩散漫谈其余 30 篇
- F/G 线：重温 SSM 4 篇、QK-Clip、Attention Residuals 回忆录等约 10 篇

## 笔记体例

每篇 NOTES 固定结构：原文链接 → 一句话 summary → 大纲 → 推导脉络（mermaid 流程图）→ 关键公式（只记骨架，自行复述）→ 我的注记。
