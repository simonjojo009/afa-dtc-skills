# Codex 技能安装验证报告

验证日期：2026-11-05。对象：`simonjojo009/afa-dtc-skills`（用户指定的 `afadtc/afa-dtc-skills` Fork），本地基线提交 `e4edb28`。

## 结论与范围

已满足 Codex 仓库级技能发现的目录与元数据要求：31 个模块各自位于 `.agents/skills/<name>/SKILL.md`，且均有匹配目录名的 `name` 和非空 `description` frontmatter。所有模块以真实目录完整复制，不依赖符号链接。原始 `skills/` 和作者其他文件保持不变。

这是文件系统层的安装验证，不等同于当前会话已重新加载技能。新建以本仓库为工作目录的 Codex 任务，检查技能列表中出现全部 31 项，并用 `$afa` 显式调用一次，才能确认客户端实际发现及调用。当前会话无法触发或证明宿主的技能索引刷新。既有会话可能需要重新打开。

## 已执行验证

- 源模块数 31，目标模块数 31，目标 `SKILL.md` 数 31；未复制工具目录为技能。
- 330 个文件的相对路径集合及文件内容逐字节一致；包括 references、scripts、Hub 的完整 `_system` 和其他资源。
- 检查 Markdown 中反引号路径及链接目标：829 处在源模块树中确实存在的显式相对路径，在目标位置仍然存在，未发现复制引入的断链。该范围不包含任意自然语言、运行时占位符或动态拼接路径，不宣称所有文本都是可执行链接。
- 模块保持同级布局，因此 `../afa/_system/…`、跨模块 references 以及模块内部 scripts 路径保持有效。
- 文中 `scripts/build_inject.py` 等工程维护说明指向原始 `skills/scripts/` 工具，不是模块运行依赖；工程工具和 evals 保留在原目录。需要维护时从仓库根目录使用 `skills/scripts/...` 和 `skills/evals/...`，不要在安装副本内执行注入命令。
- 7 个 Python 脚本均通过 AST 静态语法解析；本次未执行任何仓库业务脚本、未读取真实业务数据、未操作广告账户或网站，也未运行发布流程。

## 脚本风险检查

复制范围内只有 7 个 Python 脚本，使用 Python 标准库。已检查导入、调用及文件访问：未发现 HTTP 客户端、外部命令执行、动态 eval/exec、删除文件或写文件操作。

| 脚本 | 行为与使用注意 |
| --- | --- |
| `afa/_system/scripts/memory_manager.py` | 只读指定 JSONL 记忆文件；会向标准输出打印筛选后的记忆，应仅使用授权数据。 |
| `afa-dashboard/scripts/metrics_snapshot.py` | 只读指定订单 CSV 并输出聚合指标；订单及输出可能敏感，不应上传真实数据作为安装测试。 |
| `afa-aov/scripts/promo_breakeven.py` | 参数计算并输出促销盈亏数据。 |
| `afa-convert/scripts/ab_sample_size.py` | 参数计算并输出 A/B 样本量。 |
| `afa-expand/scripts/landed_cost.py` | 参数计算并输出关税落地成本。 |
| `afa-ops/scripts/unit_economics.py` | 参数计算并输出单位经济指标。 |
| `afa-payments/scripts/vamp_check.py` | 参数计算并输出 VAMP 指标，不连接支付账户。 |

静态检查有范围限制，不能保证未来修改后的代码行为。技能正文包含 Brand Brain 文件写入和业务执行指导；安装不会执行这些指令，后续使用仍须遵守用户授权边界。

## 模块清单

“原模块无此目录”表示作者未提供，并非复制缺失。Hub 的记忆脚本位于 `_system/scripts/`，已完整保留。

| 模块 | SKILL.md | 文件数 | references/ | scripts/ |
| --- | --- | ---: | --- | --- |
| `afa` | 是 | 22 | 是 | 原模块无此目录 |
| `afa-aov` | 是 | 14 | 是 | 是 |
| `afa-brand` | 是 | 13 | 是 | 原模块无此目录 |
| `afa-compete` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-convert` | 是 | 13 | 是 | 是 |
| `afa-creative` | 是 | 18 | 是 | 原模块无此目录 |
| `afa-cx` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-dashboard` | 是 | 11 | 是 | 是 |
| `afa-diagnose` | 是 | 10 | 是 | 原模块无此目录 |
| `afa-email` | 是 | 11 | 是 | 原模块无此目录 |
| `afa-expand` | 是 | 15 | 是 | 是 |
| `afa-explore` | 是 | 13 | 是 | 原模块无此目录 |
| `afa-fb` | 是 | 13 | 是 | 原模块无此目录 |
| `afa-foundation` | 是 | 1 | 原模块无此目录 | 原模块无此目录 |
| `afa-geo` | 是 | 11 | 是 | 原模块无此目录 |
| `afa-gg` | 是 | 13 | 是 | 原模块无此目录 |
| `afa-influencer` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-launch` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-monetize` | 是 | 1 | 原模块无此目录 | 原模块无此目录 |
| `afa-ops` | 是 | 12 | 是 | 是 |
| `afa-organic` | 是 | 1 | 原模块无此目录 | 原模块无此目录 |
| `afa-paid` | 是 | 1 | 原模块无此目录 | 原模块无此目录 |
| `afa-payments` | 是 | 5 | 是 | 是 |
| `afa-pr` | 是 | 10 | 是 | 原模块无此目录 |
| `afa-product` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-retain` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-scale` | 是 | 1 | 原模块无此目录 | 原模块无此目录 |
| `afa-seo` | 是 | 14 | 是 | 原模块无此目录 |
| `afa-sms` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-social` | 是 | 12 | 是 | 原模块无此目录 |
| `afa-tt` | 是 | 11 | 是 | 原模块无此目录 |

## 维护与审核

`git diff --cached --check` 检出复制文件中作者原有的行尾空白和文件末尾空行。为保证逐字节完整复制，本次保留这些格式，不将该检查描述为通过；它们不影响技能目录发现。

本次改动仅新增 `.agents/skills/` 和本报告，无合并、部署或外部业务变更。副本不会自动同步：未来更新作者 `skills/` 后，应审阅差异，再更新对应副本并重新验证文件一致性与路径，避免两个版本漂移。

本地安装不需要额外依赖或凭据。此前环境设置阶段 GitHub 代理连接失败；本报告针对当前本地 checkout，未验证其与远端最新版本一致，也未声称已创建远端 PR。
