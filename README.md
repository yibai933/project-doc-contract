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

## 如何触发（关键词）

在 WorkBuddy 里，当你说出以下任意意图，技能会被自动唤起（也支持英文 `project doc contract` / `AGENTS.md` / `progressive disclosure docs`）：

- 「建立项目文档架构」/「项目开始时搭文档骨架（文档地基）」
- 「写 AGENTS.md」/「写强制契约」
- 「整理 / 治理项目文档」
- 「拆分大文档」/「渐进式披露」
- 「补 changelog」/「补变更日志」
- 「把文档做法沉淀成规范」
- 「区分对外发布内容与对内文档」/「docs 不进发布目录」/「立发布边界」

> 简单记：凡是涉及「项目文档怎么管、怎么不丢、怎么和对内/对外分层」的诉求，直接说就行，技能会按工作流推进。

## 新项目 vs 老项目怎么用

### 🟢 新项目（从第一天就有契约）

1. **先画发布边界**：明确对外层最小集合（通常 `index.html` + `assets/`），把「发布根只放对外交付物、`docs/` 与脚本/凭据绝不进发布根」定为第一条不变量。
2. **建骨架**：仓库根建 `AGENTS.md` + `CHANGELOG.md`，建 `docs/` + `docs/README.md`。
3. **边开发边写**：每定下一块设计就写一篇 `docs/NN-主题.md`；每次提交/发版写一条 `docs/changelog/YYYY-MM-DD.md`。
4. **固化习惯**：把「改代码前先读 AGENTS.md」「改完即同步文档」写进系统约定/提示，让契约自动生效。

> 对应 `SKILL.md` 的 **Phase 0.5 → Phase 1~4**。

### 🟡 老项目（零文档 / 文档过期，补课）

1. **先摸清真实状态**，别凭记忆写文档：用 MCP / 云数据库工具查表数/行数/RLS/GRANT、读实际代码、跑命令拿真实版本号；引用数字一律带「查询时间」。
2. **先查发布边界是否已被打破**：`curl` 发布域名下的 `README` / `docs/` / `*.sh` / `*.json` / `.env*`，若 200 返回真文件即已泄露，按 `references/publish-boundary.md` 清理并登记 P0。
3. **从真实状态提炼不变量**，建 `AGENTS.md`；把大 PRD 移入 `docs/prd/` 归档并写差异表。
4. **倒推补写**近几天的 `docs/changelog/`，`CHANGELOG.md` 做总览，再进入日常同步节奏。

> 对应 `SKILL.md` 的 **Phase 0（老项目补课）** + `references/workflow.md` 的 **B 路径**。

**共同铁律**：改动↔文档对照表里「改 X 必须同步 Y + 写 changelog」不是建议，而是核心不变量——文档契约的价值就在于「绕过不了」。

## 更新流程（从 GitHub 同步回本地技能目录）

本仓库是技能本体。你改完 GitHub 上的内容后，需要把它同步回**本地技能目录**才能生效。三种同步方式，按你的情况选：

### 方式 A：一次性 clone + 手动复制（最简单，适合偶尔更新）

```bash
# 1. 拉到任意临时目录
git clone https://github.com/yibai933/project-doc-contract.git /tmp/pdc

# 2. 覆盖到本地技能目录
#    WorkBuddy 用户：
rm -rf ~/.workbuddy/skills/project-doc-contract
cp -R /tmp/pdc ~/.workbuddy/skills/project-doc-contract
#    其他 agent / 框架：复制到对应技能目录，例如
#    cp -R /tmp/pdc <你的-agent-技能目录>/project-doc-contract

# 3. 版本号对齐（关键）
#    本地技能目录里的 SKILL.md frontmatter `version` 必须与本次 Release 标签一致：
#    version: 1.1.1  ↔  git tag v1.1.1
```

> 注意：方式 A 是整目录覆盖，`~/.workbuddy/skills/project-doc-contract` 里你自己加的本地修改会被清掉。若你在该目录做过定制，先 `diff` 再手动 merge。

### 方式 B：git pull 增量更新（你已在本地留了仓库）

如果你之前已经把仓库 clone 到了某个固定目录（如 `~/Documents/project-doc-contract`），以后只增量拉取：

```bash
cd ~/Documents/project-doc-contract
git pull origin main
# 再按方式 A 第 2 步把更新复制进技能目录
```

### 方式 C：submodule / subtree（适合把技能作为子项目嵌进你的主仓库）

- **submodule**：`git submodule add https://github.com/yibai933/project-doc-contract.git <主仓库>/skills/project-doc-contract`，更新时 `git submodule update --remote`。
- **subtree**：`git subtree add --prefix skills/project-doc-contract https://github.com/yibai933/project-doc-contract main --squash`，更新时 `git subtree pull --prefix ... main --squash`。

> subtree / submodule 同步的是仓库本身，要让 agent 真正用上，技能目录仍需指向这个子目录（或软链过去）。

### 版本号约定

- 每次发布新版本：先 `git commit` + `git push`，再打 `git tag vX.Y.Z`，标签与 `SKILL.md` frontmatter 的 `version` 字段必须一致。
- 改了发布边界 / 沟通产物结构这类**会影响他人项目**的内容，务必升级次版本号（如 1.1.0 → 1.1.1）并写进 `changelog/`。
- 本地技能目录的 `version` 若落后于标签，说明没同步到位，按上面方式 A/B 重同步即可。

## 文件导航

- `SKILL.md` — 技能主文件（工作流 + 发布边界原则）
- `references/agents-contract-guide.md` — AGENTS.md 写法 + 不变量实战范例
- `references/workflow.md` — 详细步骤、拆分原则、维护纪律
- `references/publish-boundary.md` — 发布边界战例（同名占位覆盖清理）+ 暴露探测手法
- `assets/templates/` — 可直接复制的 AGENTS.md / docs-README / changelog-README / CHANGELOG / 架构骨架

## License

MIT
