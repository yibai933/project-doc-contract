# 文档地图（docs/）

> 🔒 **本目录不对外**：`docs/` 属于项目「对内层」，永不进入发布目录。发布根出现 `docs/`、`*.sh`、`*.json`、`README`、`.env*` 即判越界（清理法见发布边界战例）。
> 渐进式披露：每篇短文，这里做索引。按主题下钻，不必通读。

## 维护规则
- 文件命名：`NN-英文/拼音主题.md`（两位序号便于排序）。
- 单篇 >250 行 → 拆 `主题-a.md` / `主题-b.md` 或子目录。
- 链接用相对路径，保证任意 Markdown 渲染器可跳转。
- 现状快照（表数/RPC 数/页面数等）标查询时间。
- 沟通产物（决策单/验收清单/修改意见）进 `decisions/` 或 `acceptance/`，用日期前缀命名，不在项目根散落。

## 文档索引

| 文件 | 内容 |
|------|------|
| [01-architecture.md](01-architecture.md) | 技术架构、云服务配置、访问控制、现状快照 |
| [02-release.md](02-release.md) | 发版流程、CDN 行为、版本号规则、自检清单 |
| [03-frontend.md](03-frontend.md) | 加载顺序、核心层、页面注册契约、页面清单 |
| [04-database.md](04-database.md) | 表清单、关键表字段、安全缺口、备份约定 |
| [05-rpc.md](05-rpc.md) | RPC 聚合函数清单与用途 |
| [06-biz-rules.md](06-biz-rules.md) | 业务口径唯一权威（收益/消耗/余额公式、名词表） |
| [07-data-pipeline.md](07-data-pipeline.md) | 数据流、抓取、导入、清洗规则 |
| [08-pitfalls.md](08-pitfalls.md) | 踩坑总表（CDN/前端/数据库/数据/平台/排查） |
| [09-roadmap.md](09-roadmap.md) | 待办与已知限制 |
| [changelog/](changelog/README.md) | 每日变更时间线 |

## 沟通产物（沟通过程产出，不对外）
决策单 / 验收清单 / 修改意见 统一进这两个子目录，不要散落在项目根，与规格文档分离。

| 目录 | 内容 | 不覆盖什么 |
|---|---|---|
| [decisions/](decisions/) | 决策单、修改意见、方案对比（如批次修复决策单、反馈修改记录） | 现行口径 → 01~09 |
| [acceptance/](acceptance/) | 验收清单（线上/批次验收，可 html 带勾选持久化） | 版本详情 → changelog |

## 现状快照（查询时间：YYYY-MM-DD HH:MM）
- 表：__ 张 ｜ RPC：__ 个 ｜ 页面：__ 个 ｜ 成员：__ 人
- 最近发版版本号：`<版本>`

## PRD 归档
大 PRD 移入 [prd/](prd/README.md) 只读归档，不在 docs 根堆积。
