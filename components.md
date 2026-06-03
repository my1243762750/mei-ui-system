# Mei Component Rules

这些规则是跨端组件语义规范，不绑定 Flutter、Web、iOS 或 Android API。实现时必须用对应平台语法映射 token，不能硬编码视觉值。

## 全局原则

- 组件只组合 token，不发明颜色、圆角、阴影、间距、字号。
- 遵循精确的 Token 路径（如 `primary.scale.500`，`light.bg.surface`）。
- 语义色（semantic）只用于表达状态，不替代品牌色或结构色。
- 同一页面内同等级组件必须使用同一套 token 组合。

## 颜色轴 (Color Axes) 专有场景

为了避免决策模糊，三套颜色轴有严格的场景划分：
- **Primary (Indigo-Violet)**: 核心品牌色。用于全局主导航、主操作按钮 (PrimaryButton)、激活态边框。
- **Blue Axis (blueAxis)**: 信息与工具色。专门用于链接 (Links)、次要工具栏 (Toolbar/Secondary Actions)、数据展示 (Charts/Data Tables)。
- **Purple Axis (purpleAxis)**: 装饰与高级色。专门用于标签 (Tag/Badge)、会员特权/高级功能高亮、插画装饰背景。

## Button

### PrimaryButton
- background: primary.scale.500
- text/icon: [theme].text.inverse
- radius: radius.lg
- padding: spacing.inset.md + spacing.inline.xl
- typography: size.base + weight.semibold
- usage: 页面主操作，每个视图优先只出现一个主按钮组。

### SecondaryButton
- background: [theme].bg.elevated
- text/icon: primary.scale.500
- border: [theme].border.default
- radius: radius.lg
- padding: spacing.inset.md + spacing.inline.lg
- usage: 次要操作、辅助命令。

### TertiaryButton
- background: transparent
- text/icon: blueAxis.scale.600
- border: none
- radius: radius.md
- padding: spacing.inset.sm + spacing.inline.md
- usage: 低权重文本操作，工具条内的图标按钮。

## Input
- background: [theme].bg.surface
- text: [theme].text.primary
- placeholder: [theme].text.tertiary
- border: [theme].border.default
- focus border: primary.scale.500
- radius: radius.lg
- padding: spacing.inset.md + spacing.inline.lg
- typography: size.base + weight.regular

## Card
- background: [theme].bg.elevated
- border: [theme].border.default
- radius: radius.lg
- shadow: shadow.sm
- padding: spacing.inset.lg
- title: size.base + weight.semibold + [theme].text.primary
- body: size.sm/base + weight.regular + [theme].text.secondary

## StatusMessage
- success icon/text: semantic.success.base
- warning icon/text: semantic.warning.base
- error icon/text: semantic.error.base
- info icon/text: semantic.info.base
- background: semantic.[status].light (仅用于小面积提示条)
- container border: [theme].border.default (大面积容器禁止用 semantic)

## Badge / Tag
- background: purpleAxis.scale.50
- text: purpleAxis.scale.700
- radius: radius.full
- padding: spacing.inset.xs + spacing.inline.sm
- typography: size.xs + weight.medium
- usage: 分类标签、新功能提示、特殊属性标记。

## NavBar (含 BrandArea)
- background: primary.scale.500 (可用 primary.scale.500 到 primary.scale.700 的微渐变)
- text/icon: [theme].text.inverse
- radius: radius.xl
- padding: spacing.inset.lg 到 spacing.inset.xl
- typography: 标题 size.2xl/3xl (按空间选择), 副标题 size.base
- usage: 页面顶部导航、品牌展示区、视觉锚点。

## Toolbar / ButtonGroup
- 同组按钮使用同一种组件等级。
- 只有主操作可用 PrimaryButton；其余用 SecondaryButton 或 TertiaryButton。
- 文本链组合默认使用 blueAxis 系列。

## Dialog
- background: [theme].bg.elevated
- radius: radius.xl
- title: size.xl + weight.semibold + [theme].text.primary
- body: size.base + [theme].text.secondary
- actions: ButtonGroup 规则

## Sheet
- background: [theme].bg.elevated
- top radius: radius.2xl
- title: size.xl + weight.semibold + [theme].text.primary
- body: size.base + [theme].text.secondary
- actions: ButtonGroup 规则

## EmptyState
- icon: neutral.scale.400
- title: size.lg + weight.semibold + [theme].text.primary
- body: size.sm/base + [theme].text.secondary
- action: PrimaryButton

## 禁止项
- 禁止为同级操作按钮随机分配不同轴的颜色。
- 禁止用 semantic 色系作为大卡片外边框。
- 禁止脱离 radius scale 手写圆角值。
- 禁止用大面积强渐变替代普通容器。
- 禁止使用 "A 或 B" 的模糊决策，严格按照场景使用对应的 Color Axis。
