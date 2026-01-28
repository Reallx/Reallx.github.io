---
title: "Agent Skills 学习笔记"
date: 2026-01-27
author: "薛路"
summary: "这是一篇学习Agent skills的文章，包括skills的组成、使用和热门skills"
description: "这是一篇学习Agent skills的文章"
tags: ["skills", "codex"]
editPost:
    URL: "https://b23.tv/gjHwZrU"
    Text: "视频链接"
showToc: true
disableAnchoredHeadings: false 
---

> 本文总结了 Agent skills 的组成、使用方法、和近期热门的skills

---

Agent skills 在2025年由 Anthropic 发布，随后 Cursor、Codex、Opencode 开始支持，再后来社区开始涌进大量开源 skills，现在大家默认 skills 成为 Agent 领域的实践标准。
## 一、skills的工作原理

传统的 AI 聊天模式：
```text
 AI 原本学过什么（训练数据）--> 临时告诉他什么（提示词、工具、记忆）
 每次干活都要重新教一遍
```
Agent skills 是模块化的能力插件，Claude 当做超级大脑，Agent skills 是一个外接工具箱，工具箱中不仅包含了工具本身，还包含了详细的使用说明书。大脑不需要理解所有工具的用法，只要在需要的时候调用工具直接使用即可。

每个skills都是一个文件夹，放在一个固定的位置。组成如下：
```
~/project/.claude/skils/my-skills

SKILL.md    #最重要的部分--自然语言写的SOP提示词，告诉AI怎么干
reference/  #更详细的参考文档
scripts/    #Python/bash 代码能力
assets/     #图片、模版等

```
SKILL.md的写法如下（以文章润色skill为例）：
```
---
name: text-polisher
description: 用来把用户的一段话改写得更礼貌、更通顺。遇到这类需求时使用本skill，例如用户说"帮忙把下面这段话润色一下、改的礼貌一点，写成正式邮件通知"等
---
## 核心目标
   ……
## 执行流程
   ……
## 注意事项
   ……
```

