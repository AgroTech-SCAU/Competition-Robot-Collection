# 项目规划

> `Competition-Robot-Collection` 是比赛机器人导航仓库，不承担具体机器人功能开发

## 当前状态

- **定位：** 比赛机器人项目 Hub / Collection
- **当前目标：** 完成旧 `Steering-Wheel-Chassis` 多车型总仓拆分后的项目导航、公共资产关系和后续建仓规则整理

## 已完成

- [x] 建立 Collection 导航仓库
- [x] `SteerWheel Mk.1` 独立为 `Competition-Robot-2026-Mk.1`
- [x] `Atlas` 独立为 `Competition-Robot-2026-Atlas`
- [x] `Hephaestus` 独立为 `Competition-Robot-2026-Hephaestus`
- [x] 大型机械模型独立维护在 `Steering-Wheel-Chassis-Model-Collection`
- [x] 公共电控能力明确向 `Embedded-Electronic-Control-Standard` 收敛
- [x] README 改为项目清单和导航入口
- [x] 增加 `docs/repository-map.md`，明确多仓边界

## 当前整理

### 项目仓库清理

- [ ] `Competition-Robot-2026-Mk.1` 根 README 改为 Mk.1 专属说明
- [ ] `Competition-Robot-2026-Atlas` 根 README 改为 Atlas 专属说明，并逐步消除旧总仓路径层级
- [ ] `Competition-Robot-2026-Hephaestus` 修正从 Atlas 复制遗留的名称、README 和路径描述

### 旧总仓收尾

- [ ] 原 `Steering-Wheel-Chassis` README 增加迁移说明和三个新项目入口
- [ ] 停止向原总仓加入新功能
- [ ] 确认历史链接与必要资料无遗漏后，再决定是否 Archive

## 长期规则

- 新比赛机器人默认创建独立 `Competition-Robot-<year>-<name>` 仓库
- Collection 只维护导航与关系，不重新变成 monorepo
- 公共机械模型进入模型合集仓库
- 公共嵌入式模块进入电控标准 / SDK 仓库
- 只有代码依赖才使用 submodule；Collection 与机器人仓库之间只使用普通链接
- 项目仓库固定经过验证的公共 SDK tag / commit，不直接追公共仓库 `main`

## 验收条件

- [x] 从 Collection 首页可以直接找到三个独立机器人项目
- [x] 从 Collection 首页可以找到公共机械模型仓库与公共电控标准仓库
- [x] 新成员可以通过文档判断新代码应进入 Collection、机器人项目还是公共仓库
- [ ] 三个独立机器人仓库不再出现误导性的旧总仓根 README
- [ ] 原总仓明确停止作为新功能开发入口
