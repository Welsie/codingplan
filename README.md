
## AtomCode CodingPlan (serverless-api.html)

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
