---
title: "AI Agent 怀疑论者真香了：从质疑到用 Opus 4.5 写 Rust"
date: 2026-02-28T05:20:00+08:00
draft: false
tags: [AI Agent, Claude Opus 4.5, Codex 5.3, Rust, Max Woolf, AI 编程]
cover:
  image: "https://images.unsplash.com/photo-1555949963-aa79dcee981c"
  alt: "AI Agent 编程"
description: "Max Woolf 曾公开质疑 AI Agent。直到去年11月，Claude Opus 4.5 让他彻底改观。他用 Agent 写了 icon-to-image、miditui、ballin 等 Rust 项目，还开始移植 scikit-learn。性能提升最高达 100 倍。"
source: "https://minimaxir.com/2026/02/ai-agent-coding/"
---

# AI Agent 怀疑论者真香了：从质疑到用 Opus 4.5 写 Rust

去年5月，Max Woolf 写了篇文章。
标题是：《作为资深 LLM 用户，我其实不常用生成式 LLM》。

他质疑 AI Agent。
说它们不可预测、太贵、被过度吹捧。

他当时说：
"除非 LLM 进步到能解决我所有的顾虑。"
"否则我不会改变看法。"

结果11月，他真香了。

## 去年11月发生了什么？

Anthropic 在感恩节前发布了 Claude Opus 4.5。

Max 本来怀疑这是公司在假期发烂消息想蒙混过关。
结果他一测试，傻眼了。

Opus 4.5 比之前的 Sonnet 4.5 强太多了。
完全不是一个级别。

他先试了个简单任务。
写个 YouTube 频道数据抓取脚本。
Opus 4.5 一次搞定。
代码质量比他自己2021年写的还好。

他又试了个数据分析 Notebook。
指定"所有列都要分析"。
结果生成的 Notebook 非常详细。
连时间序列分析都自动加上了。

他又试了个 FastAPI web 应用。
要求用 HTMX 和 PicoCSS。
Opus 4.5 不仅功能完整。
还自己加了 YouTube 风格的缩略图设计。

Max 说：
"我试图给这个模型出难题。"
"都是我自己要花几个月才能完成的任务。"
"但 Opus 和 Codex 一直做对了。"

## 他用 Agent 写了什么？

### icon-to-image

把图标字体渲染成图片。
支持任意分辨率。
还加了抗锯齿的超采样。

用 Rust 写的。
通过 pyo3 提供 Python 接口。
比他2021年写的 Python 版本快得多。

代码已开源。
GitHub 上能找到。

### Word Clouds

他想在浏览器里生成词云。
用 Rust 编译成 WebAssembly。
这样浏览器里也能跑原生速度。

他用 Agent 写了前端界面。
要求用 shadcn/ui 风格。
Agent 搞定了。

还没发布。
他说需要再打磨一下设计。

### miditui

在终端里作曲和播放 MIDI。
是的，终端可以播放音频。
用 rodio crate 实现的。

Agent 还实现了完整的 DAW 功能。
可以作曲、编辑、播放。

已开源在 GitHub。

### ballin

某天喝了杯红酒。
他突发奇想。

能不能在终端里做物理模拟？
用 Braille 字符画高精度图形？
用 rapier 2D 物理引擎？

Agent 一次搞定。
能跑一万个小球。

已开源在 GitHub。

### rustlearn

最疯狂的项目来了。

他想把 Python 的 scikit-learn 移植到 Rust。
scikit-learn 是数据科学的黄金标准。
移植它？太狂了吧。

但他还是干了。

用 Agent 写了 UMAP、HDBSCAN、GBDT 等算法。
每个项目都用 8 步优化流程：

1. 实现功能，创建基准测试
2. 第二轮代码清理和优化
3. 扫描弱点，记录问题和解决方案
4. 优化到所有测试快 60% 以上
5. 用 CPU 特性再优化 60%
6. 加 Python 绑定
7. 创建 Python 基准测试对比
8. 确保输出和已知实现一致

他甚至让 Codex 和 Opus 轮流优化。
Codex 优化一遍。
Opus 再优化一遍。
性能能再提升 6 倍。

## 性能提升有多夸张？

他测了几个算法。

**UMAP：**
- 比 Rust 的 fast-umap 快 2-10 倍
- 比 Python 的 umap 快 9-30 倍

**HDBSCAN：**
- 比 Rust 的 hdbscan 快 23-100 倍
- 比 Python 的 hdbscan 快 3-10 倍

**GBDT：**
- 比 Python 的 xgboost 快 24-42 倍（训练）
- 比 Python 的 xgboost 快 1-5 倍（预测）

这些数字太疯狂了。
他自己都不敢信。

所以他发布了 nndex。
一个简单的向量检索库。
用来证明自己没在吹牛。

nndex 和 numpy 打平了。
numpy 可是用了 BLAS 优化的。
他又让 Opus 加了 BLAS 支持。
现在比 numpy 快 1-5 倍。

## 他的秘诀：AGENTS.md

他说 Agent 能成功，关键在 AGENTS.md。

这是一个配置文件。
告诉 Agent 怎么写代码。

比如：
- 用 uv 和 .venv，不用系统 Python
- 用 polars 不用 pandas
- API key 只能放 .env
- **绝对不要**用 emoji
- **必须**避免冗余注释

他给 Rust 也写了个 AGENTS.md。
规则包括：
- 不用 .clone() 来逃避生命周期
- 不用不必要的 .unwrap()
- 不写 unsafe 代码
- 每次改完要跑 clippy

他说：
"Agent 会严格遵守所有规则。"
"如果忘了加 AGENTS.md，代码质量立刻下降。"

这可能就是很多人用 Agent 效果不好的原因。

## 他的心态转变

他说最烦的是：

"你说 Opus 4.5 比几个月前的模型强一个数量级。"
"别人会觉得你在吹 AI。"
"但这是事实。"

他去年还是怀疑论者。
现在他说：
"我试图用复杂任务打破这个模型。"
"但 Opus 和 Codex 一直做对了。"

他现在每天写一小时代码。
因为 Agent 让编程变得有趣了。

## 写在最后

Max Woolf 的经历说明了一件事。

AI Agent 不是在吹牛。
是真的变强了。

去年11月是个转折点。
Opus 4.5 和 Codex 5.3 改变了游戏规则。

但要用好它们，需要：
- 写好 AGENTS.md
- 给明确的约束
- 用基准测试验证结果
- 让 Agent 迭代优化

这不是魔法。
是工具和方法论的组合。

Max 说他还在开发 rustlearn。
希望早点发布。

我们等着看。

---

**参考来源：**
- [Max Woolf: An AI agent coding skeptic tries AI agent coding, in excessive detail](https://minimaxir.com/2026/02/ai-agent-coding/)
