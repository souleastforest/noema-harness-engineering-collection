# 接入 Matt 规格驱动执行

准备按规格执行或用户指定 Matt 时读本页。接入已存在的原版链，不在本技能内重新实现它；普通小任务和其他已授权流程无需为此扫描依赖。

## 先找到真实入口

先看本会话可用技能与宿主登记；不足时，再按需查项目、用户级技能目录及插件登记，使用当前宿主的真实路径，不扫描全机。同名技能不代表来源正确，缓存里有文件也不代表宿主或子代理能调用。

核对入口的完整名称或路径、来源、版本、调用策略及实际依赖。以下以固定研究版 `49dd158d1076134a641b33efb035946536778336` 为依据；已装版本不同，先读它的实际合同，不能假定兼容。读取元数据仅证明查到文件，不证明已装载或运行。

固定版 `implement-spec` 标记 `disable-model-invocation: true`，调用规则禁止其他技能通过 Skill tool 调用人工触发技能。因此本接入是“检查 → 准备最小交接 → 用户亲自在当前宿主显式触发原版”，助手不代为调用。用户若已在当前请求明确触发这个真实入口，则沿用，不重复请批。使用核实过的完整入口名或路径；`/implement-spec <spec>` 只是上游示例，不据此猜当前宿主的命令前缀。

## 核对这一轮真正需要的条件

- **技能可用：**固定版需要 `implement-spec`、`tdd`、`code-review`，且 `tdd` 安装文档要求 `codebase-design` 已安装。确认四件可用、安装完整，子代理也能调用所需技能。`codebase-design` 的实际调用取决于接口或测试 seam 形状是否待定；沿用已确认的公共接口和测试边界，不每轮强制重新设计。已装版本另有声明依赖时核对实际要求。关键未决先解决，技术配置由助手消化，不让用户逐项审批。
- **已有输入：**复用权威 spec、带阻塞关系的全部 ticket graph、tracker 配置及本轮授权和验收指针。固定版按 `docs/agents/issue-tracker.md` 解析 tracker，具体以已装版本为准。`to-spec`、`to-tickets`、`setup` 不是每轮必跑；不为接入自动生成新规格、票据、配置或安装。
- **执行与验证：**核对实际链所需的后台子代理、每票 git worktree、集成分支与 merge、tracker 读写能力；仅检查会走到的分支所需能力，不机械重复无关检查。gitignored 的本地 fixtures、数据库或凭据不会随 worktree 带走，必须已有合适且获授权的验证安排；不复制凭据，不声称已在 worktree 验证未发生的行为。
- **自动动作与授权：**tracker 可能关闭票据；PR-closing flow 会在首个 merge 后开 draft PR，末尾标为 ready。merge、cleanup 及这些外部写入分别核对当前授权，不能从普通实施许可或一次入口调用外推。依赖缺失就明说，不自动安装或配置。

## 完整规格和控制边界都通过，才交接

原版完成 **entire spec 和全部 ticket graph**，最终审查也面向整份规格。只有现成、完整且自足的 spec 恰好匹配本轮授权，才可传给它。较大 spec 的一部分不能靠选中 tickets 冒充 subset，也不能自行扩授权或另造一份 spec 来绕过此门。

范围不匹配时，说明差异并停下 Matt 分支；已有流程中独立且获授权的受限工作可继续。用户特意指定必须用 Matt 时，停下这部分并带回问题，不静默换执行链。

原版没有完整的改意暂停、分轮决策与修后定向复核机制。交接前，确认当前宿主能实际打断或取消相关 worker，并阻止未授权的后续 merge、tracker 和 PR 动作。不能维持停止、改意或范围边界，就不交给这条链；“预计不用中途决策”不能替代终止能力。

若链要求的自动动作或全局修复与本轮边界冲突，须能实际约束才可进入；无法约束就停止此路由。交接文字不会改变原版能力。用户决策和新取舍仍由主助手按已约定节奏统一带回；Matt 返回后，主助手按本轮目标做有限必要的定向复核，剩余阻塞带回，不无限修复，也不将原版自报完成当作验证通过。

## 给用户一段可随入口提交的交接

引用已有材料即可，无需另建文件。以下占位内容须指向真实输入和已核实的控制安排：

```text
规格/全部票据：【完整 spec 与 ticket graph 指针】；tracker：【既有配置】。
本轮授权及验收：【指针】，覆盖完整规格；接口和验证安排：【已有材料】。
沿用【决策节奏、暂停与改意边界】；宿主可通过【实际方式】取消相关 worker，并阻止后续 merge/tracker/PR。
外部动作仅限【已有授权】；未授权动作已由【实际控制】阻止。阻塞时回主助手，不扩范围。
```

依赖缺失时可以直接说明：“当前宿主未提供 implement-spec/tdd，未启动 Matt 执行；不自动安装。不受影响且已授权的工作可继续。”用户指定 Matt 时，明确哪些部分正在等待，不暗中换链。

## 固定来源

只用于核对本页依据；实际运行合同以核实过的已装版本为准：

- [implement-spec 技能](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/skills/engineering/implement-spec/SKILL.md)
- [implement-spec 执行说明](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/docs/engineering/implement-spec.md)
- [技能调用规则](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/.agents/invocation.md)
- [tdd 技能](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/skills/engineering/tdd/SKILL.md)
- [tdd 安装前提](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/docs/engineering/tdd.md#L210-L212)
