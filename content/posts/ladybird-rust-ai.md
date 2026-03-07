---
title: "Ladybird 两周移植 25000 行代码到 Rust,AI 辅助的教科书级案例"
date: 2026-02-24T19:05:00+08:00
cover:
 image: "https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=1200"
tweet: "Ladybird 浏览器两周把 25000 行 C++ 移植到 Rust,零回归.不是 AI 自动画的,是人用 Claude Code 和 Codex 一步步翻译的--测试套件才是真正的安全网.\n\nhttps://ladybird.org/posts/adopting-rust/\n\n#AI #Rust #浏览器"
tags: [AI, Rust, 浏览器, 代码移植]
---

Ladybird 浏览器最近干了件狠事--把 JavaScript 引擎从 C++ 移植到 Rust,25000 行代码,两周搞定.按传统方式这得折腾好几个月.

有意思的不是速度,是方法.Andreas Kling 没让 AI 自主写代码,而是用了"人机协作"模式:他决定移植顺序和代码风格,Claude Code 和 Codex 负责翻译.几百个小 prompt,一步步把 lexer,parser,AST,字节码生成器全搬过去.

关键是验证.他们要求 Rust 版和 C++ 版的输出必须字节级一致.靠着 test262 测试套件,最终零回归--每个 AST,每条字节码都跟原版一模一样.

这事儿说明两件事:一是 AI 真的能干重活,前提是你得有好的测试覆盖;二是 Rust 在浏览器领域的吸引力越来越大,内存安全不是闹着玩的.Ladybird 这波算是给"AI 辅助大型重构"打了个样.