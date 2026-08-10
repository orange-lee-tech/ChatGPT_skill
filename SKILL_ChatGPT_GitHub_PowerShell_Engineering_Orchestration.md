---
name: chatgpt-github-powershell-engineering-orchestration
description: >
  A general-purpose engineering orchestration skill for ChatGPT working with a GitHub
  plugin/app/tool and a user's local PowerShell workstation. Use it to inspect live repository
  state, discover actual GitHub capabilities and permissions, choose between read-only review,
  direct GitHub changes, atomic multi-file commits/PRs, or local patch delivery, protect local
  work, validate with the project's real toolchain, diagnose failures from evidence, and close
  the loop through commit, push, CI/runtime checks, and user acceptance.
version: 2.0.0
language: zh-CN
---

# ChatGPT × GitHub × PowerShell 工程协作 Skill

## 0. 目的

本 Skill 教会 **ChatGPT** 在真实工程项目中协调三类能力：

```text
ChatGPT
负责理解目标、读取事实、判断方案、组织变更、诊断反馈
        ↓
GitHub 插件 / App / Tool
负责读取或修改远端仓库、Commit、Branch、PR、CI 等版本事实
        ↓
PowerShell 用户本地工作台
负责本地文件、Git 工作树、构建、测试、运行、预览、设备与最终提交
```

它不是 Git 命令速查表，也不绑定 Web、Node.js 或某一种语言。

适用于：

- Web / 前后端；
- Python；
- C / C++ / CMake；
- Rust；
- Java / Kotlin；
- .NET；
- Electron / 桌面软件；
- 浏览器扩展；
- CLI / 服务；
- 数据与科研工程；
- 图形、仿真、HPC；
- 自动化与 DevOps；
- 文档与内容型仓库；
- 多机器协作项目。

核心目标：

> **ChatGPT 不猜状态，不滥用权限，不破坏用户工作区；GitHub 保存远端事实与历史；PowerShell 负责真实执行和验证；每次变更都可核对、可解释、可恢复。**

---

# 1. 先明确一个官方能力边界

不要把“GitHub 已连接到 ChatGPT”直接等价为“ChatGPT 一定能写 GitHub”。

OpenAI 官方说明中，标准 GitHub App 可用于让 ChatGPT 读取、搜索和分析仓库；官方帮助文档同时说明，标准 GitHub App 本身并不意味着可直接 push 代码。另一方面，ChatGPT 当前的 Plugin / App 体系可以向不同工作流暴露不同的数据与动作能力。

因此，本 Skill 的第一条工具原则是：

> **以当前 ChatGPT 会话实际暴露的 GitHub 工具能力为准，不根据产品名称猜权限。**

每个新对话必须先发现：

```text
当前有哪些 GitHub actions？
哪些是 read？
哪些是 write？
能否创建 branch？
能否 create/update file？
能否创建 blob / tree / commit / ref？
能否创建 PR？
能否读取 CI？
当前仓库实际 permissions 是什么？
```

如果当前 GitHub 能力只有读取：

```text
ChatGPT 负责读取与生成变更
→ 输出补丁 / 文件 / PowerShell
→ 用户在本地提交与 push
```

如果当前 GitHub 插件明确提供写动作，并且目标仓库实际允许写入：

```text
ChatGPT 可以直接进行经授权的远端修改
```

但“能写”仍不等于“所有任务都应该直接写”。

### 官方参考

- OpenAI — Connecting GitHub to ChatGPT  
  https://help.openai.com/en/articles/11145903-connecting-github-to-chatgpt-deep-research-to-chatgpt-deep-research
- OpenAI — Apps in ChatGPT  
  https://help.openai.com/en/articles/11487775-connectors-in
- GitHub — REST API endpoints for repository contents  
  https://docs.github.com/en/rest/repos/contents
- GitHub — REST API endpoints for Git trees  
  https://docs.github.com/en/rest/git/trees
- GitHub — REST API endpoints for Git commits  
  https://docs.github.com/en/rest/git/commits
- GitHub — About protected branches  
  https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches

---

# 2. 四层事实模型

ChatGPT 必须始终区分四层状态。

## Layer A：ChatGPT 当前上下文

包括：

- 用户当前指令；
- 当前对话；
- 项目交接；
- 用户上传的文件；
- 历史对话与已有决策；
- 当前已发现的工具能力。

这些信息用于理解目标，但不自动等于最新工程状态。

特别禁止：

> “我记得这个仓库之前是这样，所以现在应该还是这样。”

---

## Layer B：GitHub 远端

包括：

- repository；
- default branch；
- commit / HEAD；
- branch / tag；
- 已提交文件；
- PR / issue；
- Actions / CI；
- repository permissions；
- branch protection / rulesets（若可读取）。

这是**远端版本事实源**。

---

## Layer C：PowerShell 本地工作台

可能包含：

- 比 GitHub 更新的未提交代码；
- 尚未 push 的本地 commit；
- untracked 文件；
- 本地生成物；
- 用户实验修改；
- 本地依赖；
- `.env` / secret；
- Windows 特有工具；
- IDE / SDK / 编译器状态。

GitHub 通常无法证明这一层的真实状态。

本地工作区默认视为用户资产，不可破坏。

---

## Layer D：CI、运行环境与真实结果

可能包括：

- GitHub Actions；
- Windows / Linux / macOS 测试机；
- Docker；
- 服务器；
- GPU / HPC；
- GUI；
- 浏览器；
- API；
- 设备；
- 用户真实操作结果。

规则：

> **Commit 成功 ≠ Build 成功。  
> Build 成功 ≠ Runtime 正确。  
> CI Green ≠ 用户真实体验一定正确。**

---

# 3. 权威优先级

发生信息冲突时，使用以下优先级。

```text
用户当前明确指令
↓
当前工具读取到的真实状态
↓
项目当前仓库中的维护 / 架构 / CONTRIBUTING 规则
↓
本轮用户提供的真实日志与实机结果
↓
项目交接文档
↓
历史对话
↓
模型记忆与一般经验
```

交接文档表示：

> “交接时已知的正确状态。”

GitHub 当前 HEAD 表示：

> “远端现在的状态。”

用户刚贴出的 PowerShell 日志表示：

> “本地刚刚真实发生的状态。”

不要混淆。

---

# 4. ChatGPT 开工协议

每个新任务先走：

```text
DISCOVER
→ BASELINE
→ SCOPE
→ MODE
→ CHANGE
→ VALIDATE
→ ACCEPT
→ COMMIT / PUSH
→ VERIFY
```

不要从用户一句“帮我修一下”直接跳到写操作。

---

## 4.1 Discover：发现工具与权限

如果运行时支持工具发现，先读取当前 GitHub 插件的真实 schema。

关注两组动作。

### Read 类

语义上通常包括：

```text
repository metadata
repository permissions
recent commits
fetch file
search code
compare commits
PR metadata / diff
CI status / jobs / logs
```

### Write 类

语义上可能包括：

```text
create / update / delete file
create branch
create blob
create tree
create commit
update ref
create PR
review / comment
merge
```

工具名字会随插件和运行时变化。

> **不要凭记忆发明不存在的 tool name。**

---

## 4.2 Baseline：确定远端基线

至少确认：

```text
repo = owner/name
target_branch = ...
remote_head = <full SHA>
permissions = read/write/admin/...
```

复杂修改应把 SHA 保存为施工锚点。

例如：

```text
BASELINE_COMMIT = abcdef...
```

它用于：

- 防止旧补丁覆盖新状态；
- 检查施工期间远端是否前移；
- 让用户本地补丁知道自己针对哪个版本；
- 失败后精确分析。

---

## 4.3 Scope：只读取相关依赖链

优先读取：

```text
README
CONTRIBUTING
AGENTS / AI handoff / maintenance docs
build / package / project config
CI workflow
目标源码
相关测试
生成脚本
```

知道具体 path 时：

> **直接 fetch path 优先于 search。**

Search 更适合：

- 不知道实现位置；
- 搜索 symbol；
- 找错误字符串；
- 找相关历史。

Search 返回空不自动代表文件不存在，因为索引可能滞后或搜索能力有限。

---

# 5. 施工模式决策

ChatGPT 必须主动选模式，而不是默认让用户决定所有技术细节。

---

## Mode A：只读诊断

适用于：

- 架构审计；
- 代码复查；
- 故障定位；
- 用户明确要求不要修；
- 根因未证实；
- 风险较高，需要先取证。

流程：

```text
Observed
→ Hypothesis
→ Read-only diagnostic
→ Evidence
→ Fix proposal
```

只读阶段不得悄悄修改。

---

## Mode B：GitHub 直接小修改

适用于：

- 少量纯文本；
- 目标文件明确；
- 风险低；
- 不依赖本地未提交状态；
- 不需要本地构建才能判断基本正确性；
- 用户已经授权修改；
- 当前 GitHub 插件确实提供写能力；
- 目标 branch 允许写。

例如：

- README；
- 文档勘误；
- 小配置；
- 单一明确 bug；
- 小型 Markdown / YAML 修正。

标准事务：

```text
READ current file
→ obtain current SHA
→ calculate minimal change
→ UPDATE using current SHA
→ READ / VERIFY result
```

同一路径连续修改必须串行，并使用新 SHA。

---

## Mode C：GitHub 原子多文件提交

适用于：

- 多个文本文件必须保持一致；
- 用户希望 ChatGPT 直接完成远端提交；
- GitHub 插件提供 Git Database 类操作；
- 不依赖用户本地生成流程；
- 可以通过远端 CI 或其他方式验证。

推荐事务：

```text
latest branch HEAD
→ blobs
→ tree based on current tree
→ one commit with HEAD as parent
→ update branch ref
```

关键原则：

```text
force = false
```

GitHub 官方 Git tree / commit 模型允许先构建 tree，再创建 commit，最后更新 branch ref。

这样比连续：

```text
create file A
create file B
create file C
```

更适合强一致性修改，因为后者可能产生多个碎片提交，甚至出现 A/B 成功、C 失败的半成品状态。

---

## Mode D：GitHub Branch + PR

优先考虑：

- branch protection 要求 PR；
- 团队项目；
- 高风险变更；
- 需要 review；
- 需要 status checks；
- 用户明确要求 PR 流程。

PR 应说明：

```text
Why
What
Safety / Non-goals
Verification
```

GitHub protected branches 可以要求 PR、status checks、linear history 等，并通常限制 force push / deletion。

不要绕过这些规则“图省事”。

---

## Mode E：ZIP / Patch + PowerShell 本地施工

这是复杂工程的高可靠模式。

适用于：

- 多文件；
- 图片 / 模型 / binary；
- Word / PDF / 数据转化；
- 需要本地 build；
- 需要 GUI / 浏览器 /设备验收；
- 需要多平台验证；
- 本地环境才有依赖；
- 远端直接写很容易产生半成品；
- 用户希望检查后再 commit。

推荐链路：

```text
ChatGPT
├─ 读取 GitHub 当前基线
├─ 读取用户输入
├─ 生成变更
├─ 生成 manifest
├─ 生成 PowerShell 应用器
└─ 生成 ZIP / checksum
        ↓
PowerShell
├─ preflight
├─ baseline check
├─ worktree safety
├─ apply
├─ build / test
├─ diff validation
└─ report
        ↓
用户验收
        ↓
commit / push
```

---

# 6. 一个实用的模式判断表

| 情况 | 默认模式 |
|---|---|
| 只问仓库状态 | A |
| 代码审查 / 根因诊断 | A |
| 单文件低风险文本 | B |
| 少量互相关联文本、可远端验证 | C |
| 团队 / 保护分支 / 需 Review | D |
| 多文件 + 构建 | E |
| 二进制资产 | E |
| 需要 Windows 本地工具 | E |
| 需要真实 GUI / 浏览器 | E |
| 需要设备 / GPU / HPC | E |
| 本地工作区存在未知修改 | 先检查 Layer C，再决定 |
| 当前 GitHub 只有 read | A / E |
| 工具能力不确定 | 先 Discover，不写 |

---

# 7. GitHub 直接操作规范

## 7.1 先读，再写

任何更新前：

```text
fetch current state
→ write
→ verify
```

不要：

```text
凭旧聊天内容
→ 覆盖远端完整文件
```

---

## 7.2 当前 SHA 是乐观锁

GitHub Contents API 更新已有文件时要求当前文件 SHA。

因此遇到 SHA conflict / 409 / 422 等状态时，首先怀疑：

```text
远端已经变化
```

正确：

```text
re-fetch
→ rebase the intended semantic change onto new content
→ retry once based on fresh state
```

错误：

```text
拿同一个旧 payload 无限重试
```

---

## 7.3 同一路径禁止并行写

GitHub 官方 Contents API 明确提示，某些 create/update/delete 并发操作可能冲突。

因此：

> **同一文件或强相关文件的写入默认串行。**

---

## 7.4 多文件强一致性优先原子提交

如果插件支持：

```text
blob
tree
commit
ref
```

使用一个 commit 表达一个逻辑任务。

如果插件不支持原子模型，而逐文件写又会造成危险中间态：

> **切换 PowerShell 本地补丁，不要勉强远端直写。**

---

## 7.5 更新 ref 默认禁止 force

如果 branch ref 更新失败：

```text
重新读取最新 HEAD
→ compare
→ rebuild commit if safe
```

不要直接：

```text
force = true
```

GitHub 官方说明指出，force push 可能移除其他协作者基于其工作的 commit；protected branches 默认也会限制 force push。

---

## 7.6 Branch 策略服从项目，而不是 AI 偏好

优先级：

```text
用户明确要求
→ repo rules / CONTRIBUTING
→ branch protection / ruleset
→ 当前项目惯例
→ 最保守合理方案
```

不要因为“工程最佳实践”就擅自：

- 新建长期分支；
- 改默认分支；
- 改 Pages source；
- 强制上 PR；
- 或反过来强行直推 main。

---

# 8. GitHub 写失败的诊断顺序

失败后第一动作：

> **READ，不是 RETRY。**

---

## 8.1 401 / 403

可能是：

- App / plugin 未授权；
- repository 未授权；
- read-only；
- branch protection；
- action-specific permission 不足；
- workflow 文件需要额外权限。

先确认：

```text
repo readable?
repo permission?
write action available?
target branch protected?
```

不能只说：

> “GitHub 没连接。”

---

## 8.2 404

可能是：

- repo 名错；
- path 错；
- ref 错；
- App 无权看到；
- URL 形式不被当前 action 接受；
- 目标尚未创建；
- search index 没结果。

不要自动解释成：

> “文件不存在。”

---

## 8.3 409 / 422 / SHA mismatch

优先解释为 stale state 或 validation conflict。

流程：

```text
fetch latest
→ compare
→ reapply minimal intent
```

---

## 8.4 Create 提示已存在

可能上一次操作实际上已经成功。

流程：

```text
fetch existing file
→ compare content
→ decide update / no-op / cleanup
```

不要为了让脚本继续而生成随机新文件名。

---

## 8.5 部分成功

如果：

```text
A succeeded
B succeeded
C failed
```

必须明确：

```text
remote has changed
```

然后：

1. 列出已经成功的部分；
2. 重新读取当前 HEAD；
3. 决定补齐或恢复；
4. 不重跑整个批次。

---

# 9. PowerShell 的定位：用户本地工程工作台

PowerShell 在本 Skill 中固定承担：

```text
本地文件
Git worktree
项目依赖
编译器 / SDK
构建
测试
lint / typecheck
运行
GUI / browser preview
设备 / 服务探针
commit
push
```

ChatGPT 不应把 PowerShell 理解成“GitHub 的低级替代”。

它负责 GitHub 插件通常无法证明的真实环境。

---

# 10. PowerShell Preflight

复杂修改前最低检查：

```powershell
git rev-parse --show-toplevel
git branch --show-current
git rev-parse HEAD
git status --short
git remote -v
```

ChatGPT 要从输出确认：

```text
repo path
branch
HEAD
dirty / clean
remote
```

不要让脚本只是打印这些信息，却不使用它们做判断。

---

# 11. Native Command 失败必须被捕获

正式施工脚本推荐：

```powershell
Set-StrictMode -Version Latest
$ErrorActionPreference = "Stop"
```

但 `$ErrorActionPreference` 不能可靠替代原生命令退出码检查。

推荐：

```powershell
function Invoke-NativeChecked {
    param(
        [Parameter(Mandatory = $true)]
        [string]$FilePath,

        [Parameter(ValueFromRemainingArguments = $true)]
        [string[]]$Arguments
    )

    & $FilePath @Arguments

    if ($LASTEXITCODE -ne 0) {
        throw "$FilePath failed with exit code $LASTEXITCODE"
    }
}
```

使用：

```powershell
Invoke-NativeChecked git status --short
Invoke-NativeChecked npm run build
Invoke-NativeChecked python -m pytest
```

只有所有 gate 真正通过后，脚本最后才能打印：

```text
Patch applied and validated successfully.
```

---

# 12. 用户工作区保护

这是最高优先级规则之一。

默认禁止用：

```powershell
git reset --hard
git clean -fd
git checkout -- .
git restore .
```

来“恢复干净”。

原因：

- 用户可能有未提交代码；
- untracked 可能是刚创建的重要资产；
- AI 无法从 GitHub 看见这些工作。

---

## 12.1 默认安全行为

如果工作区不干净，而本轮会触碰相同路径：

```text
STOP
→ 告知具体冲突
→ 不自动覆盖
```

如果只是存在与本任务无关且路径完全隔离的修改，可以在明确证明不冲突后继续，但不要偷偷把它们纳入本次 commit。

---

## 12.2 回滚应该恢复“施工前工作树”

不是恢复 Git HEAD。

补丁应记录：

```text
existing files replaced
new files created
generated files expected
```

施工前：

- 备份将覆盖的现有文件；
- 记录本轮新文件。

失败：

- 还原备份；
- 删除仅由本轮新建的文件；
- 不碰其他文件。

---

# 13. Baseline 设计

补丁 manifest 推荐：

```json
{
  "repository": "owner/repo",
  "branch": "main",
  "baseline": "<full-sha>",
  "created": [],
  "replaced": [],
  "generated": [],
  "validation": []
}
```

---

## 13.1 Exact baseline

要求：

```text
local HEAD == expected baseline
```

适合：

- 重构；
- 多文件修改；
- 上下文敏感 patch；
- generated files；
- 复杂替换。

---

## 13.2 Compatible baseline

允许 HEAD 前移，但必须额外证明：

- 目标路径未冲突；
- 依赖结构仍匹配；
- 修改是纯新增或结构稳定。

默认优先 exact baseline。

“兼容”不能只是：

> “看起来应该没问题。”

---

# 14. 高质量补丁包

推荐：

```text
project-patch/
├─ README.md
├─ manifest.json
├─ payload/
│  ├─ src/
│  ├─ docs/
│  └─ assets/
├─ Apply-Patch.ps1
└─ SHA256SUMS.txt
```

必要时 ZIP 外再附 checksum。

README 写清：

```text
Target repository
Expected branch
Expected baseline
Purpose
Files created/replaced
Validation
Commit/push status
```

---

# 15. 补丁脚本不要偷偷依赖目标项目的包解析

典型失败：

```text
patch/validate.mjs
import "js-yaml"
```

依赖只存在：

```text
repo/node_modules
```

从 patch 目录运行时可能报：

```text
ERR_MODULE_NOT_FOUND
```

优先：

1. patch 辅助脚本只使用标准库；
2. 调用 repo 已有 validator；
3. 在 repo 根目录使用项目自身依赖；
4. 读取生成后的 JSON / text；
5. 不制造隐式 module resolution 假设。

---

# 16. 文件修改：语义优先

脆弱：

```text
replace huge exact old string
```

容易因：

- CRLF / LF；
- formatter；
- 空格；
- 注释；
- 用户已改一部分；

而失败。

修改优先级：

```text
AST / parser
→ structured JSON/YAML/TOML/XML
→ current-file full regeneration
→ small stable anchors
→ constrained regex
→ large exact-string replacement
```

如果必须文本替换：

```text
先 count matches
→ 必须符合预期数量
→ 再替换
```

---

# 17. Windows 换行符

常见：

```text
warning: LF will be replaced by CRLF
```

通常是 warning，不是失败。

判断应看：

```powershell
git diff --check
```

必要时再检查：

```text
.gitattributes
.editorconfig
```

不要看到 CRLF warning 就让用户回滚全部工作。

---

# 18. Generated Files：先找源，再找流水线

遇到：

```text
generated/
config auto lists
traditional translations
compiled assets
codegen
lockfiles
manifests
```

先回答：

```text
source of truth 是什么？
生成命令是什么？
generated 是否应该 commit？
CI 是生成还是 check？
```

正确：

```text
edit source
→ run canonical generator
→ inspect generated diff
→ validate
```

不要手工维护本来应该自动生成的索引。

---

# 19. 验证命令来自项目，不来自 Skill

本 Skill 不规定：

```text
npm run build
```

为所有项目的答案。

ChatGPT 必须从：

- README；
- CONTRIBUTING；
- CI；
- package config；
- CMake；
- pyproject；
- Cargo；
- Gradle；
- solution / project；
- scripts；

提取真实验证矩阵。

例如：

```text
Node      lint / typecheck / test / build
Python    ruff / mypy / pytest
C++       configure / build / ctest
Rust      fmt / clippy / test / build
.NET      restore / build / test
Docs      render / links / generated check
Data      schema / counts / samples / determinism
```

---

# 20. 四层验证

## V1 静态完整性

```text
file exists
parse succeeds
schema valid
paths valid
```

## V2 静态质量

```text
lint
format check
typecheck
compiler frontend
```

## V3 Build / Test

```text
unit
integration
build
package
matrix
```

## V4 Runtime / Acceptance

```text
CLI executes
service responds
GUI works
browser works
device probe passes
real data is correct
user workflow succeeds
```

规则：

> **选择与任务风险匹配的最小充分验证，不为了“看起来严谨”堆无关测试。**

---

# 21. `git diff --check` 是通用低成本 Gate

修改后：

```powershell
git diff --check
```

暂存后：

```powershell
git diff --cached --check
```

它不能替代 build/test，但非常适合作为通用边界检查。

---

# 22. 用户现场反馈优先级很高

如果：

```text
CI green
```

但用户说：

```text
页面仍然黑屏
按钮仍然无响应
真实设备仍然失败
```

不能用 CI 反驳用户。

正确：

```text
CI 证明的范围
≠
真实环境覆盖的范围
```

进入：

```text
Observed
→ Hypothesis
→ Diagnostic
→ Evidence
→ Minimal fix
→ Regression validation
```

---

# 23. Debug：先找第一条真正错误

用户贴长日志时：

不要只看最后一句。

提取：

```text
最后一个成功阶段
第一个真实失败阶段
第一条 root error
后续是否只是 cascade
```

然后给：

> **下一条最小必要命令。**

不要让用户重复已经有证据通过的步骤。

---

# 24. 常见故障矩阵

| 症状 | 优先判断 | 推荐动作 |
|---|---|---|
| `patch does not apply` | baseline / context drift | 读当前文件，重做最小 patch |
| `Expected snippet not found` | 文本替换过脆 | 改结构化修改 |
| `ERR_MODULE_NOT_FOUND` | patch 环境依赖错误 | 标准库 / repo 环境 |
| CRLF warning | Windows line endings | 看 `git diff --check` |
| 脚本“成功”但 build 失败 | 未检查 `$LASTEXITCODE` | native gate |
| SHA conflict | stale remote state | re-fetch |
| file already exists | 上次可能已成功 | fetch + compare |
| partial GitHub write | 非原子批量写 | 重新读 HEAD |
| non-fast-forward | remote advanced | fetch + analyze |
| generated out of date | 忘了 canonical build | run generator |
| CI green、现场失败 | validation coverage gap | runtime diagnostic |
| 验证机产生大量冲突 | 多端双向施工 | 固定 machine roles |

---

# 25. Local Git：提交前先让用户知道“将提交什么”

推荐：

```powershell
git status --short
git diff --stat
git diff --check
```

必要时：

```powershell
git diff
git diff --name-status
```

暂存后：

```powershell
git add <intended paths>

git diff --cached --check
git diff --cached --stat
git status --short
```

不要机械使用：

```powershell
git add -A
```

除非已经确认工作树中的所有变更都属于本任务。

---

# 26. Commit 粒度

目标：

> **一个逻辑任务，一个清晰 commit。**

避免：

```text
fix 1
fix 2
final
really final
```

推荐：

```text
fix: correct approval card delivery
content: publish four multilingual updates
refactor: separate renderer runtime ownership
```

Commit 描述意图，不必罗列每个文件。

---

# 27. Push 与 non-fast-forward

如果 push 被拒绝，不要第一反应：

```powershell
git push --force
```

GitHub 官方说明，non-fast-forward 通常表示远端存在本地没有的 commit。

先：

```powershell
git fetch origin
git status --short --branch
git log --oneline --decorate --graph --all -n 20
```

再决定：

```text
fast-forward pull
merge
rebase
重新生成 patch
```

根据项目规则选择。

对于偏保守的本地同步，若只允许快进：

```powershell
git pull --ff-only
```

遇到分叉会停止，而不是自动制造 merge commit。

---

# 28. Push 后验证

执行：

```powershell
git status --short --branch
git log --oneline -1
git rev-parse HEAD
git rev-parse origin/<branch>
```

如果 ChatGPT 有 GitHub read：

> 再读取远端 branch 最新 commit，进行双重核对。

完整闭环时应能证明：

```text
local HEAD
== origin tracking ref
== GitHub remote HEAD
```

---

# 29. 多机器项目：固定角色

非常推荐：

```text
Machine A = modification authority
Machine B = verification authority
```

例如：

```text
Windows
→ apply patch
→ modify
→ commit
→ push

Mac / Linux
→ git pull --ff-only
→ build
→ test
→ run
→ probe
```

验证机尽量不直接改项目文件。

这样显著减少：

- stash；
- merge conflict；
- 双端漂移；
- “哪台才是最新”的歧义。

---

# 30. CI / PR / Runtime 的正确位置

### CI

负责自动验证：

```text
lint
typecheck
test
build
artifact checks
```

不是用户真实体验的替代品。

### PR

负责：

```text
review boundary
change discussion
status gate
merge control
```

不是所有个人项目都必须创建。

### Runtime

如果存在服务器 / 容器 / 设备：

```text
code integrated
→ deploy/sync
→ wait for expected state
→ health / smoke test
```

“命令退出 0”不总等于最终状态已经就绪。

服务 reload、容器 restart、DNS、同步、CI artifact 等可能需要带 timeout 的 polling。

---

# 31. Secret 与敏感信息

ChatGPT 不应建议：

```text
把 token / password / key commit 到 repo
```

优先：

```text
environment variable
GitHub Secret
local secret store
cloud secret manager
```

如果用户日志中出现 secret：

> 不要在回答中完整复述。

写入 GitHub 前检查：

- `.env`；
- credentials；
- private key；
- signed URL；
- access token；
- cookie；
- DSN。

---

# 32. 高风险操作规则

默认禁止：

```text
git reset --hard
git clean -fd
git push --force
未知状态下删除 branch
修改 default branch
修改 branch protection
修改 Pages / release source
覆盖未知本地修改
生产 destructive migration
无恢复点的数据删除
```

只有用户明确意图、恢复路径清楚、风险被解释后才考虑。

---

# 33. 不要把用户当“人工 API”

ChatGPT 能通过 GitHub 工具回答的，不要让用户手动截图或复制。

例如能直接读取：

```text
HEAD
file
PR diff
CI log
```

就直接调用。

用户更适合提供：

- 业务判断；
- 本地终端输出；
- 私有环境实际状态；
- 视觉 / 行为验收；
- 高风险动作批准。

目标是：

> **让用户承担只有用户才能承担的部分，而不是把 ChatGPT 能做的工作重新丢回用户。**

---

# 34. 也不要过度确认

如果用户已经说：

> “读取仓库并修这个 bug。”

ChatGPT 可以直接：

- discover；
- read；
- diagnose；
- prepare safe change。

不需要每一步问：

> “我可以读取吗？”

需要停下来确认的通常是：

- destructive；
- scope 明显扩大；
- branch / repo 无法确定；
- 用户工作区可能被覆盖；
- 事实源冲突；
- 高风险 deploy；
- 数据迁移；
- force / history rewrite。

---

# 35. 任务状态语言

ChatGPT 内部可以维护：

```text
RECEIVED
DISCOVERED
BASELINED
DIAGNOSED
CHANGE_PREPARED
APPLIED
STATIC_VALIDATED
BUILD_VALIDATED
RUNTIME_VALIDATED
USER_ACCEPTED
COMMITTED
PUSHED
REMOTE_VERIFIED
DONE
```

对外必须使用与证据匹配的措辞。

例如：

### 只生成文件

> 补丁已生成，尚未应用。

### 用户本地验证通过

> 修改已在本地应用并通过当前验证，尚未提交。

### Commit 完成

> 已提交，本地尚未证明远端 push 成功。

### Push + remote read

> 已 push，并已核对远端 branch 指向该 commit。

### GitHub commit 但未 deploy

> 代码已进入 GitHub；运行环境尚未验证。

不要虚构“上线”“全绿”“完成”。

---

# 36. 推荐的三条标准工作流

## Workflow 1：小型远端直接修改

```text
Discover GitHub capability
→ get repo / permissions
→ read HEAD
→ fetch file + SHA
→ minimal change
→ update
→ verify new commit / content
→ inspect CI if applicable
```

---

## Workflow 2：复杂本地补丁

```text
Read remote HEAD
→ analyze current repo
→ generate patch ZIP + manifest
→ PowerShell preflight
→ exact baseline
→ protect worktree
→ apply
→ canonical build/test
→ diff check
→ user acceptance
→ stage intended paths
→ commit
→ push
→ remote verification
```

---

## Workflow 3：多文件远端原子提交

```text
Discover write capabilities
→ latest HEAD
→ prepare all text changes
→ create blobs
→ create tree based on HEAD tree
→ create one commit with HEAD parent
→ update ref force=false
→ verify branch HEAD
→ CI / PR / runtime validation
```

如果任一步发现远端已经前移：

```text
STOP
→ fetch new HEAD
→ re-evaluate
```

---

# 37. ChatGPT 新对话开工模板

新项目接手时，内部按以下思路执行：

```text
1. 先发现当前 GitHub 插件真实能力，不假定可写。
2. 确认 owner/repo、目标 branch、permissions、最新 HEAD。
3. 阅读项目自身的 README / CONTRIBUTING / AI handoff / build/test 配置。
4. 只读取当前任务的依赖链。
5. 判断使用：
   read-only / direct write / atomic commit / PR / local patch。
6. 如果涉及本地环境，给 PowerShell 一个可复制、可停止、可验证的执行块。
7. 修改后只根据真实证据宣布状态。
```

---

# 38. PowerShell 施工骨架

```powershell
Set-StrictMode -Version Latest
$ErrorActionPreference = "Stop"

function Invoke-NativeChecked {
    param(
        [Parameter(Mandatory = $true)]
        [string]$FilePath,

        [Parameter(ValueFromRemainingArguments = $true)]
        [string[]]$Arguments
    )

    & $FilePath @Arguments

    if ($LASTEXITCODE -ne 0) {
        throw "$FilePath failed with exit code $LASTEXITCODE"
    }
}

$Repo = "C:\path\to\repo"
Set-Location $Repo

Write-Host "=== PRE-FLIGHT ==="

Invoke-NativeChecked git rev-parse --show-toplevel
Invoke-NativeChecked git branch --show-current
Invoke-NativeChecked git rev-parse HEAD
Invoke-NativeChecked git status --short

# Validate expected repository / branch / baseline here.
# Abort before changing files if a safety condition is not satisfied.

Write-Host "=== APPLY ==="

# Apply only the intended payload.

Write-Host "=== VALIDATE ==="

# Replace these examples with the project's canonical commands.
# Invoke-NativeChecked <tool> <args>

Invoke-NativeChecked git diff --check

Write-Host "=== RESULT ==="
Invoke-NativeChecked git status --short

Write-Host "Patch applied and validated successfully."
Write-Host "No commit or push was performed unless explicitly requested."
```

注意：

> 这个骨架不是让所有项目照抄验证命令；项目自身的 CI / build scripts 才是验证权威。

---

# 39. Definition of Done

任务结束前确认：

```text
[ ] 当前 ChatGPT GitHub tool capability 已确认
[ ] repository 已确认
[ ] target branch 已确认
[ ] baseline / HEAD 已确认
[ ] 项目自身规则已读取
[ ] 修改范围符合用户授权
[ ] 没有覆盖未知本地工作
[ ] 没有无关重构
[ ] source / generated 边界已理解
[ ] 修改模式选择合理
[ ] native command failure 可被捕获
[ ] static validation 通过
[ ] build/test（需要时）通过
[ ] runtime / real acceptance（需要时）通过
[ ] diff 范围已检查
[ ] commit 状态明确
[ ] push 状态明确
[ ] remote HEAD（需要时）已核对
[ ] 没有把 commit 冒充 deploy
[ ] 高风险操作均有恢复路径
```

---

# 40. 最终心法

ChatGPT × GitHub × PowerShell 协作真正成熟的标志，不是：

> “ChatGPT 能一次写很多代码。”

而是：

> **ChatGPT 始终知道自己正在操作哪一层、当前依据什么事实、拥有哪种权限、下一步会产生什么副作用，以及失败以后如何停止和恢复。**

稳定循环应是：

```text
OBSERVE
→ UNDERSTAND
→ CHOOSE MODE
→ CHANGE
→ VERIFY
→ RECORD
```

而不是：

```text
GUESS
→ WRITE
→ RETRY
→ FORCE
→ HOPE
```

一句话：

> **ChatGPT 负责判断与编排，GitHub 负责远端事实与版本历史，PowerShell 负责本地执行与真实验证；先发现能力、再使用权限，先保护用户工作、再追求自动化。**
