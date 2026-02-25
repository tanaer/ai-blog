---
title: "2周迁移2.5万行代码：Ladybird用AI把C++变成Rust，6.5万测试零回归"
date: 2026-02-25T13:05:00+08:00
draft: false
tags: ["AI", "Rust", "浏览器", "代码迁移", "Claude Code", "Codex"]
categories: ["技术热点"]
cover:
  image: "https://opengraph.githubassets.com/ladybird-rust-migration"
  alt: "Ladybird 浏览器 Rust 迁移"
  caption: "Ladybird 浏览器 - 新一代开源浏览器项目"
---

如果你曾经在周末试图把一个几千行的项目从一种语言迁移到另一种，你就知道那是什么感觉——痛苦、漫长、充满 bug。

那如果告诉你，有人用 **2 周** 完成了 **25,000 行** 代码的迁移，而且 **65,359 个测试全部通过，零回归**？

这不是科幻，这是 Ladybird 浏览器刚刚干完的事。

## 发生了什么？

Ladybird 是一个从零开始的开源浏览器项目，由 SerenityOS 作者 Andreas Kling 发起。他们一直在寻找一种内存安全的语言来替代 C++。之前试过 Swift，但 C++ 互操作性不够好，而且平台支持有限。

**这次他们选了 Rust。**

但真正让人震惊的不是 "又一个项目用 Rust"，而是他们迁移的方式——**用 AI 辅助，但完全人工主导**。

## 他们是怎么做到的？

Kling 选择了 LibJS（Ladybird 的 JavaScript 引擎）作为第一个迁移目标。具体是 lexer、parser、AST 和 bytecode generator——这些模块相对独立，而且有 test262 这样的完整测试覆盖。

工具选择：**Claude Code + OpenAI Codex**。

但重点来了——Kling 强调：

> "This was human-directed, not autonomous code generation. I decided what to port, in what order, and what the Rust code should look like. It was hundreds of small prompts, steering the agents where things needed to go."

这不是 "AI 你给我把代码翻译一下"，而是 "AI 帮我写这段，好，下一段，注意这个细节，再来"——**数百个小 prompt，精准控制**。

### 关键创新：字节级验证

这是整个项目最聪明的地方：

> "The requirement from the start was byte-for-byte identical output from both pipelines."

C++ 和 Rust 两套管道同时运行，每一段 JavaScript 产生的 AST 和 bytecode 必须**完全一致**。任何差异立即暴露，不用猜 bug 在哪边。

这解决了传统重写的最大问题：很多人在迁移时想顺便"改进"代码，结果新旧行为不一致，追 bug 追到怀疑人生。

## 成果有多硬核？

| 指标 | 数据 |
|------|------|
| 迁移代码量 | 25,000 行 Rust |
| 耗时 | 2 周 |
| 手工预估 | 数月 |
| test262 测试 | 52,898 通过，0 回归 |
| Ladybird 内部测试 | 12,461 通过，0 回归 |
| 性能回归 | 0 |

Kling 还做了 "lockstep 模式"——用迁移后的浏览器实际冲浪，两套管道同时跑，验证每一帧的输出。

这质量，比我见过的大多数企业级软件都硬。

## 代码是 "翻译腔" Rust，但这不重要

Kling 很诚实：

> "If you look at the code, you'll notice it has a strong 'translated from C++' vibe. That's because it is translated from C++."

他们故意让 Rust 代码模仿 C++ 的寄存器分配模式，确保字节级一致。地道？不地道。能跑？绝对能跑。内存安全？Rust 编译器保证。

**先能跑，再优化**——这才是务实的工程思维。

## 这意味着什么？

### 1. AI 不是取代程序员，是加速程序员

HN 上有人问：这算不算 AI 抢饭碗？

恰恰相反。Kling 的工作证明：**AI 是杠杆，不是替代品**。

没有 AI，这活要干几个月。有 AI，两周搞定。但关键是——**每一行代码的决策都是人做的**。AI 只是帮你把意图变成代码，不用一个字符一个字符敲。

### 2. "字节级验证" 应该成为迁移标配

这个方法论值得所有做语言迁移的团队学习：

1. **先定义一致性标准**（字节级输出相同）
2. **并行运行新旧管道**
3. **diff 驱动调试**

比 "我重写了一遍，测试好像都过了" 靠谱一万倍。

### 3. Rust 在系统编程的胜利又添一城

Firefox 在用，Chromium 在用，现在 Ladybird 也加入了。内存安全不再是一个口号，而是正在发生的现实。

## 最后一点想法

Ladybird 的这次迁移让我想起一个观点：**好的工具不是让你少干活，而是让你在同样时间内干更多有价值的事**。

2 周迁移 2.5 万行代码，零回归。这不是魔法，这是 AI + 严谨工程方法的化学反应。

下次有人问你 "AI 能不能写代码"，把这个案例甩给他——然后补一句：**能，但得有人告诉它写什么、怎么写、写得对不对**。

---

**参考来源**：
- [Ladybird 官方博客：Adopting Rust](https://ladybird.org/posts/adopting-rust/)
- [Hacker News 讨论](https://news.ycombinator.com/item?id=47120899) - 1251 points, 690 comments
