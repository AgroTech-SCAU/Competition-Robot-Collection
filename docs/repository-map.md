# Competition Robot Repository Map

本文档定义 AgroTech-SCAU 比赛机器人仓库之间的职责边界，目标是让机器人项目独立迭代，同时把真正可复用的能力沉淀为公共资产

## 1. 总体结构

```text
AgroTech-SCAU/
│
├── Competition-Robot-Collection
│   └── 比赛机器人导航、关系说明、建仓规范
│
├── Competition-Robot-2026-Mk.1
│   └── SteerWheel Mk.1 独立项目
│
├── Competition-Robot-2026-Atlas
│   └── Atlas 独立项目
│
├── Competition-Robot-2026-Hephaestus
│   └── Hephaestus 独立项目
│
├── Steering-Wheel-Chassis-Model-Collection
│   └── 大型机械模型与历史机械资产
│
└── Embedded-Electronic-Control-Standard
    └── 公共电控标准与 infra / domain / device SDK
```

## 2. Collection 的边界

Collection 是 Hub，不是 monorepo，也不是所有项目的 Git submodule 聚合仓

Collection 可以保存：

- 项目清单
- 项目简介与状态
- 项目演化关系
- 公共仓库入口
- 命名和拆分规则
- 迁移记录

Collection 不保存：

- 任意机器人的完整源码副本
- ROS workspace
- MCU 固件工程
- 地图与比赛运行配置
- 大型机械模型
- 为了“方便下载”而嵌入的项目 submodule

## 3. 独立机器人仓库的边界

每个机器人仓库应能够独立回答以下问题：

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

不要求统一保留旧仓中的机器人名称一级目录；完成迁移后，可按项目自身需要逐步把真正的项目内容提升到仓库根目录

## 4. 公共 SDK 的边界

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
└── serial arm / other reusable models

device
├── bus motor
├── bus servo
├── IMU
├── remote receiver
└── RGB / common peripherals
```

不要为了消除项目内所有源码而强行公共化；与某台机器人硬件强绑定、接口还不稳定的代码，可以先留在项目内，验证成熟后再上移

## 5. 依赖规则

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

## 6. 新项目命名

默认：

```text
Competition-Robot-<year>-<robot-name>
```

原则：

- 一个独立比赛机器人 / 明确整机项目对应一个仓库
- 同一台机器人跨多个比赛但软件主线相同，不必按比赛重复建仓
- 软件体系已经明显分叉、生命周期独立时，再拆为新项目仓库
- Collection 只增加链接，不增加项目代码目录

## 7. 当前迁移状态

| 项目 | 独立仓库 | 状态 |
| --- | --- | --- |
| SteerWheel Mk.1 | `Competition-Robot-2026-Mk.1` | 已拆分 |
| Atlas | `Competition-Robot-2026-Atlas` | 已拆分 |
| Hephaestus | `Competition-Robot-2026-Hephaestus` | 已拆分 |
| 公共机械模型 | `Steering-Wheel-Chassis-Model-Collection` | 已独立 |
| 公共电控标准 / SDK | `Embedded-Electronic-Control-Standard` | 已独立，持续迁移复用资产 |

## 8. 当前遗留整理

三个独立机器人仓库目前仍可见从旧总仓迁移留下的根 README / 路径描述，因此下一阶段建议按项目逐一做轻量清理：

```text
Competition-Robot-2026-Mk.1
    → README 只描述 Mk.1

Competition-Robot-2026-Atlas
    → README 只描述 Atlas

Competition-Robot-2026-Hephaestus
    → README / 内部命名只描述 Hephaestus
```

清理时以“路径整理 + 文档修正”为主，不应为了目录好看而一次性重写已验证的运行代码
