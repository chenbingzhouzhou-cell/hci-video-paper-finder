# HCI Video Paper Finder — AI Agent Skill

&gt; 一个用于 cursor/Claude/Codex/Kimi等 AI 的 Agent Skill，帮助观众从小红书等人机交互（HCI）科普视频中，快速定位并理解视频中提到的学术论文。

## 适用场景

- 观看小红书 HCI 视频后，想找到视频里提到的 CHI/UIST 论文原文
- 需要获取论文的开放获取 PDF、DOI 链接
- 希望用通俗中文快速理解论文核心内容

## 核心能力

| 步骤 | 功能 |
|------|------|
| 索引匹配 | 优先查询 `video-paper-index.md` 中的视频↔论文对照表 |
| 智能搜索 | 按 DOI → Semantic Scholar → Google Scholar → arXiv → ACM 的优先级定位论文 |
| 链接聚合 | 返回官方页面 + 开放获取 PDF + 预印本链接 |
| 通俗解读 | 用中文总结研究问题、方法、发现与 HCI 设计启示 |

## 文件说明

| 文件 | 作用 |
|------|------|
| `SKILL.md` | Skill 主定义文件，包含完整的工作流程、交互原则与搜索策略 |
| `video-paper-index.md` | 视频与论文对照表（由创作者维护，持续更新） |
| `search-guide.md` | 深度搜索策略参考，用于索引未命中时的补充检索 |

## 使用方法

### 作为经常使用agent用户
1. 将本仓库的 `SKILL.md` 内容粘贴到 AI 会话中（或作为上下文上传三个文件）
2. 向 Agent 提供小红书视频链接、标题、截图或关键词
3. Agent 将自动执行 skill 流程，返回论文链接与解读

### 作为创作者维护索引
每发布一期新视频，在 `video-paper-index.md` 中按格式追加条目：
```markdown
### 视频标题关键词
- 视频链接：https://...
- 发布日期：YYYY-MM-DD
- 论文标题：...
- 作者：...
- 会议/期刊：...
- DOI：...
- 官方链接：...
- 开放 PDF：...
- 备注：...
