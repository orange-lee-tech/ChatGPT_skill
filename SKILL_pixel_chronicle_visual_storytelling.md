# Pixel Chronicle — Fact-Grounded Pixel Visual Storytelling

**Version:** 1.0.0  
**Primary language:** 简体中文  
**Secondary language:** English  
**Primary output:** 单张静态图片  
**Primary style:** 高细节复古像素插画 / High-detail retro pixel illustration  
**Primary use cases:** 工作汇报、项目验收、阶段成果、年度回顾、个人成长、研究纪事、公众号配图、里程碑纪念、长期档案视觉化

---

# 0. Skill Mission

本 Skill 用于把**真实事实、项目记录、工作材料、个人经历、研究进展、聊天历史或结构化总结**转换为一张具有统一视觉语言的像素纪事图片。

它不是：

- 普通信息图模板
- 图标拼贴器
- “关键词 → icon” 转换器
- 赛博朋克海报生成器
- 年终总结模板
- Canva 卡片替代品
- 任意像素风滤镜
- 为了好看而自由编造细节的插画器

它是：

> **Fact → Evidence → Visual Semantics → Narrative Concentration → Pixel Chronicle**

核心目标：

> **在不背叛事实的前提下，把复杂信息压缩成一张值得看、看得懂、看得久、具有个体辨识度的像素视觉作品。**

---

# 1. Design Constitution / 设计宪法

本 Skill 遵循以下优先级：

> **事实 > 叙事 > 辨识度 > 可读性 > 构图 > 风格 > 装饰**

任何视觉优化，只要造成重要事实被误解、虚构、偷换、夸大或错误归因，就必须放弃。

## 1.1 One World, Different Concentration

本 Skill 只有**一个视觉世界**，但有两种主要信息组织方式：

- **Narrative Mode — Centralized Composition**
  - 叙事型
  - 集中式构图
  - 多个事实被凝结进同一个主要场景
  - 强调整体意味、身份密度、记忆点

- **Factual Mode — Distributed Composition**
  - 事实型
  - 分散式构图
  - 多组事实被拆成若干小型场景或局部模块
  - 强调解释效率、验收感、汇报清晰度

二者**不是两种画风**。

它们必须看起来像：

> **同一家视觉工作室、同一个像素世界、同一套材质与光照哲学，只是信息浓度不同。**

可以将两者理解为一条连续轴：

```text
高集中                                                        高分散
│                                                              │
▼                                                              ▼

年度肖像 → 项目纪念 → 阶段成果 → 项目验收 → 工作汇报 → 数据复盘

一个主场景       少数区域        多个小场景        清晰模块
低文字量         中低文字量      中等文字量        较高文字量
强隐喻           叙事+解释       解释优先          事实确认优先
```

内部可使用：

`narrative_concentration = high | medium | low`

但不要把它当作三套风格。

---

# 2. Core Principle

## 2.1 Do not illustrate the topic. Illustrate the evidence.

> **不要画“这个主题通常长什么样”，要画“这些事实具体留下了什么”。**

错误：

- AI → 机器人
- 成功 → 奖杯
- 成长 → 向上箭头
- 创意 → 灯泡
- 发布 → 火箭
- 程序员 → 黑色终端
- 科研 → 原子图标
- 教育 → 学士帽

这些不是绝对禁止，但默认都属于**低辨识度第一反应**。

优先：

- 实际出现的工具
- 实际使用的设备
- 实际完成的页面
- 实际研究对象
- 实际项目环境
- 实际生活痕迹
- 实际工作仪式
- 实际文件、手册、图表、终端、材料、模型、记录

---

## 2.2 Do not draw the person. Draw the evidence that the person was here.

叙事型尤其遵循：

> **不要急着画人。画出这个人曾经在这里生活、思考、研究、工作过的证据。**

优秀的叙事图应具有“离开房间后的考古感”：

- 屏幕还亮着
- 手册摊开
- 笔压在纸上
- 咖啡或茶还剩半杯
- 工具没有归位
- 某个窗口停留在最后一次工作状态
- 便签、图纸、仪器、材料形成真实痕迹

重点不是“辛苦”“努力”这些抽象词，而是：

> **让观众自己从物件推断发生过什么。**

---

## 2.3 Compress wording, never compress truth.

事实型允许压缩语言，但不得压缩掉关键事实。

例如源事实：

> 修复首页按钮异常、白屏与历史 403 问题；处理静态资源与浏览器缓存错配风险；电脑端和手机端访问恢复正常。

可以视觉压缩为：

> **稳定性修复**  
> 按钮 / 白屏 / 403 / 缓存错配  
> PC + Mobile 已恢复

但不能改成：

> **全面重构完成**

如果源材料没有支持“全面重构”。

---

## 2.4 A memorable image does not contain every fact. It contains the right traces.

叙事型允许舍弃低代表性事实。

目标不是覆盖率最大，而是：

> **用少数高辨识度痕迹建立整体身份。**

因此：

- 高频事实不一定必须入画
- 低频但极具个体辨识度的事实可能更重要
- 一个微小但独特的真实物件，可能比“编程”“学习”“工作”这类大主题更有价值

---

# 3. Evidence Model / 事实证据模型

生成前先建立 Evidence Ledger。

所有视觉元素分三层：

## 3.1 Grounded Anchor

**强事实锚点。**

必须来自源材料，决定“这是谁 / 这是什么项目”。

例如：

- PMX / VMD
- GitHub 仓库
- IELTS 笔记插件
- 某个具体模型
- 某篇论文
- 某台设备
- 某份工程手册
- 某个网站页面
- 某类真实测试结果
- 某种长期使用工具
- 某个极具辨识度的个人物件

规则：

> 任何具有身份、成果、职业、研究、项目或人生经历含义的核心物件，必须有事实依据。

---

## 3.2 Contextual Prop

**上下文道具。**

由事实合理推出，用于把场景组织得自然。

例如：

- 长期桌面工作 → 台灯、纸张、键盘
- 实验环境 → 记录纸、标签、工具架
- 软件开发 → 数据线、终端窗口、设备
- 长时间阅读 → 书签、批注、笔
- 移动端适配 → 手机设备作为辅助展示

这些不必在源材料逐字出现，但必须是**保守推导**。

不得用 Contextual Prop 暗示：

- 新的奖项
- 新的职业身份
- 新的合作单位
- 新的地点
- 新的重大设备
- 新的成就
- 新的人际关系
- 新的资产或身份

---

## 3.3 Atmospheric Detail

**纯环境连接物。**

用于统一光线、材质、生活感和空间连续性。

可包括：

- 光影
- 灰尘
- 木纹
- 桌面磨损
- 蒸汽
- 小型植物
- 杯垫
- 墙面
- 窗外夜色
- 电源灯
- 纸张卷边
- 轻微凌乱

规则：

> Atmospheric Detail 可以自由度较高，但不得暗示新的重要事实。

---

# 4. Source Reading / 材料解析

生成前不要直接写图像 Prompt。

先完成：

## 4.1 Fact Extraction

提取：

- 人
- 项目
- 时间
- 事件
- 成果
- 数字
- 技术
- 工具
- 地点
- 对象
- 物件
- 工作流程
- 重复出现的主题
- 稀有但高度独特的细节
- 情绪或阶段性基调（仅在源材料明显支持时）

---

## 4.2 Fact Ranking

每个候选事实至少评估：

### Importance
这件事是否重要？

### Distinctiveness
它是否具有个体辨识度？

### Visualizability
它是否可以被可靠视觉化？

### Composability
它能否与其他元素自然共处？

### Evidence Strength
证据是否足够明确？

可用内部思路：

```text
visual_value
≈ importance
× distinctiveness
× visualizability
× composability
× evidence_strength
```

无需机械计算数字，但必须有这一判断逻辑。

---

# 5. Distinctiveness / 辨识度优先

不要只做主题频率排序。

例：

```text
编程：出现 400 次
工作：出现 300 次
学习：出现 250 次
某个非常独特的自制工具：出现 2 次
```

如果自制工具真实、重要且极具辨识度，它可能比“学习”更适合进入叙事型主画面。

判断标准：

> **哪些元素放在其他人的图里很普通，放在这个人/项目里才必然成立？**

---

# 6. Semantic Collision / 语义碰撞

叙事型最重要的创意机制之一。

不要只找“最相似的两个代表物”。

应尝试寻找：

> **两个都真实属于主体，但来自不同语义世界的核心物件。**

例如：

- 工程手册 + 英语评分表
- MRI Slice + Coffee Mug
- Gavel + Circuit Board
- Runestone + Scrabble Tile
- Boiler + LaTeX Screen

它们之间的距离会产生故事。

内部问题：

> “为什么这两个东西会同时出现在一个人的桌上？”

如果答案具有事实基础而且令人好奇，这通常是好组合。

---

# 7. Narrative Thesis / 叙事母题

事实很多时，先寻找：

> **这些事实共同讲述了什么？**

不要写成职业标签。

弱：

> 一个做工程、英语、科研和 AI 的人。

强：

> 一个在不同知识体系之间不断切换、把工程问题、语言问题与数字工具同时放在同一张工作桌上的阶段。

叙事母题用于指导：

- 主场景
- 物件选择
- 光线
- 空间
- 密度
- caption
- 是否需要留白

但母题不能凌驾事实。

---

# 8. Visual DNA / 统一像素视觉语言

无论叙事型还是事实型，都必须共用这一套视觉 DNA。

## 8.1 Pixel Language

目标不是粗糙 8-bit sprite。

默认：

> **high-detail retro pixel illustration**

特征：

- 清晰像素阶梯边缘
- 中等像素粒度
- 高密度物件细节
- 有限制感的色阶
- 稳定轮廓
- 局部高光
- 暖暗部
- 屏幕或技术元素可有冷色发光
- 物体材质可辨认
- 不追求摄影写实

---

## 8.2 Material Language

优先明确表现：

- 木材
- 纸张
- 屏幕
- 金属
- 塑料
- 布料
- 玻璃
- 机械零件
- 印刷品
- 仪器表面
- 手写痕迹

不要让所有物件都像扁平 icon。

---

## 8.3 Lighting Philosophy

默认：

> **生活光 + 技术光**

例如：

- 暖色台灯 / 环境光
- 冷色屏幕 / 仪器光
- 局部高亮
- 柔和暗部
- 有空间层次但不过度电影化

叙事型可更强调气氛。

事实型应保持更均匀、更清楚，但不能突然变成企业蓝白 PPT。

---

## 8.4 Palette

默认：

- 低饱和深背景
- 暖木色 / 暖灰
- 深蓝 / 青蓝技术光
- 米白纸张
- 小范围高亮色

可以因题材变化，但同一张图最多使用一个主强调色体系。

禁止：

- 彩虹色
- 高饱和霓虹堆叠
- 赛博朋克紫蓝泛滥
- 事实型突然切换成扁平企业蓝

---

## 8.5 Object Density

像素纪事允许丰富，但必须有层级。

不要：

> 每个角落都塞东西。

要：

- 主锚点清楚
- 辅助物围绕主锚点
- 背景负责连续性
- 留出视觉呼吸区域

---

# 9. Narrative Mode — Centralized Composition

## 9.1 Purpose

适合：

- 年度回顾
- 人物阶段肖像
- 项目纪念
- 长期成长记录
- 研究阶段回顾
- 公众号纪念性配图
- 个人工作世界

核心问题：

> **看完整张图以后，什么会留在脑子里？**

---

## 9.2 Composition

默认：

- 一个主要空间
- 一个主视觉中心
- 2–4 个核心 Grounded Anchor
- 2–6 个 Supporting Clues
- 少量 Contextual Props
- 足够 Atmospheric Details
- 极少文字

常见空间：

- 书桌
- 工作台
- 实验桌
- 编辑台
- 车间一角
- 研究台
- 工程桌
- 旅行工作台
- 专业工具台

空间必须服务事实，不要机械选择“书桌”。

---

## 9.3 Frozen Moment / 冻结时刻

不要画“物件清单”。

要问：

> **这些物件在怎样的一个时刻共同出现？**

例如：

- 清晨出发前
- 深夜收工前
- 实验刚结束
- 网站刚部署完成
- 论文修改中
- 长时间学习后的桌面
- 某个关键里程碑完成后的现场

画面应暗示：

> **主体刚刚还在这里。**

---

## 9.4 Text Budget

默认：

- 画面内部：0–30 中文字
- 优先 0–15 字
- 不做大段解释
- 不给每个物件贴标签

文字主要用于：

- 很短的真实文件名
- 屏幕中的少量真实 token
- 真实设备/技术标记
- 必要但极短的作品文字

如果图像生成模型无法稳定生成准确文字，宁可减少。

---

## 9.5 Artwork Framing

可选生成：

### Artwork Title
推荐形式：

> Still Life with X and Y

或中文：

> 《X 与 Y 的静物》

X 与 Y 应来自两个高辨识度、具有语义距离的真实锚点。

### Curatorial Caption
1–3 句即可。

作用：

- 不是解释每个物件
- 不是写总结
- 而是给整幅图一个“策展式收束”

风格：

- 克制
- 具体
- 不煽情
- 不夸大
- 不造事实

---

# 10. Factual Mode — Distributed Composition

## 10.1 Purpose

适合：

- 项目验收
- 阶段成果
- 版本发布
- 工作汇报
- 周报 / 月报
- 科研进展
- 运营复盘
- 多项成果展示
- 微信公众号汇报图

核心问题：

> **一眼需要知道什么？**

---

## 10.2 Distributed, Not Fragmented

事实型可以分散，但不能割裂。

原则：

> **分区，但不割裂。**

整张图仍应是一幅完整作品。

小场景之间可通过：

- 同一个桌面
- 延伸线缆
- 相同背景墙
- 连续光线
- 工具架
- 纸张路径
- 服务器环境
- 轨道
- 工作流程
- 共用边框语言

产生联系。

禁止直接做成：

> 四张互不相干的小插画 + 四个卡片。

---

## 10.3 Miniature Scene Rule

> **一个模块 ≠ 一个 icon。**  
> **一个模块 = 一个 miniature scene。**

例如：

### 稳定性修复

弱：

> 扳手图标

强：

> 浏览器 / 终端 / 错误日志组成小场景，错误状态被明确修复。

### 移动端优化

弱：

> 手机图标

强：

> PC 与手机并排显示同一页面，形成响应式验证场景。

### SEO

弱：

> 放大镜

强：

> 搜索结果、索引、站点地图或结构化信息形成可理解的小工作台。

### 发布部署

弱：

> 火箭

强：

> 仓库 → 构建 → 服务器 → 浏览器的像素化链路。

---

## 10.4 Information Hierarchy

事实型必须有：

1. 一个第一视觉中心
2. 3–7 个核心模块
3. 每个模块一个清楚主题
4. 必要的事实标签
5. 关键数字 / 状态
6. 最终结论或总状态（若源材料支持）

不要所有模块同样大、同样亮、同样重要。

---

## 10.5 Text Budget

默认：

- 80–250 中文字
- 复杂汇报可适当增加
- 每个模块尽量只保留：
  - 标题
  - 2–5 个关键词 / 短句
  - 1 个关键数字或状态（如存在）

文字承担：

> **消歧与精确化**

画面承担：

> **理解与记忆**

目标：

> **只看图能懂大概；看文字能确认事实。**

---

# 11. Shared World / 同一家工作室原则

叙事型与事实型必须共享：

- 同一像素粒度
- 同一轮廓语言
- 同一材质逻辑
- 同一光照哲学
- 同一色彩体系
- 同一事实纪律
- 同一物件选择原则
- 同一反俗套原则
- 同一构图审美
- 同一世界观

事实型不能为了“更清楚”突然变成：

- 扁平矢量
- 企业蓝图标
- 白底卡片
- PPT 六宫格

叙事型也不能为了“更艺术”突然变成：

- 摄影写实
- 油画
- 3D 渲染
- 赛博朋克

---

# 12. Visual Semantics / 视觉语义设计

每一个重要视觉元素都应能回答：

> **为什么它在这里？**

内部建立：

| 元素 | 来源事实 | 证据等级 | 视觉作用 | 是否核心 |
|---|---|---|---|---|
| 物件 A | 源材料事实 | Grounded | 身份锚点 | 是 |
| 物件 B | 源材料事实 | Grounded | 语义碰撞 | 是 |
| 桌灯 | 合理推导 | Contextual | 冻结时刻 | 否 |
| 木桌纹理 | 环境设计 | Atmospheric | 统一材质 | 否 |

无需向用户展示，但生成逻辑应遵循。

---

# 13. Anti-Cliché Review / 反俗套审查

正式生成前检查是否出现：

- AI = 机器人
- 编程 = 黑终端
- 成功 = 奖杯
- 发布 = 火箭
- 灵感 = 灯泡
- 成长 = 向上箭头
- 教育 = 学士帽
- 科研 = 原子
- 网络 = 地球连线
- 安全 = 盾牌
- 医疗 = 十字
- 数据 = 柱状图
- 全球化 = 世界地图

如果出现，必须问：

> **源材料里有没有更具体、更私人、更有辨识度的替代物？**

只有找不到更好表达时，才允许保留通用符号。

---

# 14. Symbol Selection / 物件选择规则

优先级：

> **真实具体物件 > 专业对象 > 工作痕迹 > 真实界面 > 通用 icon**

例如：

“软件工程”：

优先：

- 真实 IDE
- 仓库结构
- 构建日志
- 测试矩阵
- 版本号
- 具体设备

而不是直接：

- `</>` 图标
- 机器人
- 抽象代码雨

“科研”：

优先：

- 具体图表
- LaTeX
- 实验记录
- 设备
- 模型
- 数据片段
- 论文草稿

而不是：

- 原子图标

“英语教育”：

优先：

- Grammar Rubric
- 批注页
- 词汇本
- 评分表
- 教材
- 钢笔

而不是：

- 英国国旗

---

# 15. Ritual Object / 仪式物件

咖啡、茶、保温杯、耳机、钢笔、书签、零食等，常常不是核心事实，而是：

> **连接专业世界与生活世界的视觉胶水。**

原则：

> **优先寻找主体自己的 ritual object，再使用通用 ritual object。**

如果源材料明显有：

- 茶
- 保温杯
- 特定耳机
- 特定钢笔
- 特定零食
- 特定工具

不要自动放咖啡。

---

# 16. Composition Logic / 构图逻辑

## 16.1 One Primary Focus

整张图只能有一个第一视觉中心。

其他元素通过：

- 大小
- 明暗
- 饱和度
- 位置
- 光线
- 空间关系

建立层级。

---

## 16.2 Eye Flow

叙事型：

> 主锚点 → 第二锚点 → 辅助痕迹 → 环境 → 回到整体

事实型：

> 总标题/总状态 → 主模块 → 次模块 → 数据 → 结论

---

## 16.3 Spatial Relationship

不要把物件随机散落。

应建立：

- 前后关系
- 遮挡
- 使用关系
- 同一工作链
- 同一桌面
- 同一时间状态

让画面看起来像：

> **真的有人在这里使用这些东西。**

---

# 17. Typography / 图片内文字

## 17.1 General

- 中文优先简体中文
- 技术 token 保留原字符
- 少用长句
- 避免小字号密集文本
- 不让模型自由改写数字、状态、版本号

重要数字、版本、项目名应先冻结。

---

## 17.2 Freeze Strings

需要精确显示的文本先确定为最终字符串，例如：

```text
149 Tests
35 Test Files
R1.7
已验收
PC / Mobile
SEO
```

生成时要求：

> **preserve these strings exactly**

如果模型仍无法可靠呈现：

1. 减少文字
2. 用更短 token
3. 让画面承担更多信息
4. 必要时后期排字

---

# 18. Data and Numbers

数字属于高风险事实。

规则：

- 必须来自源材料
- 不估算
- 不自动换算
- 不为了“漂亮”补百分比
- 不为了“完整”添加不存在的 KPI
- 不把测试数量写错
- 不把“计划”画成“已完成”

区分：

- Completed
- In Progress
- Planned
- Experimental
- Failed
- Blocked

视觉上也不能混淆。

---

# 19. Mode Selection

默认根据任务目标判断。

## 19.1 Prefer Narrative Mode when

- 目标是纪念
- 目标是人物/阶段画像
- 信息跨度大
- 用户希望“耐看”“有意味”
- 事实很多但无需逐项验收
- 需要公众号头图 / 年度图 / 项目纪念图

---

## 19.2 Prefer Factual Mode when

- 目标是汇报
- 需要展示多项成果
- 需要验证“做了什么”
- 读者需要迅速理解
- 存在明确模块
- 存在状态 / 数字 / 阶段 / 结论

---

## 19.3 Medium Concentration

若既要作品感，又要说明事实：

- 一个主场景
- 2–4 个局部区域
- 少量标签
- 中低文字量

适合：

- 项目里程碑
- 公众号项目总结头图
- 阶段回顾

---

# 20. Processing Pipeline

```text
SOURCE
  │
  ▼
01. Evidence Ledger
事实账本
  │
  ▼
02. High-Level Themes
高层主题
  │
  ▼
03. Distinctive Traces
独特痕迹
  │
  ▼
04. Fact Ranking
重要性 / 辨识度 / 可视化 / 可组合 / 证据强度
  │
  ▼
05. Communication Goal
汇报 / 纪念 / 解释 / 发布 / 总结
  │
  ▼
06. Narrative Concentration
High / Medium / Low
  │
  ▼
07. Visual Anchors
核心物件
  │
  ▼
08. Semantic Collision
语义碰撞
  │
  ▼
09. Scene Logic
Frozen Moment / Miniature Scenes
  │
  ▼
10. Composition
视线流 / 空间关系 / 层级
  │
  ▼
11. Text Budget
文字预算
  │
  ▼
12. Pixel Rendering Brief
统一视觉 DNA
  │
  ▼
13. Prompt Assembly
最终生成指令
  │
  ▼
14. Grounding QA
事实审查
  │
  ▼
15. Aesthetic QA
审美审查
  │
  ▼
FINAL PIXEL CHRONICLE
```

---

# 21. Internal Visual Brief

正式生成前，内部至少形成：

```yaml
subject:
audience:
purpose:
narrative_concentration:
core_facts:
supporting_facts:
distinctive_traces:
narrative_thesis:
primary_anchor:
secondary_anchor:
semantic_collision:
supporting_clues:
scene_or_modules:
frozen_moment:
text_budget:
exact_strings:
lighting:
palette:
emotional_tone:
forbidden_cliches:
```

无需默认展示给用户。

---

# 22. Prompt Assembly

最终 Prompt 不要堆砌形容词。

推荐顺序：

## 22.1 Context / Purpose

说明：

- 这张图是什么
- 给谁看
- 承担什么传播任务

---

## 22.2 Scene / Layout

叙事型：

- 一个什么空间
- 什么视角
- 主锚点在哪里
- 第二锚点在哪里
- 辅助物如何围绕
- 什么冻结时刻

事实型：

- 整体画面结构
- 3–7 个 miniature scenes
- 主次层级
- 模块之间如何共享世界
- 总标题 / 总状态在哪里

---

## 22.3 Evidence Anchors

明确：

- 哪些元素必须存在
- 哪些关系必须保留
- 哪些数字必须精确
- 哪些内容禁止更改

---

## 22.4 Pixel Visual DNA

统一描述：

- high-detail retro pixel illustration
- clear pixel-step edges
- medium pixel granularity
- restrained palette
- strong material readability
- warm environmental light
- cool screen / technical glow where appropriate
- dense but controlled object detail
- coherent single-world composition
- no photorealism
- no flat vector infographic style

---

## 22.5 Constraints

明确禁止：

- 无依据新增重大事实
- 奖杯 / 火箭 / 机器人等俗套自动加入
- 过度霓虹
- 摄影写实
- 扁平企业图标
- 卡片拼贴感
- 无层级堆物
- 大段小字
- 错误数字
- 把计划画成完成

---

# 23. Prompt Template — Narrative Mode

```text
Create a fact-grounded high-detail retro pixel-art still-life portrait.

PURPOSE
This image is a visual chronicle of [subject / period]. It should feel like a personal artifact rather than an infographic.

NARRATIVE THESIS
[one concise sentence]

SCENE
Use one coherent [desk / workbench / lab table / other evidence-grounded space].
Depict a frozen moment suggesting the subject has just stepped away.

PRIMARY IDENTITY ANCHORS
- [Anchor A]
- [Anchor B]

SUPPORTING CLUES
- [Clue C]
- [Clue D]
- [Clue E]

SEMANTIC RELATION
Anchor A and Anchor B should come from different semantic worlds but both be strongly grounded in the source. Their coexistence should create curiosity and identity density.

ATMOSPHERE
Use only conservative contextual props and atmospheric details. These may unify the scene but must not imply new achievements, professions, locations, awards, relationships, or major life facts.

TEXT
Keep image text minimal.
Preserve these exact strings if shown:
[exact strings]

VISUAL DNA
High-detail retro pixel illustration, clear pixel-step edges, medium pixel granularity, restrained warm-and-deep palette, readable wood/paper/metal/screen materials, warm ambient light with restrained cool technical glow, strong object hierarchy, handcrafted game-art feeling, coherent still-life composition.

AVOID
Generic AI robots, trophies, rockets, lightbulbs, growth arrows, unnecessary logos, flat vector icons, cyberpunk neon, photorealism, random decorative objects that imply new facts.
```

---

# 24. Prompt Template — Factual Mode

```text
Create a fact-grounded distributed pixel chronicle for a work/project report.

PURPOSE
The image must communicate several verified results clearly while preserving the same visual language as a narrative pixel still life.

OVERALL COMPOSITION
Build one coherent pixel-art world divided into [N] readable miniature scenes.
The scenes may be spatially separated but must feel connected through shared surfaces, background, lighting, cables, papers, architecture, workflow, or environment.
Do not make them look like unrelated infographic cards.

PRIMARY STATUS / MESSAGE
[verified summary]

MINIATURE SCENES

1. [Module title]
Facts:
- [fact]
- [fact]
Visualize as:
- [miniature scene logic]

2. [Module title]
Facts:
- [fact]
Visualize as:
- [miniature scene logic]

[...]

TEXT
Use short factual labels only.
Preserve exact strings:
[exact strings]

INFORMATION HIERARCHY
One primary visual center.
Clear module priority.
Use image for comprehension and short text for disambiguation.

VISUAL DNA
High-detail retro pixel illustration, clear pixel-step edges, medium pixel granularity, restrained palette, warm environmental light, restrained cool screen glow, strong material readability, miniature working scenes rather than icons, unified single-world composition.

AVOID
Flat corporate infographic styling, blue-white card grids, generic icons, trophy/rocket/lightbulb clichés, excessive text, fake metrics, invented achievements, fragmented collage appearance, photorealism.
```

---

# 25. Caption Policy

可选，不强制。

## Narrative Mode

推荐：

### Title
`Still Life with X and Y`

### Caption
1–3 句微型策展文字。

规则：

- 具体
- 克制
- 允许诗意
- 不虚构事实
- 不解释每个物件
- 不写鸡汤
- 不把画面变成总结报告

---

## Factual Mode

caption 应更直接：

- 项目阶段
- 时间
- 核心结论
- 状态

不写长散文。

---

# 26. QA — Grounding

生成后检查：

- [ ] 所有核心身份物件有事实依据
- [ ] 所有数字准确
- [ ] 项目状态准确
- [ ] 没有把计划画成完成
- [ ] 没有新增奖项
- [ ] 没有新增职业
- [ ] 没有新增组织关系
- [ ] 没有新增地点
- [ ] 没有新增重要设备
- [ ] Contextual Props 没有暗示新事实
- [ ] Atmospheric Details 仅承担环境作用

若失败：

> 重新生成或编辑，不接受“差不多”。

---

# 27. QA — Narrative

叙事型：

- [ ] 是否有一个清楚的整体场景
- [ ] 是否有主锚点
- [ ] 是否存在真正的语义碰撞
- [ ] 是否有“刚刚有人在这里”的感觉
- [ ] 是否避免逐物件标签解释
- [ ] 是否具有个体辨识度
- [ ] 是否不是“职业模板”
- [ ] 是否留下观看后的余味

---

# 28. QA — Factual

事实型：

- [ ] 一眼能否知道最重要结论
- [ ] 模块数量是否合理（建议 3–7）
- [ ] 每个模块是否为 miniature scene 而非 icon
- [ ] 模块是否清楚但不割裂
- [ ] 是否存在主次层级
- [ ] 文字是否只用于确认事实
- [ ] 是否避免企业 PPT 卡片感
- [ ] 是否仍然明显属于 Pixel Chronicle 世界

---

# 29. QA — Aesthetic

- [ ] 像素语言一致
- [ ] 像素粒度一致
- [ ] 材质可辨
- [ ] 光线统一
- [ ] 色彩克制
- [ ] 无霓虹泛滥
- [ ] 无随机装饰堆叠
- [ ] 无无意义巨大标题
- [ ] 无过度 logo
- [ ] 无 flat vector 感
- [ ] 无摄影写实
- [ ] 主视觉中心明确
- [ ] 视线流自然
- [ ] 有留白和呼吸区域

---

# 30. Failure Policy

若视觉需求与事实准确发生冲突：

> **牺牲视觉，不牺牲事实。**

若信息太多：

1. 提高集中度判断
2. 减少次要事实
3. 合并同类事实
4. 分成 miniature scenes
5. 减少文字
6. 必要时生成第二张图

不要：

- 缩成无法阅读的小字
- 塞满画面
- 把十几项事实画成十几枚 icon
- 编造统一叙事
- 用泛化词替代关键事实

---

# 31. Research Boundary

本 Skill 的视觉思想参考了：

- OpenAI 2025 `Your Year with ChatGPT` 的公开产品表现
- OpenAI 官方对图像生成、上下文理解、符号表达与复杂 Prompt 组织的公开说明
- 大量用户公开分享的 `Your year, painted in pixels` 样本

必须明确：

> **OpenAI 并未公开 `Your Year with ChatGPT` 年度像素图的完整内部生成 Prompt。**

因此：

- 不得声称本 Skill 复制了 OpenAI 官方 system prompt
- 不得把网络流传文本冒充官方提示词
- `Still Life with X and Y`
- 语义碰撞
- 作品化包装
- 静物构图
- 物件组合规律

这些属于：

> **基于公开成品样本的设计逆向总结 / sample-derived design inference**

而不是官方内部实现声明。

---

# 32. Design Maxims

以下句子可作为执行时的最高提醒：

> **One world, different concentration.**  
> 同一个世界，不同的信息浓度。

> **Do not illustrate the topic. Illustrate the evidence.**  
> 不要画主题的刻板印象，画事实留下的证据。

> **Do not draw the person. Draw the evidence that the person was here.**  
> 不要急着画人，画出这个人曾经在这里工作、生活和思考过的证据。

> **Choose objects that would look unrelated on anyone else’s desk, but inevitable on this person’s.**  
> 选择那些放在别人桌上显得毫无关系，放在这个人桌上却必然成立的物件。

> **Compress wording, never compress truth.**  
> 可以压缩文字，不能压缩事实。

> **A memorable image does not contain every fact. It contains the right traces.**  
> 一张值得记住的图，不需要容纳全部事实，只需要留下正确的痕迹。

> **Distributed does not mean fragmented.**  
> 分散不等于割裂。

> **A module is not an icon. A module is a miniature scene.**  
> 一个模块不是一个图标，而是一处小型叙事现场。

---

# 33. Final Output Standard

最终图片应满足：

### 如果是 Narrative Mode

观众应产生：

> “这张图像是在讲一个具体的人 / 一段具体经历，而不是一个职业模板。”

### 如果是 Factual Mode

观众应产生：

> “我很快知道这项工作做了什么，同时它仍然是一张完整、有生命、有作者感的像素作品。”

### 无论哪种模式

都必须达到：

> **事实可追溯、视觉统一、信息有层级、物件有意义、构图有匠心。**

---

# 34. Final Definition

> **Pixel Chronicle 是一套基于真实事实的像素视觉叙事方法。它不因“叙事”或“汇报”而更换画风，而是在同一个像素世界中调整信息的集中程度：集中式构图把多重经历凝结成一个耐人寻味的场景；分散式构图则把事实拆成若干清晰的小型场景，使信息更容易理解，同时保持整幅作品统一、连续而有生命。**

最终目标不是：

> “生成一张像素风图片。”

而是：

> **把事实转化成一个可以被看见、被理解、被记住的世界。**
