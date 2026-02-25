---
title: "Mercury 2 发布：首个商用 Diffusion LLM，推理速度碾压传统模型"
date: 2026-02-25T14:05:00+08:00
draft: false
cover:
  image: ""
  alt: "Mercury 2 Diffusion LLM"
  caption: "Inception Labs"
tags: ["LLM", "Diffusion", "AI推理", "Inception", "速度突破"]
categories: ["AI技术"]
---

## 打字员 vs 编辑

传统大模型生成文本，就像打字员——一个字一个字敲，手速再快也有天花板。

Mercury 2 不一样。它像编辑——拿到初稿，然后整篇整篇地改，几轮下来就成型了。

**结果？每秒 1,009 个 token。**

这是 Inception Labs 今天发布的 Mercury 2，全球首个商用的 diffusion 大语言模型。比 GPT-5.2 至少快 2 倍，比 Claude 4.5 Haiku 快 5 倍，成本却只有四分之一。

## Diffusion 架构：从图像搬到文本

你可能用过 Stable Diffusion 或 DALL-E 生成图片。它们用的就是 diffusion——从噪声开始，一步步"去噪"，最后得到清晰的图像。

Mercury 2 把这个思路搬到了文本。

传统 LLM（GPT、Claude、Gemini）都是 autoregressive（自回归）：生成第一个词，等它出来，再生成第二个……永远在等。GPU 再快也没用，瓶颈是"必须按顺序"。

Diffusion 不一样。它从一堆"噪声文本"开始，并行地 refining（精炼），几轮之后就是完整回答。**并行处理 vs 串行等待，这是架构层面的碾压。**

创始人 Stefano Ermon 是斯坦福计算机教授，正是他把 diffusion 技术带进 Stable Diffusion 和 DALL-E 的男人。现在他赌的是：**同样的 trick 对文本也管用。**

## 为什么速度这么重要？

你可能觉得：快几秒有什么大不了？

对于聊天机器人，确实。但对于：

- **Agent 工作流**：一个任务可能要调 30 次模型，每次慢 1 秒，整体就慢 30 秒
- **语音 AI**：用户说话后等 2 秒才回复，对话感直接崩
- **代码补全**：打字停顿等建议，思路断了

Zed 编辑器联合创始人 Max Brunsfeld 的原话：

> "快到感觉是思考的一部分，而不是你要等的东西。"

Skyvern CTO Suchintan Singh 说得更直接：

> "至少比 GPT-5.2 快两倍。"

## 价格屠夫

$0.25/百万 input tokens，$0.75/百万 output tokens。

对比一下：
- Claude 4.5 Haiku：$0.80/$4.00
- GPT-5.2：$2.50/$10.00

**同样预算，能跑 4-10 倍的量。**

Inception 的算盘很清楚：不是要干掉 frontier reasoning models（Opus 4.6 那种），而是抢占"高吞吐、低延迟"的生产场景——客服路由、文档分类、实时搜索摘要。这些场景之前用不起大模型，现在可以了。

## 行业在跟进

Inception 不是孤军奋战。

- Google 的 Gemini Diffusion 已展示商业级能力
- Together AI 本月发布的 CDLM 技术，在代码 benchmark 上把延迟砍了 14.5 倍

一年前，Inception 是唯一做商用 diffusion LLM 的。现在 Google、Together AI 都在追。**这说明方向对了。**

## 对开发者的启示

1. **API 兼容 OpenAI**：直接替换，不用改代码
2. **128K context + tool use + JSON mode**：生产该有的都有
3. **跑在普通 NVIDIA GPU 上**：不需要定制芯片

如果你在做 agent、语音、或任何"延迟敏感"的 AI 产品，Mercury 2 值得一试。

**速度不是锦上添花，是决定产品能不能用的生死线。**

---

*参考来源：Inception Labs 官方博客、Bloomberg 报道、Implicator.ai 分析*
