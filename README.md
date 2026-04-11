# PaperLens · 文献智能批注

> 让文献阅读拥有**结构与深度**

PaperLens 是一个纯前端的学术论文 AI 批注工具，直接从浏览器调用 Anthropic API，将 PDF 论文自动生成专业的双栏批注页面。

---

## 功能特性

- **双输入方式**：本地上传 PDF 或粘贴 arXiv / bioRxiv 等文献直链
- **双批注模式**：逻辑分析 或 阅读问题清单
- **双语支持**：批注语言可选中文或 English
- **流式生成**：实时展示生成进度，无需等待
- **结果导出**：下载批注结果为 HTML 文件
- **历史记录**：自动保存最近 8 篇分析结果，可随时重新查看
- **隐私安全**：API Key 和历史记录仅存储在本地浏览器，不经过任何中间服务器

---

## 快速开始

### 1. 获取 Anthropic API Key

前往 [console.anthropic.com](https://console.anthropic.com) 注册并充值，获取 API Key（格式为 `sk-ant-...`）。

> **注意**：Claude.ai Plus 订阅与 Anthropic API 是两套独立的计费系统，需要单独在 console 充值。最低充值 $5，每篇论文约消耗 $0.20–0.35。

### 2. 打开 PaperLens

直接在浏览器中打开 `index.html`，或访问 [chensy618.github.io/PaperLens](https://chensy618.github.io/PaperLens)。

### 3. 设置 API Key

点击右上角 **API Key** 按钮，输入 Key 后保存。绿点亮起表示 Key 已就绪。

### 4. 上传论文并分析

选择输入方式、批注模式、语言，点击 **开始分析**，等待 1–2 分钟即可。

---

## 批注模式详解

### 模式 A：有 Question 清单版

自动生成（或使用自定义）阅读问题，用颜色标记原文中与每个问题相关的段落。

**适合场景**：带着特定问题精读论文、文献综述、组会汇报准备。

页面结构：
1. 顶部导航栏（论文标题）
2. 章节跳转栏
3. 问题卡片列表（Q1–Q5+，每个问题配有颜色标识）
4. 双栏批注正文（左栏原文 + 颜色标注，右栏对应问题的分析卡片）
5. 底部答案工作区（每个问题的核心论点、关键证据、潜在局限）

**自定义问题**：选择此模式后，在"自定义阅读问题"框中每行输入一个问题（留空则自动生成 5 个标准问题）。

### 模式 B：纯逻辑分析版

不依赖预设问题，专注分析论文的论证结构，识别核心论点、证据、让步与反驳。

**适合场景**：评估论文论证质量、批判性阅读、写作参考。

高亮颜色含义：

| 颜色 | 含义 |
|------|------|
| 黄色 | 核心论点 / 主张 |
| 粉红 | 关键定义术语 |
| 蓝色 | 数据 / 统计 / 实验结果 |
| 绿色 | 让步 / 反驳处理 |
| 紫色 | 方法论选择 |

页面结构：
1. 顶部导航栏（论文标题 + 图例）
2. 章节跳转栏
3. 论证链可视化（问题 → 论点 → 证据 → 反驳 → 结论）
4. 双栏批注正文（左栏高亮原文，右栏含逻辑位置与论证技巧分析）
5. 底部总览（核心主张、论证骨架、最强论据、最薄弱处）

---

## 输入方式

### 本地上传
- 支持格式：`.pdf`
- 最大文件大小：10 MB
- 支持拖拽或点击选择文件

> 若文件超过 10MB，推荐使用 [smallpdf.com](https://smallpdf.com) 或 [ilovepdf.com](https://ilovepdf.com) 压缩后再上传。

### 链接输入
- 支持 arXiv、bioRxiv 等平台的 PDF 直链
- arXiv 摘要页链接（`arxiv.org/abs/...`）会自动转换为 PDF 链接
- 网络问题时自动尝试多个 CORS 代理

---

## 费用参考

使用 `claude-3-5-sonnet-20241022` 模型：

| 项目 | 费率 |
|------|------|
| 输入 | $3 / 100万 tokens |
| 输出 | $15 / 100万 tokens |

**每篇论文约 $0.20–0.35**（取决于 PDF 大小和分析深度），$5 可分析约 15–20 篇论文。

实时用量查看：[console.anthropic.com/usage](https://console.anthropic.com/usage)

---

## 文件说明

| 文件 | 说明 |
|------|------|
| `index.html` | 主应用 |
| `graphcast_logic_analysis.html` | 示例：GraphCast 论文逻辑分析版输出 |
| `graphcast_question_list.html` | 示例：GraphCast 论文问题清单版输出 |
| `paper_annotator.html` | 早期版本（保留备用） |

---

## 本地运行

PaperLens 是纯静态页面，无需任何后端或构建工具：

```bash
# 直接用浏览器打开
open index.html

# 或启动本地服务器（推荐，避免部分浏览器的跨域限制）
python3 -m http.server 8080
# 然后访问 http://localhost:8080
```

---

## 数据隐私

- API Key 存储在浏览器 `localStorage`，仅在本机有效
- 历史分析结果存储在浏览器 `localStorage`，最多保留 8 条
- PDF 内容直接从浏览器发送至 Anthropic API，不经过任何第三方服务器
- 清除浏览器数据会同时删除 Key 和历史记录

---

## 技术栈

- 纯 HTML / CSS / JavaScript，无框架依赖
- [Anthropic Messages API](https://docs.anthropic.com/en/api/messages) — 流式输出
- Google Fonts：Playfair Display、DM Sans、DM Mono
