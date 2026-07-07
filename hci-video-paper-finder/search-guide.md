# 论文搜索策略参考

本文件供 Agent 在 [SKILL.md](SKILL.md) 主流程搜索未果时深入参考。观众通常无需阅读。

## 从小红书视频常见线索反推论文

| 视频里常见的呈现方式 | 对应搜索策略 |
|---------------------|-------------|
| 标题含「CHI 2024 最佳论文」 | Google Scholar: `"best paper" CHI 2024` + 视频关键词 |
| 简介写作者机构 | `site:stanford.edu OR site:mit.edu {关键词} pdf` |
| 画面 References 列表 | 逐条提取 `"标题片段" 年份` 精确搜索 |
| 口播只说了研究方向 | Semantic Scholar 按 topic + year 筛选，列出 Top 5 候选 |
| 视频讲的是一个系统/产品名 | 先搜系统名 + paper/demo，再反向找论文 |

## 开放获取 PDF 查找顺序

1. 论文页面上的 **Author Version** / **Preprint** 按钮
2. arXiv（cs.HC 分类）：https://arxiv.org/list/cs.HC/recent
3. 作者 Google Scholar 主页 → 「PDF」标记的条目
4. Semantic Scholar → Open Access PDF
5. 机构仓储（如 `site:eprints.`，`site:researchgate.net` 仅作者官方上传）

## 付费墙时的合法替代

- 发邮件模板（Agent 可帮用户生成）向通讯作者索取 preprint
- 查论文是否在 arXiv 有预印本（很多 CHI 论文投稿前会上 arXiv）
- 通过学校图书馆「文献传递」服务

## 解读深度分级

根据用户需求调整输出长度：

| 用户说 | 输出深度 |
|--------|----------|
| 「链接就行」 | 仅第五步结果格式 |
| 「简单说说」 | 一句话总结 + 3 条要点 |
| 「帮我精读」 | 完整第六步 + 方法细节 + 图表说明 |
| 「和 UX 工作有什么关系」 | 强调设计启示、可落地建议 |

## 置信度判断

- **高**：DOI/标题+作者+年份完全匹配
- **中**：标题相似、作者部分匹配、年份一致
- **低**：仅关键词或研究方向匹配 → 必须列出候选让用户确认
