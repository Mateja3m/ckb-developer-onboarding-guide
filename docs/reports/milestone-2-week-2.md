# Week 2 Milestone 2 Progress Report

## Status

Milestone 1 has been completed.

Milestone 2 has now been completed as the CKB-specific onboarding documentation layer.

The second week of Milestone 2 focused on replacing the remaining placeholder sections with practical onboarding documentation, while preserving the repository rule that exact commands should only be included where they are already validated locally.

## Work Completed

### 1. Indexer Setup Documentation Added

The placeholder section at docs/06-indexer-setup.md was expanded into a real onboarding page.

The completed section now explains:

- what an indexer does in the CKB workflow
- when a beginner needs one and when it is reasonable to postpone it
- the difference between local and hosted indexer choices
- what should be verified before treating indexer access as ready
- validated local and public testnet indexer health-check examples

### 2. First Developer Workflow Documentation Added

The placeholder section at docs/08-first-developer-workflow.md was expanded into a real beginner workflow page.

The completed section now provides:

- one small happy path from local setup into a confirmed chain interaction
- a narrow success definition that does not overclaim contract, deployment, or production readiness
- a simple record-keeping habit for later troubleshooting

### 3. Common Errors And Remediation Documentation Added

The placeholder section at docs/09-common-errors-and-remediation.md was expanded into a real failure-handling page.

The completed section now documents beginner-facing issues such as:

- missing tooling
- DNS or hostname-resolution failures
- first-run missing-binary confusion
- warning-like startup output
- browser misuse of RPC endpoints
- stopped local node processes
- endpoint confusion
- low block-height misinterpretation

Each entry now includes symptom, likely cause, and a practical next action.

### 4. Troubleshooting Matrix Added

The placeholder section at docs/10-troubleshooting-matrix.md was expanded into a structured troubleshooting matrix.

The completed section now provides:

- symptom-to-cause mapping
- what to check first
- a clear next action for common onboarding failures

This gives the repository a faster lookup layer in addition to the more descriptive remediation page.

### 5. AI-Assisted Debugging Guidance Added

The placeholder section at docs/11-ai-assisted-debugging.md was expanded into a real guidance page.

The completed section now explains:

- what AI is useful for during onboarding
- what AI should not be trusted to invent
- what information a developer should share when asking for help
- how to use AI without breaking the repository’s validation-first approach

### 6. CKB Mental Model Documentation Added

The placeholder section at docs/12-ckb-mental-model.md was expanded into a real conceptual guide.

The completed section now explains the relationship between:

- CKB
- Nervos
- node
- RPC
- indexer
- devnet

This gives beginners a simpler conceptual map before deeper development work begins.

### 7. Common Misconceptions Documentation Added

The placeholder section at docs/13-common-misconceptions.md was expanded into a real misconception guide.

The completed section now addresses assumptions such as:

- treating a browser visit as an RPC test
- treating a low block number as failure
- assuming one success proves the whole environment is ready
- assuming public RPC and local node success mean the same thing
- assuming every warning is fatal
- assuming local endpoints are interchangeable

### 8. Top-Level Scope Messaging Updated

The repository messaging was updated so it now reflects Milestone 2 completion rather than Milestone 2 being only partially started.

Updated scope messaging now makes it clear that:

- Milestone 1 remains the completed documentation foundation
- Milestone 2 is complete as the CKB-specific onboarding documentation layer
- TODO notes still mark exact commands or provider-specific details that have not yet been validated locally
- the remaining work now moves beyond Milestone 2 documentation completion

### 9. Public RPC And Indexer Validation Added

After the main Week 2 documentation pass, an additional validation pass was completed to close the two most proposal-relevant open points from Milestone 2.

That validation confirmed:

- a public testnet RPC example using `https://testnet.ckb.dev/rpc`
- a local indexer health check using `get_indexer_tip`
- a public testnet indexer health check using `https://testnet.ckb.dev/indexer`

This allowed the repository to move beyond conceptual-only wording for those two areas and document tested examples instead.

## Validation Handling During This Week

The Week 2 Milestone 2 documentation pass stayed aligned with the existing repository validation rules.

This means:

- exact commands were reused only where repository validation already existed
- conceptual and workflow sections were expanded without inventing unsupported setup steps
- public RPC and indexer examples were added only after direct validation output was captured
- validation boundaries remained visible where broader installation or later-stage provider coverage still falls outside the current onboarding path

## Outcome Against Week 2 Scope

Week 2 of Milestone 2 successfully delivered:

- indexer setup documentation
- first developer workflow documentation
- common errors and remediation documentation
- troubleshooting matrix documentation
- AI-assisted debugging guidance
- CKB mental model guidance
- common misconceptions guidance
- top-level scope updates reflecting Milestone 2 completion
- validated public RPC and indexer examples aligned with the proposal's onboarding scope

Milestone 2 should now be considered complete as a documentation milestone.

## Remaining Scope For Milestone 3

After Milestone 2, the remaining scope moves into Milestone 3 activities rather than unfinished Milestone 2 content.

That later scope should focus on:

- final refinement and polish
- translation work where needed
- publication readiness
- any final validation cleanup needed before broader release

---

# 第2周里程碑2进展报告

## 状态

里程碑1已经完成。

里程碑2现已完成，作为 CKB 专项入门文档层已经闭环。

里程碑2的第二周重点是将剩余的占位章节替换为实际可用的入门文档，同时继续遵守本仓库的规则：只有在本地已经验证过的情况下，才写入精确命令。

## 已完成工作

### 1. 已补充 Indexer Setup 文档

原本的占位章节 docs/06-indexer-setup.md 已扩展为真实的入门页面。

完成后的章节现在说明了：

- indexer 在 CKB 工作流中的作用
- 初学者什么时候需要它，什么时候可以暂时不引入它
- 本地 indexer 与托管 indexer 的差异
- 在把 indexer 视为“已就绪”之前应验证什么
- 已验证的本地与公共测试网 indexer health-check 示例

### 2. 已补充 First Developer Workflow 文档

原本的占位章节 docs/08-first-developer-workflow.md 已扩展为真实的初学者工作流页面。

完成后的章节现在提供：

- 一条从本地设置进入已确认链交互的最小 happy path
- 不夸大 contract、deployment 或 production readiness 的狭义成功定义
- 一种便于后续 troubleshooting 的简单记录习惯

### 3. 已补充 Common Errors And Remediation 文档

原本的占位章节 docs/09-common-errors-and-remediation.md 已扩展为真实的故障处理页面。

完成后的章节现在记录了初学者常见问题，例如：

- 缺少本地工具
- DNS 或主机名解析失败
- 首次运行时缺失二进制文件带来的误解
- 看起来像 warning 的启动输出
- 用浏览器错误地测试 RPC 端点
- 本地节点进程已停止
- 端点混淆
- 对较低 block height 的误判

每个条目现在都包含症状、可能原因和实际的下一步动作。

### 4. 已补充 Troubleshooting Matrix

原本的占位章节 docs/10-troubleshooting-matrix.md 已扩展为结构化的 troubleshooting matrix。

完成后的章节现在提供：

- symptom 到 cause 的映射
- 应先检查什么
- 针对常见入门故障的明确下一步动作

这使仓库除了更详细的 remediation 页面之外，又多了一层更快的查找层。

### 5. 已补充 AI-Assisted Debugging 指导

原本的占位章节 docs/11-ai-assisted-debugging.md 已扩展为真实的指导页面。

完成后的章节现在解释了：

- AI 在入门过程中适合做什么
- 哪些内容不应交给 AI 凭空推断
- 开发者在求助时应提供哪些信息
- 如何在不破坏本仓库 validation-first 原则的前提下使用 AI

### 6. 已补充 CKB Mental Model 文档

原本的占位章节 docs/12-ckb-mental-model.md 已扩展为真实的概念指导页面。

完成后的章节现在解释了以下关系：

- CKB
- Nervos
- node
- RPC
- indexer
- devnet

这为初学者在进入更深入的开发工作之前提供了更清晰的概念地图。

### 7. 已补充 Common Misconceptions 文档

原本的占位章节 docs/13-common-misconceptions.md 已扩展为真实的误区说明页面。

完成后的章节现在处理了如下常见误解：

- 把浏览器访问当作 RPC 测试
- 把较低 block number 当作失败
- 认为一次成功就代表整个环境已经准备就绪
- 认为 public RPC 和 local node 的成功意义相同
- 认为所有 warning 都是致命错误
- 认为所有本地端点都可以互换

### 8. 已更新顶层范围说明

仓库顶层说明已更新，因此现在反映的是里程碑2已经完成，而不是只完成了里程碑2的一部分。

更新后的范围说明现在明确表示：

- 里程碑1仍然是已完成的文档基础
- 里程碑2已完成，作为 CKB 专项入门文档层已经建立完成
- TODO note 仍然用于标记那些尚未在本地验证的精确命令或 provider-specific 细节
- 剩余工作现在已经进入里程碑2之后的阶段，而不是里程碑2未完成内容

### 9. 已补充 Public RPC 与 Indexer 验证

在第2周主要文档整理完成后，又进行了额外的一轮验证，用于关闭里程碑2中与 proposal 最相关的两个开放点。

该轮验证确认了：

- 使用 `https://testnet.ckb.dev/rpc` 的公共测试网 RPC 示例
- 使用 `get_indexer_tip` 的本地 indexer health check
- 使用 `https://testnet.ckb.dev/indexer` 的公共测试网 indexer health check

因此，这两个部分现在不再只停留在概念性表述，而是已经具备实际测试过的示例。

## 本周的验证处理方式

里程碑2第2周的文档整理继续遵守本仓库既有的验证规则。

这意味着：

- 只有在仓库已有验证证据的情况下才复用精确命令
- 概念性与工作流类章节在扩展时没有捏造未经支持的 setup 步骤
- public RPC 与 indexer 示例只在拿到直接验证输出后才被加入
- 对于更广泛的安装路径或更后期 provider 覆盖，仍然保留清晰的验证边界

## 对照第2周范围的结果

里程碑2第2周已经成功交付：

- indexer setup 文档
- first developer workflow 文档
- common errors and remediation 文档
- troubleshooting matrix 文档
- AI-assisted debugging 指导
- CKB mental model 指导
- common misconceptions 指导
- 反映里程碑2完成状态的顶层范围更新
- 与 proposal 入门范围一致的已验证 public RPC 与 indexer 示例

里程碑2现在应被视为一个文档里程碑，已经完成。

## 里程碑3剩余范围

在里程碑2之后，剩余范围将转入里程碑3活动，而不再属于未完成的里程碑2内容。

后续范围应重点放在：

- 最终润色与细化
- 所需的翻译工作
- 发布准备
- 在更广泛发布前需要完成的最后验证整理
