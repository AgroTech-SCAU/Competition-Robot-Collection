# 项目规划

> `Competition-Robot-Collection` 是比赛机器人导航仓库，不承担具体机器人功能开发

## 当前定位

- **类型：** Competition Robot Hub / Collection
- **职责：** 维护比赛机器人索引、比赛归属、公共资产入口、仓库边界和后续建仓规则
- **当前阶段：** 2026 比赛机器人拆分整理已基本完成，进入长期维护阶段

## 2026 项目清单

| 机器人 | 比赛 | 仓库 | 状态 |
| --- | --- | --- | --- |
| SteerWheel Mk.1 | 中国机器人及人工智能大赛（机器人应用赛·智慧农业赛项） | `Competition-Robot-2026-Mk.1` | 已独立维护 |
| Atlas | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | `Competition-Robot-2026-Atlas` | 开发中 |
| Hephaestus | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | `Competition-Robot-2026-Hephaestus` | 开发中 |

## 已完成

- [x] 建立 `Competition-Robot-Collection`
- [x] `SteerWheel Mk.1` 独立为 `Competition-Robot-2026-Mk.1`
- [x] `Atlas` 独立为 `Competition-Robot-2026-Atlas`
- [x] `Hephaestus` 独立为 `Competition-Robot-2026-Hephaestus`
- [x] 三个项目根 README 已改为各机器人专属说明
- [x] 大型机械模型独立维护在 `Competition-Robot-2026-Model-Collection`
- [x] 公共电控能力明确向 `Embedded-Electronic-Control-Standard` 收敛
- [x] Collection README 改为项目清单和导航入口
- [x] 增加 `docs/repository-map.md`，明确多仓边界
- [x] 明确 2026 比赛归属：Mk.1 对应中国机器人及人工智能大赛；Atlas / Hephaestus 对应睿抗机器人大赛智械争锋赛道
- [x] 原多车型总仓停止作为新功能开发入口

## 后续维护

- [ ] 新机器人或新比赛确定后更新 Collection 项目表
- [ ] 机器人仓库改名、归档或职责变化后同步更新链接
- [ ] 公共机械模型新增车型后同步更新 Collection
- [ ] 成熟的重复 `device / domain / infra` 能力继续迁移到公共 SDK
- [ ] 公共 SDK 升级时保持项目使用固定 tag / commit，并完成回归验证

## 长期规则

- 新比赛机器人默认创建独立 `Competition-Robot-<year>-<name>` 仓库
- 同一机器人跨比赛且软件主线一致时，不因比赛名称重复建仓
- Collection 只维护导航与关系，不重新变成 monorepo
- 公共机械模型进入对应 Model Collection
- 公共嵌入式模块进入 `Embedded-Electronic-Control-Standard`
- Collection 与机器人仓库之间只使用普通链接；只有真实代码依赖才考虑 submodule
- 项目仓库固定经过验证的公共 SDK tag / commit，不直接追公共仓库 `main`

## 验收状态

- [x] Collection 首页可以直接找到三台 2026 比赛机器人
- [x] Collection 首页明确标注每台机器人的比赛归属
- [x] Collection 首页可以找到公共机械模型与公共电控标准仓库
- [x] 三个机器人项目拥有独立根 README
- [x] 新成员可以通过文档判断新代码应进入 Collection、机器人项目还是公共仓库
