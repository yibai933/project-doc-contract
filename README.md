# project-doc-contract

为软件项目建立「**AGENTS.md 强制契约 + docs/ 渐进式披露文档架构 + changelog**」的文档治理体系，并先立「发布边界」把对外交付物与对内文档在建立文档时就分开。

> 灵感来自宝玉老师的项目 doc 管理经验：把文档维护纳入开发的「核心不变量」，用渐进式披露把大文档拆成小文件 + 链接。

## 解决什么问题

- 文档「事后补」永远补不上 → 改成开发的**核心不变量**，违反即拦。
- 大文档堆成单块难维护 → `docs/` 渐进式披露，每篇短文 + 索引。
- 内部文档 / 脚本 / 凭据混进发布目录被公网抓到 → 先立**发布边界**（对外层 vs 对内层）。

## 三件套

1. **AGENTS.md**（仓库根，不发布）：核心不变量 + 改动↔文档对照表。
2. **docs/**（不发布）：按主题拆小文件，`docs/README.md` 做地图；含 `decisions/`（决策单 / 修改意见）、`acceptance/`（验收清单）、`changelog/`、`prd/`。
3. **changelog/**：每次发版写一条 `docs/changelog/YYYY-MM-DD.md`，`CHANGELOG.md` 做总览。

## 发布边界（重点）

任何要发布的项目，写第一篇文档前先画「两区图」：

| 层 | 放什么 | 公网可见 |
|---|---|---|
| 对外层（发布根） | `index.html` + `assets/` | ✅ |
| 对内层（项目根） | AGENTS / README / CHANGELOG / docs / scripts / 快照 / 凭据 / 备份 | ❌ |

发布根只允许 `index.html` + `assets/`；`docs/` 与脚本 / 凭据 / 备份绝不进发布根。同名目录（`项目/docs/` vs `发布根/docs/`）是最大陷阱，靠一条不变量兜底。战例与清理手法见 `references/publish-boundary.md`。

## 目录结构

```
<项目根>/
├── AGENTS.md
├── README.md
├── CHANGELOG.md
├── docs/
│   ├── README.md
│   ├── 01-architecture.md … 09-roadmap.md
│   ├── changelog/
│   ├── prd/
│   ├── decisions/   # 决策单 / 修改意见 / 方案对比
│   └── acceptance/  # 验收清单（可 html 带勾选）
└── scripts/
<发布根>/
├── index.html
└── assets/
```

## 安装 / 使用

- **WorkBuddy 用户**：复制到 `~/.workbuddy/skills/project-doc-contract/`（或经技能市场安装），在新项目开局时调用本技能。
- **其他**：参考 `SKILL.md` 工作流（Phase 0 → 0.5 → 1~4），或直接复制 `assets/templates/` 下的模板到你的项目。

## 文件导航

- `SKILL.md` — 技能主文件（工作流 + 发布边界原则）
- `references/agents-contract-guide.md` — AGENTS.md 写法 + 不变量实战范例
- `references/workflow.md` — 详细步骤、拆分原则、维护纪律
- `references/publish-boundary.md` — 发布边界战例（同名占位覆盖清理）+ 暴露探测手法
- `assets/templates/` — 可直接复制的 AGENTS.md / docs-README / changelog-README / CHANGELOG / 架构骨架

## License

MIT
