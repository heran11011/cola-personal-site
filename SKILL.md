---
name: personal-site-generator
description: >
  根据用户的记忆、对话风格和性格，一键生成高质量个人品牌网站并部署到 GitHub Pages。
  Use when the user wants to: create a personal website, build a portfolio site,
  make a personal homepage, or says things like
  "帮我做个个人网站", "搭建个人主页", "做一个关于我的网站",
  "我想要一个个人网站", "帮我建个主页", "personal site",
  "portfolio", "个人品牌站", "做个展示页", "build me a website",
  "make my homepage", "我想有个自己的网站", "帮我搭个站",
  "能不能给我做个网页", "做个人主页", "个人介绍页",
  "给我做个网站吧", "搭个人站", "build my personal page",
  "create my website", "做个作品集网站", "展示我的作品".
---

# Personal Site Generator — Cola 执行手册

你（Cola）收到用户任何跟「做个人网站/搭建主页/个人品牌站」相关的指令后，按本手册执行全流程。

## 核心理念

这不是模板套壳。你和用户有长期对话记忆——你比任何工具都了解他。
利用这个优势：从记忆中提取信息，从对话风格推断审美，生成真正「懂他」的网站。

**每个网站都必须是独一无二的**——绝对禁止收敛到通用 AI 审美。

## 流程总览

```
信息提取 → 性格/风格推断 → 确认方向（唯一等待点）→ 生成代码 → 部署 → 交付
```

唯一等用户确认的环节：风格方向。确认后全自动跑完。

---

## Stage 0: 信息提取

从 `memory_read` 和对话历史中提取以下信息：

### 必须提取的字段

| 字段 | 说明 | 示例 |
|---|---|---|
| 名字/昵称 | 用户的称呼 | heran / 禾冉 |
| 身份标签 | 职业/角色（最多3个） | ColaOS 运营 · AI Skills 开发 · 物联网工程 |
| 一句话介绍 | slogan 或 bio | 学 AI，也分享 AI |
| 社交账号 | 所有已知平台链接 | GitHub / 小红书 / B站 / 抖音 / 邮箱 |
| 代表作品 | 项目/帖子/内容（含链接） | cola-video-clipper / 小红书爆款帖 |
| 技能标签 | 技术栈或能力标签 | Prompt Engineering / IoT / Python |
| 数据亮点 | 有说服力的数字 | 6119赞藏 / 8h日均AI / 5+ Skills |

### 可选提取的字段

| 字段 | 说明 |
|---|---|
| 头像图片 | 本地路径或URL |
| 工具箱 | 常用工具/软件 |
| 经历时间线 | 里程碑事件 |
| 个人宣言/座右铭 | 如果对话中提到过 |

**如果信息不足**：直接问用户补充，但不要一次问超过 3 个问题。先用已有信息，缺什么问什么。

---

## Stage 1: 性格/风格推断

根据对话历史中用户的沟通风格，推断适合的网站审美方向。

### 风格映射表（共 25 种）

根据用户性格 + 对话风格，从以下 25 种风格中匹配最适合的：

#### 🖥️ 技术系

| # | 风格名 | 设计关键词 | 适合谁 |
|---|---|---|---|
| 1 | **Tech-Craft 硬核科技** | 深黑底(#0a0a0f) + 蓝色强调(#3b82f6) + 玻璃拟态 + JetBrains Mono + 技能进度条 + stagger 动效 | 话少直接、逻辑强、做技术的 |
| 2 | **Terminal Dev 终端风** | 纯黑底(#0a0a0a) + 电子绿(#00ff9f) + JetBrains Mono/VT323 + 打字机动效 + ASCII art + 命令行交互 | 技术宅、Geek、爱折腾 |
| 3 | **Cyberpunk 赛博朋克** | 极暗底(#0d0d1a) + 霓虹蓝(#00d4ff) + 品红(#ff00ff) + Orbitron + 故障动效(glitch) + 扫描线 + HUD 元素 | 游戏/安全/黑客圈 |
| 4 | **Retro Computing 复古计算** | 琥珀色(#ffb000) on 深底(#1a1a1a) + VT323/IBM Plex Mono + CRT 弯曲效果 + 像素边框 | 怀旧、老派程序员 |
| 5 | **3D Isometric 等轴视觉** | 浅底 + 多彩等轴插画 + Space Grotesk + 悬浮卡片 + 立体阴影 + 几何装饰 | 全栈/产品人 |

#### 🎨 创意系

| # | 风格名 | 设计关键词 | 适合谁 |
|---|---|---|---|
| 6 | **Creative Spark 创意活力** | 渐变色 + 圆角大卡片 + Clash Display + 动效丰富 + 亮色点缀 + 作品瀑布流 + 不对称布局 | 热情、表达欲强、爱分享 |
| 7 | **Neon Brutalist 霓虹野蛮** | 纯白/纯黑 + 荧光粉(#ff006e) + IBM Plex Mono + 粗线框 + 极端字重对比 + 不规则网格 | 反叛、个性强 |
| 8 | **Vapor Wave 蒸汽波** | 渐变粉紫(#ff71ce→#01cdfe) + 网格地面 + 希腊雕塑元素 + Synth 字体 + 霓虹光晕 + 80s 棕榈树 | 审美独特、喜欢复古未来 |
| 9 | **Y2K 千禧复古** | 银色/铬色 + 泡泡字体 + 星星装饰 + 塑料质感 + 高饱和色块 + 圆角一切 | 00后、时尚潮流 |
| 10 | **Pop Art 波普艺术** | 高饱和撞色 + Ben-Day 圆点 + 粗黑描边 + 漫画气泡 + Bangers 字体 + 对角分割 | 活泼外向、爱表达 |

#### ✨ 极简系

| # | 风格名 | 设计关键词 | 适合谁 |
|---|---|---|---|
| 11 | **Minimal Warm 温暖极简** | 暖白底(#faf9f6) + 深海军蓝(#1a1a2e) + Playfair Display + 大留白 + 柔和阴影 + 细线分隔 | 安静、文艺、注重质感 |
| 12 | **Clean Pro 专业简洁** | 冷灰(#e5e5e5) + 石板蓝(#475569) + Outfit + 网格布局 + 极少动效 + 信息密度高 | 商务、专业 |
| 13 | **Nordic Minimal 北欧极简** | 米白(#f5f5f0) + 炭灰(#2d2d2d) + 原木色点缀 + DM Sans + 圆角柔和 + 大量呼吸空间 | 注重生活品质、设计师 |
| 14 | **Japanese Wabi-Sabi 日式侘寂** | 和纸底色(#f7f3e9) + 墨黑 + 朱红点缀(#c41e3a) + Noto Serif JP + 竖排元素 + 留白即美 + 枯山水意境 | 内敛、有东方美学意识 |
| 15 | **Swiss Grid 瑞士平面** | 纯白底 + 纯黑文字 + 红色强调(#ff0000) + Helvetica Neue/Archivo + 严格网格 + 极端排版层次 | 设计专业、排版控 |

#### 🌈 氛围系

| # | 风格名 | 设计关键词 | 适合谁 |
|---|---|---|---|
| 16 | **Midnight Galaxy 午夜星河** | 深紫底(#0f0a1a) + 星光粒子 + 渐变紫蓝 + Syne + 发光文字 + 浮动动效 | 梦幻、浪漫 |
| 17 | **Sunset Boulevard 日落大道** | 暖橙(#ff6b35) + 珊瑚(#ff8c69) + 金色 + Bricolage Grotesque + 柔和渐变背景 + 圆润卡片 | 温暖、有亲和力 |
| 18 | **Desert Rose 沙漠玫瑰** | 柔粉(#e8b4b4) + 沙色(#d4a574) + 棕褐 + Cormorant Garamond + 有机曲线 + 柔焦效果 | 温柔细腻 |
| 19 | **Forest Canopy 森林冠层** | 深绿(#1a3a2a) + 苔藓绿(#4a7c59) + 棕色 + Libre Baskerville + 叶片纹理 + 有机形状 | 自然主义、环保意识 |
| 20 | **Ocean Depths 深海** | 深蓝底(#0a1628) + 青色(#00bcd4) + 珊瑚色点缀 + Source Sans 3 + 波浪动效 + 气泡粒子 | 沉稳、有深度 |

#### 🔥 个性系

| # | 风格名 | 设计关键词 | 适合谁 |
|---|---|---|---|
| 21 | **Editorial Luxury 编辑奢华** | 奶油底(#faf9f6) + 深海军蓝(#1a1a2e) + 金色点缀 + Playfair Display + 杂志式大图 + 极致排版 | 写作者、内容创作者 |
| 22 | **Industrial Raw 工业粗犷** | 水泥灰底 + 铁锈橙(#c35831) + Archivo Black + 粗体大字 + 金属质感 + 工厂标识感 | 硬核、不修边幅 |
| 23 | **Paper & Ink 纸墨质感** | 纸色底(#fffef5) + 墨水黑 + 手写体装饰 + Newsreader + 纸张纹理 + 手绘插画风 + 圆珠笔线条 | 文艺、手工感、学生 |
| 24 | **Glassmorphism 纯玻璃** | 渐变彩色背景 + 毛玻璃卡片(blur 20px) + 白色细边 + Plus Jakarta Sans + 半透明层叠 + 光影变化 | 追求潮流感 |
| 25 | **Dark Academia 暗学院** | 深棕底(#1a1510) + 米色文字(#d4c5a9) + 金色 + EB Garamond + 书籍/图书馆元素 + 古典装饰线 | 人文学科、读书人 |

### 推断规则

1. 从对话历史中分析：回复长度、用语风格、emoji 使用频率、技术话题占比、审美偏好表达
2. 如果用户曾经明确表达过审美偏好（如「我要高级的」「暗色系」「简洁一点」），直接采用
3. 如果无法确定，给出 2-3 个选项让用户选

### 输出格式

向用户确认时，用这个格式：

```
基于我们的对话，我觉得你适合 [风格名] 方向：
- [3个视觉关键词]
- 参考感觉：[一句话描述]

要不要这个方向？还是你有别的想法？
```

---

## Stage 2: 网站生成

确认方向后，生成完整网站代码。

### 技术规范

- **纯静态**：HTML + CSS + Vanilla JS，无框架依赖
- **单文件优先**：尽量 index.html + style.css，JS 内联或单独 main.js
- **响应式必须**：移动端（< 768px）单栏布局，桌面端自由发挥
- **性能要求**：首屏加载 < 1s，无外部大依赖
- **字体**：Google Fonts CDN，选 2-3 个（标题 + 正文 + 等宽）
- **图标**：SVG inline，社交平台用 Simple Icons 官方 path（从 simpleicons.org 获取）
- **全局 CSS Reset**：必须包含 `a { text-decoration: none; color: inherit; }`

### 设计原则（融合 frontend-design + frontend-aesthetics）

#### 字体选择——绝对禁止平庸

**禁用字体**：Inter, Roboto, Open Sans, Lato, Arial, 系统默认字体

**推荐字体池**：
- 代码感：JetBrains Mono, Fira Code, Space Grotesk
- 编辑/杂志感：Playfair Display, Crimson Pro, Newsreader
- 技术感：IBM Plex family, Source Sans 3
- 独特个性：Bricolage Grotesque, Syne, Outfit, Plus Jakarta Sans
- 高端感：Cabinet Grotesk, Satoshi, General Sans, Clash Display

**字体配对原则**：高对比 = 有意思。Display + Monospace，衬线 + 几何无衬线，Variable font 跨字重。

**字重要极端**：100/200 vs 800/900，不要 400 vs 600 这种无感对比。字号跳跃 3x+，不要 1.5x。

#### 配色——拒绝 AI 通病

**禁止**：紫色渐变配白色背景（AI slop 标志性配色）

**好的配色来源**：
- IDE 主题：Dracula, Nord, One Dark, Catppuccin, Tokyo Night
- 文化美学：日式极简、北欧设计、Brutalism
- 行业色板：金融(海军蓝/金)、健康(teal/白)、Gaming(霓虹/暗)

**原则**：主导色 + 锐利强调色 > 胆怯的均匀分布配色。用 CSS 变量保持一致。

#### 动效——克制但有记忆点

- 首选 CSS-only 方案（@keyframes + animation-delay）
- **一个精心编排的入场动画** > 散落各处的微交互
- Stagger reveal（错落渐显）是最高性价比的动效
- Hover 效果：位移/发光/缩放，选一种做到位
- Scroll-triggered 效果用 IntersectionObserver

#### 背景与氛围——不要纯色平铺

- 叠加 CSS 渐变（radial + linear 组合）
- Noise 纹理 / Grain overlay
- 几何图案或网格
- 微妙的背景动画
- 玻璃拟态的 backdrop-filter: blur()

#### 空间构图——打破预期

- 不对称布局
- 元素重叠
- 对角线流动
- 打破网格的元素
- 大量留白 或 控制密度——不要折中

### 必须包含的区块

1. **Hero 区**：名字 + 身份标签 + 一句话介绍 + 头像（如有）
2. **数据区**：2-4 个关键数字（赞藏/粉丝/项目数/日均AI时间等）
3. **作品区**：卡片形式展示代表作，每张卡可点击跳转
4. **社交链接区**：所有平台入口
5. **Footer**：`Built with Cola ☕`

### 可选区块（根据信息丰富度决定）

- 技能进度条/雷达图
- 工具箱（常用工具 logo 展示）
- 时间线
- 状态组件（🟢 Active & Creating）
- 跑马灯标签（CSS infinite scroll）
- 「关于我」文字区

### 代码质量要求

- 所有链接 `target="_blank" rel="noopener"`
- 所有卡片/作品**必须用 `<a>` 标签包裹**，不是 `<div>`
- 入场动画用 CSS `@keyframes` + `animation-delay` 做 stagger
- Hover 效果要有，但不能浮夸
- 暗色主题必须检查对比度（文字 vs 背景 ≥ 4.5:1）
- 移动端触控目标 ≥ 44px

---

## Stage 3: 部署

生成完成后，自动部署到 GitHub Pages。

### 部署流程

1. 检查 `gh auth token` 是否可用
2. 创建/更新仓库 `{username}/{reponame}`（默认 `personal-site`，如果用户有指定用指定的）
3. 推送到 `gh-pages` 分支
4. 返回在线地址：`https://{username}.github.io/{reponame}/`

### 部署前确认

如果是首次部署，告知用户：
- 仓库会是 public 的（GitHub Pages 免费版要求）
- 网站内容会公开可见

如果用户已有同名仓库，提醒会覆盖。

---

## Stage 4: 交付

部署完成后，输出：

```
✅ 你的个人网站上线了：{URL}

包含：
- {列出包含的区块}
- 移动端适配 ✓
- 所有链接可点击 ✓

源码：{GitHub 仓库地址}
本地文件：{本地路径}

想改什么直接说，一句话搞定。
```

---

## 迭代规则

用户说「不好看」「太单调」「换个风格」等，回到 Stage 1 重新推断或让用户选方向。
用户说具体修改（「把标题改大一点」「加个项目」），直接改代码重新推送。
不需要每次都重新确认方向——小改直接做。

---

## 风格展示（可选）

如果用户不确定风格，展示 25 种风格的分类概览，让用户按感觉选。
也可以说「你平时喜欢什么 APP/网站的设计感？」从用户的审美参照物反推风格。

---

## 注意事项

1. **永远不要用模板语气**——每个网站都应该是独一无二的，基于这个用户的真实信息
2. **信息来自记忆，不是问卷**——体现 Cola「最懂你」的价值
3. **拒绝 AI 通病审美**——不用 Inter、不用紫色渐变白底、不用对称均匀布局
4. **字体选择要有态度**——挑一个 distinctive font，果断用，不要安全牌
5. **SVG 图标用官方 path**——不要手画，去 Simple Icons (simpleicons.org) 找
6. **每次部署前本地预览确认**——用 snapshot 或截图检查一次再推
7. **Cola 品牌统一**——Footer 固定 `Built with Cola ☕`
8. **不要过度设计**——宁可简洁有力，也不要塞太多花哨效果；大胆极简和精致极繁都行，关键是意图明确
9. **关键决策：一个让人记住的点**——每个网站都要有一个 unforgettable 的设计决策，而不是面面俱到却平庸
