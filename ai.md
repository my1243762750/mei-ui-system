# Mei UI AI Rules

## 职责

AI 在所有平台上产出视觉一致的 UI，严格遵循 `mei-ui-system` 的 token 体系。

## 核心规则

### 1. 绝对禁止

- AI 自行发明主色、圆角值、阴影值、间距值
- 修改 token 定义（改 token 要先问用户）
- 跨平台同一组件出现不同视觉风格

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

### 5. Dark Mode

- 所有组件必须同时支持 light/dark
- 背景色用 `[theme].bg.*` token
- 文字色用 `[theme].text.*` token
- 阴影用 `shadow.[theme].*`（shadow.scale 对应 light，shadow.dark 对应 dark）

### 6. 色调用法

- Primary (indigo-violet) → 主要按钮、导航栏、品牌元素
- Blue Axis               → 链接、信息提示、次要操作
- Purple Axis             → 装饰、徽章、高亮
- Neutral                 → 背景、边框、正文
- Semantic                → 成功/警告/错误/信息提示

语义色只表达状态，不承担品牌结构：

- success/warning/error/info 可用于图标、状态文字、小徽标、轻量提示背景
- 大面积容器背景、卡片边框、页面结构边框默认使用 bg/border/primary token
- 不要把 success/warning/error 作为大卡片外框，除非用户明确要求强告警样式

### 7. 工作流

1. 按第 3 条顺序读取文件和规则
2. 先按 `patterns.md` 确定产品类型、密度和布局
3. 再按 `components.md` 选择具体组件
4. 从 `tokens/` 取精确值生成代码，不要硬编码
5. 检查生成结果是否符合以上规则
