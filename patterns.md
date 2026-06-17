# Mei Pattern Rules

针对不同产品类型，定义布局结构和信息密度的选择规则。与 tokens（有什么值）和 components（长什么样）并列，解决"怎么排好看"的问题。

## 全局原则

- 每个页面/区块只设**一个视觉焦点**，其余元素主动弱化（颜色/大小/间距上让步）
- 每个页面/区块只允许一个主要操作（Primary Action），其余操作降级为 Secondary / Tertiary
- **密度按类型定** —— 不要一刀切"留白多就是好"，通讯/列表类该紧凑时紧凑，展示类该宽松时宽松
- 大面积背景优先用 `[theme].bg.surface`；纯白背景在文档/工作台/数据表场景下合理
- 字体层级按类型拉开 2-3 档（展示型拉 3 档，工作台/表单拉 2 档）
- 相关元素用间距分组（`spacing.semantic.stack`），不依赖边框
- 大区块之间用 `spacing.semantic.stack.2xl` / `spacing.semantic.stack.xl`，不用边框分割
- 装饰用 purpleAxis 或蓝色系点缀，但不超过总面积 **5%**（展示型页面如 Landing 可放宽至 15%）
- 所有弹窗/浮层必须有 `shadow.scale.lg~2xl` / `shadow.dark.lg~2xl` + `[theme].bg.overlay` 背景遮罩
- 除 token 源文件外，不写固定像素尺寸；宽高用 token、比例、内容宽度或密度语义表达
- 先确定信息优先级，再决定颜色和尺寸；颜色不能代替结构层级

## 视觉权重

- Primary Action：当前页面最重要的提交、确认、开始、保存操作；每个区块最多一个。
- Secondary Action：同区块内的辅助操作；使用 SecondaryButton 或中性色按钮。
- Tertiary Action：低频、轻量、导航类操作；使用文本/图标/透明按钮。
- 禁止同一操作组出现多个高饱和度按钮。
- 语义色按钮只用于危险、错误、警告等强语义操作，不用于普通功能区分。
- 主内容优先级高于容器装饰；容器边框、阴影、背景必须弱于内容本身。
- 同一屏幕若已有强品牌导航或 Hero，正文区减少品牌色使用。
- 状态色只表达状态，不参与普通功能分组。

## 布局决策

- 窄屏优先单列；宽屏可用多列，但主内容列必须最显眼。
- 操作区靠近其影响对象；页面级操作放在页面头部或底部固定区，区块级操作放在区块内。
- 表单、卡片、弹窗使用舒适阅读宽度；数据表、画布、消息区可扩展占满剩余空间。
- 同级区块使用同一密度；不同级区块通过间距和标题层级区分。
- 避免“大空白 + 小控件孤岛”；空白必须服务于聚焦、阅读或分组。
- 边框用于边界，阴影用于浮层，背景用于层级；三者不要在同一普通容器上同时强化。

## 长内容处理

- 链接、哈希、路径、日志、JSON、系统生成文本属于低视觉优先级内容。
- 默认使用 LongText / CodeBlock，不直接裸露在主布局中。
- 超过 2-4 行时限制高度，提供展开、复制或查看详情。
- 长内容不得抢占 Primary Action、状态信息和用户内容的视觉焦点。

## 状态与反馈

- 处理中状态应弱化触发按钮，展示进度或短状态，不改变页面主结构。
- 成功状态应确认结果并暴露下一步操作；不要用大面积成功色重绘布局。
- 错误状态应靠近错误来源，提供可恢复操作；不把普通错误升级为全屏告警。
- 空状态需要说明当前没有内容，并提供一个最合理的下一步。

## 密度分层

定义了 5 档密度。每个产品类型根据自身场景选择主密度，个别区块可以浮动 1 档。

| 档位 | 卡片 inset | inline 间距 | stack 间距 | 适用场景 |
|---|---|---|---|---|
| **宽松** | spacing.semantic.inset.lg ~ spacing.semantic.inset.xl | spacing.semantic.inline.lg ~ spacing.semantic.inline.xl | spacing.semantic.stack.lg ~ spacing.semantic.stack.2xl | 展示型、内容消费 |
| **标准** | spacing.semantic.inset.md ~ spacing.semantic.inset.lg | spacing.semantic.inline.md ~ spacing.semantic.inline.lg | spacing.semantic.stack.md ~ spacing.semantic.stack.lg | 通用默认 |
| **紧凑** | spacing.semantic.inset.sm ~ spacing.semantic.inset.md | spacing.semantic.inline.sm ~ spacing.semantic.inline.md | spacing.semantic.stack.sm ~ spacing.semantic.stack.md | 数据密集、工具型 |
| **极紧** | spacing.semantic.inset.sm | spacing.semantic.inline.sm | spacing.semantic.stack.xs ~ spacing.semantic.stack.sm | 仪表盘、列表 |
| **展示** | 无卡片或轻卡片 | spacing.semantic.inline.xl | spacing.semantic.stack.2xl | 落地页、品牌展示 |

---

## Pattern 类型

### 1. Communication / Messaging

**主密度**：紧凑

**布局模式**——根据屏幕、输入方式和信息结构选择：

| 模式 | 结构 | 适用场景 |
|---|---|---|
| **单列** | 全屏消息列表 + 底部输入栏 | 窄屏、AI 对话、轻量通讯 |
| **双栏** | 左侧会话列表 + 右侧消息区 | 宽屏通讯、邮件客户端 |
| **三栏** | 会话列表 + 消息区 + 详情面板 | 协作工具 |
| **浮窗** | 消息气泡 → 展开为小窗 | 客服插件、嵌入式通讯 |

| 属性 | 规则 |
|---|---|
| 顶部栏 | 品牌型：background: color.primary.scale.500 + [theme].text.inverse；工作台型：background: [theme].bg.page + color.primary.scale.500。高度使用 Communication 顶部栏密度语义，标题 typography.size.base |
| 会话列表 | 双栏/三栏时存在，作为辅助列窄于主内容区，背景 [theme].bg.page，列表项高度使用 Communication 列表项密度语义 |
| 消息区背景 | [theme].bg.surface |
| 气泡（自己） | color.primary.scale.500 + [theme].text.inverse |
| 气泡（对方） | [theme].bg.elevated + [theme].text.primary |
| 气泡圆角 | border-radius.scale.lg（主圆角），border-radius.scale.sm（指向角） |
| 气泡间距 | spacing.semantic.stack.xs（同组），spacing.semantic.stack.md（跨组） |
| 输入栏 | 固定在底部，上下 padding spacing.semantic.inset.md，左右 spacing.semantic.inset.lg |
| 时间戳 | typography.size.xs + [theme].text.tertiary，居中在气泡组之间 |
| 头像 | border-radius.scale.full，size 使用 spacing.scale.8 ~ spacing.scale.10 |
| 列表项分割 | 不用分割线，只靠 stack 间距 |
| 操作组 | 发送/提交为唯一 Primary Action；附件、表情、更多等为 Tertiary Action |
| 装饰色占比 | < 5%，只用于未读标记或在线状态 |

### 2. Workspace / Analytics

**主密度**：极紧 → 紧凑

| 属性 | 规则 |
|---|---|
| 卡片 inset | spacing.semantic.inset.sm ~ spacing.semantic.inset.md |
| 卡片间距 | spacing.semantic.stack.sm |
| 字体层级 | 最小用 typography.size.xs，关键数字用 typography.size.3xl ~ typography.size.5xl |
| 数据表格 | 行高用 spacing.semantic.stack.sm，字体 typography.size.sm |
| 图表 | 用 color.blueAxis 作为数据系列色，不占 color.primary / color.purpleAxis |
| 悬浮态 | 可交互卡片 hover 时用 [theme].bg.surface 浅色反馈 |
| 侧边栏 | 作为辅助列窄于主内容区，背景 [theme].bg.surface |
| 操作组 | 页面级 Primary Action 最多一个；表格行内操作使用 Tertiary Action |
| 装饰色占比 | < 3%，纯粹功能优先 |

### 3. Marketing / Landing

**主密度**：宽松 → 展示

| 属性 | 规则 |
|---|---|
| 大区块 | hero 作为首屏主视觉，可接近视口高度，但应露出下一段内容提示。以下区块用 spacing.semantic.stack.2xl 隔开 |
| hero 标题 | typography.size.5xl ~ typography.size.6xl + typography.fontWeight.bold，行距 typography.lineHeight.tight |
| hero 副标题 | typography.size.lg ~ typography.size.xl + [theme].text.secondary |
| 卡片 | 可选 shadow 或无边框，不做强分割 |
| CTA 按钮 | 唯一 PrimaryButton，其余用 TertiaryButton 保持干净 |
| 品牌背景 | 可用 color.primary.scale.500 ~ color.purpleAxis.scale.500 的微渐变 Hero（dark 模式下改用 color.primary.scale.700 ~ color.purpleAxis.scale.700） |
| 装饰色占比 | 10-15%，用于强调区块和视觉过渡 |
| **禁止** | 大段纯白背景、过多分割线、多个 CTA 抢焦点 |

### 4. Form / Settings

**主密度**：标准 → 紧凑

| 属性 | 规则 |
|---|---|
| 表单宽度 | 使用舒适阅读宽度，居中或左对齐，不在宽屏强行铺满 |
| 字段间距 | spacing.semantic.stack.md |
| label 位置 | 顶对齐，上方 spacing.semantic.stack.xs |
| 分组标题 | typography.size.sm + typography.fontWeight.semibold + [theme].text.secondary |
| 错误提示 | color.semantic.error.base，行内显示在字段下方，不用 Modal |
| 按钮布局 | 提交 PrimaryButton + 取消 TertiaryButton，底部右对齐或底部左对齐 |
| 长内容 | API Key、URL、路径、说明文本使用 LongText / CodeBlock，默认折叠或限高 |
| **禁止** | 表单超过 7 个字段不分组的 |

### 5. Content / Feed

**主密度**：标准 → 宽松

| 属性 | 规则 |
|---|---|
| 列表项 | 优先用 spacing.semantic.stack.md 间距隔开，密集列表可用 border.default 分割线 |
| 标题+摘要 | 标题 typography.size.base + typography.fontWeight.semibold，摘要 typography.size.sm + [theme].text.secondary |
| 缩略图 | 右侧或左侧，border-radius.scale.md，比例 1:1 或 16:9 |
| 空状态 | EmptyState 组件（见 components.md），不返回空列表 |
| 分页/加载更多 | 用 SecondaryButton 或自动 Infinite scroll |
| 长内容 | 摘要超过 2-3 行时截断，详情进入下一级页面或展开区 |
| 装饰色占比 | < 5%，只在特殊条目上加标签 |

### 6. Overlay / Modal

**主密度**：标准

| 属性 | 规则 |
|---|---|
| 背景遮罩 | [theme].bg.overlay，点击遮罩可关闭 |
| 宽度 | Dialog 使用中等阅读宽度；Sheet 可全宽并保留顶部圆角 |
| 内间距 | spacing.semantic.inset.lg |
| 标题 | typography.size.xl + typography.fontWeight.semibold |
| 操作按钮 | 底部右对齐，PrimaryButton + TertiaryButton 组合 |
| 关闭按钮 | 右上角 × 或 手势下拉（Sheet） |
| 动画 | 淡入 + 轻微上移（motion.duration.normal + motion.easing.easeOut） |
| **禁止** | Modal 叠 Modal、Modal 内再弹 Sheet |

---

## AI 工作流

1. 先确定当前页面的**产品类型**（Communication / Workspace / Marketing / Form / Content / Overlay）
2. 按对应 Pattern 规则选择密度和布局
3. 再按 `components.md` 选具体组件
4. 从 `tokens/` 取精确值
5. 完成后检查：这个页面**有没有一个明确的视觉焦点**
6. 检查是否存在固定尺寸、业务绑定色、多个同级高饱和按钮；有则降级或改用 token
