# dev-plan-skill

> 一个给 AI 编程助手用的**开发方案规划技能**。让 AI 在你提出新需求时，先产出可评审的完整方案，而不是直接闷头写代码。

## 先看这里

| 你想做什么 | 去哪里 |
|---|---|
| **马上就用** | 打开 👉 [**SKILL.md**](./SKILL.md) ← 这就是技能本体，AI 只需要这一个文件 |
| 接进自己的 IDE / 让 AI 自动加载 | 看下面 [怎么让别的 AI IDE 读到它](#怎么让别的-ai-ide-读到它) |
| 先看输出长什么样 | [examples/example-output.md](examples/example-output.md) |
| 想改规则、加自己的检查项 | [references/](references/) 四个附件 |

## 它解决什么问题

把需求丢给 AI，最常见的结果是：上来就开始写代码，写到一半发现技术路线不对、范围失控、漏了关键约束，全部返工重来。

这个技能给 AI 一套固定的工作流和硬约束，让它在动手之前先回答六个问题：

| # | 输出 | 关键约束 |
|---|---|---|
| 1 | 可行性分析 | 必须给出「可行 / 有条件可行 / 不可行」明确结论，不许含糊 |
| 2 | 核心功能模块拆解 | 每个模块可回溯到需求，必须有 Out of Scope 清单，MVP ≤ 5 条 |
| 3 | 技术栈推荐 | 先定约束再选型，必须有对比表和被否候选的否决理由 |
| 4 | 项目目录结构 | 每行带职责注释，能回答「加功能改哪几个文件」 |
| 5 | 开发步骤 | 里程碑式，每步有可验证的验收标准，每个里程碑结束系统可运行 |
| 6 | 风险与难点 | 每个风险必须有**早期触发信号**和回退方案 |

内置两条铁律：**不写业务代码**、**不虚构版本号和性能数字**。

## 文件结构

```
.
├── SKILL.md                            # 核心技能正文（AI 读这个就够用）
├── README.md
├── references/
│   ├── plan-template.md                # 六段式输出模板，可直接套用
│   ├── tech-stack-matrix.md            # 按项目形态的技术栈候选与反过度设计检查
│   ├── risk-checklist.md               # 分类风险清单（7 类，含嵌入式专项）
│   └── embedded-adaptation.md          # 嵌入式 / MCU 项目专项规划检查项
└── examples/
    └── example-output.md               # 一份完整示例输出
```

**只想快速用起来，只需要 `SKILL.md`。** 其余是 AI 按需深读的参考文件。

---

## 怎么让别的 AI IDE 读到它

### 方式 A：直接丢链接（最快，零配置）

在任何 AI 对话里贴这段：

```
请先读取并遵循这份开发方案规划技能：
https://raw.githubusercontent.com/yz200202/dev-plan-skill/main/SKILL.md

然后按它的工作流，为下面这个需求制定完整开发方案：
<你的需求>
```

需要深度参考时再补一句：

```
如需模板和检查清单，另读：
https://raw.githubusercontent.com/yz200202/dev-plan-skill/main/references/plan-template.md
https://raw.githubusercontent.com/yz200202/dev-plan-skill/main/references/risk-checklist.md
```

> 如果 AI 的联网能力受限读不到 raw 链接，用方式 B 或 C。

### 方式 B：放进项目的规则文件（推荐，一次配置长期生效）

Clone 或下载本仓库，把内容并入项目根目录的规则文件，之后这个项目里每次对话 AI 都会自动带上：

| 工具 | 规则文件位置 |
|---|---|
| Cursor | `.cursor/rules/dev-plan.mdc`，或根目录 `AGENTS.md` |
| Claude Code | 根目录 `CLAUDE.md`，或 `~/.claude/skills/dev-plan/SKILL.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Windsurf | `.windsurf/rules/` 或 `.windsurfrules` |
| Cline / Roo Code | `.clinerules` |
| 其他 | 找该工具的「自定义规则 / 系统提示 / 项目指令」入口 |

**最简做法**：把 `SKILL.md` 全文复制进规则文件，末尾加一行参考文件路径说明。各工具规则文件的加载优先级以官方最新文档为准。

### 方式 C：装成本地技能（原生支持 Skills 的工具）

```bash
git clone https://github.com/yz200202/dev-plan-skill.git
mkdir -p ~/.claude/skills
cp -r dev-plan-skill ~/.claude/skills/dev-plan
```

WorkBuddy 用户放到 `~/.workbuddy/skills/dev-plan/`。

### 方式 D：作为知识库/附件上传

把 `SKILL.md` 和 `references/` 一起上传到支持知识库的 AI 产品（如各类企业版助手），在对话里 @ 引用即可。

---

## 分享给别人怎么发

仓库是公开的，任何人无需登录即可读取。但**发给「人」和发给「AI」的地址不一样**，发错了对方就用不起来。

| 对象 | 发什么 | 地址 |
|---|---|---|
| 同事 / 朋友（自己看、自己配） | 仓库主页 | `https://github.com/yz200202/dev-plan-skill` |
| AI 编程助手（让它自动遵守） | **raw 纯文本地址** | `https://raw.githubusercontent.com/yz200202/dev-plan-skill/main/SKILL.md` |

### 发给 AI 的现成话术（直接复制）

钉钉 / 微信 / 飞书里发给对方，让他粘进 AI 对话框：

```
请先读取并严格遵循这份开发方案规划技能：
https://raw.githubusercontent.com/yz200202/dev-plan-skill/main/SKILL.md

读完再按它的工作流，为下面这个需求制定完整开发方案（先规划，不要直接写代码）：
<把你的需求写在这里>
```

### 对方拉不到链接怎么办（国内网络最常见）

按顺序降级，三个方案都能用：

1. **换镜像地址**（jsDelivr 的 GitHub 缓存，国内通常可达）
   ```
   https://cdn.jsdelivr.net/gh/yz200202/dev-plan-skill@main/SKILL.md
   ```
2. **下载到本地**：仓库页 `Code` → `Download ZIP`，解压后把 `SKILL.md` 放进对方项目的 `.cursor/rules/`、`CLAUDE.md` 或 `.github/copilot-instructions.md`
3. **直接粘全文**：把 `SKILL.md` 内容整段粘贴进对话，说「按这份技能的要求制定开发方案」。几百行文本，聊天窗口塞得下

> 判断标准很简单：让 AI 复述一句技能里的规则（比如问「这个技能有几条铁律」），答得上来说明读到了，答不上就是没读到链接。

---

## 触发方式

配置好之后，出现这些说法时 AI 会自动启用：

- 「我有一个新需求，帮我制定开发方案」
- 「这个功能怎么做，先给我个技术方案」
- 「帮我评估一下这个项目能不能做」
- 「技术选型帮我看看用哪套」
- 「帮我把需求拆解一下」

也可以显式点名：`用 dev-plan 技能分析这个需求`。

## 适用范围

**适合**：新项目立项、新功能模块规划、技术选型、架构设计评审、需求拆解、工期评估。

**不适合**：调 bug、代码审查、单点技术问答、已定方案的实现执行。这些场景直接说需求即可，不需要方案层。

## 嵌入式项目

如果需求涉及 MCU、固件、硬件联调、量产，AI 会额外读取 `references/embedded-adaptation.md`，补充这些检查项：

- 资源预算表（Flash / RAM / 功耗，各项余量下限）
- 硬件版本 × 固件版本兼容矩阵
- 通信协议先行（帧格式、版本字段、幂等、超时出口）
- 可靠性（看门狗喂狗点、异常现场保留、掉电保护、弱网重连）
- 可观测性（日志分级、量产可开关、现场问题导出）
- OTA（分区、回滚、断点续传、灰度）与量产（烧录、产测、校准、SN 分发）
- 认证周期前置（SRRC / CE / FCC 等以月计）
- 每阶段 20%~30% 硬件联调缓冲、M0 必须是最小可运行验证板

## 修改与扩展

- 调整流程或铁律 → 改 `SKILL.md`
- 项目有固定技术栈 → 在 `references/tech-stack-matrix.md` 里把默认组合改成自己的
- 团队有专属检查项 → 加到 `references/risk-checklist.md`
- 想让它默认用某个模板 → 直接用 `references/plan-template.md` 覆盖输出格式

改完提交即可，所有引用本仓库的项目下次对话自动生效。

## License

MIT
