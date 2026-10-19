# collaborative-work

一个帮助人和 AI 一起推进任务的协作技能（skill）：先把重要取舍说清楚，再按已授权的范围执行。适合需求还模糊、你不熟悉相关领域，或复杂任务需要人来作关键决定的场景。

你不必先填完需求问卷。助手先消化已有背景，解释少量有意义的选择，给出有条件的建议，每轮聚焦一个关键决定。普通协作模式下，明确的小任务直接处理。

这是一个**早期可用版本**，将根据真实使用继续迭代。技能包已完成结构、链接和字节检查；这些不等于实际装载、行为改善或完整的跨宿主验证。

## 先看它怎样协作

以下是示意对话，不是实测结果：

> 你：我想给工作室做个网站，但不知道要有哪些页面。
>
> 助手：先看访客来这里要做什么。服务介绍帮助人判断你是否合适；作品展示帮助人了解风格和能力；直接交易还需要考虑商品、付款和售后。如果你现在主要想接到合适的咨询，我建议先围绕服务介绍和联系入口讨论。访客看完之后，你最希望他做哪件事？

回答后，再讨论依赖这个决定的内容。若你只是说“把现有页面标题改成预览版”，就直接做这个小改动，不重新访谈。

“这个计划可以”确认方向；“请按这个范围开始”或清楚的具体任务请求可以授权相应工作。已经获得的本轮授权继续有效，不每一步重复询问。暂定、暂留和计划认可不自动扩大范围，也不自动授权实验或发布。

## 开始一次普通协作或团队协作

安装后，在 Codex 中可显式提及 `$collaborative-work`；也可由助手按技能描述发现它。其他宿主使用其实际支持的技能入口。

普通协作可以这样开场：

```text
请用 collaborative-work 帮我梳理这个想法。我不熟悉这个领域，先解释眼前最重要的选择和主要代价，给一个有条件的建议，再一起确定下一轮范围。
```

需要主控专门负责方向和沟通时，可以启用团队模式：

```text
这轮启用团队编排：主控负责方向、分派、审阅代理证据和综合结论，把检索、实现与必要验证交给代理。沿用我已指定的角色、模型和思考强度；其余按当前宿主实际能力选择。明确要求无法满足时先告诉我，不静默替换。
```

团队模式下，小任务也可只交给一名执行者，不额外组队或增加审批。启用后沿用约定，直到你调整或关闭。角色职责与模型选择分开；它不自动改变当前主会话模型，也不授予实验权限。详情见[团队编排模式](dist/collaborative-work/references/team-orchestration.md)。

## 安装到 Codex

选一种方式即可。其他助手需使用其支持的技能目录和安装工具，不保证同一命令或路径通用。

### 手动复制完整技能目录

1. 在本仓库页面选择 **Code → Download ZIP** 并解压，或克隆本仓库。
2. 从仓库根目录找到 `dist/collaborative-work/`，把**整个目录**复制到 Codex 用户级技能目录：Windows 为 `%USERPROFILE%\.agents\skills\collaborative-work`，macOS/Linux 为 `~/.agents/skills/collaborative-work`。
3. 检查目标目录：应同时有 `SKILL.md`、`references/`、`agents/` 和 `LICENSE.superpowers`，不能只复制 `SKILL.md`。

只给某个项目使用时，也可放到该项目的 `.agents/skills/collaborative-work/`。目录依据见 [Codex 官方技能文档](https://developers.openai.com/codex/skills)。

如果已有同名目录，先停止复制，检查现有版本和本地修改。Agent 安装时应停止并说明，不自动覆盖或搬走已有目录。

### 把这段请求交给 Agent

Codex 可优先使用内置 `$skill-installer`。下面的 URL 精确指向本技能子目录，不会要求安装整个仓库：

```text
请用当前可用的 $skill-installer 安装这个确切的 GitHub skill 子目录：
https://github.com/souleastforest/noema-harness-engineering-collection/tree/main/dist/collaborative-work

只安装 collaborative-work，保留完整目录中的 references、agents 和许可证；不安装 Matt 或 Superpowers，不运行实验。如果已有同名目标目录，先停止并告知，不覆盖。完成后报告实际安装位置，并提示如何刷新会话加载。
```

安装器管理自己的目标位置，未必与手动目录相同。其他 Agent 若没有这个工具，可使用其确实具备的安装能力，或按上面的手动步骤操作；不要把 `$skill-installer` 当作所有宿主都有的命令。

### 确认加载与以后更新

Codex 通常会检测技能变更。安装后可在新回合提及 `$collaborative-work`；若没有出现，或仍沿用旧上下文，开新会话或重启宿主。文件存在只说明安装内容就位，实际是否装载、是否改善协作，仍需观察使用结果。

更新时从同一来源取得完整技能目录，先比较现有版本和本地修改；明确确认更新范围后，再备份旧版并更新。内置安装器遇到已有目标会停止，不是自动覆盖更新器。

## 暂时不安装，也可以阅读本地指引

如果助手能读取本地文件，可以把下面的“本地仓库路径”替换成下载或克隆的位置：

```text
请读取 <本地仓库路径>/dist/collaborative-work/SKILL.md，并按其中流程协助当前任务。仅在需要时读取它链接的参考文件，按我已授权的范围工作，不安装依赖或试跑实验。
```

这种方式供当前任务按文件指引协作，不会自动注册为已安装技能。

## 想了解更细的工作方式

- [技能入口](dist/collaborative-work/SKILL.md)：共同决策、授权、分轮执行、改意与有限收尾。
- [设计讨论适配](dist/collaborative-work/references/brainstorming-dialogue.md)：怎样补足背景、筛选路线、分段回放并判断是否足够继续。
- [协作情境与来源](dist/collaborative-work/references/collaboration-patterns.md)：清楚小任务、陌生领域和中途改意的简短例子。
- [Matt 执行接入](dist/collaborative-work/references/matt-execution.md)：可选的规格驱动执行，包含真实入口、依赖、整份规格范围和停止能力检查。

## 能力边界与来源

这份技能提供协作指引，实际检索、实现、委派和验证依赖当前宿主的能力。团队模式需要可用的代理委派能力；明确指定的模型或思考强度无法使用时，应报告限制，不静默替换。它不能仅凭文件检查保证实际行为或产物质量。

讨论行为兼容性改编了 Superpowers `brainstorming`，适配方法已包含在技能包中，无须安装原版 Superpowers。随包的 [LICENSE.superpowers](dist/collaborative-work/LICENSE.superpowers) 保留 MIT 许可及 Jesse Vincent 的版权声明；这不构成给整个仓库新增统一许可证。

Matt `implement-spec` 是可选外部执行入口，仍需核对用户环境中的实际依赖，并由用户显式触发。普通协作不依赖这条链，本项目不会自动安装 Matt、Superpowers 或启动实验。

可以先选一个真实的小任务使用，再根据实际对话与产物判断哪些规则帮助了选择、授权和交付。
