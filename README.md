# job-screener-engine

通用岗位筛选与评分引擎。对用户提供的岗位进行多维度量化评估（0-100分），输出评分和建议。

## 安装

```bash
npx skills add CalmDownTR/job-screener-engine
```

或者指定技能名称安装：

```bash
npx skills add CalmDownTR/job-screener-engine -s job-screener-engine
```

## 首次使用

配置后会自动通过 AI 引导填写你的求职信息（薪资底线、技术方向、公司偏好等），完成后即可评估岗位。

### 快速开始

告诉 AI：

> "帮我看看这个岗位值不值得投"

提供公司名称和岗位信息，AI 会自动搜索补充信息并进行多维度评分。

## 技能结构

```
skills/job-screener-engine/
├── SKILL.md                        # 技能定义（AI 读取）
├── CHANGELOG.md                    # 版本历史
├── README.md                       # 技能说明
└── references/
    ├── scoring_framework.md        # 评分标准框架
    ├── setup_wizard.md             # 首次配置向导
    ├── user_profile.TEMPLATE.md    # 用户画像模板
    └── info_checklist.md           # 信息收集清单
```

## 核心理念

- **量化代替直觉**：6 个维度、明确评分标准
- **一票否决**：不满足底线的岗位直接标记
- **面试/入职解耦**：即使不建议入职，也可能值得面试练手
- **信息透明**：信息不足的维度诚实标注，不猜测

## 许可

MIT
