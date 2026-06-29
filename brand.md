# Mei Brand Rules

Mei 是统一母品牌体系。接入 `mei-ui-system` 的项目应该看起来属于同一套平台，但不要求所有项目使用同一个 logo。

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

- 有项目 logo 时，保留项目 logo，只接入 Mei UI 风格。
- 没有项目 logo 时，生成一个 Mei 风格子项目 logo，不直接复用 Mei 主 logo。
- Mei 主 logo 只用于 Mei UI System、本体系文档、母品牌入口和明确属于 Mei 母品牌的页面。
- 子项目 logo 必须保持 Mei 体系：蓝紫色轴、几何造型、统一圆角、安全留白、清晰小尺寸识别。
- 子项目 logo 容器不固定为方形；可根据目标载体适配为圆形、圆角方形或其他基础几何容器。
- 若目标载体没有明确形状约束，默认优先使用圆形或大圆角容器，以延续 Mei 体系的柔和感。
- 子项目 logo 可根据项目名称、首字母、功能对象或抽象符号设计。
- 是否使用 `mei`、`M`、中文或完整文字，由项目识别需求、尺寸场景和可读性决定；默认不强制携带。
- 小尺寸图标优先使用简洁图形；文字只在清晰、不拥挤且有识别价值时使用。
- 前端页面优先使用 SVG；README、应用商店、三方平台上传等位图场景使用 PNG 导出物。
- 禁止脱离 Mei 体系随机生成风格完全不同的 logo。
- 禁止拉伸、裁切、模糊化或随意改色已确定的 Mei 主 logo / 子项目 logo。
- logo 周围至少保留一个图标主体宽度的视觉留白，不能贴边或塞进复杂背景。
