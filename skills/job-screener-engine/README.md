# Job Screener Engine — 通用岗位筛选与评分引擎

[![ClawHub](https://img.shields.io/badge/ClawHub-发布-4B44C0)](https://clawhub.ai/CalmDownTR/job-screener-engine)

对用户提供的岗位机会进行结构化评估，输出多维量化评分和行动建议。

---

## 这是什么

这是一个通用 AI Agent 技能（Skill），帮助求职者理性评估工作机会。适用于支持 `npx skills` 标准的各类 AI 编程助手。它通过 6 个维度对岗位进行量化评分（0-100 分），并给出投递建议。

**核心设计理念：**
- 量化代替直觉：每个评分维度都有明确标准，减少主观偏见
- 一票否决：不满足底线的岗位直接标记，节省精力
- 面试/入职解耦：即使不建议入职，也可能值得面试练手
- 信息透明：信息不足的维度诚实标注，不猜测不编造

## 安装

### 方式一：自动安装（推荐）

```bash
# 如果已发布到技能市场
find-skills job-screener-engine
# 按照提示安装即可
```

### 方式二：手动安装

```bash
# 复制到你的技能目录
cp -r job-screener-engine/ ~/.workbuddy/skills/job-screener-engine/
```

## 首次使用（必须配置）

第一次使用前，需要填写你的个人求职信息。有**两种方式**：

### 方式一：AI 引导配置（推荐）

告诉 AI：

> "帮我用 job-screener-engine 看看这个岗位"

AI 会自动检测到没有 `user_profile.md`，然后按以下步骤逐一提问：

```
1. 你叫什么？（可选）
2. 工作年限？
3. 期望城市？
4. Base 薪资底线？
5. 期望薪资？
6. 核心技术方向？（Agent/LLM / 前端 / 后端 / ...）
7. 偏好的公司类型？（大厂 / 外企 / 国企 / 创业 / 不拘）
8. 工作节奏要求？
9. 管理风格偏好？
10. 稳定性要求？
```

完成后自动生成 `references/user_profile.md`。

### 方式二：自行填写

复制模板并编辑：

```bash
cp references/user_profile.TEMPLATE.md references/user_profile.md
# 然后填写所有 [占位符]
```

## 使用

配置完成后，直接告诉 AI：

| 你说 | AI 会做 |
|------|---------|
| "帮我看下这家公司" + 公司名、岗位名 | 搜索信息 → 评分 → 输出报告 |
| "这个岗位值得投吗" + JD 链接 | 解析 JD → 搜索补充 → 评分 |
| "帮我对比这两个机会" + 两个岗位信息 | 分别评分 → 同分排序 → 对比输出 |

### 输出示例

```
## 📋 岗位评估 | XX公司 - AI应用开发工程师

### 基本信息
- 薪资：25K-35K
- 公司规模：B轮 / 200人
- 地点：北京
- 信息来源：用户提供 + 脉脉/看准网搜索补充

### 评分明细

| 维度 | 分值 | 说明 |
|------|------|------|
| 薪资匹配度 | 12/18 | Base 符合期望，略低于最优 |
| 公司规模 | 10/20 | B轮初创，规范度一般 |
| 技术成长 | 12/15 | Agent方向，偏应用层 |
| 工作节奏 | 10/15 | 弹性工作，偶有加班 |
| 稳定性 | 10/20 | B轮融资充足但未盈利 |
| 区域可行性 | 9/12 | 周边租房中等偏上 |
| **总分** | **63/100** | |

### 判定：⚠️ 可以考虑

### 面试练手建议：高价值
岗位与 Agent 方向相关，即使不入职也值得面试积累经验。

### ⚠️ 风险提示
- 融资可维持多久？建议面试时问清楚
- 产品方向是否稳定？
```

## 自定义配置

所有评估参数都通过 `references/user_profile.md` 配置：

| 配置项 | 说明 | 示例 |
|--------|------|------|
| Base 底线 | 最低接受薪资 | 18K |
| Base 期望 | 理想薪资 | 28K |
| 技术方向 | 你的核心赛道 | 后端 / 数据工程 |
| 公司偏好 | 目标公司类型 | 中大厂 / 外企 |
| 工作节奏 | 能接受的强度 | 双休优先 |
| 维度权重 | 各维度重要性 | 可自定义 |
| 一票否决 | 直接跳过的条件 | 996、Base<底线 |
| 同分排序 | 分数相同时的优先级 | 稳定 > 薪资 > 通勤 |

## 文件结构

```
job-screener-engine/
├── SKILL.md                          # 技能主定义（AI 读取）
├── _meta.json                        # 版本元数据
├── README.md                         # 本文件（人类阅读）
├── references/
│   ├── scoring_framework.md          # 评分标准框架
│   ├── setup_wizard.md               # 首次配置向导（AI 使用）
│   ├── user_profile.TEMPLATE.md      # 用户画像模板
│   ├── user_profile.md               # 你的配置（首次使用后生成）
│   └── info_checklist.md             # 信息收集清单（AI 使用）
```

## 发布到市场

本技能已发布到 [ClawHub](https://clawhub.ai/CalmDownTR/job-screener-engine)——OpenClaw 官方技能市场。
WorkBuddy 用户可以直接通过「技能 → SkillHub」搜索安装。

如需自行发布 fork 版本：

```bash
# 安装 ClawHub CLI
npm i -g clawhub

# 登录
clawhub login

# 发布
clawhub publish ./job-screener-engine \
  --slug your-slug \
  --name "Job Screener Engine" \
  --version 1.0.0
```

## 许可

MIT — 自由使用、修改、分享。
