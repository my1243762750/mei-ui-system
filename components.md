# Mei Component Rules

这些规则是跨端组件语义规范，不绑定 Flutter、Web、iOS 或 Android API。实现时必须用对应平台语法映射 token，不能硬编码视觉值。

## 全局原则

- 组件只组合 token，不发明颜色、圆角、阴影、间距、字号。
- **严格遵循完整 Token 路径**：必须包含文件名前缀且对齐 JSON 物理路径（如 `primary.scale.500`, `typography.size.base`, `border-radius.scale.lg`）。
- **[theme] 映射规则**：
  - **对于颜色 (`color.json`)**：`[theme]` 映射为 `light.` 或 `dark.`。
  - **对于阴影 (`shadow.json`)**：`[theme]` 在浅色模式下映射为 `scale.`，在深色模式下映射为 `dark.`。
  - **对于其他属性**：若无浅深色区分，则不使用 `[theme]`。
- 语义色（semantic）只用于表达状态，不替代品牌色或结构色。

## 颜色轴 (Color Axes) 专有场景

- **Primary (Indigo-Violet)**: 核心品牌色。用于全局主导航、主操作按钮 (PrimaryButton)、激活态边框、进度条。
- **Blue Axis (blueAxis)**: 信息与工具色。专门用于链接 (Links)、次要工具栏 (Toolbar/Secondary Actions)、数据展示 (Charts/Data Tables)。
- **Purple Axis (purpleAxis)**: 装饰与高级色。专门用于标签 (Tag/Badge)、会员特权/高级功能高亮、插画装饰背景、Avatar 默认背景。

---

## Button

### PrimaryButton
- background: primary.scale.500
- text/icon: [theme].text.inverse
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.xl
- typography: typography.size.base + typography.fontWeight.semibold

### SecondaryButton
- background: [theme].bg.elevated
- text/icon: primary.scale.500
- border: [theme].border.default
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg

### TertiaryButton
- background: transparent
- text/icon: blueAxis.scale.600
- radius: border-radius.scale.md
- padding: spacing.semantic.inset.sm + spacing.semantic.inline.md

---

## Form Controls

### Input
- background: [theme].bg.surface
- text: [theme].text.primary
- border: [theme].border.default
- focus border: primary.scale.500
- radius: border-radius.scale.lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg

### Switch / Checkbox / Radio
- active background: primary.scale.500
- inactive background: [theme].bg.elevated
- checkmark/dot: [theme].text.inverse
- border (inactive): [theme].border.strong
- radius (Checkbox): border-radius.scale.sm
- radius (Switch/Radio): border-radius.scale.full

### Select / Dropdown
- background: [theme].bg.elevated
- border: [theme].border.default
- radius: border-radius.scale.lg
- shadow: shadow.[theme].md
- typography: typography.size.base

---

## Navigation & Feedback

### NavBar
- background: primary.scale.500
- text/icon: [theme].text.inverse
- radius: border-radius.scale.xl
- padding: spacing.semantic.inset.lg 到 spacing.semantic.inset.xl
- typography: typography.size.2xl/3xl

### Tabs / SegmentedControl
- background: [theme].bg.surface
- active indicator: primary.scale.500 或 [theme].bg.elevated
- text (active): primary.scale.600
- text (inactive): [theme].text.secondary
- radius: border-radius.scale.lg

### Toast / Snackbar
- background: [theme].text.primary (反转色)
- text: [theme].text.inverse
- radius: border-radius.scale.md
- shadow: shadow.[theme].lg
- padding: spacing.semantic.inset.md + spacing.semantic.inline.lg

### Loading / Spinner / Skeleton
- spinner color: primary.scale.500
- skeleton background: [theme].bg.surface
- skeleton shimmer: [theme].bg.elevated
- animation: motion.duration.normal + motion.easing.easeInOut

---

## Data Display

### Card
- background: [theme].bg.elevated
- border: [theme].border.default
- radius: border-radius.scale.lg
- shadow: shadow.[theme].sm
- padding: spacing.semantic.inset.lg

### Avatar
- background: purpleAxis.scale.100
- text: purpleAxis.scale.700
- border: [theme].bg.page (作为描边)
- radius: border-radius.scale.full

### Badge / Tag
- background: purpleAxis.scale.50
- text: purpleAxis.scale.700
- radius: border-radius.scale.full
- padding: spacing.semantic.inset.xs + spacing.semantic.inline.sm

### StatusMessage (Inline)
- success: semantic.success.base
- warning: semantic.warning.base
- error: semantic.error.base
- background (light): semantic.[status].light
- radius: border-radius.scale.md

---

## Layout & Structures

### Dialog / Sheet
- background: [theme].bg.elevated
- radius (Dialog): border-radius.scale.xl
- top radius (Sheet): border-radius.scale.2xl
- shadow: shadow.[theme].2xl

### List / Menu / Divider
- divider color: [theme].border.default
- item hover background: [theme].bg.surface
- menu radius: border-radius.scale.lg
- list spacing: spacing.semantic.stack.sm

### EmptyState
- icon: neutral.scale.400
- title: typography.size.lg + typography.fontWeight.semibold + [theme].text.primary
- body: typography.size.base + [theme].text.secondary
- action: PrimaryButton

---

## 禁止项
- **禁止使用简写路径**：必须包含文件名（如 `typography.`）和完整物理层级（如 `.scale.`）。
- **禁止硬编码颜色**：必须通过 `[theme]` 引用语义色。
- **禁止混用色轴**：同一组操作严禁混用 Primary 和 BlueAxis。
- **禁止自创圆角**：必须从 `border-radius.scale` 中选择。
