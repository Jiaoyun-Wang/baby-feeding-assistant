# 宝宝档案与喂养记录

这是可选的最小数据结构。默认只在当前对话中临时维护；只有用户明确同意并指定可用存储目标后才持久保存。

## 宝宝档案

```yaml
baby_profile:
  profile_id: "由存储系统提供；不要使用证件号"
  birth_date: null
  gestational_age_at_birth_weeks: null
  corrected_age: null
  feeding_method: null
  allergies: []
  suspected_reactions: []
  tried_foods: []
  disliked_foods: []
  dietary_preferences: []
  texture_stage: null
  notes: null
  updated_at: null
```

只有早产或确需评估矫正月龄时才收集出生孕周。不要索取与任务无关的姓名、证件号、住址等信息。

## 单条喂养记录

```yaml
feeding_record:
  profile_id: null
  occurred_at: null
  timezone: null
  milk:
    type: null
    amount_ml: null
  complementary_foods:
    - food: null
      amount: null
      texture: null
      preparation: null
      is_new: null
  reactions:
    observed: null
    onset: null
    symptoms: []
    duration: null
  notes: null
  source: "user_reported"
```

未知字段保留为 `null` 或显示“未提供”，不可根据常识补写。只有档案内没有该食材且用户确认此前未吃过时，才将 `is_new` 标为 `true`。

## 疑似反应记录

```yaml
suspected_reaction:
  suspected_foods: []
  eaten_at: null
  amount: null
  reaction_started_at: null
  symptoms: []
  duration: null
  action_taken: null
  medical_advice_received: null
```

该结构只记录事实，不写“确诊过敏”。医生明确诊断后，才在用户要求下更新 `allergies`。

## 保存确认

保存前简要复述：目标档案、记录日期、食材、奶量/辅食量、反应及新食材标记。保存后报告实际目标；若没有存储工具或写入失败，明确说未保存，并提供可复制的数据。

