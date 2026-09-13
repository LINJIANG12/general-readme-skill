<a id="readme-top"></a>

# General README Skill

<p align="center">
  <b>以证据图为约束、单一结构、严格门禁的开源级 README 生成技能</b>
</p>

<p align="center">
  <a href="https://github.com/LINJIANG12/general-readme-skill"><img src="https://img.shields.io/badge/版本-3.1-3178C6?style=flat" alt="版本 3.1" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/许可证-MIT-yellow?style=flat" alt="许可证：MIT" /></a>
  <a href="https://github.com/KieranGao/general-readme-skill"><img src="https://img.shields.io/badge/改编自-KieranGao%2Fgeneral--readme--skill-8A2BE2?style=flat" alt="改编自 KieranGao/general-readme-skill" /></a>
</p>

<p align="center">
  <a href="install/codebuddy.md"><img src="https://img.shields.io/badge/CodeBuddy-支持-blue?style=flat" alt="CodeBuddy 支持" /></a>
  <a href="install/claude-code.md"><img src="https://img.shields.io/badge/Claude_Code-支持-D97706?style=flat" alt="Claude Code 支持" /></a>
  <a href="install/copilot.md"><img src="https://img.shields.io/badge/GitHub_Copilot-支持-black?style=flat" alt="GitHub Copilot 支持" /></a>
  <a href="install/cursor.md"><img src="https://img.shields.io/badge/Cursor-支持-gray?style=flat" alt="Cursor 支持" /></a>
</p>

<p align="center">
  简体中文 &nbsp;|&nbsp; <a href="README.en.md">English</a>
</p>

<p align="center">
  <a href="#概览">概览</a> &bull;
  <a href="#演示">演示</a> &bull;
  <a href="#快速开始">快速体验</a> &bull;
  <a href="#基本工作流程">工作流程</a> &bull;
  <a href="#使用方法">使用方法</a> &bull;
  <a href="#运行环境与依赖">运行环境</a> &bull;
  <a href="#贡献与社区">贡献</a> &bull;
  <a href="#许可证">许可证</a>
</p>

---

## 概览

这是一个面向 AI 编程助手设计的技能系统：指导助手全面理解当前代码仓库，并产出一份具备顶级开源项目质感的 `README.md`。

技能的核心机制在于**将「每条断言都要有出处」落实为刚性校验流程**。在撰写任何文档前，AI 必须通过三步发现式扫描深入分析代码，构建包含 `declared`（代码显式声明）与 `inferred`（逻辑合理推导）的证据图（Evidence Map）。没有静态代码支持的断言直接拦截或删除，杜绝凭空脑补。

章节不套用固定清单：按读者提问的顺序组织（身份 → 演示 → 上手 → 机制 → 细节 → 运维 → 社区），按项目实际需要选取与增删，未探测到数据的章节整节隐去，绝不写成占位。成稿后由七道自动化质量门禁（证据、结构、语气、视觉、链接、无障碍与国际化）做终审。主要语言占位 `README.md`，次要语言通过双向顶栏切换。

用户只需一条指令 `/readme`，AI 即可在几秒内自主完成代码深度理解、证据图构建、正文装配与质量审计。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 演示

技能生成的文档强调**展示真实效果**。在宿主 AI 编程助手中，直接输入 `/readme` 即可启动装配：

<div align="center">
  <img src="assets/intro.png" alt="General README Skill 运行演示" width="85%" />
</div>

<br />

### 真实生成效果参考

项目中随附了三种典型工程形态下生成的真实示例，可供直接查阅对比：

- **基础库与 SDK 范例**：[`examples/library-readme.md`](examples/library-readme.md) — 适合轻量包与 TypeScript 库，重点呈现清晰的 Quick Start、API 接口调用与无外部依赖特点。
- **命令行工具 CLI 范例**：[`examples/app-readme.md`](examples/app-readme.md) — 适合二进制与命令行工具，重点呈现子命令调用方法、参数标志验证与跨平台环境要求。
- **微服务与后端范例**：[`examples/oxyteamtasks-readme.md`](examples/oxyteamtasks-readme.md) — 适合多服务协作系统，重点呈现服务拓扑流程图、gRPC/REST 接口定义及多环境配置。

> [!TIP]
> **真实效果建议**：针对具体项目生成 README 时，若仓库中已有真实运行截图、录屏动图（GIF/WebP）或在线 Demo/Playground 链接，请在此处提供展示；未提供素材时，技能将在此保留标准的占位提示引导开发者补充。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 快速开始

选择你当前使用的编辑器或 AI 助手，执行对应的配置命令即可安装：

<details open>
<summary><b>1. CodeBuddy（推荐）</b></summary>

```bash
mkdir -p "$HOME/.codebuddy/skills/general-readme-skill"
cp SKILL.md README.md README.en.md LICENSE "$HOME/.codebuddy/skills/general-readme-skill/"
cp -r references/ install/ examples/ assets/ "$HOME/.codebuddy/skills/general-readme-skill/"
```
</details>

<details>
<summary><b>2. Claude Code</b></summary>

```bash
mkdir -p .claude/skills/general-readme-skill
cp SKILL.md .claude/skills/general-readme-skill/
cp -r references/ .claude/skills/general-readme-skill/
```
</details>

<details>
<summary><b>3. GitHub Copilot</b></summary>

```bash
mkdir -p .github
cp SKILL.md .github/copilot-instructions.md
cp -r references/ .github/references/
```
</details>

<details>
<summary><b>4. Cursor</b></summary>

```bash
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/general-readme.mdc
cp -r references/ .cursor/rules/references/
```
</details>

在编辑器内打开任意项目，向 AI 助手发送：
```text
/readme
```
技能将自动激活，依次执行扫描、证据提取、章节装配与门禁校验。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 基本工作流程

技能按照五阶段线性流完成文档生成，并由七道门禁实施闭环检验：

```mermaid
flowchart LR
    P0["0 配置"] --> P1["1 扫描"] --> P2["2 组合"] --> P3["3 校验"] --> P4["4 输出"]

    classDef step fill:#10B981,stroke:#059669,color:#fff,stroke-width:2px
    classDef gate fill:#F59E0B,stroke:#D97706,color:#fff,stroke-width:2px

    class P0,P1,P2,P4 step
    class P3 gate
```

### 阶段执行细节

- **0 配置（Configure）** — 解析主要语言（默认简体中文）、次要语言以及入口模式（新建或增量升级）。
- **1 扫描（Scan）** — 执行三步发现式扫描（文件树分层映射 &rarr; 清单及核心业务代码精读 &rarr; 细节按需样读），构建「断言 &rarr; 来源」证据图。敏感信息（密钥、私有主机名）在读取时自动脱敏。
- **2 组合（Compose）** — 从章节库中按需选取，并按读者提问顺序装配；无数据章节整节隐去，绝不产生空洞占位符。
- **3 校验（Verify）** — 运行 G1~G7 七道门禁，对任何未达标项执行修复或剔除。
- **4 输出（Output）** — 产出符合现代开源审美的 `README.md` 与多语言镜像文件。

<details>
<summary><b>点击展开：查看章节库与选取规则</b></summary>
<br />

按需选取，无需全写；项目特有的内容可新增自定义章节，命名以其内容为准。下表按读者提问顺序排列。

| # | 章节名称 | 何时选取 |
|---|---|---|
| 1 | **概览 / Overview** | 项目有明确的定位、背景或解决的核心痛点 |
| 2 | **演示 / Demo** | 必须展示真实效果（截图、录屏、动图或在线链接）；未提供时生成占位提示引导补充 |
| 3 | **快速开始 / Quick Start** | 检测到可运行的代码入口、启动指令或安装脚本 |
| 4 | **基本工作流程 / How It Works** | 源码中可提取出架构流向、数据流转或系统协作流程 |
| 5 | **使用方法 / Usage** | 存在公开 API、函数接口、导出的 SDK 或核心方法 |
| 6 | **运行环境与依赖 / Requirements** | 源码声明了明确的运行时版本、宿主平台或底层依赖 |
| 7 | **配置 / Configuration** | 检测到配置文件或环境变量模版（`*.config.*`, `.env.example`, `*.toml` 等） |
| 8 | **项目结构 / Project Structure** | 仓库包含多层源码目录且组织结构具备参考价值 |
| 9 | **API 定义 / API** | 检测到路由表、Schema 描述或导出服务接口定义 |
| 10 | **命令手册 / Commands** | 存在 CLI 工具入口（如 `bin/`, `cmd/`, `[[bin]]`） |
| 11 | **技术栈 / Tech Stack** | 依赖清单中有明确的核心依赖项 |
| 12 | **部署指南 / Deployment** | 检测到 Dockerfile、K8s 配置、CI/CD 脚本或云平台部署清单 |
| 13 | **路线图 / Roadmap** | 存在里程碑、成文规划或未竟功能清单 |
| 14 | **常见问题 / FAQ** | 存在 FAQ 文件或记录了重复出现的疑问与排错指南 |
| 15 | **贡献与社区 / Contributing & Community** | 存在 `CONTRIBUTING.md`、Issue 模板或社区指引 |
| 16 | **赞助与采纳 / Sponsors & Adopters** | 检测到 Funding 配置或企业/商业采纳名单 |
| 17 | **安全策略 / Security** | 存在 `SECURITY.md` 或项目涉及敏感数据、认证机制 |
| 18 | **引用 / Citation** | 存在 `CITATION.cff` 或项目关联已发表学术论文 |
| 19 | **许可证 / License** | 存在开源许可证文件 |

</details>

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 使用方法

### 触发指令与交互

在宿主助手聊天框中直接输入：
```text
/readme
```
支持的口令匹配还包括：`generate readme`、`write readme`、`更新README`、`生成项目文档`。

### 入口模式

- **新建模式（Create）**：用于项目缺少 `README.md`，或明确要求“重新生成文档”时，全量扫描并从零组装。
- **升级模式（Upgrade）**：当项目已有成型 README 时自动激活。AI 保持原文档中人工维护的手写段落，仅对陈旧断言进行增量替换。若原文档包含无法放入标准章节的独有内容（如迁移说明、详细设计背景），严禁静默删除，而是自动迁移至对应文档（如 `CONTRIBUTING.md`、`docs/`）或向用户汇报确认。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 运行环境与依赖

- **宿主环境**：CodeBuddy、Claude Code、GitHub Copilot、Cursor。
- **运行时环境**：零额外依赖。纯 Markdown + 标准 HTML 架构，不依赖任何构建工具或 CLI 二进制。
- **渲染要求**：支持标准 GitHub Flavored Markdown (GFM) 与原生 Mermaid 图表渲染。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 贡献与社区

欢迎参与维护与补充多语言词汇表！提交 Pull Request 前请确认：
- 严格遵循 [`references/writing-style.md`](references/writing-style.md) 的禁用词规则（杜绝夸张形容词与无据对比）。
- 新增或调整章节配方须同步修改 `references/sections-core.md`、`SKILL.md` 与双语切换栏。

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>

---

## 许可证

本项目基于 [MIT 许可证](LICENSE) 开源。

Copyright (c) 2026 OxyTheCrack / LINJIANG12. Derived from [KieranGao/general-readme-skill](https://github.com/KieranGao/general-readme-skill).

<p align="right"><a href="#readme-top">返回顶部 &uarr;</a></p>
