# Mei Component Rules

这些规则是跨端组件语义规范，不绑定任何具体平台 API。实现时必须用对应平台语法映射 token，不能硬编码视觉值。

## 全局原则

- 组件只组合 token，不发明颜色、圆角、阴影、间距、字号。
- 组件规范只描述语义、状态和行为，不描述任何平台专属 API 或业务专属语法。
- `*.base` 是该色轴默认入口，等价于对应主色阶；需要明暗层级时必须使用 `*.scale.*`。
- **严格遵循完整 Token 路径**：必须包含文件名前缀且对齐 JSON 物理路径（如 `color.primary.scale.500`, `typography.size.base`, `border-radius.scale.lg`）。
- **[theme] 映射规则**：
  - **颜色 (`color.json`)**：`[theme]` 映射为 `light.` 或 `dark.`。
  - **阴影 (`shadow.json`)**：`[theme]` 在浅色模式下映射为 `scale.`，深色模式下映射为 `dark.`。AI 写作：`light` → `shadow.scale.*`，`dark` → `shadow.dark.*`。
  - **其他属性**：若无浅深色区分，则不使用 `[theme]`。
- 语义色（semantic）只用于表达状态，不替代品牌色或结构色。
- 除 token 源文件外，组件规则不得出现固定数值尺寸；需要尺寸时使用 token、比例、密度或内容关系描述。
- `border-radius.scale.none` 只用于无圆角的分割线、表格网格、贴边容器，不作为默认容器圆角。

## 颜色轴 (Color Axes) 专有场景

- **Primary (Indigo-Violet)**: 核心品牌色。用于全局主导航、主操作按钮 (PrimaryButton)、激活态边框、进度条。
- **Blue Axis (blueAxis)**: 信息与工具色。专门用于链接 (Links)、次要工具栏 (Toolbar/Secondary Actions)、数据展示 (Charts/Data Tables)。
- **Purple Axis (purpleAxis)**: 装饰与强调色。专门用于标签 (Tag/Badge)、高亮标识、插画装饰背景、Avatar 默认背景。

---

## Button

### Button Behavior Constraints

- 同一操作组中只能有一个 PrimaryButton。
- SecondaryButton / TertiaryButton 不得使用高饱和度填充色。
- 窄屏主要操作默认使用容器宽度；宽屏主要操作按内容或布局需要决定宽度。
- 工具按钮、图标按钮、短命令按钮不强制通栏。
- 禁止同一操作组混用 primary / blueAxis / purpleAxis 作为同等级按钮颜色。
- 按钮组按重要性排序：Primary → Secondary → Tertiary；危险操作与普通主操作不能同时争夺视觉焦点。
- 加载中按钮保持原位置和尺寸语义，不因文案变化造成布局跳动。
- 禁用按钮使用 neutral 低对比样式，不使用透明度叠加代替语义状态。

### PrimaryButton
- background: color.primary.scale.500
- text/icon: [theme].text.inverse
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.xl
- typography: typography.size.base + typography.fontWeight.semibold

### SecondaryButton
- background: [theme].bg.elevated
- text/icon: color.primary.scale.500
- border: [theme].border.default
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg

### TertiaryButton
- background: transparent
- text/icon: color.blueAxis.scale.600
- radius: border-radius.scale.md
- padding: spacing.semantic.inset.sm + spacing.semantic.inline.md

### Link
- text/icon: [theme].text.link
- typography: typography.size.base
- background: transparent
- radius: border-radius.scale.none
- 用于导航、外链、文本内跳转；不作为主要操作按钮。

---

## Form Controls

### Input
- background: [theme].bg.surface
- text: [theme].text.primary
- border: [theme].border.default
- focus border: color.primary.scale.500
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg
- 错误、提示、说明文本放在输入区下方或附近，使用 typography.size.sm / typography.size.xs + [theme].text.secondary；错误色使用 color.semantic.error.base。
- 长输入内容默认可滚动或截断，不撑开表单主布局。

### Switch / Checkbox / Radio
- active background: color.primary.scale.500
- inactive background: [theme].bg.elevated
- checkmark/dot: [theme].text.inverse
- border (inactive): [theme].border.strong
- radius (Checkbox): border-radius.scale.sm
- radius (Switch/Radio): border-radius.scale.full

### Select / Dropdown
- background: [theme].bg.elevated
- border: [theme].border.default
- radius: border-radius.scale.lg
- shadow: shadow.scale.md ~ shadow.dark.md
- typography: typography.size.base

---

## Navigation & Feedback

### NavBar
- background: color.primary.scale.500
- text/icon: [theme].text.inverse
- radius: border-radius.scale.xl
- padding: spacing.semantic.inset.lg ~ spacing.semantic.inset.xl
- typography: typography.size.2xl/3xl

### Tabs / SegmentedControl
- background: [theme].bg.surface
- active indicator: color.primary.scale.500 / [theme].bg.elevated
- text (active): color.primary.scale.600
- text (inactive): [theme].text.secondary
- radius: border-radius.scale.lg
- 同一组 tab 只用一个激活态；未激活项不得使用品牌高饱和填充。
- tab 用于同层视图切换，不用于提交、保存、删除等动作。

### Toast / Snackbar
- background: [theme].text.primary (反转色)
- text: [theme].text.inverse
- radius: border-radius.scale.md
- shadow: shadow.scale.lg ~ shadow.dark.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg
- 只承载短反馈，不承载长说明、表单或多操作。
- 成功/失败反馈优先使用状态图标和短文本，不创建大面积语义色背景。

### Loading / Spinner / Skeleton
- spinner color: color.primary.scale.500
- skeleton background: [theme].bg.surface
- skeleton shimmer: [theme].bg.elevated
- animation: motion.duration.normal + motion.easing.easeInOut

---

## Data Display

### Card
- background: [theme].bg.elevated
- border: [theme].border.default
- radius: border-radius.scale.lg
- shadow: shadow.scale.sm ~ shadow.dark.sm
- padding: spacing.semantic.inset.lg
- Card 用于承载一个明确主题；不得把多个无关区块塞进同一 Card。
- Card 内部只允许一个主视觉焦点；次要信息使用 [theme].text.secondary/tertiary。
- 嵌套 Card 默认禁止；需要分组时优先用 spacing、标题、divider。

### ActionGroup
- 只能包含一个 PrimaryButton。
- 2-3 个操作时：Primary + Secondary/Tertiary；超过 3 个操作时折叠低频操作。
- 同组按钮高度、圆角、字体语义一致，靠颜色和填充区分层级。
- 图标按钮必须有明确点击区域和可理解图标；不使用装饰图标代替操作反馈。

### Avatar
- background: color.purpleAxis.scale.100
- text: color.purpleAxis.scale.700
- border: [theme].bg.page (作为描边)
- radius: border-radius.scale.full

### Badge / Tag
- background: color.purpleAxis.scale.50
- text: color.purpleAxis.scale.700
- radius: border-radius.scale.full
- padding: spacing.semantic.inset.xs + spacing.semantic.inline.sm
- Badge / Tag 只表达标签、状态、计数或轻量分类，不作为主要操作入口。
- 同一容器内 Badge 数量过多时折叠或弱化，避免抢占主内容。

### StatusMessage (Inline)
- success: color.semantic.success.base
- warning: color.semantic.warning.base
- error: color.semantic.error.base
- info: color.semantic.info.base
- background (light): color.semantic.[status].light
- radius: border-radius.scale.md
- 状态提示可用 semantic 色，但状态容器边框默认不使用 semantic 色，除非是强告警。
- 状态提示不替代页面标题或主操作。

### LongText / CodeBlock
- 用于链接、哈希、日志、路径、ID、JSON、系统生成文本。
- 默认限制高度或行数，提供展开/复制能力。
- background: [theme].bg.surface
- text: [theme].text.primary
- border: [theme].border.default / none
- radius: border-radius.scale.md
- padding: spacing.semantic.inset.md
- typography: typography.fontFamily.mono + typography.size.sm
- 禁止让长文本直接撑开主要布局。
- 默认视觉权重低于用户内容、状态标题和主操作。
- 复制、展开、查看详情等操作使用 TertiaryButton 或图标按钮。

### Media / Preview
- 图片、视频、图表预览必须有稳定比例，避免加载后推动布局。
- 媒体内容优先保留主体，不使用无意义裁切制造装饰感。
- 媒体上的播放、放大、关闭等浮层操作使用中性半透明背景，不引入新的品牌色。

---

## Layout & Structures

### Dialog / Sheet
- background: [theme].bg.elevated
- radius (Dialog): border-radius.scale.xl
- top radius (Sheet): border-radius.scale.2xl
- shadow: shadow.scale.2xl ~ shadow.dark.2xl
- Dialog 用于需要用户明确决策的中断任务；普通反馈用 Toast/StatusMessage。
- 操作区遵循 ActionGroup：一个 Primary，其余降级。
- 内容过长时内部滚动，底部操作区保持可见。

### List / Menu / Divider
- divider color: [theme].border.default
- item hover background: [theme].bg.surface
- menu radius: border-radius.scale.lg
- list spacing: spacing.semantic.stack.sm
- 列表项主信息、辅助信息、状态信息必须有明确层级。
- 可点击列表项使用 hover/pressed/focus 状态，不靠大面积品牌色区分。
- Divider 只在高密度或边界不清时使用，不能替代空间分组。

### EmptyState
- icon: color.neutral.scale.400
- title: typography.size.lg + typography.fontWeight.semibold + [theme].text.primary
- body: typography.size.base + [theme].text.secondary
- action: PrimaryButton
- EmptyState 只保留一个建议操作；其他说明保持弱化。
- 图标使用 neutral 或低饱和品牌色，不使用强语义色制造误导。

---

## 禁止项
- **禁止使用简写路径**：必须包含文件名（如 `typography.`）和完整物理层级（如 `.scale.`）。
- **禁止硬编码色值**：必须通过 token 路径引用（如 `color.primary.scale.500`、`[theme].text.primary`），禁止直接使用 `#FFFFFF`、`rgb()` 等具体色值。
- **禁止混用色轴**：同一组操作严禁混用 Primary 和 BlueAxis。
- **禁止自创圆角**：必须从 `border-radius.scale` 中选择。
- **禁止业务绑定**：不得规定某业务动作固定使用某个色轴。
- **禁止平台绑定**：不得把某平台组件名或框架 API 当作规范内容。
