<div align="center">

# Competition-Robot-Collection

</div>

> AgroTech-SCAU 比赛机器人项目导航仓库
>
> 本仓库用于统一索引协会比赛机器人、比赛归属、公共模型与公共开发资产，不存放具体机器人的整机源码

---

## 1. 仓库定位

`Competition-Robot-Collection` 是 AgroTech-SCAU 比赛机器人项目的统一入口，主要负责：

- 导航各比赛机器人的独立项目仓库
- 记录机器人对应比赛、项目定位与演化关系
- 统一指向公共机械模型、电控标准与 SDK 等共享资产
- 约定后续比赛机器人的建仓方式，避免重新形成超大型总仓

本仓库 **不保存**：

- MCU / ROS2 / 视觉 / 导航等具体机器人源码
- SolidWorks、STL 等大型机械模型源文件
- 某一台机器人的地图、标定结果、比赛参数与运行配置

以上内容分别维护在对应机器人项目仓库或公共资产仓库中

---

## 2. 2026 比赛机器人

| 机器人 | 比赛 | 项目仓库 | 定位 | 状态 |
| --- | --- | --- | --- | --- |
| SteerWheel Mk.1 | 中国机器人及人工智能大赛（机器人应用赛·智慧农业赛项） | [`Competition-Robot-2026-Mk.1`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Mk.1) | 初代四舵轮 + 五自由度机械臂原型，承担底盘、电控、机械臂一体化与比赛方案验证 | 独立维护 / 原型平台 |
| Atlas | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | [`Competition-Robot-2026-Atlas`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Atlas) | 在 Mk.1 基础上发展出的自主轮式机器人，包含 MCU、Pi ROS2、导航、视觉、机械臂与比赛任务链路 | 开发中 / 全自主主线 |
| Hephaestus | 2026 睿抗机器人开发者大赛 · 智械争锋赛道 | [`Competition-Robot-2026-Hephaestus`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Hephaestus) | 独立的中型舵轮机器人项目，包含 MCU、ROS2、导航、视觉、机械臂、语音与比赛任务链路 | 开发中 / 全自主主线 |

> 三台机器人已经分别独立建仓；具体功能开发、Issue、PR、Release 与实车资料均进入对应项目仓库，本 Collection 只维护索引与关系

---

## 3. 公共资产

### 3.1 比赛机器人机械模型

[`Competition-Robot-2026-Model-Collection`](https://github.com/AgroTech-SCAU/Competition-Robot-2026-Model-Collection)

用于集中维护 2026 比赛机器人相关的大型机械模型与机械源文件，当前主要包含：

- SteerWheel Mk.1
- Atlas

比赛项目仓库原则上只保留运行必需的轻量描述资产；完整 SolidWorks 等大型机械源文件优先放入模型合集仓库

### 3.2 嵌入式电控标准与 SDK

[`Embedded-Electronic-Control-Standard`](https://github.com/AgroTech-SCAU/Embedded-Electronic-Control-Standard)

用于维护协会公共嵌入式分层标准与可复用 SDK：

```text
sdks/
├── infra/
├── domain/
└── device/
```

新比赛机器人需要公共电机、舵机、IMU、PID、运动学等能力时，应优先复用或完善公共 SDK，而不是在每个机器人项目中长期复制独立版本

项目需要固定使用公共 SDK 时，推荐通过 `external/` submodule 锁定经过验证的 tag 或 commit

---

## 4. 当前仓库体系

```text
AgroTech-SCAU/
│
├── Competition-Robot-Collection
│   └── 比赛机器人导航、比赛归属、仓库关系与建仓规则
│
├── Competition-Robot-2026-Mk.1
│   └── 中国机器人及人工智能大赛机器人项目
│
├── Competition-Robot-2026-Atlas
│   └── 睿抗机器人大赛 · 智械争锋赛道机器人项目
│
├── Competition-Robot-2026-Hephaestus
│   └── 睿抗机器人大赛 · 智械争锋赛道机器人项目
│
├── Competition-Robot-2026-Model-Collection
│   └── 比赛机器人机械模型与大型机械资产
│
└── Embedded-Electronic-Control-Standard
    └── 公共电控标准与 infra / domain / device SDK
```

更完整的职责边界见 [`docs/repository-map.md`](docs/repository-map.md)

---

## 5. 项目关系

### SteerWheel Mk.1

初代四舵轮机器人原型，主要用于中国机器人及人工智能大赛，同时承担舵轮底盘、五自由度机械臂、自研电控和手动任务方案验证

### Atlas

在 Mk.1 基础上继续发展，加入 ROS2、Pi 通信桥、导航定位、视觉、任务状态机等能力，当前面向睿抗机器人开发者大赛智械争锋赛道的全自主任务

### Hephaestus

与 Atlas 分别作为独立机器人项目维护，同样面向睿抗机器人开发者大赛智械争锋赛道，拥有自己的 MCU、Pi、视觉、语音与任务执行链路

公共能力不再通过复制某一台机器人的目录继承，而应逐步沉淀到公共模型仓或公共标准 / SDK 仓库中

---

## 6. 新比赛机器人建仓规则

以后新增比赛机器人时，默认直接创建独立仓库，不在 Collection 中新增整机源码目录

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
├── firmware/        # MCU / embedded，可选
├── ros2_ws/         # ROS2 系统，可选
├── vision/          # 独立视觉资产，可选
├── config/          # 整机运行配置，可选
├── docs/
└── external/        # 公共 SDK / 外部依赖，可选
```

目录应服从项目实际需要，不要求所有机器人机械套用完全一致的结构

### 优先沉淀到公共仓库

- 两个及以上机器人都会使用的设备驱动或算法
- 与具体比赛任务无关的基础能力
- 接口能够稳定定义的 `infra / domain / device` 模块
- 大型、跨项目复用的机械模型资产

### 留在机器人项目仓库

- 比赛状态机与任务逻辑
- 本车硬件装配和 platform 绑定
- 本车 ROS2 bringup 与任务后端
- 地图、导航点、视觉 ROI、标定结果等本车配置
- 本车特有执行器、机构与实验逻辑

---

## 7. 拆分结果

原多车型总仓已完成项目级拆分，当前形成：

```text
Competition-Robot-Collection           # 只做导航
Competition-Robot-2026-Mk.1           # 独立机器人项目
Competition-Robot-2026-Atlas          # 独立机器人项目
Competition-Robot-2026-Hephaestus     # 独立机器人项目
Competition-Robot-2026-Model-Collection # 公共机械模型
Embedded-Electronic-Control-Standard  # 公共电控标准 / SDK
```

后续不再建立“一仓多车”的比赛机器人总仓模式

---

## 8. 当前状态

- [x] 建立比赛机器人 Collection 导航仓库
- [x] Mk.1、Atlas、Hephaestus 分别独立建仓
- [x] 三个独立项目根 README 已切换为机器人专属说明
- [x] 机械模型独立为 `Competition-Robot-2026-Model-Collection`
- [x] 公共电控能力明确向 `Embedded-Electronic-Control-Standard` 收敛
- [x] 明确 2026 三台机器人的比赛归属
- [x] 原多车型总仓停止作为新功能开发入口
- [ ] 后续按实车验证情况继续把成熟的重复 `device / domain / infra` 能力迁移到公共 SDK
- [ ] 新比赛项目出现时持续更新本 Collection 的项目索引与比赛信息

---

## 9. 协作

本仓库主要修改项目索引、比赛信息和仓库关系，仍遵循协会统一流程：

**Issue → Branch → Commit → Push → Pull Request → Merge**

协作说明见 [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md)

具体机器人的代码问题请在对应机器人项目仓库创建 Issue，不要集中提交到 Collection
