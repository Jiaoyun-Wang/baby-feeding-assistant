# baby-feeding-assistant

面向 0–2 岁宝宝家庭的 Codex Skill，用于记录每日喂养、判断食材与月龄适配、生成辅食菜单，并提醒过敏、噎食及常见喂养风险。

> 本 Skill 提供一般性喂养信息和记录辅助，不能替代儿科医生、营养师或急救服务，不进行医学诊断，也不提供药物建议。

## 主要能力

- 整理每日奶量、辅食量、宝宝反应及新食材记录
- 根据月龄、过敏史和已尝试食材判断食材是否适合
- 生成单日或一周辅食菜单，并标注新食材与观察事项
- 对疑似过敏、呕吐、腹泻、皮疹和噎食风险进行分级提醒
- 在用户明确要求时生成菜单图、计划图或食材说明图
- 保存前明确征得同意；默认只在当前对话中临时整理记录

## Skill 结构

```text
baby-feeding-assistant/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── feeding-profile.md
    ├── output-templates.md
    └── safety-rules.md
```

## 安装

### 方法一：让 Skill Installer 从 GitHub 安装

在 Codex 中调用 `$skill-installer`，并让它从本仓库安装：

```text
使用 $skill-installer 从以下 GitHub 仓库安装 baby-feeding-assistant：
https://github.com/Jiaoyun-Wang/baby-feeding-assistant
```

### 方法二：手动安装为个人 Skill

下载或克隆本仓库，将整个目录放到：

```text
$HOME/.agents/skills/baby-feeding-assistant
```

Codex 通常会自动检测 Skill 变化；如果没有出现，请重启 Codex。

也可以把 Skill 放到项目的 `.agents/skills/baby-feeding-assistant`，仅供该项目使用。安装与目录规则请参考 [OpenAI 官方 Build skills 文档](https://learn.chatgpt.com/codex/build-skills)。

## 使用

可以显式调用：

```text
使用 $baby-feeding-assistant，帮我判断 8 个月宝宝能不能吃三文鱼。
```

也可以直接描述需求；当请求与 Skill 的适用范围匹配时，Codex 可以自动调用它。

### 第一次使用建议提供

- 宝宝实际月龄；早产宝宝必要时提供矫正月龄相关信息
- 已知过敏和曾经出现的疑似食物反应
- 已尝试食材
- 当前能接受的食物形态，例如泥、碎末、软条状
- 奶喂养情况及家长的制作时间、忌口或偏好

不要提供身份证件号、详细住址等与喂养建议无关的敏感信息。

## 示例

### 判断食材

```text
使用 $baby-feeding-assistant。宝宝 7 个半月，没有已知过敏，吃过米粉、鸡蛋黄、南瓜和西兰花，现在可以吃牛肉吗？
```

### 生成一周菜单

```text
使用 $baby-feeding-assistant。宝宝 10 个月，对鸡蛋过敏，已经吃过牛肉、猪肉、鳕鱼和常见蔬菜。请安排下周一到周日的辅食，做法尽量控制在 20 分钟内。
```

### 整理喂养记录

```text
使用 $baby-feeding-assistant。今天 8:00 喝配方奶 180 ml，12:00 吃南瓜牛肉粥约半碗，没有明显不适。请帮我整理记录。
```

Skill 会先整理记录，再询问是否需要持久保存；只有明确同意并存在可用保存位置时才会写入。

### 异常反应

```text
使用 $baby-feeding-assistant。宝宝第一次吃某种食物后出现皮疹，我现在应该怎么做？
```

若宝宝出现呼吸困难、面唇舌肿胀、意识异常、皮肤发青或疑似严重噎食，应立即停止喂食并联系当地急救服务，不要等待在线回复。

## 工具说明

涉及食材安全、月龄适配、过敏风险或异常反应时，Skill 会优先使用可用的联网检索能力进行核验；涉及“今天、本周、下周”等表达时，会确认日期和时区；只有用户明确要求图片时才调用图片生成能力。

如果指定工具不可用，Skill 不会假装已经查询或生成，而会说明限制并采取保守的降级方案。

## 重要安全提醒

- 未满 12 月龄不吃蜂蜜
- 不提供整颗坚果及其他高噎食风险形态
- 避免高盐、高糖、成人重口味调味和未充分加热的食物
- 宝宝进食时应坐直、保持清醒，并由成人近距离持续看护
- 曾对某种食物出现可疑反应时，不要自行在家再次挑战，先咨询儿科医生或过敏专科

