# Mei UI 系统 (Mei UI System)

Mei UI 系统是一个面向 AI 辅助项目的共享 UI 标准。

其目的是使不同的 AI 代理和不同的项目能够产生一致的视觉风格：蓝紫色彩体系、一致的 Token、统一的组件规则、布局密度以及 Mei 品牌资产。

![Mei UI 系统预览](assets/preview/mei-ui-preview.svg)

## AI 快速入门

AI 和其他自动化系统必须将 `ai.md` 作为执行入口点。

1. 阅读 `ai.md`。
2. 按照 `ai.md` 定义的顺序阅读 Token 文件。
3. 阅读 `patterns.md` 以决定产品类型、密度和布局。
4. 阅读 `components.md` 以选择组件组合规则。
5. 在使用或创建任何 logo / 应用图标 / favicon 之前，阅读 `brand.md`。
6. 仅使用 Token 路径生成 UI；**严禁**硬编码颜色、间距、圆角、阴影或字体排版。

## 品牌规则

如果目标项目没有现有的 logo / 应用图标 / 品牌标识，应生成一个 Mei 风格子项目 logo，而不是直接复用 Mei 主 logo。

统一的是蓝紫色轴、几何风格、圆角、留白和小尺寸识别，不是所有项目共用同一张图标。

## 目录结构

```
tokens/       → JSON 设计变量 / Design Tokens (事实来源)
assets/logo/  → 统一的 Mei Logo 资产 (SVG 源码 + PNG/favicon 导出文件)
ai.md         → AI 执行规则与指令
patterns.md   → 按产品类型划分的布局模式
components.md → 组件组合规则
brand.md      → Logo 及品牌使用规则
```
