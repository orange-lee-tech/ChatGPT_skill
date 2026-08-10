# WeChat Technical Chronicle Word Publisher

**Version:** 1.0.0  
**Primary language:** 简体中文  
**Secondary language:** English  
**Primary input:** Markdown  
**Final deliverable:** A4 竖版 `.docx`  
**Primary use cases:** 微信公众号文章、个人成长日志、技术项目记录、科研/工程复盘、长期档案留存

---

## 0. 最高优先级规则：SOURCE FIDELITY / 源文件忠实性

本 Skill 的第一原则不是“漂亮”，而是**忠实**。

### 0.1 不得删改内容

除非用户明确要求编辑正文，否则：

- 不得删除 Markdown 中任何正文内容。
- 不得概括、压缩、重写或改写原文。
- 不得合并两个原本独立的段落以减少篇幅。
- 不得删除“重复”“冗长”“不够优美”但确实存在于源文件中的内容。
- 不得擅自修正文意、事实、观点、语气、用词、拼写或技术术语。
- 不得把长列表缩成摘要。
- 不得把表格信息改写成遗漏字段的卡片。
- 不得把代码、命令、日志节选为“关键部分”。
- 不得为了视觉简洁删除图片、图注、脚注、引用、链接、公式或附录。
- 不得为了微信公众号阅读体验而主动裁剪内容。
- 不得因为 Word 分页或版面限制而省略内容。

### 0.2 允许的“微调整”

只有在**不改变语义、不减少信息量、不改变原文顺序**时，允许进行排版级微调：

- 调整分页和换页位置。
- 调整段前、段后、行距、缩进。
- 将普通空格替换为不换行空格以保护技术 token。
- 在 Word 内部插入软换行、软连字符或零宽断点以避免溢出。
- 调整图片尺寸、位置、图文间距，但不得裁掉有效信息。
- 对超宽表格调整列宽、字号或拆成“连续表”，但表格数据必须全部保留。
- 对代码块进行视觉换行，但原始字符内容必须可恢复。
- 为视觉组件添加非源文本标签，例如 `PROJECT LOG`、`DATA SNAPSHOT`、章节视觉编号；这些标签必须属于“装饰/导航层”，不得冒充原文。
- 自动编号章节时，只生成视觉编号，不写回 Markdown，不改变源标题文本。

### 0.3 默认不做文字校对

若用户仅要求“排版”：

- 不纠错。
- 不润色。
- 不翻译。
- 不统一术语。
- 不重写标题。
- 不重排论证顺序。

如发现明显错别字、语法问题、事实冲突，可在交付说明中单独提示，但**不得擅自改入正文**。

### 0.4 内容原子必须全部保留

解析 Markdown 后至少识别并保留以下 Content Atoms：

- article title
- headings
- paragraphs
- ordered/unordered list items
- nested lists
- task lists
- blockquotes
- callouts
- fenced code blocks
- inline code
- tables
- images
- image alt text
- image captions（若源文件存在）
- links
- footnotes
- horizontal rules
- equations / math
- raw text
- appendices
- metadata written as visible body content

### 0.5 顺序不变

除非用户明确要求重新组织内容：

> **所有源内容原子必须保持原始相对顺序。**

视觉资产可以插入在对应内容附近，但不得把后文提前、把前文移后、把两个相隔很远的段落合并展示。

### 0.6 Fidelity QA

生成 DOCX 前后都必须执行内容完整性检查：

1. 对 Markdown 提取“源文本清单”。
2. 对生成的 DOCX 提取正文文本。
3. 去除纯视觉生成文本：
   - `01 /`
   - `PROJECT LOG`
   - `DATA SNAPSHOT`
   - `END`
   - 自动图号
   - 自动表号
   - 自动页眉页脚
4. 进行规范化比较：
   - 忽略分页符
   - 忽略软换行
   - 忽略连续空白差异
   - 保留标点、数字、英文 token、代码字符
5. 若出现源文本缺失，则生成失败，不得交付。

**宁可牺牲排版，也不得牺牲内容。**

---

# 1. Skill Purpose

将结构化 Markdown 转换为：

> **内容完整、视觉克制、层级明确、适合长期留档，并可作为微信公众号导入源的 A4 竖版 Word 文档。**

本 Skill 不是：

- 内容重写器
- 摘要器
- 微信 HTML 编辑器
- 海报生成器
- 动态网页生成器
- PPT 模板
- PDF-only 排版器

本 Skill 是：

> **Markdown → Editorial Understanding → Static Visual Grammar → Word Design System → DOCX Publisher**

---

# 2. Language Policy

## 2.1 默认语言

Primary language:

> **简体中文 zh-CN**

Secondary language:

> **English**

### 默认行为

- 中文决定正文的整体阅读节奏。
- 英文自然嵌入中文排版。
- 不主动翻译英文。
- 不主动把技术英语改写为中文。
- 不主动把中文标题翻译成英文。
- 原文若包含双语，则双语均完整保留。

## 2.2 技术 Token 保护

以下类型优先视为不可随意拆分 token：

- `GitHub`
- `ChatGPT`
- `VSCode`
- `PowerShell`
- `C++`
- `CMake`
- `OpenGL`
- `Vulkan`
- `WSL`
- `PMX`
- `VMD`
- `v1.0.0`
- `R1.6`
- `Phase 0C`
- 文件名
- 路径
- 命令
- URL
- API 名称
- 类名 / 函数名 / 变量名

排版时可使用不换行空格、软断点等方式保护视觉完整性，但不改变字符内容。

## 2.3 大写英文限制

ALL CAPS 仅建议用于：

- Metadata
- 极短 Label
- Code language label
- 非正文性视觉标记

例如：

- `PROJECT LOG`
- `TECHNICAL NOTE`
- `POWERSHELL`
- `DATA SNAPSHOT`

正文标题默认使用正常大小写或保留原文大小写。

---

# 3. Output Contract

## 3.1 唯一正式交付物

最终正式输出必须为：

> `.docx`

所有视觉设计必须最终收拢到 Word 文档内部。

### 可存在的内部中间资产

- PNG
- JPG / JPEG
- WebP 转换后的 PNG
- 临时 SVG
- 临时图表数据
- 临时词云素材

但最终必须：

> 嵌入 `.docx`

除非用户另有要求，不把这些中间资产作为独立正式交付物。

## 3.2 页面

- A4
- Portrait
- Single column
- White background
- No bleed
- No decorative full-page background

推荐页面边距：

- Top: 20 mm
- Bottom: 20 mm
- Left: 22 mm
- Right: 22 mm

正文有效宽度约：

> 166 mm

允许因超宽表格或特殊内容局部调整，但默认不切换横向页面。

## 3.3 封面

默认：

> `cover_page = false`

普通公众号文章、技术日志、成长记录、复盘文章直接从第一页进入内容。

仅以下场景可考虑独立封面：

- 正式研究报告
- 长篇调研报告
- 明确要求“报告封面”
- 用户指定

---

# 4. Design Philosophy

核心原则：

> **内容优先，结构优先，留白优先，装饰最后。**

视觉优先级：

1. 内容完整
2. 层级清楚
3. 阅读顺畅
4. 中英混排稳定
5. Word 兼容稳定
6. 微信导入可用
7. 静态视觉增强
8. 装饰

禁止倒置。

## 4.1 科技感来源

科技感应来自：

- 网格
- 编号
- Metadata
- 数据
- 代码
- 图表
- 时间线
- 工程结构
- 精确对齐
- 克制配色

不依赖：

- 霓虹
- 电路线
- 芯片纹理
- 蓝紫渐变背景
- 大面积科技插画
- 假终端窗口装饰
- 过度赛博朋克元素

## 4.2 Global Design References

可参考但不照搬：

- GitHub Primer
- GitHub Docs / GitHub Brand
- IBM Carbon Design System
- Microsoft Fluent 2
- GOV.UK Design System
- Material Design
- Quarto Word publishing
- Typst report templates
- 高质量技术报告
- 高质量编辑出版物
- 高质量研究报告

原则：

> **Learn the rule, not the skin.**

---

# 5. Font Policy

## 5.1 通用优先

不得依赖小众字体，不嵌入字体，不要求用户安装特定字体后文档才能正常显示。

### 中文正文优先

1. Microsoft YaHei / 微软雅黑
2. 系统默认中文无衬线字体

### 英文、数字

1. Arial
2. Aptos
3. 系统无衬线字体

### 代码

1. Consolas
2. Courier New
3. 系统等宽字体

## 5.2 Font Roles

定义角色而不是绑定字体：

- `FONT_CN_SANS`
- `FONT_LATIN_SANS`
- `FONT_MONO`

文档设计必须即使 fallback 后仍成立。

---

# 6. Typography Tokens

默认字号体系：

| Token | 用途 | 建议字号 |
|---|---|---:|
| T0 | Article Title | 20–22 pt |
| T1 | Subtitle | 10.5–11 pt |
| T2 | H1 | 15 pt |
| T3 | H2 | 12.5–13 pt |
| T4 | H3 | 11–11.5 pt |
| T5 | Body | 11 pt |
| T6 | Quote / Lead | 10.5 pt |
| T7 | Table | 9.5–10 pt |
| T8 | Code | 9–9.5 pt |
| T9 | Caption | 9 pt |
| T10 | Metadata / Label | 7.5–9 pt |

## 6.1 正文

- 11 pt
- 左对齐
- 不强制两端对齐
- 默认无首行缩进
- 行距约 1.55–1.6 倍
- 段后留白代替首行缩进

## 6.2 Title

- 左对齐
- 20–22 pt
- Bold
- 长标题允许自动降至 19–20 pt
- 不为了放大标题强制拆句
- 不改写标题

## 6.3 H1

默认视觉：

> `01 / 原始 H1 标题`

规则：

- `01 /` 为自动视觉编号
- 原始 H1 文本原样保留
- 编号属于展示层
- Accent Color 仅用于编号或极细锚点
- H1 约 15 pt Bold

## 6.4 H2

- 12.5–13 pt Bold
- 通常不使用色块
- 主要依靠字号与前后留白建立层级

## 6.5 H3

- 11–11.5 pt Bold
- 视作正文内部小标题
- 不建立新的复杂视觉体系

---

# 7. Spacing Tokens

禁止每个组件随意发明间距。

建议使用有限 spacing scale：

| Token | 建议 |
|---|---:|
| S1 | 3 pt |
| S2 | 6 pt |
| S3 | 8 pt |
| S4 | 12 pt |
| S5 | 16 pt |
| S6 | 20 pt |
| S7 | 28 pt |
| S8 | 36 pt |

### 常见映射

- Body paragraph after: S2–S3
- Quote before/after: S3–S4
- H2 before: S5
- H1 before: S6–S7
- Image before/after: S4–S5
- Article title → subtitle: S2–S3
- Metadata → lead/body: S5–S6
- END before: S7

具体值可因分页微调，但只能从相邻 token 范围内选择。

---

# 8. Color Tokens

## 8.1 默认颜色

- `TEXT_PRIMARY`: `#303642`
- `TEXT_HEADING`: `#182230`
- `TEXT_SECONDARY`: `#6B7280`
- `TEXT_MUTED`: `#8A919E`
- `BORDER_LIGHT`: `#E5E7EB`
- `SURFACE_LIGHT`: `#F6F8FA`
- `ACCENT_DEFAULT`: `#2563EB`

## 8.2 Accent

一篇文章默认只使用一个主强调色。

推荐类别：

- Technical / AI / Software → Blue
- Research / Engineering → Teal
- Chronicle / Growth → Amber-muted
- Reflection / Humanities → Purple-muted
- Formal Report → Deep blue / neutral

但 Accent 只应用于：

- H1 编号
- 极细结构线
- 超链接
- 小 Label
- 少量指标
- 图表重点

禁止大面积高饱和色块。

## 8.3 颜色不能承担唯一语义

例如 Warning 不能只靠红色表达，必须有标签或文本。

---

# 9. Word Style Registry

至少创建以下 Word Styles：

- `TC-Title`
- `TC-Subtitle`
- `TC-Metadata`
- `TC-H1`
- `TC-H2`
- `TC-H3`
- `TC-Body`
- `TC-Lead`
- `TC-Quote`
- `TC-Note`
- `TC-Tip`
- `TC-Warning`
- `TC-KeyPoint`
- `TC-Code`
- `TC-InlineCode`
- `TC-Caption`
- `TC-TableHeader`
- `TC-TableBody`
- `TC-Footnote`
- `TC-Appendix`

优先使用 Style 管理，而不是逐段写死格式。

---

# 10. Markdown → Word Mapping

## 10.1 Headings

- Article title → `TC-Title`
- H1 → `TC-H1`
- H2 → `TC-H2`
- H3 → `TC-H3`
- H4+ → 作为更轻量层级处理，但原文字必须保留

## 10.2 Paragraph

普通段落 → `TC-Body`

## 10.3 Blockquote

普通引用：

- 左侧细线
- 轻微缩进
- `TC-Quote`
- 不使用大面积背景
- 不增加巨大引号

## 10.4 Callout

识别：

- NOTE
- TIP
- IMPORTANT
- WARNING

视觉：

- 细边框
- 极浅底色
- 小标签
- 不改变内部文本
- 不把多段内容缩成一句摘要

## 10.5 Code

Fenced code block：

- `TC-Code`
- Consolas / mono fallback
- 9–9.5 pt
- 浅灰底
- 细边框
- 保留全部代码
- 允许视觉换行
- 不删除日志行
- 不自动省略为 `...`

语言标签可显示，但不写入代码正文。

Inline code：

- `TC-InlineCode`
- mono
- 极浅灰背景
- 保留原字符

## 10.6 List

- 保留每一个 list item
- 保留嵌套关系
- 不擅自转成摘要卡
- 不把有序列表改为无序列表
- 不把 checklist 状态丢失

## 10.7 Horizontal Rule

可渲染为：

- 轻分隔线
- 或增加垂直留白

但不得删除其结构意义。

---

# 11. Article First Screen

第一页默认结构：

1. 顶部留白
2. Article Title
3. Optional Subtitle（仅源文件存在或用户明确允许生成时）
4. Metadata
5. Optional Lead
6. 正文 / 第一章节

### Metadata

可包含：

- 日期
- 类型
- 项目名称
- Human Hours
- Version
- Category

如果源文件中没有这些信息：

> 不得凭空编造。

可只保留日期或不显示。

---

# 12. Images

## 12.1 基本规则

- Inline
- Center
- Lock aspect ratio
- 不使用浮动环绕
- 最大宽度不超过正文版心
- 不裁掉有效信息

## 12.2 截图类

截图、终端、UI、图表等白底图可添加极细浅灰边框。

## 12.3 照片类

人物、风景、实物照片默认不加边框。

## 12.4 Caption

若源 Markdown 有 caption：

> 原文 caption 必须保留。

若只有 alt text：

- 可将 alt text 作为图注使用
- 但不得改写其含义

自动图号属于展示层，例如：

> 图 3 · Linux 软件渲染验证

## 12.5 图片质量

优先：

- 高清 PNG / JPG
- 不模糊
- 不过度压缩
- 保证 Word 文件大小与清晰度平衡

---

# 13. Tables

## 13.1 默认视觉

- 不使用 Office 默认蓝色表格主题
- 尽量无竖线
- 表头轻灰
- 顶部、表头下方、底部保留细横线
- 单元格留白充分

## 13.2 内容完整性

所有单元格必须保留。

禁止：

- 删除列
- 删除行
- 合并掉重复数据
- 用“等”代替原数据
- 转卡片时丢字段

## 13.3 超宽表格

处理顺序：

1. 优化列宽
2. 缩小 table font，但不低于可读阈值
3. 横向压缩空白
4. 按逻辑拆为“连续表”
5. 必要时局部横向页面（仅正式报告）

禁止：

> 通过删除列解决溢出。

---

# 14. Visual Grammar

视觉化不是装饰，是信息编码。

AI 在生成视觉之前必须问：

> “这个视觉是否让理解明显快于纯文字？”

若否，则不生成。

## 14.1 可用静态视觉

- Timeline
- Flowchart
- Architecture Diagram
- Metric Strip
- Data Cards
- Comparison Matrix
- Bar chart
- Line chart
- Scatter chart
- Simple pie/donut only when justified
- Word Cloud
- Hierarchy Tree
- Before → After
- Milestone Map
- Pull Quote

所有视觉最终必须：

> 静态化并嵌入 Word。

禁止依赖：

- animation
- hover
- JavaScript
- CSS interaction
- embedded web app

---

# 15. Visualization Competition

同一段信息如果可以有多种视觉表达，必须比较信息效率。

例如：

工具按时间出现：

- Word Cloud：弱
- Timeline：强
- 普通正文：中

应优先：

> Timeline

关键词频率：

- Timeline：不适合
- Word Cloud：适合
- Bar chart：若需要精确比较则更优

原则：

> **选择信息编码最准确的形式，而不是最炫的形式。**

---

# 16. Word Cloud Policy

## 16.1 使用场景

仅当文章存在明显“主题词 / 概念词聚类”时使用。

适合：

- 长篇项目总结
- 年度复盘
- 大型技术文章
- 阅读笔记集合
- 访谈 / 开放文本主题总结

不适合：

- 短文
- 只有少量关键词
- 时间顺序明显比词频更重要
- 精确数据比较

## 16.2 Pipeline

1. 提取可视化候选正文
2. 排除代码块
3. 排除 URL
4. 排除纯格式字符
5. 中文分词
6. 英文技术 token 保护
7. 停用词过滤
8. 大小写归并
9. 同义词规范化（仅在不会改变原意时用于统计，不改正文）
10. 权重计算
11. 生成静态图
12. 嵌入 Word

## 16.3 Visual

- 不使用彩虹色
- 默认同一 Accent 系
- 深灰 / 中灰 / Accent
- 一篇普通文章最多 1 个词云
- 不得让词云替代正文

---

# 17. Data Visualization

## 17.1 指标块

适用于 3–5 个真正关键数字。

例如：

- 149 Tests
- 35 Test Files
- 3 Platforms

条件：

> 数字必须在源文中真实存在。

不得凭空推导或估计。

## 17.2 Chart

图表必须：

- 有明确轴标签
- 单位清楚
- 字体可读
- 不依赖颜色区分唯一类别
- 来源数据可追溯到 Markdown 或用户提供数据

如数据不足：

> 不生成图表。

---

# 18. Timeline / Flow / Architecture

## 18.1 Timeline

适合：

- 时间顺序
- 工具逐步出现
- 项目阶段
- 里程碑

## 18.2 Flowchart

适合：

- 工作流程
- 输入输出
- 决策链
- 工程步骤

## 18.3 Architecture Diagram

适合：

- 组件关系
- 软件模块
- 系统层级
- 数据流

### 内容忠实

视觉图只允许使用源文件中已有关系。

不得为了画图“补全”不存在的架构事实。

---

# 19. Editorial Modes

Skill 可识别但不改变正文：

## `technical`

特征：

- 代码多
- 工程名词多
- 项目过程多

视觉偏：

- Blue
- Code
- Flow
- Architecture
- Metrics

## `chronicle`

特征：

- 时间线
- 个人成长
- 项目里程碑

视觉偏：

- Timeline
- Milestone
- Metadata
- Pull Quote

## `reflection`

特征：

- 思考
- 人文
- 感悟

视觉偏：

- 更少图表
- 更大留白
- Quote
- 低饱和 Accent

## `report`

特征：

- 正式结构
- 表格
- 数据
- 附录

视觉偏：

- Table
- Chart
- Running header
- Section hierarchy

## `hybrid`

默认允许混合，但不能导致视觉语言冲突。

---

# 20. Visual Budget

默认视觉预算用于约束“过度设计”。

普通 3000–6000 字文章建议：

- 1 个首屏
- 3–6 个 H1
- 0–3 个 Data Visual
- 0–1 个 Word Cloud
- 0–2 个 Pull Quote
- 必要数量图片
- 必要数量表格
- 必要数量代码块

不是硬上限，但超出前必须有内容理由。

原则：

> 一段纯正文往往比一个无必要卡片更高级。

---

# 21. Pull Quote

只能从原文中：

> **原样抽取**

禁止重写成“更有金句感”的版本。

抽出的原文仍需保留在原位置，除非 Pull Quote 仅作为重复展示。

如果重复会严重影响阅读，可不生成 Pull Quote。

---

# 22. Header / Footer

普通日志：

- 可使用轻量 Running Header
- 页脚页码

但正文重要信息不得只存在于页眉页脚。

公众号导入时：

- 页眉页脚可自然舍弃
- 正文信息不能依赖其存在

---

# 23. Ending

普通档案文档正文结束后可增加视觉闭合：

> `— END —`

以及可选 Metadata：

> `2026.08.09 · TECHNICAL CHRONICLE`

这些属于展示层。

如果源文件本身包含：

- 后记
- 附录
- 参考文献
- 注释

则必须全部先排完，再出现 END。

---

# 24. WeChat Compatibility

Word 是正式档案版，同时应尽量方便导入微信公众号。

因此：

- 单栏优先
- Inline image
- 简单表格
- 避免复杂浮动对象
- 避免文本框承载关键正文
- 避免 SmartArt 作为唯一信息载体
- 避免 WordArt
- 避免大面积形状叠加
- 避免复杂多栏
- 避免依赖页眉页脚传递正文信息
- 避免嵌入视频、GIF、动态对象
- 所有复杂视觉优先渲染成静态高分辨率图片

---

# 25. Pagination

## 25.1 标题

避免：

- H1 孤零零出现在页尾
- 标题后只剩 1 行正文

需要时将标题整体移至下一页。

## 25.2 图片

避免：

- 图片与图注跨页
- 图注单独落在下一页

图片与图注尽量视作同一视觉块。

## 25.3 表格

- 表头允许重复
- 不让单行被不合理切断
- 长表允许跨页
- 不删除数据

## 25.4 代码

代码块长时可跨页。

不得为了“代码完整在一页”缩小到不可读。

---

# 26. Accessibility & Robustness

- 正文与背景保持高对比度
- 不只靠颜色表达分类
- 图片尽量保留 alt 信息
- 图表应有标题/说明
- 表格保留清晰表头
- 字号不低到难以阅读
- 视觉图不应成为正文唯一信息来源

---

# 27. Forbidden Patterns

默认禁止：

- 大面积蓝色/渐变背景
- 霓虹科技风
- 满页电路纹理
- 复杂封面
- 多栏正文
- 过多卡片
- 过多阴影
- 多种 Accent 同时抢视线
- 彩虹词云
- Mac 假终端红黄绿按钮
- 巨大装饰引号
- WordArt
- 过多 emoji 装饰
- 用图替代全部文字
- 把技术日志排成营销海报
- 为“简洁”删除源内容

---

# 28. Content-Adaptive Overrides

允许变化：

- Accent
- Visual Grammar 组件数量
- Metadata 强弱
- 是否 running header
- 是否正式封面
- 表格/图表密度
- 代码视觉密度

不允许变化：

- 源内容完整性
- 简体中文主语言规则
- Word 最终输出规则
- A4 默认规则
- 单栏默认规则
- 字体通用性
- 静态视觉规则
- Fidelity QA

---

# 29. Processing Pipeline

```text
Markdown Source
      │
      ▼
01. Source Preservation Snapshot
      │
      ▼
02. Markdown Semantic Parse
      │
      ▼
03. Language Analysis
      │
      ▼
04. Editorial Classification
      │
      ▼
05. Visual Opportunity Detection
      │
      ▼
06. Visualization Competition
      │
      ▼
07. Visual Budget
      │
      ▼
08. Word Style Mapping
      │
      ▼
09. Static Visual Rendering
      │
      ▼
10. DOCX Assembly
      │
      ▼
11. Pagination QA
      │
      ▼
12. Fidelity QA
      │
      ▼
13. Render / Visual QA
      │
      ▼
14. Final DOCX
```

---

# 30. QA Checklist

## A. Source Fidelity

- [ ] 所有标题存在
- [ ] 所有段落存在
- [ ] 所有列表项存在
- [ ] 所有代码存在
- [ ] 所有表格行列存在
- [ ] 所有图片存在
- [ ] 所有引用存在
- [ ] 所有链接存在
- [ ] 所有脚注存在
- [ ] 所有附录存在
- [ ] 内容顺序未改变
- [ ] 未主动润色
- [ ] 未主动摘要
- [ ] 未主动翻译

## B. Typography

- [ ] 中文字体通用
- [ ] 英文字体通用
- [ ] 代码字体有 fallback
- [ ] Title/H1/H2/H3 层级清楚
- [ ] 中英文混排正常
- [ ] 技术 token 未异常拆分

## C. Layout

- [ ] A4 竖版
- [ ] 单栏
- [ ] 无横向溢出
- [ ] 无异常空白页
- [ ] 无孤立标题
- [ ] 图片与图注关系正确
- [ ] 表格无缺失

## D. Visuals

- [ ] 所有视觉均为静态
- [ ] 所有视觉嵌入 DOCX
- [ ] 无无意义装饰
- [ ] Visual Budget 合理
- [ ] 图表数据来自源内容
- [ ] 词云没有破坏技术 token
- [ ] Pull Quote 原样取自原文

## E. WeChat Compatibility

- [ ] 关键正文不在文本框
- [ ] 关键正文不在页眉页脚
- [ ] 图片 Inline
- [ ] 表格不过度复杂
- [ ] 不依赖动态对象

## F. Final Fidelity Diff

- [ ] DOCX 提取文本与 Markdown 源文本对照完成
- [ ] 无源文本缺失
- [ ] 无源表格数据缺失
- [ ] 无源代码缺失
- [ ] 无源图注缺失
- [ ] 新增文本均可明确识别为展示层内容

---

# 31. Failure Policy

若出现以下情况：

- 内容无法完整放入现有视觉设计
- 表格严重超宽
- 代码严重超长
- 图片过大
- 字体 fallback 失败
- 视觉图无法稳定嵌入 Word

处理原则：

> **降级视觉，不降级内容。**

优先级：

1. 保留原文
2. 简化视觉
3. 调整分页
4. 调整字号/间距至可读范围
5. 拆分视觉组件
6. 放弃该视觉增强

绝不：

> 删除源内容以“修复排版”。

---

# 32. Output Naming

默认：

`<原Markdown文件名>_公众号排版版.docx`

如存在明确标题，可使用：

`YYYY-MM-DD_<文章短标题>_公众号排版版.docx`

不得因文件名美化改动正文标题。

---

# 33. Delivery Notes

交付时简洁说明：

- 已生成 DOCX
- 是否使用了静态可视化
- 是否发现源文件潜在错误但未修改
- 是否存在因 Word 兼容性采取的视觉降级

不需要输出冗长排版过程。

---

# 34. Design Constitution

最终遵循以下顺序：

> **忠实 > 可读 > 结构 > 稳定 > 视觉 > 装饰**

再强调一次：

> **任何视觉优化，只要会导致源 Markdown 的内容缺失、语义改变、顺序改变或信息量减少，就必须放弃该视觉优化。**

本 Skill 的目标不是把文章“改得更像设计作品”，而是：

> **在不背叛原文的前提下，让原文以更清楚、更稳定、更有秩序、更适合长期保存的方式进入 Word。**
