# Mei Brand Rules

Mei 是统一母品牌。除非目标项目已有明确 logo / app icon / brand mark，否则所有接入 `mei-ui-system` 的项目都必须使用 Mei 默认标识，不允许 AI 为每个项目临时重新设计 logo。

## Logo Assets

| 资产 | 用途 |
|---|---|
| `assets/logo/mei-mark.svg` | favicon、app icon、移动端启动图标、窄侧边栏、头像式品牌入口 |
| `assets/logo/mei-mark.png` | README、文档预览、第三方平台上传，512x512 |
| `assets/logo/mei-mark@2x.png` | 高清文档、应用图标源图、需要位图但要保留精度的场景，1024x1024 |
| `assets/logo/favicon.svg` | 浏览器 favicon 的首选矢量资产 |
| `assets/logo/favicon.png` | 不支持 SVG favicon 的兼容资产，64x64 |
| `assets/logo/mei-wordmark.svg` | 系统左上角、顶部导航、登录页、空状态、关于页的横向留白版本 |
| `assets/logo/mei-lockup.svg` | 独立展示、品牌页、文档封面、启动页、大尺寸留白版本 |

## AI Rules

- 没有项目 logo 时，必须使用 Mei 默认 logo。
- 有项目 logo 时，保留项目 logo，只接入 Mei UI 风格。
- 禁止为不同系统生成不同 Mei logo。
- 禁止拉伸、重绘、换色或改变 Mei logo 结构。
- 默认 logo 只使用图形，不包含 `mei`、`mei yang`、`梅洋` 等文字。
- logo 必须保持几何精密感：曲线使用矢量路径，圆点使用标准圆形，左右结构保持视觉对称，不使用手绘、抖动、粗细随意变化的线条。
- 小于等于图标场景使用 `mei-mark.svg`；导航和产品头部优先使用 `mei-wordmark.svg`；独立展示使用 `mei-lockup.svg`。
- 前端页面优先使用 SVG；README、应用商店、三方平台上传等位图场景使用 PNG 导出物。
- logo 周围至少保留一个图标主体宽度的视觉留白，不能贴边或塞进复杂背景。
