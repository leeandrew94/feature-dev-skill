# Feature Dev

**知识驱动开发（KDD）** 的 AI Coding Skill。让 AI 在写代码之前，先读 Obsidian 项目知识库里的架构、规范、表结构、历史决策，确保每次实现都有业务依据，而不是凭空猜测。

## 解决什么问题

AI 写代码很快，但真实业务项目里最难的从来不是代码怎么写，而是：

- 这个需求真正影响哪个模块
- 这个字段背后有什么隐含逻辑
- 那段历史代码还能不能动
- 这个方案符不符合项目现有约定

这个 Skill 的核心规则就一条：**AI 动手写代码前，必须先翻项目知识库。**

## 6 阶段流程

```
需求进入 → 读知识库 → 需求澄清 → 实现计划 → 编码 → 测试 → 归档（手动触发）
```

1. **需求进入** — 拉取或粘贴任务需求
2. **读知识库** — 读取 Obsidian 中的 `INDEX.md`，按需求匹配相关知识文件
3. **需求澄清** — 基于已加载知识提出问题，确保理解到位
4. **实现计划** — 输出带知识依据的改动计划，每个决策都要回答"凭什么"
5. **编码** — 严格按照项目架构和规范实现
6. **归档** — 手动触发，将本次学到的知识沉淀回知识库

## 怎么配置

1. 在 Obsidian 中按项目建立知识库目录，必须有 `INDEX.md`。示例结构：

```
coding/materialPlatform/
├── INDEX.md
├── architecture.md
├── conventions.md
├── schema/
├── sources/
├── decisions/
├── requirements/
└── tests/
```

2. 在 skill 同目录下放 `feature-dev.json`：

```json
{
  "knowledge_base_root": "/Users/xxx/Documents/工作文档/coding"
}
```

Skill 会自动用当前项目目录名匹配 Obsidian 知识库子目录。

3. 在 Claude Code 中调用：

```
/feature-dev
```

## 依赖

- [Obsidian](https://obsidian.md) 项目知识库
- 可选：Obsidian MCP 服务（更丰富的知识读写能力）
- 可选：需求管理 MCP 服务

## 核心设计

- 项目知识放在 Obsidian 里，不散落在 `CLAUDE.md` 或 Cursor Rules 里 — 知识库是团队资产，不绑定某个 Agent
- 实现计划的每个决策必须标注依据：知识库文件 / 代码现状 / 用户确认
- 追踪表把需求点、知识依据、改动位置、验证方式、归档位置串起来
- 知识库描述与代码现状冲突时，标记为"疑似过期"，不以文档为准
