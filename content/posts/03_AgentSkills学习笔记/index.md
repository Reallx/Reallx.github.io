---
title: "Agent Skills 学习笔记"
date: 2026-02-28
author: "薛路"
summary: "Agent Skills的学习笔记"
description: "学习AI Agent Skills的笔记"
tags: ["AI", "Agent","Skills"]
showTOC: true
disableAnchoredHeadings: false 
editPost:
    URL: "https://www.bilibili.com/video/BV1GXzaByEEo"
    Text: "参考视频"
---

---
从 MCP 到 Skills，Agent出现了新的标准实践。从2025年10月 Anthropic 开始，随后，Cursor, Codex, Opencode 开始支持。再后来社区涌现大量开源 Skills。Skills （以下称为Skills）成为目前 AI Agent 的技术插件，相较于 MCP 能够用较少的 Token 解决相同的问题。这是我的学习笔记。在学习后，我尝试搭建了Excel Data Analysis Skills系统，马上将在 Project 板块中更新。

## 一、Skills 工作原理
在传统的 AI 聊天模式中，通过 AI 原本学过什么（训练数据）和临时告诉的内容（提示词、上下文）得到输出。Skills 是 **Agent 模块化的能力插件**以我使用的 Codex 为例。Codex 是超级大脑，Skills是一个外接工具箱，里面包含工具和使用的详细说明书。大脑不需要理解具体有哪些工具，只需要在人调用的时候查阅说明书，拿出工具直接使用即可。

## 二、Skill的组成和使用方式
Skills 存放在每个项目的一个固定的文件夹里，每个 Skill 都是一个文件夹，组成如下
```text
~/project/.claude/skills/my_skill

❗SKILL.md --> 这个 Skill 的详细说明书，告诉 AI 怎么使用这个 Skill
(optional) reference 
(optional) scripts --> Python/Bash 代码能力
(optional) assets --> 图片、模板等
```
在 Agent 执行目录里放了该 Skill 文件夹，在和 Agent 对话时，它就可以自动根据需求选择 Skill 使用。

## 三、Skills的优点
直接对话、系统提示词、封装的Workflow、Rules，这些方式本质上都是把提示词放在不同的位置，每次对话都会带上所有内容，在真实业务场景中，一个大脑会配备很多技能，这就导致每次对话都会有很大的上下文消耗，注意力也会被分散。
Skills 的核心机制在于**渐进式披露**，按需加载，用多少拿多少。
```text
Layer1: 元数据层 --> 仅加载 Skills 的名字和 Description（YAML 头）让 Agent 知道自己会什么
Layer2：指令层 --> 加载 SKILL.md，当匹配用户需求时才会加入上下文
Layer3：执行层 --> 加载 scripts，assets，reference
```
Agent 会根据 SKILL.md 中的指引执行操作，而执行层的内容不会被 Agent 读取，不会占用Token。

## 四、参考资料
[Agent Skills Marketplace](https://skillsmp.com/zh)：Manus 的Skills 开源社区

[B站学习视频](https://www.bilibili.com/video/BV1GXzaByEEo)




