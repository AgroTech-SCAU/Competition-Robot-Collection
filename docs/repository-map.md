# Competition Robot Repository Map

本文档定义 AgroTech-SCAU 比赛机器人仓库之间的职责边界，让机器人项目独立迭代，同时将真正可复用的能力沉淀为公共资产

## 1. 总体结构

```text
AgroTech-SCAU/
│
├── Competition-Robot-Collection
│   └── 比赛机器人导航、比赛归属、关系说明、建仓规范
│
├── Competition-Robot-2026-Mk.1
│   └── SteerWheel Mk.1 / 中国机器人及人工智能大赛
│
├── Competition-Robot-2026-Atlas
│   └── Atlas / 睿抗机器人大赛 · 智械争锋赛道
│
├── Competition-Robot-2026-Hephaestus
│   └── Hephaestus / 睿抗机器人大赛 · 智械争锋赛道
│
├── Competition-Robot-2026-Model-Collection
│   └── 2026 比赛机器人大型机械模型与机械资产
│
└── Embedded-Electronic-Control-Standard
    └── 公共电控标准与 infra / domain / device SDK
```

## 2. 2026 比赛映射

| 机器人 | 比赛 | 独立仓库 |
| --- | --- | --- |
| SteerWheel Mk.1 | 中国机器人及人工智能大赛（机器人应用赛·智慧农业赛项） | `Competition-Robot-2026-Mk.1` |
| Atlas | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | `Competition-Robot-2026-Atlas` |
| Hephaestus | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | `Competition-Robot-2026-Hephaestus` |

比赛归属用于项目导航，不意味着 Collection 承担比赛运行配置；赛场参数、状态机、地图、视觉配置等仍归对应机器人仓库维护

## 3. Collection 的边界

Collection 是 Hub，不是 monorepo，也不是所有项目的 Git submodule 聚合仓

Collection 可以保存：

- 项目清单
- 比赛归属与项目简介
- 项目演化关系
- 公共仓库入口
- 命名和拆分规则
- 历史迁移结果

Collection 不保存：

- 任意机器人的完整源码副本
- ROS workspace
- MCU 固件工程
- 地图与比赛运行配置
- 大型机械模型
- 为了“方便下载”而嵌入的项目 submodule

## 4. 独立机器人仓库的边界

每个机器人仓库应能够独立回答：

1. 这台机器人是什么
2. 用于哪项比赛 / 实验
3. 当前硬件组成是什么
4. 如何安装、编译、启动和验收
5. 哪些代码是本车特有的
6. 使用了哪些公共 SDK / 外部依赖

机器人仓库可以包含：

```text
firmware/
ros2_ws/
vision/
config/
docs/
external/
```

目录只作为推荐边界，不要求为了统一外观强制重构已经验证可运行的项目

## 5. 公共机械模型的边界

`Competition-Robot-2026-Model-Collection` 主要保存：

- SolidWorks 装配体与零件
- 大型 STL / STEP 等机械源资产
- 多项目共享或需要长期归档的机械资料

机器人项目本体只保留软件运行、仿真或可视化真正需要的轻量描述资源

## 6. 公共 SDK 的边界

公共嵌入式能力统一向 `Embedded-Electronic-Control-Standard` 收敛

优先公共化：

```text
infra
├── PID
├── matrix
├── protocol parser
├── HFSM
└── log

domain
├── steer wheel kinematics
└── serial arm / reusable models

device
├── bus motor
├── bus servo
├── IMU
├── remote receiver
└── RGB / common peripherals
```

不要为了消除项目内所有源码而强行公共化；与某台机器人硬件强绑定、接口还不稳定的代码，可以先留在项目内，验证成熟后再上移

## 7. 依赖规则

推荐方向：

```text
Competition Robot Project
        │
        ├── project app / service / config
        ├── project platform / hardware assembly
        │
        └── external/
             └── Embedded-Electronic-Control-Standard
```

项目依赖公共 SDK 时：

- 优先锁定经过真机验证的 tag 或 commit
- 不建议比赛项目直接追标准仓库最新 `main`
- SDK 升级应单独提交并完成回归验证
- 项目特有补丁不要长期复制粘贴，应判断是回馈公共 SDK 还是保留为项目 adapter

## 8. 新项目命名

默认：

```text
Competition-Robot-<year>-<robot-name>
```

原则：

- 一个独立比赛机器人 / 明确整机项目对应一个仓库
- 同一台机器人跨多个比赛但软件主线相同，不必按比赛重复建仓
- 软件体系已经明显分叉、生命周期独立时，再拆为新项目仓库
- Collection 只增加链接，不增加项目代码目录

## 9. 当前拆分状态

| 项目 | 独立仓库 | 状态 |
| --- | --- | --- |
| SteerWheel Mk.1 | `Competition-Robot-2026-Mk.1` | 已完成拆分并独立维护 |
| Atlas | `Competition-Robot-2026-Atlas` | 已完成拆分并独立维护 |
| Hephaestus | `Competition-Robot-2026-Hephaestus` | 已完成拆分并独立维护 |
| 2026 公共机械模型 | `Competition-Robot-2026-Model-Collection` | 已独立维护 |
| 公共电控标准 / SDK | `Embedded-Electronic-Control-Standard` | 已独立维护，持续沉淀复用资产 |

原多车型总仓已退出新功能开发流程；后续新增机器人直接建立独立项目仓库

## 10. 维护原则

Collection 后续只需在以下情况更新：

- 新比赛机器人创建
- 机器人参加比赛发生变化
- 项目仓库改名、迁移或归档
- 公共模型仓 / SDK 仓职责调整
- 仓库体系出现新的公共基础设施

不要因为单个机器人内部目录变化而频繁同步 Collection；内部实现细节由机器人项目自身 README 和 docs 负责
