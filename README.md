# PaperLens · 文献智能批注系统

> 由 Claude AI 驱动的学术论文双栏批注工具

---

## 文件说明

| 文件 | 说明 | 用途 |
|------|------|------|
| `paperlens.html` | **主应用（推荐使用）** | 完整的上传 + AI 分析 + 批注生成网页服务 |
| `graphcast_logic_analysis.html` | 示例输出：纯逻辑分析版 | GraphCast 论文的 Prompt B 批注示例 |
| `graphcast_question_list.html` | 示例输出：有 Question 清单版 | GraphCast 论文的 Prompt A 批注示例 |
| `paper_annotator.html` | 早期版本（已被 paperlens 取代） | 保留备用 |

---

## 快速开始

1. 用浏览器直接打开 `paperlens.html`
2. 点击右上角 **API Key** 按钮，填入 Anthropic API Key（`sk-ant-...`）
3. 上传 PDF 或粘贴链接，选择批注模式，点击「开始分析」

---

## 批注模式

### Prompt B · 纯逻辑分析版
分析论文的论证结构与逻辑层次，适合深度阅读：
- 五色高亮：核心论点 / 关键概念 / 实证证据 / 让步反驳 / 方法论
- 每段批注标注逻辑位置与论证技巧
- 底部生成全文论证骨架、最强论据、最薄弱处

### Prompt A · 有 Question 清单版
围绕阅读问题组织批注，适合课程学习：
- 自定义 or 自动生成 5 个阅读问题
- 颜色与题号对应，批注卡片标注每段回答哪个问题
- 底部生成答题索引 Worksheet

---

## 技术说明

- 纯前端单文件，无需服务器，双击 HTML 即可运行
- 直接调用 Anthropic API（`claude-sonnet-4`），流式输出
- API Key 仅保存在浏览器 localStorage，不上传任何服务器
- URL 下载支持 arXiv、bioRxiv 等，自动尝试 CORS 代理
- 历史记录保存最近 8 次分析结果

---

*Generated with Claude · PaperLens v2*
