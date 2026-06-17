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

- Mei 是统一母品牌；没有项目 logo / app icon / brand mark 时，必须使用 `brand.md` 定义的 Mei 默认 logo。
- 有项目 logo 时，保留项目 logo，只接入 Mei UI 风格。
- 禁止 AI 为不同系统临时生成不同 Mei logo。
- 禁止重绘、换色、拉伸或改变 Mei logo 结构。
- 默认 logo 只使用图形，不包含 `mei`、`mei yang`、`梅洋` 等文字。
- logo 必须保持几何精密感：曲线使用矢量路径，圆点使用标准圆形，左右结构保持视觉对称，不使用手绘、抖动、粗细随意变化的线条。
- logo 资产按场景选择：favicon/app icon 用 `assets/logo/mei-mark.svg` 或 `assets/logo/favicon.svg`，导航/登录页用 `assets/logo/mei-wordmark.svg`，独立展示/品牌页用 `assets/logo/mei-lockup.svg`。
- README、应用商店、三方平台上传等位图场景直接使用 `assets/logo/mei-mark.png` 或 `assets/logo/mei-mark@2x.png`，不要在接入项目里重新导出。

### 8. 工作流

1. 按第 3 条顺序读取文件和规则
2. 先按 `patterns.md` 确定产品类型、密度和布局
3. 再按 `components.md` 选择具体组件
4. 从 `tokens/` 取精确值生成代码，不要硬编码
5. 检查生成结果是否符合以上规则
6. 若规则冲突，优先级为：可读性/可用性 > 视觉焦点 > 组件行为 > 装饰效果
