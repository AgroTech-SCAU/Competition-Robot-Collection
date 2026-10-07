<div align="center">

# Competition-Robot-Collection

</div>

> AgroTech-SCAU 比赛机器人项目导航仓库
>
> 本仓库只负责汇总比赛机器人项目、公共资产与仓库关系，不再存放具体机器人的整机代码

---

## 1. 仓库定位

`Competition-Robot-Collection` 是协会比赛机器人项目的统一入口，主要用于：

- 导航各届比赛机器人的独立项目仓库
- 记录机器人之间的继承与演化关系
- 统一指向公共机械模型、电控标准与 SDK 等共享资产
- 约定后续比赛机器人的建仓方式，避免再次形成超大型总仓

本仓库 **不保存**：

- MCU / ROS / 视觉 / 导航等具体项目源码
- SolidWorks、STL 等大型机械模型
- 某一台机器人的运行配置、地图、标定结果或比赛参数

这些内容应分别维护在对应机器人项目仓库或公共资产仓库中

---

## 2. 当前比赛机器人

| 机器人 | 项目仓库 | 定位 | 当前状态 |
| --- | --- | --- | --- |
| SteerWheel Mk.1 | [`Competition-Robot-2026-Mk.1`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Mk.1) | 初代四舵轮 + 五自由度机械臂原型，用于验证底盘、电控与机械臂一体化方案 | 历史原型 / 技术资产保留 |
| Atlas | [`Competition-Robot-2026-Atlas`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Atlas) | 在 Mk.1 基础上发展出的中型自主轮式机器人，包含 MCU、Pi ROS2、导航、视觉、机械臂与比赛任务链路 | 2026 主力比赛平台 |
| Hephaestus | [`Competition-Robot-2026-Hephaestus`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Hephaestus) | 从原总仓独立出的另一套比赛机器人项目，当前代码包含 MCU、ROS2、导航、视觉/作业后端等整车链路 | 已拆分 / 独立维护 |

> 三个项目已从原 `Steering-Wheel-Chassis` 大仓拆分为独立仓库；后续功能开发、Issue、PR 和 Release 均应进入对应项目仓库，本 Collection 不再承载机器人源码开发

---

## 3. 公共资产

### 3.1 机械模型

[`Steering-Wheel-Chassis-Model-Collection`](https://github.com/AgroTech-SCAU/Steering-Wheel-Chassis-Model-Collection)

用于集中保存体积较大的车辆机械模型，目前主要包含：

- SteerWheel Mk.1
- Atlas

比赛项目仓库原则上只保留运行必需的轻量描述资产；完整 SolidWorks 等机械源文件优先放入模型合集仓库

### 3.2 嵌入式电控标准与 SDK

[`Embedded-Electronic-Control-Standard`](https://github.com/AgroTech-SCAU/Embedded-Electronic-Control-Standard)

用于维护协会公共嵌入式分层标准与可复用 SDK：

```text
sdks/
├── infra/
├── domain/
└── device/
```

新比赛机器人需要公共电机、舵机、IMU、PID、运动学等能力时，应优先复用或完善该仓库，而不是在每个比赛项目内继续复制一份公共驱动

项目需要固定使用公共 SDK 时，推荐由项目仓库通过 `external/` submodule 锁定经过验证的 tag 或 commit

---

## 4. 仓库关系

```text
Competition-Robot-Collection
│
├── Competition-Robot-2026-Mk.1
├── Competition-Robot-2026-Atlas
├── Competition-Robot-2026-Hephaestus
│
├── Steering-Wheel-Chassis-Model-Collection
│   └── 公共 / 历史机械模型
│
└── Embedded-Electronic-Control-Standard
    ├── sdks/infra
    ├── sdks/domain
    └── sdks/device
```

更完整的仓库边界和新项目建仓规则见 [`docs/repository-map.md`](docs/repository-map.md)

---

## 5. 演化关系

当前可以将三台机器人的关系理解为：

```text
SteerWheel Mk.1
      │
      │  底盘 / 电控 / 五自由度机械臂原型验证
      ▼
    Atlas
      │
      ├── ROS2 / Pi 通信桥
      ├── 导航与定位
      ├── 视觉与任务状态机
      └── 更完整的自主比赛系统

Hephaestus
      └── 从原总仓独立出的另一条比赛机器人项目线
```

共享能力不再通过复制某一台机器人的目录继承，而应逐步沉淀到公共标准 / SDK 仓库中

---

## 6. 新比赛机器人建仓规则

以后新增比赛机器人时，默认直接创建独立仓库，不再在 Collection 中新增整机源码目录

推荐命名：

```text
Competition-Robot-<year>-<robot-name>
```

例如：

```text
Competition-Robot-2027-Example
```

推荐项目边界：

```text
Competition-Robot-20XX-Name/
├── firmware/        # MCU / embedded
├── ros2_ws/         # ROS2 系统，可选
├── vision/          # 独立视觉资产，可选
├── config/          # 整机运行配置，可选
├── docs/
└── external/        # 公共 SDK / 外部依赖
```

目录应以实际项目需要为准，不要求所有机器人机械套用完全一致的结构

### 应拆为公共仓库的内容

满足以下条件之一时，优先沉淀到公共仓库：

- 两个及以上机器人都会使用
- 与具体比赛任务无关
- 可以定义稳定、清晰的公共接口
- 设备驱动、基础算法、运动学、协议解析等通用能力

### 应留在机器人仓库的内容

- 比赛状态机和任务逻辑
- 本车硬件装配与 platform 绑定
- 本车 ROS2 bringup
- 地图、导航点、视觉 ROI、标定结果等本车配置
- 本车特有执行器或机构逻辑

---

## 7. 旧总仓迁移说明

原 [`Steering-Wheel-Chassis`](https://github.com/AgroTech-SCAU/Steering-Wheel-Chassis) 曾同时维护多台机器人，随着项目增长出现仓库体积过大、公共代码复制、项目边界不清等问题

当前整理方向为：

```text
旧模式
Steering-Wheel-Chassis/
├── Mk.1/
├── Atlas/
└── Hephaestus/

        ↓ 拆分

新模式
Competition-Robot-Collection       # 只做导航
Competition-Robot-2026-Mk.1       # 独立项目
Competition-Robot-2026-Atlas      # 独立项目
Competition-Robot-2026-Hephaestus # 独立项目
```

后续不应再向旧总仓增加新的比赛机器人主线代码

---

## 8. 当前整理事项

- [x] 建立 `Competition-Robot-Collection`
- [x] Mk.1 拆分为独立仓库
- [x] Atlas 拆分为独立仓库
- [x] Hephaestus 拆分为独立仓库
- [x] Collection 改为项目导航仓库
- [x] 关联公共机械模型仓库
- [x] 关联公共嵌入式标准 / SDK 仓库
- [ ] 清理三个独立项目仓库根 README 中残留的旧总仓描述和路径
- [ ] 根据各项目实际情况继续把重复 `device / domain / infra` 能力迁移到公共 SDK
- [ ] 原 `Steering-Wheel-Chassis` 完成迁移说明后停止承载新功能，是否归档由维护者最终决定

---

## 9. 协作

本仓库主要修改导航信息和仓库关系，仍遵循协会统一开发流程：

**Issue → Branch → Commit → Push → Pull Request → Merge**

协作说明见 [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md)

具体机器人的代码问题请在对应机器人项目仓库创建 Issue，不要集中提交到 Collection
