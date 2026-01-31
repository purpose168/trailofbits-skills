# 构建安全合约

基于 Trail of Bits 的[构建安全合约](https://github.com/crytic/building-secure-contracts)框架的综合智能合约安全工具包。

**作者：** Omar Inuwa

## 概述

此插件为多个区块链平台提供 11 个专业智能合约安全技能：

- **6 个漏洞扫描器**用于平台特定攻击模式
- **5 个开发指南助手**用于安全开发实践

## 安装

```
/plugin install trailofbits/skills/plugins/building-secure-contracts
```

---

## 漏洞扫描器

基于 Trail of Bits 的[不那么智能合约](https://github.com/crytic/not-so-smart-contracts)仓库的特定平台漏洞检测。

### Algorand 漏洞扫描器
**技能：** `/algorand-vulnerability-scanner`

扫描 Algorand/TEAL 代码库中的 11 种漏洞模式，包括：
- 重密钥漏洞
- 未检查的交易费用
- 资产关闭问题
- 组大小检查
- 基于时间的重放攻击
- 以及其他 6 种模式

### Cairo 漏洞扫描器
**技能：** `/cairo-vulnerability-scanner`

分析 StarkNet/Cairo 智能合约中的 6 种漏洞模式：
- 算术溢出/下溢
- 重入
- 未初始化的存储
- 授权绕过
- 以及其他 2 种模式

### Cosmos 漏洞扫描器
**技能：** `/cosmos-vulnerability-scanner`

检测 Cosmos SDK 模块中的 9 种安全问题：
- 解除委托时间验证
- 数量验证
- 解除绑定验证
- 舍入问题
- 以及其他 5 种模式

### Solana 漏洞扫描器
**技能：** `/solana-vulnerability-scanner`

扫描 Solana/Anchor 程序中的 6 个关键漏洞：
- 任意 CPI
- 不正确的 PDA 验证
- 缺少所有权检查
- 签名者授权
- 以及其他 2 种模式

### Substrate 漏洞扫描器
**技能：** `/substrate-vulnerability-scanner`

分析 Substrate  pallet 的 7 个安全问题：
- BadOrigin 处理
- 不足的权重
- 溢出时panic
- 无符号交易验证
- 以及其他 3 种模式

### TON 漏洞扫描器
**技能：** `/ton-vulnerability-scanner`

检测 TON 智能合约中的 3 种漏洞模式：
- 重放保护
- 未保护的接收器
- 发送者验证问题

---

## 开发指南助手

基于 Trail of Bits 的[开发指南](https://github.com/crytic/building-secure-contracts/tree/master/development-guidelines)。

### 审计准备助手
**技能：** `/audit-prep-assistant`

使用综合清单准备代码库进行安全审查：
1. **设定审查目标** - 定义目标和关注点
2. **解决简单问题** - 运行静态分析（Slither、dylint、golangci-lint）
3. **确保可访问性** - 构建说明、固定提交、范围清晰
4. **生成文档** - 流程图、用户故事、术语表

**使用此技能：** 审计前 1-2 周以最大化审查效果。

### 代码成熟度评估器
**技能：** `/code-maturity-assessor`

使用 Trail of Bits 的 9 类别框架进行系统代码成熟度评估：
- 算术安全
- 审计实践
- 认证/访问控制
- 复杂性管理
- 去中心化
- 文档质量
- 交易排序风险
- 低级操作
- 测试和验证

**输出：** 带有基于证据的评分和改进路线图的专业成熟度记分卡。

### 指南顾问
**技能：** `/guidelines-advisor`

综合开发最佳实践顾问，涵盖：
- **文档和规范** - 生成系统描述和架构图
- **架构分析** - 优化链上/链下分布
- **可升级性审查** - 评估升级模式和 delegatecall 代理
- **实现质量** - 审查函数、继承、事件
- **常见陷阱** - 识别安全反模式
- **依赖项** - 评估库使用情况
- **测试** - 建议改进

**使用此技能：** 在整个开发过程中用于架构和实现指导。

### 安全工作流指南
**技能：** `/secure-workflow-guide`

交互式 5 步安全开发工作流：
1. **已知安全问题** - 运行 Slither，包含 70+ 检测器
2. **特殊功能** - 检查可升级性、ERC 合规性、代币集成
3. **视觉检查** - 生成继承图、函数摘要、授权映射
4. **安全属性** - 记录属性，设置 Echidna/Manticore
5. **手动审查** - 分析隐私、前置运行、密码学、DeFi 风险

**使用此技能：** 每次提交或部署前进行持续安全验证。

### 代币集成分析器
**技能：** `/token-integration-analyzer`

对实现和集成进行综合代币安全分析：
- **ERC20/ERC721 合规性** - 验证标准合规性
- **合约组成** - 评估复杂性和 SafeMath 使用
- **所有者权限** - 审查可升级性、铸币、暂停、黑名单
- **20+ 种奇怪代币模式** - 检查非标准行为（缺少返回、转移费用、重基准等）
- **链上分析** - 查询已部署合约的稀缺性和分布
- **集成安全性** - 验证防御模式和安全的转移使用

**使用此技能：** 构建代币或与外部代币集成时。

---

## 技能组织

```
building-secure-contracts/
└── skills/
    ├── algorand-vulnerability-scanner/
    ├── audit-prep-assistant/
    ├── cairo-vulnerability-scanner/
    ├── code-maturity-assessor/
    ├── cosmos-vulnerability-scanner/
    ├── guidelines-advisor/
    ├── secure-workflow-guide/
    ├── solana-vulnerability-scanner/
    ├── substrate-vulnerability-scanner/
    ├── token-integration-analyzer/
    └── ton-vulnerability-scanner/
```

---

## 示例工作流

### 审计前准备
1. 运行 `/secure-workflow-guide` 确保干净的 Slither 报告
2. 使用 `/code-maturity-assessor` 评估整体成熟度
3. 运行 `/audit-prep-assistant` 准备文档和清单
4. 与审计员共享准备好的包

### 特定平台安全审查
1. 为您的平台运行适当的漏洞扫描器
2. 使用 `/guidelines-advisor` 获取实现最佳实践
3. 运行 `/secure-workflow-guide` 进行全面安全检查
4. 解决发现并重新扫描

### 代币开发/集成
1. 运行 `/token-integration-analyzer` 检查合规性和奇怪模式
2. 使用 `/guidelines-advisor` 获取特定于代币的最佳实践
3. 运行 `/secure-workflow-guide` 进行完整验证
4. 自信地部署

### 持续安全
1. 每次提交时运行 `/secure-workflow-guide`
2. 使用平台扫描器进行漏洞检测
3. 使用 `/code-maturity-assessor` 监控代码成熟度
4. 使用 `/guidelines-advisor` 维护文档

---

## 工具集成

许多技能在可用时利用安全工具：
- **Slither** - Solidity 静态分析（70+ 检测器、视觉图表、可升级性检查）
- **Echidna** - 基于属性的模糊测试
- **Manticore** - 符号执行
- **Tealer** - TEAL/PyTeal 静态分析器
- **Web3/Ethers** - 已部署合约的链上查询

**注意：** 当工具不可用时，技能会优雅地适应，转而进行手动分析。

---

## 源材料

此插件基于 Trail of Bits 的开源安全资源：
- [构建安全合约](https://github.com/crytic/building-secure-contracts)
- [不那么智能合约](https://github.com/crytic/not-so-smart-contracts)
- [奇怪的 ERC20](https://github.com/d-xo/weird-erc20)

---

## 相关技能

- **audit-context-building** - 在漏洞挖掘之前构建深层架构上下文
- **issue-writer** - 将发现转化为专业审计报告
- **solidity-poc-builder** - 为 Solidity 漏洞构建概念验证利用

---

## 支持

有问题或问题：
- [Trail of Bits 办公时间](https://meetings.hubspot.com/trailofbits/office-hours) - 每个星期二
- Empire Hacking Slack：#crytic 和 #ethereum 频道
