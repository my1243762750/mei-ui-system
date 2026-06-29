# Mei UI AI Rules

## 职责

AI 在所有平台上产出视觉一致的 UI，严格遵循 `mei-ui-system` 的 token 体系。

## 核心规则

### 1. 绝对禁止

- AI 自行发明主色、圆角值、阴影值、间距值
- 修改 token 定义（改 token 要先问用户）
- 跨平台同一组件出现不同视觉风格
- 使用平台专属组件名、框架语法或业务场景作为设计规范
- 为具体业务写死颜色含义（例如某动作固定用某色轴）
- 用多个高饱和品牌色表达同级操作
- 在规则层写固定尺寸；除 token 源文件外，尺寸必须引用 token 或使用比例/密度语义

### 2. 引用方式

所有 UI 代码必须引用 token，不允许硬编码值：

```
✅ 正确：color.primary.scale.500, spacing.semantic.inset.md, border-radius.scale.md
❌ 错误：#任意色值, 随意圆角, 随意间距
```

### 3. 读取顺序

按以下顺序读取规则和 token 文件构造组件：

```
1. tokens/color.json            → 取色
2. tokens/typography.json       → 取字体
3. tokens/spacing.json          → 取间距
4. tokens/border-radius.json    → 取圆角
5. tokens/shadow.json           → 取阴影
6. tokens/motion.json           → 取动画
7. patterns.md                  → 先按产品类型定结构和密度
8. components.md                → 再选具体组件组合规则
```

所有 token 文件在 `tokens/` 目录下，相对于项目根路径。

### 4. 跨平台一致性原则

- 同一组件在不同平台的视觉语义必须一致
- padding/margin 用同一 token key
- 色值用同一 token key（即使各平台语法不同）
- 圆角/阴影使用同一 token key，由平台适配层转换语法
- 平台实现可封装本端组件，但组件语义和行为必须来自 `components.md`

### 5. Dark Mode

- 所有组件必须同时支持 light/dark
- 背景色用 `[theme].bg.*` token
- 文字色用 `[theme].text.*` token
- 阴影浅色模式用 `shadow.scale.*`，深色模式用 `shadow.dark.*`

### 6. 色调用法

- Primary (indigo-violet) → 主要按钮、导航栏、品牌元素
- Blue Axis               → 链接、信息提示、次要操作
- Purple Axis             → 装饰、徽章、高亮
- Neutral                 → 背景、边框、正文
- Semantic                → 成功/警告/错误/信息提示

语义色只表达状态，不承担品牌结构：

- success/warning/error/info 可用于图标、状态文字、小徽标、轻量提示背景
- 普通链接文字使用 `[theme].text.link`，信息提示使用 `color.semantic.info.*`
- 大面积容器背景、卡片边框、页面结构边框默认使用 bg/border/primary token
- 不要把 success/warning/error 作为大卡片外框，除非用户明确要求强告警样式

### 7. Logo / Brand

- Mei 是统一母品牌体系；统一的是视觉语言，不是所有项目共用同一个 logo。
- 有项目 logo 时，保留项目 logo，只接入 Mei UI 风格。
- 没有项目 logo / app icon / brand mark 时，AI 必须按 `brand.md` 生成一个 Mei 风格的子项目 logo，而不是直接复用 Mei 主 logo。
- Mei 主 logo 只用于 Mei UI System、本体系文档、母品牌入口和明确属于 Mei 母品牌的页面。
- 子项目 logo 必须保持 Mei 体系：蓝紫色轴、几何造型、统一圆角、安全留白、清晰小尺寸识别。
- 子项目 logo 容器不固定为方形；可根据目标载体适配为圆形、圆角方形或其他基础几何容器。
- 若目标载体没有明确形状约束，默认优先使用圆形或大圆角容器，以延续 Mei 体系的柔和感。
- 子项目 logo 可根据项目名称、首字母、功能对象或抽象符号设计；是否使用 `mei`、`M`、中文或完整文字，由识别需求、尺寸场景和可读性决定。
- 小尺寸图标优先使用简洁图形；文字只在清晰、不拥挤且有识别价值时使用。
- 禁止脱离 Mei 体系随机生成风格完全不同的 logo。
- 禁止拉伸、裁切、模糊化或随意改色已确定的 Mei 主 logo / 子项目 logo。

### 8. 工作流

1. 按第 3 条顺序读取文件和规则
2. 先按 `patterns.md` 确定产品类型、密度和布局
3. 再按 `components.md` 选择具体组件
4. 从 `tokens/` 取精确值生成代码，不要硬编码
5. 检查生成结果是否符合以上规则
6. 若规则冲突，优先级为：可读性/可用性 > 视觉焦点 > 组件行为 > 装饰效果
