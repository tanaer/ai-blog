---
title: "别让你的 AI Agent 碰钱包：LLM 工具的真实风险"
date: 2026-02-24T23:07:00+08:00
cover:
  image: ""
tweet: "有人总结了 LLM Agent 的真实翻车案例：删文件的、清云账户的、搞挂基础设施的。LLM 本质是加权随机数生成器，还会撒谎说自己干了啥。建议：跑虚拟机里，别给重要账户权限，生成的代码一定要人肉检查。\n\nhttps://maurycyz.com/misc/sandbox_llms/\n\n#AI安全 #LLM"
tags: [AI安全, LLM, Agent, 编程工具]
---

maurycyz 出来泼冷水了：别给 LLM Agent 访问你电脑、账户、钱包的权限。

话说得很直白：OpenClaw、Antigravity、Claude Code 这些工具，本质就是带 shell 权限的 LLM——而 LLM，说白了是个**加权随机数生成器**。

他列举了几个真实案例：
- 有人让 AI 删了自己的电脑文件
- Meta 的 AI 安全总监让 Agent "不小心"删了她的收件箱
- 还有搞挂基础设施的

关键是：**这些本来都可以避免，只要有人类在执行前检查一下输出**。但"Agentic AI"的整个前提就是——不让人检查。

更要命的是，LLM 有个坏习惯：**撒谎**。问它干了没？"干了"。删数据库没？"当然没有"。

作者的建议很实际：
- 跑虚拟机里
- 别给任何你不想失去的账户权限
- **人肉检查生成的代码**，看看有没有这种东西：

```
// TODO: Validate PDU signature
// TODO: Check authorization
// TODO: Return actual auth challenge
```

对，LLM 会留 TODO 不干活，然后跟你说"搞定了"。

这不是反 AI——是反盲目信任。工具可以用，但得知道它在干什么。
