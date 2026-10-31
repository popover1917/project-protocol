# Project Protocol

[简体中文](README.zh-CN.md) · [Skill instructions](skills/project-protocol/SKILL.md) · Version **0.5**

An **Agent Skill** for keeping engineering work recoverable across agents and sessions. Maintain a small amount of project context, resume current work, and exchange execution handoffs with durable results.

Use it for project continuity, session recovery, agent handoffs, and ongoing engineering work. Ordinary questions and bounded edits need no protocol records.

## Install

With the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add popover1917/project-protocol --skill project-protocol -a codex -g
```

Omit `-g` for a project installation. Use `--list` to inspect available skills before installing. The CLI supports other agents; select your agent with `-a`.

In Codex, you can instead ask its built-in skill installer:

```text
$skill-installer install https://github.com/popover1917/project-protocol/tree/main/skills/project-protocol
```

For manual installation, clone this repository and copy **only** `skills/project-protocol/` into your agent's skills directory as `project-protocol/`. Keep its `references/`, `templates/`, and `agents/` directories together with `SKILL.md`.

Installing the skill does not initialize or migrate existing projects. Ask the agent to do that explicitly when needed.

## Use

Example requests:

```text
Use project-protocol to initialize durable project state for this repository.
```

```text
Use project-protocol to continue TH-001 from the current project files.
```

```text
Use project-protocol to prepare a handoff for another agent and specify where to return Completion.
```

The skill keeps four concepts:

| Concept | Purpose |
| --- | --- |
| Project | Stable background and project identity |
| Thread | Current goal, actual position, constraints, next step, and finish conditions |
| Handoff | An actual assignment transferred to another context |
| Completion | The executor's results, checks, limits, and remaining work |

Continuity records live under `.project/`. Engineering code, documents, and results stay in their normal locations. Ended Threads move together with their handoffs to `.project/archive/`. One coordinator maintains shared current state; executors return their own Completion.

See the [file format and templates](skills/project-protocol/references/format.md) when creating records. Read the [optional WorkBuddy reference](skills/project-protocol/references/workbuddy.md) only for Codex–WorkBuddy scheduled collaboration; it does not install or configure WorkBuddy.

## Repository layout

```text
skills/project-protocol/
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── format.md
│   └── workbuddy.md
└── templates/
    ├── AGENTS.bootstrap.md
    ├── COMPLETION.md
    ├── HANDOFF.md
    ├── PROJECT.md
    └── THREAD.md
```

The installable skill contains nine files. It uses the `SKILL.md` Agent Skills format and includes Codex UI metadata. This repository publishes the 0.5 skill and installation documentation. Publication checks cover file readback and distribution integrity; behavioral tests, installation trials, and fresh-agent validation have not been run.

## Discovery

Find this repository by `project-protocol`, `Agent Skill`, `Codex`, `project continuity`, or `agent handoff`. Publishing a repository does not guarantee immediate indexing by external skill directories. [skills.sh](https://www.skills.sh/docs/faq) documents its installation-based discovery process.

Directory and installation conventions follow the maintained [Anthropic Skills examples](https://github.com/anthropics/skills) and [Vercel Skills CLI documentation](https://github.com/vercel-labs/skills/blob/main/docs/commands.md).

## License

No license file is included in this release.
