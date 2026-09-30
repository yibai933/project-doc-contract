# AGENTS.md · <项目名> 强制契约

> 本项目任何代码改动前，必须先读此文件并遵守以下核心不变量。
> 违反任一条即视为破坏项目，须立即停下修正。

## 核心不变量（Core Invariants）

1. <不变量1：可验证、违反会出事、可拦。例：发版必须用路径级版本号，禁止用 ?v= 刷新缓存>
2. <不变量2>
3. <不变量3>
...
（建议 8–15 条，收敛到最致命的硬约束；软约定不要混进来）

0. <发布边界（有发布动作的项目必放第一条）：发布根只放 `index.html` + `assets/`；`AGENTS.md`/`README`/`CHANGELOG`/`docs/`/`scripts/`/快照/凭据/备份 一律放项目根，绝不进发布根。同名目录（项目/docs/ vs 发布根/docs/）是最大陷阱，靠本条兜底。战例与清理法见 references/publish-boundary.md>

## 目录地图（两层，先画边界）

<项目根>/                  ← 🟦 对内层（开发侧，不发布）
├── AGENTS.md             ← 本文件
├── README.md / CHANGELOG.md
├── docs/                 ← 🔒 全部规格文档（不对外）
│   ├── decisions/        ← 💬 决策单 / 修改意见 / 方案对比
│   └── acceptance/       ← ✅ 验收清单（可 html 带勾选）
├── scripts/              ← 数据管道脚本
└── 快照 / 备份 / .env*    ← 测试桩、备份、凭据，全在对内层
<发布根>/                  ← 🟥 对外层（只放用户要加载的最小集合）
├── index.html
└── assets/               ← JS/CSS/图片（源码在对内层改，这里是发布产物）

## 改动↔文档强制对照表

| 改动类型 | 必须同步的文档 | 必须写 changelog |
|----------|----------------|------------------|
| 改发版流程 / 版本号 | `docs/02-release.md` | ✅ |
| 改前端核心层 | `docs/03-frontend.md` | ✅ |
| 改数据库表 / RPC | `docs/04-database.md` / `docs/05-rpc.md` | ✅ |
| 改业务口径 | `docs/06-biz-rules.md` | ✅ |
| 改数据流 / 导入 | `docs/07-data-pipeline.md` | ✅ |
| 任何踩坑 | `docs/08-pitfalls.md` | 视影响 |
| 新增页面 / 接口 | `docs/03-frontend.md` + README 索引 | ✅ |

**纪律**：改完即同步文档 + 写 changelog，「以后补」不被接受——文档契约是核心不变量。
