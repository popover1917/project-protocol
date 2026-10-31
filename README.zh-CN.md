# Project Protocol

[English](README.md) · [技能入口](skills/project-protocol/SKILL.md) · 当前版本 **0.5**

让工程工作跨 Agent、会话和时间继续的轻量 **Agent Skill**。只保存恢复工作所需的项目背景、当前工作与实际交接结果，支持工程接续、上下文恢复和多 Agent 交接。

普通查询和局部小修改无需创建协议记录。

## 安装

使用 [Skills CLI](https://github.com/vercel-labs/skills) 为 Codex 全局安装：

```bash
npx skills add popover1917/project-protocol --skill project-protocol -a codex -g
```

去掉 `-g` 可安装到当前项目；使用 `--list` 可先查看仓库提供的技能。其他 Agent 可通过 `-a` 选择。

也可以在 Codex 中直接请求内置技能安装器：

```text
$skill-installer install https://github.com/popover1917/project-protocol/tree/main/skills/project-protocol
```

手动安装时，克隆本仓库，仅将 `skills/project-protocol/` 整个文件夹复制到 Agent 的技能目录，保留名称 `project-protocol` 和内部所有子目录。

安装技能不会初始化或迁移已有项目，需要时另行明确提出。

## 使用

可以直接提出：

```text
使用 project-protocol，为当前仓库初始化可持续接续的项目状态。
```

```text
使用 project-protocol，读取当前项目文件并继续 TH-001。
```

```text
使用 project-protocol，为另一位 Agent 准备执行交接，明确 Completion 保存位置。
```

协议只保留四个概念：

| 概念 | 用途 |
| --- | --- |
| Project | 稳定的项目背景与身份 |
| Thread | 当前目标、实际位置、约束、下一步与结束条件 |
| Handoff | 实际转交给另一上下文的任务 |
| Completion | 执行者的结果、检查、限制与剩余工作 |

连续性记录保存在 `.project/`。代码、文档和工程结果保留在各自维护的位置。已结束 Thread 连同交接一起移入 `.project/archive/`；协调者维护共享当前状态，各执行者保存自己的 Completion。

创建记录时按需查看[格式与模板](skills/project-protocol/references/format.md)。仅在采用 Codex–WorkBuddy 周期协作时读取 [WorkBuddy 参考](skills/project-protocol/references/workbuddy.md)；该参考不安装或配置 WorkBuddy。

## 目录与验证范围

可安装的技能位于 `skills/project-protocol/`，共九个文件：`SKILL.md`、Codex 元数据、两个按需参考和五个模板。根目录说明不属于安装必需文件。

本次公开发布保留 0.5 技能内容。检查范围限于文件保存读回与发行复制完整性，未运行行为测试、安装演练或 Fresh Agent 验证。

## 检索

可使用 `project-protocol`、`Agent Skill`、`Codex`、`project continuity`、`agent handoff` 等关键词检索。公开仓库不等于已被第三方技能目录收录；[skills.sh FAQ](https://www.skills.sh/docs/faq)说明了基于安装使用统计的发现机制。

目录与安装方式参考 [Anthropic 技能仓库](https://github.com/anthropics/skills)及 [Vercel Skills CLI 文档](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。

## 许可

本次公开发布暂不附带许可证文件。
