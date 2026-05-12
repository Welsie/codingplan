# AtomCode 落地页合集

两个独立的单文件 HTML 落地页，共享同一套橙黑视觉与交互体系（cursor aurora · 字符 scramble · 磁性按钮 · 滚动进度条 · 点击 ripple）。

| 文件 | 路径 | 内容 |
|---|---|---|
| **index.html** | `/` | AtomCode 100B 原子创造者激励计划 · 1000 亿 Tokens 免费发放 · 代码雨 + 玻璃放大镜 |
| **serverless-api.html** | `/serverless-api.html` | AtomCode CodingPlan · 昇腾算力订阅制 · 三档套餐 + 模型橱窗 + 接入示例 |

所有 CSS / JS / SVG 内联，零外部依赖，可直接发布到 GitHub Pages、Vercel、Netlify 或任意静态托管。

---

## 页面 1 · AtomCode 100B 激励计划 (index.html)

> 限时 Token 发放活动落地页 · 设计参考 [100t.xiaomimimo.com](https://100t.xiaomimimo.com)

---

## 页面结构

| 板块 | 内容 |
|---|---|
| **Header** | Logo、状态点（呼吸动画）、倒计时、Discord、微信二维码弹窗、分享 / EN |
| **Hero** | 打字机标题 · 剩余 Tokens 实时递减 · 立即申请按钮 · 滚动指示器 |
| **横向跑马灯** | 滚动展示关键词 · 30 天 · 1000 亿 · 全球开放 |
| **三档权益卡** | Starter · Creator（推荐）· Enterprise，三档 5/30/100 亿 Tokens |
| **申请流程** | Apply · Review · Notify · Receive 四步时间线 |
| **FAQ** | 10 条常见问题，可点击展开 |
| **Footer** | 链接 · 版权 |
| **申请弹窗** | 蒙层模态 · 姓名 · 邮箱 · 身份 · 工具 · 项目描述 |

---

## 交互设计

整页围绕"代码 + 放大镜"的中心隐喻展开，每个区块都有鼠标响应：

### 全页面

- **Aurora 光晕** — 暖橙 + 冷蓝双层径向渐变随鼠标移动，`mix-blend-mode: screen` 叠在内容之上
- **点击涟漪** — 任意位置点击触发 160px 橙色光环扩散
- **顶部进度条** — 2px 渐变流光，滚动时实时反映位置，越过 Hero 后自动切深色
- **磁性按钮** — Apply / Tier CTA / Submit / Share / EN 在鼠标进入 1.4× 半径范围时被"吸引"过去
- **字符级解码抖动** — 标题类元素 hover 时按字符位置 stagger 随机替换字符再渐进还原（中英双字符池）

### Hero 区

- **代码雨背景** — Canvas 上 ~70 行 AtomCode 主题代码片段（SDK 调用、Token Plan、curl、agent.run、Python dataclass…）持续向上滚动，每帧随机突变 3 处字符
- **玻璃放大镜** — 260px 极简圆形玻璃片，2.6× 缩放采样代码 canvas，3 层超细描边 + 暖橙外光晕 + 阴影；hover 立即申请 / 滚动按钮 / 顶栏时自动让位给系统光标
- **视差** — 标题与 Tokens 数字相对鼠标位置反向位移，营造深度

### 权益卡区

- **3D 倾斜** — 卡片基于鼠标位置 `rotateX/rotateY` ±8°，离开缓动归零
- **聚光灯** — 卡内 220px 暖橙径向光斑跟随鼠标

### 申请流程

- **磁吸数字** — 步骤数字圆按 22% 强度跟向鼠标
- **旋转光环** — hover 时数字外圈出现 conic 旋转光环（`@property --ang`）

### FAQ 区

- **光带横扫** — hover 整行从左到右扫过一道渐变高光（900ms）
- **手风琴** — 点击展开，`+` 旋转 45° 为 `×`，配橙色高亮

---

## 技术栈

- **HTML / CSS / JavaScript** —— 原生，无框架，无构建步骤
- **Canvas 2D** —— 代码雨动画 + 放大镜采样
- **CSS 自定义属性 + `@property`** —— 锥光环动画、聚光灯坐标传递
- **`IntersectionObserver`** —— 权益卡 / 步骤进入视口淡入
- **`backdrop-filter`** —— 玻璃质感
- **`mix-blend-mode: screen`** —— Aurora 光晕跨内容叠加

文件大小：单 HTML ~57 KB（未压缩），首屏即时可用。

---

## 部署到 GitHub Pages

```bash
unzip atomcode-dist.zip
cd dist

git init
git add .
git commit -m "init"
git branch -M main
git remote add origin https://github.com/<USER>/<REPO>.git
git push -u origin main
```

仓库 **Settings → Pages → Source** 选 `main` 分支根目录，约一分钟后访问：
```
https://<USER>.github.io/<REPO>/
```

`.nojekyll` 文件已包含，避免 Jekyll 处理；以 `_` 开头的资源也能被正常服务。

---

## 本地预览

```bash
# 任选其一
python3 -m http.server 8000
npx serve .
```

打开 `http://localhost:8000/`。

也可以直接双击 `index.html`，部分浏览器对 `file://` 协议下的某些特性会有限制，建议起本地服务。

---

## 文件结构

```
dist/
├── index.html    主页面 · 一切内联 · 无外部依赖
├── README.md     本文档
└── .nojekyll     关闭 GitHub Pages 的 Jekyll 处理
```

---

## 二次定制

所有可调参数集中在 `index.html` 顶部 `:root` 与各个 IIFE 模块内：

| 想改什么 | 改哪里 |
|---|---|
| 主色（强调橙） | CSS `:root --accent` |
| 总 Tokens 数 | JS 倒计时模块 `total` 常量 |
| 活动持续天数 | JS 倒计时模块 `end` 计算 |
| 代码雨内容 | JS `SNIPPETS` 数组 |
| 代码亮度 | `mkRow()` 内 `alpha` 取值范围 |
| 放大镜大小 / 倍率 | 放大镜 JS `SIZE` / `ZOOM` 常量 |
| 蒙版深度 | CSS `.hero-overlay` `background` |
| 标题轮播文案 | JS 打字机模块 `phrases` 数组 |
| FAQ 内容 | HTML `.faq-list` 区块 |
| 三档权益 | HTML `.tier-grid` 区块 |

---

## 浏览器兼容

- 现代 Chromium / Safari / Firefox（最近两个大版本）
- 移动端：自动禁用放大镜与跟随光标，保留所有静态视觉
- 不支持 IE 11

---

## 页面 2 · AtomCode CodingPlan (serverless-api.html)

> 昇腾算力订阅制编码服务落地页 · 优化自 [ai.atomgit.com/serverless-api](https://ai.atomgit.com/serverless-api)

### 主要交互

- **顶部进度条** + **左侧锚点轨道**（首页 / 套餐 / 模型 / 接入），滚动同步高亮
- **粘性名额条** —— 实时倒计时 + 名额随机递减
- **任务 chip 筛选** —— 7 个任务（文本/图文/文生图/图生图/文生视频/图生视频/句子相似度），点选后下方套餐 ttag 高亮
- **三档套餐**
  - hover 聚焦时其他卡淡出 `.4` + 缩 `.97`，被聚焦卡升降阴影
  - Pro 推荐档：顶部 2px 流动渐变带 + `RECOMMENDED` 角标
  - Lite 描边 / Pro 实心橙 + 扫码下载副链 / Max disabled + 邮箱通知表单
  - 数字进入视口 `count-up` 缓动
- **模型卡橱窗（12 张）**
  - 顶部 1px License 色带（MIT 蓝 / Apache 绿 / Qwen 紫 / DeepSeek 橙）
  - 3D 倾斜 + 鼠标位置 200px 暖色光斑跟随
  - `HOT` 角标呼吸光环
- **粘性搜索 + 多维筛选** —— 按任务 / License / 关键词过滤，实时显示匹配数
- **接入示例弹窗** —— cURL / Python / Node.js 三 Tab，一键复制 + toast
- **移动端** —— 套餐变 85% 宽 carousel + scroll-snap；模型网格 4→2→1 列

### 二次定制

| 想改什么 | 改哪里 |
|---|---|
| 套餐内容 | HTML `.tiers` 三张 `<article class="tier">` |
| 模型列表 | JS `MODELS` 数组 |
| License 颜色 | CSS `:root` 的 `--mit / --apache / --qwen / --deepseek` |
| 接入代码模板 | JS `buildSnippet(lang, m)` 函数 |
| 任务 chip 名称 | HTML `.chips` 区块 + JS `TASK_NAMES` 表 |
| 名额起始值 / 倒计时 | JS `qLeft` 初值 + `end` 计算 |

---

## License

MIT
