# 贡献技能

## 资源

**官方 Anthropic 文档（始终优先查看这些）：**

- [Claude Code 插件](https://docs.anthropic.com/en/docs/claude-code/plugins)
- [代理技能](https://docs.anthropic.com/en/docs/claude-code/skills)
- [最佳实践](https://docs.anthropic.com/en/docs/claude-code/skills#best-practices)

**参考技能** - 通过不同复杂程度的示例学习：

| 复杂度 | 技能 | 演示内容 |
|--------|------|----------|
| **基础** | [ask-questions-if-underspecified](plugins/ask-questions-if-underspecified/) | 最小的前置元数据，简单指导 |
| **中级** | [constant-time-analysis](plugins/constant-time-analysis/) | Python 包，references/，语言特定文档 |
| **高级** | [culture-index](plugins/culture-index/) | 脚本，workflows/，templates/，PDF 提取，多个入口点 |

**有疑问时，复制其中一个并 adapting 它。**

**技能创作深度文章：**
- [Claude 技能深度剖析](https://leehanchung.github.io/blogs/2025/10/26/claude-skills-deep-dive/) - 技能架构的全面分析
- [Claude Code 技能训练](https://huggingface.co/blog/sionic-ai/claude-code-skills-training) - 实用创作指南

**值得研究的示例插件：**
- [superpowers](https://github.com/obra/superpowers) - 高级工作流模式，TDD 强制执行，多技能编排
- [compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin) - 生产级插件结构

**对于 Claude：** 使用 `claude-code-guide` 子代理处理插件/技能问题 - 它可以访问官方文档。

## 技术参考

### 插件结构

```
plugins/
  <plugin-name>/
    .claude-plugin/
      plugin.json         # 插件元数据（名称、版本、描述、作者）
    commands/             # 可选：斜杠命令
    agents/               # 可选：自主代理
    skills/               # 可选：知识/指导
      <skill-name>/
        SKILL.md          # 带有前置元数据的入口点
        references/       # 可选：详细文档
        workflows/        # 可选：逐步指南
        scripts/          # 可选：实用脚本
    hooks/                # 可选：事件钩子
    README.md             # 插件文档
```

**重要**：组件目录（`skills/`、`commands/`、`agents/`、`hooks/`）必须在插件根目录，**不是**在 `.claude-plugin/` 内。只有 `plugin.json` 属于 `.claude-plugin/`。

### 前置元数据

```yaml
---
name: skill-name              # 短横线命名，最大 64 字符
description: "第三人称描述，说明它是做什么的以及何时使用"
allowed-tools:                # 可选：限制为需要的工具
  - Read
  - Grep
---
```

### 命名约定

- **短横线命名**：使用 `constant-time-analysis`，而不是 `constantTimeAnalysis`
- **优先使用动名词形式**：使用 `analyzing-contracts`、`processing-pdfs`（而不是 `contract-analyzer`、`pdf-processor`）
- **避免模糊名称**：不要使用 `helper`、`utils`、`tools`、`misc`
- **避免保留词**：不要使用 `anthropic`、`claude`

### 路径处理

- 使用 `{baseDir}` 表示路径，**永远不要**硬编码绝对路径
- 即使在 Windows 上也使用正斜杠（`/`）

### Python 脚本

当技能包含带有依赖项的 Python 脚本时：

1. **使用 PEP 723 内联元数据** - 在脚本头部声明依赖项：
   ```python
   # /// script
   # requires-python = ">=3.11"
   # dependencies = ["requests>=2.28", "pydantic>=2.0"]
   # ///
   ```

2. **使用 `uv run`** - 启用自动依赖解析：
   ```bash
   uv run {baseDir}/scripts/process.py input.pdf
   ```

3. **包含 `pyproject.toml`** - 保存在 `scripts/` 中用于开发工具（ruff 等）

4. **记录系统依赖项** - 在工作流中列出非 Python 依赖项（poppler、tesseract），并提供特定平台的安装命令

### 钩子

PreToolUse 钩子在每个 Bash 命令上运行——性能至关重要：

- **优先使用 shell + jq** 而不是 Python——解释器启动（Python + tree-sitter）会添加明显的延迟
- **快速失败** - 对于不匹配的命令立即退出 0，以便大多数调用是即时的
- **优先使用正则表达式而不是 AST 解析** - 如果性能提升显著且 Claude 可以重新表述，接受罕见的误报
- **预期误报模式** - 诊断命令（`which python`）、搜索工具（`grep python`）和文件名（`cat python.txt`）不应触发拦截
- **在 PR 描述中记录权衡** - 让审查者理解故意设计的选择

## 质量标准

这些是 Trail of Bits 在 Anthropic 要求之上的内部标准。

### 描述质量

你的技能与 100+ 其他技能竞争。描述必须正确触发。

- **第三人称语气**："Analyzes X" 而不是 "I help with X"
- **包含触发词**："Use when auditing Solidity" 而不是仅仅 "Smart contract tool"
- **具体**："Detects reentrancy vulnerabilities" 而不是 "Helps with security"

### 增值

技能应该提供 Claude 不 already 拥有的指导，而不是重复参考资料。

- **行为指导 over 参考资料转储** - 不要粘贴整个规范；教何时以及如何查找
- **解释 WHY，而不仅仅是 WHAT** - 包含权衡、决策标准、判断
- **用解释记录反模式** - 说明为什么是错误的，而不仅仅是它是错误的

**示例**：DWARF 技能不包括完整的 DWARF 规范。它教会 Claude 如何使用 `dwarfdump`、`readelf` 和 `pyelftools` 来查找所需内容，加上关于何时使用每个工具的判断。

### 范围边界

规定性应匹配任务风险：

- **对 fragile 任务严格** - 安全审计、加密实现、合规检查需要严格的逐步强制执行
- **对可变任务灵活** - 代码探索、文档、重构可以提供选项和判断

### 必需部分

每个 SKILL.md 必须包含：

```markdown
## 何时使用
[此技能适用的具体场景]

## 何时不使用
[其他方法更好的场景]
```

### 安全技能

对于审计/安全技能，还要包含：

```markdown
## 要拒绝的合理化
[导致遗漏发现的常见捷径或合理化]
```

### 内容组织

- 保持 SKILL.md **在 500 行以下** - 拆分为 `references/`、`workflows/`
- 使用**渐进式披露** - 快速入门在前，详细内容在链接文件中
- **一级深度** - SKILL.md 链接到文件，文件不要链到更多文件

注意：目录深度没问题（`references/guides/topic.md`）。参考*链*不行（`SKILL.md → file1.md → file2.md`，其中 file1 引用 file2）。问题是链式引用，不是嵌套文件夹。

### 渐进式披露模式

```markdown
## 快速入门
[核心说明在此]

## 高级用法
详见 [高级用法](references/ADVANCED.md) 了解详细模式。

## API 参考
详见 [API](references/API.md) 了解完整的方法文档。
```

## PR 清单

提交前：

**技术（CI 验证这些）：**
- [ ] 有效的 YAML 前置元数据，包含 `name` 和 `description`
- [ ] 名称为短横线命名，≤64 字符
- [ ] 所有引用的文件存在
- [ ] 没有硬编码路径（`/Users/...`、`/home/...`）

**质量（审查者检查这些）：**
- [ ] 描述正确触发（第三人称、具体）
- [ ] 包含"何时使用"和"何时不使用"部分
- [ ] 示例是具体的（输入 → 输出）
- [ ] 解释 WHY，而不仅仅是 WHAT

**文档：**
- [ ] 插件有 README.md
- [ ] 添加到根目录 README.md 表格
- [ ] 在 marketplace.json 中注册
