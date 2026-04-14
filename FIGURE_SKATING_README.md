# 花样滑冰计分计算器

## 项目概述

基于HarmonyOS ArkTS开发的花样滑冰计分计算器应用,实现了ISU(国际滑冰联盟)官方评分系统。

## 功能特性

### 1. 技术分计算
- 支持所有跳跃动作(1周至4周)
  - Toe Loop (后外点冰)
  - Salchow (后内结环)
  - Loop (后外结环)
  - Flip (后内点冰)
  - Lutz (后外点冰)
  - Axel (前外点冰)

- 支持旋转动作
  - Upright Spin (直立旋转)
  - Sit Spin (蹲转)
  - Camel Spin (驼转)
  - Layback Spin (弓身旋转)

- 支持步法序列
  - Step Sequence Level 1-4

### 2. GOE评分系统
- 9位裁判评分机制
- GOE范围: -5 到 +5
- 自动去掉最高分和最低分
- 计算平均GOE值

### 3. 评分计算规则
- 基础分值 + GOE调整分 = 最终得分
- GOE调整分 = 平均GOE × 基础分值 × 0.1
- 支持多个动作累加计算总分

## 文件结构

```
entry/src/main/ets/
├── pages/
│   ├── MainPage.ets              # 主页面(计算器选择)
│   ├── HomePage.ets              # 普通计算器页面
│   └── FigureSkatingPage.ets     # 花样滑冰计分页面
├── viewmodel/
│   ├── SkatingScoreModel.ets     # 评分数据模型
│   ├── SkatingViewModel.ets      # 花样滑冰视图模型
│   ├── PressKeysItem.ets         # 按键数据模型
│   └── PresskeysViewModel.ets    # 按键视图模型
└── common/
    ├── constants/
    │   └── CommonConstants.ets   # 公共常量
    └── util/
        ├── ScoreCalculator.ets   # 评分计算工具
        ├── CalculateUtil.ets     # 计算工具
        ├── CheckEmptyUtil.ets    # 空值检查工具
        └── Logger.ets            # 日志工具
```

## 使用说明

### 启动应用
1. 应用启动后显示主页面
2. 选择"花样滑冰计分"进入计分页面

### 计分流程
1. **选择动作**: 从动作列表中选择要评分的动作
2. **查看基础分值**: 系统自动显示该动作的基础分值
3. **输入GOE评分**: 为9位裁判输入GOE评分(-5到+5)
4. **添加动作**: 点击"添加动作"将当前动作加入列表
5. **计算总分**: 所有动作添加完成后,点击"计算总分"

### 示例
- 选择动作: 3Lz (三周Lutz跳)
- 基础分值: 5.90
- 裁判GOE: +2, +3, +2, +1, +2, +3, +2, +2, +1
- 平均GOE: 2.0 (去掉最高分3和最低分1)
- GOE调整分: 2.0 × 5.90 × 0.1 = 1.18
- 最终得分: 5.90 + 1.18 = 7.08

## 技术实现

### 核心算法
```typescript
// GOE计算
averageGOE = calculateAverage(goeScores)
goeValue = averageGOE * baseValue * 0.1
finalScore = baseValue + goeValue

// 平均值计算(去掉最高最低分)
sorted = sort(goeScores)
trimmed = sorted[1:-1]  // 去掉首尾
average = sum(trimmed) / length(trimmed)
```

### 数据模型
- `SkatingScore`: 单个动作评分数据
- `JudgeScore`: 裁判评分数据
- `ProgramComponent`: 节目内容分数据
- `CompetitionResult`: 完整比赛成绩数据

## 扩展功能

### 未来可添加功能
1. 节目内容分(Program Components)计算
   - 滑行技术 (Skating Skills)
   - 动作衔接 (Transitions)
   - 表演/执行 (Performance/Execution)
   - 编舞/构成 (Choreography/Composition)
   - 音乐诠释 (Interpretation of the Music)

2. 扣分项计算
   - 跌倒扣分
   - 时间违规扣分
   - 音乐违规扣分

3. 数据导出功能
   - 导出PDF成绩单
   - 导出Excel数据表

4. 历史记录功能
   - 保存比赛记录
   - 查看历史成绩

## 开发环境

- HarmonyOS SDK
- ArkTS语言
- DevEco Studio

## 版本信息

- 版本: 1.0.0
- 更新日期: 2024
- 开发者: 基于SimpleCalculator项目扩展

## 许可证

Apache License 2.0
