<div align="center">

<a name="readme-top"></a>

<h1>General README Skill</h1>

<p>
  <strong>让 AI 读懂你的仓库，再写出一份每条断言都有出处的 README</strong>
  <br />
  <em>纯 Markdown · 证据图约束 · 零额外依赖 · CodeBuddy / Claude Code / Copilot / Cursor</em>
</p>

<p>
  <a href="#快速开始"><img src="https://img.shields.io/badge/快速开始-2E7D32?style=for-the-badge" alt="快速开始" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/许可证-MIT-2E7D32?style=for-the-badge" alt="许可证：MIT" /></a>
</p>

<p>
  <a href="https://github.com/LINJIANG12/general-readme-skill"><img src="https://img.shields.io/badge/版本-3.1-3178C6?style=flat" alt="版本 3.1" /></a>
  <a href="https://github.com/KieranGao/general-readme-skill"><img src="https://img.shields.io/badge/改编自-KieranGao-7C3AED?style=flat" alt="改编自 KieranGao/general-readme-skill" /></a>
</p>

<p>
  <strong>简体中文</strong> ·
  <a href="README.en.md">English</a>
</p>

</div>

## 目录

- [概览](#概览)
- [演示](#演示)
- [快速开始](#快速开始)
- [基本工作流程](#基本工作流程)
- [使用方法](#使用方法)
- [运行环境与依赖](#运行环境与依赖)
- [项目结构](#项目结构)
- [贡献与社区](#贡献与社区)
- [许可证](#许可证)

## 概览

General README Skill 是一个面向 AI 编程助手的技能包：它先读懂仓库，再写出一份可以直接交付的 `README.md`。

它要解决的是 AI 写文档时最常见的失败方式——**编造**。写出不存在的命令、凭空的版本号、没有的配置项，这类内容在人工复核时很难逐条发现。技能把这层风险前置为流程约束：撰写之前必须完成三步发现式扫描，建立「断言 → 来源」的证据图，来源分 `declared`（清单或代码中明确声明）与 `inferred`（从目录结构推导）两级。没有来源的断言不会改用模糊措辞，而是直接从稿子里删除。

章节不套固定清单，按读者提问的顺序选取：身份 → 演示 → 上手 → 机制 → 细节 → 社区。探测不到数据的章节整节隐去，不写"暂无"也不留占位。成稿后由七道门禁（证据、结构、语气、视觉、链接、无障碍、国际化）终审，未达标项就地修复或删除。你要做的只是在项目里输入一条指令。

## 演示

技能在宿主助手中被指令激活后，直接扫描当前仓库并装配文档：

<div align="center">
  <img src="assets/intro.png" alt="在 CodeBuddy 中输入 /readme 后，技能扫描仓库并输出 README" width="85%" />
</div>

> [!TIP]
> 为具体项目生成时，若仓库已有运行截图、录屏动图或在线 Demo 链接，技能会在本节直接引用；检测不到素材时保留占位提示，引导维护者补充，而不是虚构一张效果图。

### 生成效果范例

仓库随附三种工程形态下的完整产物，可对照查看不同形态的取舍：

- **库与 SDK** — [`examples/library-readme.md`](examples/library-readme.md)：轻量包的安装、接口调用与零依赖说明
- **命令行工具** — [`examples/app-readme.md`](examples/app-readme.md)：子命令调用、参数标志验证与跨平台要求
- **微服务与后端** — [`examples/oxyteamtasks-readme.md`](examples/oxyteamtasks-readme.md)：服务拓扑图、gRPC/REST 接口与多环境配置

## 快速开始

安装是唯一的准备步骤。技能由纯 Markdown 与 HTML 组成，不需要构建工具或运行时依赖。

### 安装到 CodeBuddy

```bash
mkdir -p "$HOME/.codebuddy/skills/general-readme-skill"
cp SKILL.md README.md README.en.md LICENSE "$HOME/.codebuddy/skills/general-readme-skill/"
cp -r references/ install/ examples/ assets/ "$HOME/.codebuddy/skills/general-readme-skill/"
```

### 安装到 Claude Code

```bash
mkdir -p .claude/skills/general-readme-skill
cp SKILL.md .claude/skills/general-readme-skill/
cp -r references/ .claude/skills/general-readme-skill/
```

### 安装到 GitHub Copilot

```bash
mkdir -p .github
cp SKILL.md .github/copilot-instructions.md
cp -r references/ .github/references/
```

### 安装到 Cursor

```bash
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/general-readme.mdc
cp -r references/ .cursor/rules/references/
```

### 调用

在任意项目中，向助手输入：

```text
/readme
```

技能随即执行扫描、证据提取、章节装配与门禁校验。各宿主的差异说明见 [`install/`](install)。

## 基本工作流程

技能按五个阶段线性推进，全部产物都要通过七道门禁的闭环检验：

```mermaid
flowchart LR
    P0["0 配置"] --> P1["1 扫描"] --> P2["2 组合"] --> P3["3 校验"] --> P4["4 输出"]

    classDef step fill:#F8FAFC,stroke:#475569,color:#334155,stroke-width:1.5px
    classDef gate fill:#FFFBEB,stroke:#D97706,color:#78350F,stroke-width:1.5px
    classDef focal fill:#1D4ED8,stroke:#1E40AF,color:#FFFFFF,stroke-width:1.5px

    class P0,P1,P2 step
    class P3 gate
    class P4 focal
```

### 各阶段产出

- **0 配置** — 解析主要语言（默认简体中文）、次要语言与入口模式，并确认所用参考文件存在且可读。
- **1 扫描** — 三步发现式扫描：文件树分层映射，再精读清单、入口与核心业务代码，细节按需样读。产出「断言 → 来源」证据图，读取时对密钥与私有主机名脱敏。
- **2 组合** — 按读者提问顺序选取章节并装配，逐节选择最易读的形式；Hero 与其他 HTML 区块直接以 HTML 撰写。
- **3 校验** — 运行 G1 至 G7 七道门禁，可修复项就地修复，无法修复的断言直接删除，同一门禁最多迭代三次。
- **4 输出** — 写出主要语言文件与各语言镜像文件，并统一换行、编码与空白。

<details>
<summary><b>展开：章节库与选取条件</b></summary>

<br />

章节按需选取，不要求写全；项目特有的内容可新增自定义章节，以内容而非位置命名。下表按读者提问顺序排列。

| # | 章节 | 何时选取 |
|---|---|---|
| 1 | **概览 / Overview** | 项目有明确的定位、背景或要解决的核心问题 |
| 2 | **演示 / Demo** | 需要展示真实效果；无素材时输出占位提示而非虚构图 |
| 3 | **快速开始 / Quick Start** | 检测到可运行入口、启动指令或安装脚本 |
| 4 | **基本工作流程 / How It Works** | 源码中可提取出流程、架构或组件协作关系 |
| 5 | **使用方法 / Usage** | 存在公开 API、导出接口或核心调用方式 |
| 6 | **运行环境与依赖 / Requirements** | 声明了运行时版本、宿主平台或底层依赖 |
| 7 | **配置 / Configuration** | 检测到配置文件或环境变量模版（`*.config.*`、`.env.example`、`*.toml`） |
| 8 | **项目结构 / Project Structure** | 存在多个顶层源码目录，且组织结构具备参考价值 |
| 9 | **API 定义 / API** | 检测到路由表、Schema 或导出的服务接口定义 |
| 10 | **命令手册 / Commands** | 存在 CLI 入口，如 `bin/`、`cmd/`、`[[bin]]` |
| 11 | **技术栈 / Tech Stack** | 依赖清单中声明了核心依赖 |
| 12 | **部署指南 / Deployment** | 检测到 Dockerfile、compose、CI 配置或平台清单 |
| 13 | **路线图 / Roadmap** | 存在里程碑、成文规划或未竟功能清单 |
| 14 | **常见问题 / FAQ** | 存在 FAQ 文档，或记录了反复出现的问题 |
| 15 | **贡献与社区 / Contributing & Community** | 存在贡献指南、Issue 模板或社区入口 |
| 16 | **赞助与采纳 / Sponsors & Adopters** | 检测到资助配置或成文采纳者名单 |
| 17 | **安全策略 / Security** | 存在 `SECURITY.md`，或项目涉及鉴权、网络与用户数据 |
| 18 | **引用 / Citation** | 存在 `CITATION.cff`，或项目关联已发表论文 |
| 19 | **许可证 / License** | 存在许可证文件 |

</details>

## 使用方法

在宿主助手的聊天框中输入指令即可启动：

```text
/readme
```

以下表述同样触发技能：`generate readme`、`write readme`、`更新README`、`生成项目文档`。

### 入口模式

技能按仓库状态自动判定模式，不需要手动切换。

**新建模式**用于项目尚无 `README.md`，或你明确要求重新生成。此时全量扫描，每个章节从证据图重新撰写。

**升级模式**用于已有成型 README 的项目。技能先建立内容台账，逐条记录原文档的章节与事实，再合并：人工维护的段落与未标记的手写章节原地保留，自动区域重新生成。无法放入标准章节的内容不会被静默删除，而是迁移到 `CONTRIBUTING.md`、`MIGRATION.md`、`docs/` 等文件并回链，或向你确认去向。

## 运行环境与依赖

- **宿主** — CodeBuddy、Claude Code、GitHub Copilot、Cursor 之一。
- **运行时** — 无。技能为纯 Markdown 与标准 HTML，不依赖构建工具或 CLI 二进制。
- **渲染** — 需要支持 GitHub Flavored Markdown；流程图依赖宿主的 Mermaid 渲染能力。
- **加载格式** — 以 `SKILL.md` 作为入口清单，规则与模板按需从 `references/` 加载。

## 项目结构

```text
general-readme-skill/
├── SKILL.md          # 入口：设计原则、章节库、门禁定义与参考文件路由
├── references/       # 16 个参考文件：章节配方、模板与规则，按需加载
├── install/          # 四个宿主各自的安装说明
├── examples/         # 三种工程形态下的完整生成范例
├── assets/           # 文档图片素材
└── LICENSE
```

`SKILL.md` 只承担路由职责，具体模板与规则分散在 `references/` 下，由当前任务决定加载哪几个文件，避免一次性占用上下文。

## 贡献与社区

欢迎补充多语言词汇表、修正规则或新增范例。

- 遵循 [`references/writing-style.md`](references/writing-style.md) 的禁用词表撰写文案，排除夸张形容词与无据对比。
- 同步更新章节配方：`references/sections-core.md`、`references/sections-reference.md` 与 `SKILL.md` 中的章节库保持一致。
- 新增图表时，填充色、描边色与文字色取自 [`references/diagram-templates.md`](references/diagram-templates.md) 的成对取色表。
- 新增次要语言时，确保所有语言文件的顶栏切换双向可达。

## 许可证

本项目基于 [MIT 许可证](LICENSE) 发布。

Copyright (c) 2026 OxyTheCrack
Copyright (c) 2026 LINJIANG12

本仓库改编自 [KieranGao/general-readme-skill](https://github.com/KieranGao/general-readme-skill)。

<div align="right">

[![返回顶部][badge-top]](#readme-top)

</div>

<!-- LINKS & IMAGES -->

[badge-top]: https://img.shields.io/badge/-返回顶部-151515?style=flat
