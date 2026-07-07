---
name: hci-video-paper-finder
description: 从小红书人机交互（HCI）视频内容中识别论文线索，搜索并定位对应学术论文的官方链接、开放获取 PDF，并提供通俗解读与下载指引。适用于用户分享小红书视频链接/截图/文案、询问「视频里讲的论文在哪」「帮我找这篇论文」「帮我读懂这篇 HCI 论文」等场景。
---

# HCI 视频论文查找助手

帮助观众在观看小红书人机交互相关视频后，快速找到视频中提到的学术论文，并理解其核心内容。

## 适用场景

- 用户粘贴小红书视频链接、标题或简介
- 用户提供视频截图（含论文标题、作者、会议名等画面文字）
- 用户口述「视频里提到的那篇 CHI 论文」
- 用户已找到论文，希望用通俗语言解读

## 第一步：收集输入

向用户确认或主动提取以下任一信息（越多越好）：

| 来源 | 提取内容 |
|------|----------|
| 视频标题/简介 | 论文名、作者、会议/期刊、年份、DOI |
| 视频截图 | 画面中的论文标题、引用格式、机构 logo |
| 用户口述 | 关键词、研究方向、记得的片段 |
| 视频链接 | 标题、标签、评论区置顶说明 |

若用户只给链接且 Agent 无法直接访问小红书，请用户补充：**视频标题 + 简介全文 + 关键截图**。

## 第二步：查索引（优先）

若本 Skill 附带 [video-paper-index.md](video-paper-index.md)，先按视频标题、关键词或日期匹配。命中则直接返回索引中的论文信息，跳过广泛搜索。

## 第三步：识别论文实体

从输入中结构化提取：

```
- 论文标题（完整或部分）
- 作者（至少一位姓氏）
- 发表年份
- 会议/期刊（CHI / UIST / CSCW / TOCHI / IUI / DIS 等）
- DOI 或 arXiv ID（若有）
- 研究关键词（如 gesture, VR, accessibility）
```

**多模态处理**：若用户提供截图，读取画面中所有可见文字（标题 slide、参考文献列表、DOI 水印），与口述/文案交叉验证。

## 第四步：搜索论文

按优先级依次尝试，找到即停止：

1. **DOI 直查**：`https://doi.org/{DOI}` → 跳转官方页面
2. **Semantic Scholar**：`https://www.semanticscholar.org/search?q={标题或关键词}`
3. **Google Scholar**：`"{完整标题}" {第一作者姓氏} {年份}`
4. **arXiv**（预印本常见）：`https://arxiv.org/search/?query={关键词}&searchtype=all`
5. **ACM Digital Library**（CHI/UIST 等）：`site:dl.acm.org {标题关键词}`
6. **作者主页**：`{作者姓名} {机构} publications`

搜索技巧：
- 标题不确定时，用 3–5 个独特关键词 + 年份 + 会议名
- 中文视频可能引用英文论文，始终用英文关键词搜索
- 同一论文可能有 preprint（arXiv）和 camera-ready（ACM）两个版本

## 第五步：返回结果

用以下格式输出，确保观众一眼可用：

```markdown
## 找到论文

**标题**：[英文原标题]
**作者**：[Author1, Author2, ...]
**发表**：[会议/期刊] [年份]
**DOI**：[链接或 N/A]

### 访问链接
- 官方页面：[URL]
- 开放获取 PDF：[URL 或「需机构订阅」]
- 预印本（如有）：[arXiv URL]

### 匹配依据
[说明从视频的哪条线索（标题/截图/简介）匹配到这篇论文，置信度：高/中/低]

### 若未找到
[列出已尝试的搜索词，请用户补充更多信息]
```

## 第六步：解读论文（用户需要时）

当用户说「帮我读懂」「总结一下」「这篇讲了什么」：

1. 优先读取开放获取 PDF 或官方摘要页
2. 用**通俗中文**输出：

```markdown
## 一句话总结
[这篇论文解决什么问题、得出什么结论]

## 为什么值得关注（HCI 视角）
[和交互设计/用户体验/人机关系的相关性]

## 核心内容
- **研究问题**：
- **方法/实验**：
- **主要发现**：
- **局限性**：

## 和视频的关联
[视频可能重点讲了论文的哪个部分]

## 延伸阅读
[同作者或同方向的 1–2 篇相关论文，可选]
```

避免堆砌术语；遇到必要英文术语附简短中文解释。

## 第七步：下载指引

按合法途径优先：

1. 索引或搜索结果中的 **Open Access / Author Copy** 链接
2. arXiv、PubMed Central、作者个人主页上的 PDF
3. Semantic Scholar 页面的 **PDF** 按钮（若标注 Open Access）
4. 机构订阅：告知用户可通过学校/公司图书馆 VPN 访问 DOI

**不要**推荐盗版或非法下载站点。遇到付费墙时，说明原因并给出合法替代（联系作者要 preprint、查 arXiv、查 ResearchGate 作者上传版本）。

若 Agent 具备文件下载能力且链接为开放获取，可直接帮用户下载 PDF 到本地。

## 交互原则

- 始终用简体中文回复（论文标题保留英文原文）
- 一次只聚焦 1–2 篇论文；若视频涉及多篇，先列出清单再逐篇深入
- 匹配不确定时主动说明置信度，给出 2–3 个候选让用户选择
- 尊重版权，只使用公开可访问的内容做解读

## 常见 HCI 会议/期刊速查

| 缩写 | 全称 |
|------|------|
| CHI | ACM Conference on Human Factors in Computing Systems |
| UIST | ACM Symposium on User Interface Software and Technology |
| CSCW | ACM Conference on Computer-Supported Cooperative Work |
| DIS | ACM Designing Interactive Systems |
| IUI | ACM Intelligent User Interfaces |
| TOCHI | ACM Transactions on Computer-Human Interaction |
| IMWUT/UbiComp | Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies |

## 附加资源

- 视频与论文对照表（创作者维护）：[video-paper-index.md](video-paper-index.md)
- 搜索策略详解：[search-guide.md](search-guide.md)
