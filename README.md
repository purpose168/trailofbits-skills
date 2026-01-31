# Trail of Bits 技能市场

这是来自 Trail of Bits 的 Claude Code 插件市场，提供了一系列技能来增强 AI 辅助安全分析、测试和开发工作流。

## 安装

### 添加市场

```
/plugin marketplace add trailofbits/skills
```

### 浏览和安装插件

```
/plugin menu
```

### 本地开发

要在本地添加市场（例如用于测试或开发），请导航到此仓库的**父目录**：

```
cd /path/to/parent  # 例如，如果仓库位于 ~/projects/skills，则应在 ~/projects
/plugins marketplace add ./skills
```

## 可用插件

### 智能合约安全

| 插件 | 描述 |
|------|------|
| [building-secure-contracts](plugins/building-secure-contracts/) | 智能合约安全工具包，包含针对 6 条区块链的漏洞扫描器 |
| [entry-point-analyzer](plugins/entry-point-analyzer/) | 识别智能合约中会改变状态的入口点，用于安全审计 |

### 代码审计

| 插件 | 描述 |
|------|------|
| [audit-context-building](plugins/audit-context-building/) | 通过超细粒度代码分析构建深层架构上下文 |
| [burpsuite-project-parser](plugins/burpsuite-project-parser/) | 从 Burp Suite 项目文件中搜索和提取数据 |
| [differential-review](plugins/differential-review/) | 对代码变更进行安全重点的差异审查，包含 git 历史分析 |
| [semgrep-rule-creator](plugins/semgrep-rule-creator/) | 创建和完善 Semgrep 规则，用于自定义漏洞检测 |
| [semgrep-rule-variant-creator](plugins/semgrep-rule-variant-creator/) | 使用测试驱动验证将现有 Semgrep 规则移植到新的目标语言 |
| [sharp-edges](plugins/sharp-edges/) | 识别易出错的 API、危险配置和"脚枪"设计 |
| [static-analysis](plugins/static-analysis/) | 静态分析工具包，包含 CodeQL、Semgrep 和 SARIF 解析 |
| [testing-handbook-skills](plugins/testing-handbook-skills/) | 来自[测试手册](https://appsec.guide)的技能：模糊测试、静态分析、清理器、覆盖率 |
| [variant-analysis](plugins/variant-analysis/) | 使用基于模式分析在代码库中查找类似漏洞 |

### 验证

| 插件 | 描述 |
|------|------|
| [constant-time-analysis](plugins/constant-time-analysis/) | 检测加密代码中编译器引起的时间侧信道攻击 |
| [property-based-testing](plugins/property-based-testing/) | 针对多种语言和智能合约的属性测试指南 |
| [spec-to-code-compliance](plugins/spec-to-code-compliance/) | 区块链审计的规范到代码合规性检查器 |

### 审计生命周期

| 插件 | 描述 |
|------|------|
| [fix-review](plugins/fix-review/) | 验证修复提交是否解决了审计发现，且没有引入新错误 |

### 逆向工程

| 插件 | 描述 |
|------|------|
| [dwarf-expert](plugins/dwarf-expert/) | 与 DWARF 调试格式交互并理解它 |

### 移动安全

| 插件 | 描述 |
|------|------|
| [firebase-apk-scanner](plugins/firebase-apk-scanner/) | 扫描 Android APK 中的 Firebase 安全配置错误 |

### 开发

| 插件 | 描述 |
|------|------|
| [ask-questions-if-underspecified](plugins/ask-questions-if-underspecified/) | 在实现前澄清需求 |
| [modern-python](plugins/modern-python/) | 现代 Python 工具和最佳实践，使用 uv、ruff 和 pytest |

### 团队管理

| 插件 | 描述 |
|------|------|
| [culture-index](plugins/culture-index/) | 解释个人和团队的 Culture Index 调查结果 |

### 工具

| 插件 | 描述 |
|------|------|
| [claude-in-chrome-troubleshooting](plugins/claude-in-chrome-troubleshooting/) | 诊断和修复 Chrome 中 Claude MCP 扩展连接问题 |

## 奖杯案例

使用 Trail of Bits 技能发现的漏洞。发现了什么？[告诉我们！](https://github.com/trailofbits/skills/issues/new?template=trophy-case.yml)

报告你发现的漏洞时，可以随意提及：
> 使用 [Trail of Bits 技能](https://github.com/trailofbits/skills) 发现

| 技能 | 漏洞 |
|------|------|
| constant-time-analysis | [ML-DSA 签名中的时序侧信道攻击](https://github.com/RustCrypto/signatures/pull/1144) |

## 贡献

我们欢迎贡献！请参阅 [CLAUDE.md](CLAUDE.md) 了解技能创作指南。

## 许可证

本作品采用[知识共享署名-相同方式共享 4.0 国际许可证](https://creativecommons.org/licenses/by-sa/4.0/)授权。

## 关于 Trail of Bits

[Trail of Bits](https://www.trailofbits.com/) 是一家安全研究和咨询公司。
