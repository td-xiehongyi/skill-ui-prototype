# UI Prototype

一个面向 Codex 的界面原型与 UI 对照验收 Skill。它把页面目标转成可查看、可操作、可评审的 HTML 原型，并为后续实现保留清晰的交互、状态、版本和验收依据。

## 适用场景

- 想在正式前端开发前先做一个独立 HTML 原型
- 需要比较两种页面布局或关键交互顺序
- 需要根据截图、设计稿或已确认版本调整原型
- 需要把实际运行界面与已确认的原型进行对照验收

不适用于普通文案修改、纯后端任务，或没有页面和交互问题的单项代码修复。

## 能做什么

### 设计原型

Skill 会先明确页面要解决的任务，再根据当前状态进入两种模式：

- **探索方案**：业务目标已经清楚，但布局或交互顺序尚未确定。可以制作多个候选 HTML，用共同任务和模拟数据进行比较。
- **落实设计**：已有截图、设计稿或确认版本。以指定材料为依据调整，不重新发起不必要的设计访谈。

原型默认使用本地 HTML、CSS 和少量 JavaScript，数据和操作均为明确标注的模拟内容。文件选择、登录、AI、真实写入和后端调用不会被偷偷接入。

### UI 对照验收

对照验收需要真实可访问的已确认基准。检查会区分页面可用尺寸、窗口外框、缩放、字体、数据、状态和键盘操作，并逐项记录通过、差异或未验证。构建成功或原型模拟成功都不能代替真实界面验收。

## 版本和交付

一个典型的原型目录如下：

```text
docs/ui-prototype/
├── draft/index.html              # 当前工作草案
├── reviews/draft-01/             # 交付评审时的不可覆盖快照
├── versions/v1/                  # 用户确认后生成的基准版本
└── design.md                     # 目标、交互、状态、验收和确认记录
```

评审编号绑定用户实际看到的快照。确认可以只覆盖某个页面、区域或流程；部分确认不会自动升级为整版确认。后续改动从新评审编号开始，不能覆盖旧基准来消除实现差异。

交付记录至少说明：

- 原型入口、评审编号和确认状态
- 页面路径、主要操作、返回和重置方式
- 样式变量、状态规则和模拟范围
- 验收条件、实际检查环境和未验证项
- 新发现、受影响需求及下一步授权边界

## 如何调用

在 Codex 中直接使用：

```text
使用 $ui-prototype，为这个页面先做一个可交互 HTML 原型，使用模拟数据，并记录关键状态和验收条目。
```

进行已确认设计的对照验收时，可以说明：

```text
使用 $ui-prototype，对照已确认的 v1 原型检查当前运行界面，记录逐项差异和未验证项。
```

设计原型的授权只覆盖独立演示文件；正式前端改造、后端接入、安装和发布需要单独授权。用户确认原型也不等于确认业务规则或批准实现。

## 安装

将本仓库目录复制到 Codex 的个人 Skill 目录，目录名保持为 `ui-prototype`：

### Windows PowerShell

```powershell
$skillRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $HOME '.codex\skills' }
Copy-Item -Path . -Destination (Join-Path $skillRoot 'ui-prototype') -Recurse
```

### macOS / Linux

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
cp -R . "$skill_root/ui-prototype"
```

安装后重新开始一个 Codex 对话，或显式使用 `$ui-prototype`。

## 目录说明

- `SKILL.md`：运行入口和主要工作边界
- `references/deliverables.md`：原型交付、评审快照和确认记录约定
- `references/acceptance.md`：UI 对照验收方法
- `references/behavior-tests.md`：维护 Skill 时使用的行为场景
- `agents/openai.yaml`：Codex 界面展示信息
- `validation/`：格式、行为和交接验证记录，不是运行时指令

## 验证边界

维护时会分别记录结构校验、情景复核、真实文件交接、浏览器运行、UI 对照和安装后的触发验证。某一层通过不代表其他层也已通过。当前验证详情见 [`validation/`](validation/)。

## 相关项目

- [Project Kickoff](https://github.com/td-xiehongyi/skill-project-kickoff)：在需求、流程或范围尚未明确时协助项目启动
