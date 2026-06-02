# UI Style Skill

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
✅ 正确：--color-primary-500, spacing.4, border-radius.md
❌ 错误：#任意色值, 随意圆角, 随意间距
```

### 3. 读取顺序

按以下顺序读取 token 文件构造组件：

```
1. design-tokens.json    → 系统概览
2. color.json            → 取色
3. typography.json       → 取字体
4. spacing.json          → 取间距
5. border-radius.json    → 取圆角
6. shadow.json           → 取阴影
7. motion.json           → 取动画
```

所有 token 文件在 `tokens/` 目录下，相对于项目根路径。

### 4. 跨平台一致性原则

- 同一组件在不同平台的 layout 结构必须一致
- padding/margin 用同一 token key
- 色值用同一 token key（即使各平台语法不同）
- 圆角/阴影数值必须匹配

### 5. Dark Mode

- 所有组件必须同时支持 light/dark
- 背景色用 `bg.*` token
- 文字色用 `text.*` token
- 阴影用 `shadow.dark.*`（dark 模式下）

### 6. 色调用法

- Primary (indigo-violet) → 主要按钮、导航栏、品牌元素
- Blue Axis               → 链接、信息提示、次要操作
- Purple Axis             → 装饰、徽章、高亮
- Neutral                 → 背景、边框、正文
- Semantic                → 成功/警告/错误/信息提示

### 7. 工作流

1. 按第 3 条顺序读取 token 文件
2. 按 token 生成代码，不要硬编码
3. 检查生成结果是否符合以上规则
