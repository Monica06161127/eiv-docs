# EIV Docs — Project Documentation

> **AI × Web3 Agentic Builders Hackathon · Z.AI 赛道**

本仓库包含 EIV 项目的所有文档和资料。

## 文档结构

```
eiv-docs/
├── onboarding/              # 新成员入门文档
│   ├── EIV-DOCS.md          # 完整项目文档（v3，onboarding 真相）
│   └── quick-start.md       # 快速入门指南
├── design/                  # 设计文档
│   ├── DESIGN.md            # 设计细节和第一性推导
│   └── architecture.md      # 架构图和系统设计
├── api/                     # API 文档
│   ├── core-api.md          # Core API 文档
│   └── dashboard-api.md     # Dashboard API 文档
├── deployment/              # 部署指南
│   ├── contracts-deployment.md  # 合约部署指南
│   └── dashboard-deployment.md  # Dashboard 部署指南
└── README.md
```

## 核心文档

### 入门文档
- [EIV-DOCS.md](onboarding/EIV-DOCS.md) - 完整项目文档（v3）
  - 问题定义
  - 系统定位
  - 架构设计
  - 团队分工
  - Week 4 计划

### 设计文档
- [DESIGN.md](design/DESIGN.md) - 设计细节和第一性推导
  - 验证循环
  - Violation Taxonomy
  - Grounding Guard
  - 标准整合

## 快速入门

1. **了解项目**：阅读 [EIV-DOCS.md](onboarding/EIV-DOCS.md)
2. **理解设计**：阅读 [DESIGN.md](design/DESIGN.md)
3. **运行代码**：参考 [eiv-core README](https://github.com/Monica06161127/eiv-core)
4. **查看 Dashboard**：参考 [eiv-dashboard README](https://github.com/Monica06161127/eiv-dashboard)

## 相关仓库

- [eiv-core](https://github.com/Monica06161127/eiv-core) - 核心验证逻辑
- [eiv-dashboard](https://github.com/Monica06161127/eiv-dashboard) - 前端展示层
- [eiv-contracts](https://github.com/Monica06161127/eiv-contracts) - Solidity 合约和部署脚本

## 团队

- **John** — 技术 lead
- **Kieran** — Dashboard / Demo UI
- **Luvia** — 运营 / 协调

## 更新日志

- **2026-06-08**：创建文档仓库，迁移现有文档
- **2026-06-07**：完成 EIV-DOCS.md v3