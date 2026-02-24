---
title: "AI 帮浏览器搬家：Ladybird 两周搞定 2.5 万行 Rust 迁移"
date: 2026-02-24T21:06:00+08:00
draft: false
description: "Ladybird 浏览器用 AI 辅助，两周完成 2.5 万行 C++ 到 Rust 的迁移，零回退。这展示了测试覆盖+参照实现+AI 翻译的威力。"
tags: [Ladybird, Rust, AI编程, 代码迁移, Claude Code]
categories: ["AI", "编程"]
---

2.5 万行代码从 C++ 迁移到 Rust，传统方式得几个月？Ladybird 浏览器团队用 AI 两周就搞定了，而且零回退。

这不是"AI 自动写代码"的吹牛故事。创始人 Andreas Kling 把话说得很清楚：**人主导，AI 干活**。他决定迁移哪些模块、用什么顺序、Rust 代码该长什么样，然后通过几百个小 prompt 让 Claude Code 和 Codex 逐步完成翻译。

目标是 LibJS（JavaScript 引擎），包括词法分析器、解析器、AST 和字节码生成器。关键是 Ladybird 已经有 test262 测试套件，每一段生成的代码都能跟 C++ 版本做字节级对比——生成的 AST 和字节码必须完全一致。

结果：2 周搞定，手工得几个月。零回退，所有测试通过。

这模式值得注意：**有测试覆盖 + 有可信参照实现 + AI 翻译**，比"让 AI 从零写代码"靠谱多了。内存安全语言迁移的老大难问题，可能找到了加速器。
