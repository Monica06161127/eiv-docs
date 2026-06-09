# EIV 架构设计文档

## 一句话总结

EIV = 检查 AI agent 有没有"照章办事"的审计系统。

---

## 系统全景图

```
用户签名授权 ──▶ AI Agent 执行交易 ──▶ EIV 验证引擎 ──▶ 链上存证
    │                  │                    │                │
    │                  │                    │                │
 IntentSpec        实际操作             判定结果          ERC-8004
 (合同)           (执行记录)           (审计报告)        (公证处)
```

---

## 四大模块

### 1. eiv-core（验证引擎）🔑

**类比：审计员**

职责：
- 接收"授权书"（IntentSpec）和"执行记录"（ExecutionTrace）
- 逐条对比，找出差异
- 输出"审计报告"（PASS / FAIL + violations）

关键文件：
- `predicates.py` — 核心判定逻辑（审计员的"检查清单"）
- `service.py` — 编排流程（审计员的"工作流程"）
- `api.py` — HTTP 接口（审计员的"接待窗口"）

### 2. eiv-dashboard（前端展示）🖥️

**类比：审计报告的"展示板"**

职责：
- 调用 eiv-core 的 API 获取验证结果
- 展示"授权 vs 执行"的差异对比
- 用颜色标记 PASS（绿色）、FAIL（红色）、WARN（黄色）

关键文件：
- `index.html` — 页面结构
- `style.css` — 样式（暗色主题）
- `app.js` — 逻辑（API 调用 + 渲染）

### 3. eiv-contracts（链上合约）📜

**类比：公证处**

职责：
- 提供链上存储空间
- 记录验证结果（谁验证了什么，结果是什么）
- 基于 ERC-8004 标准

关键文件：
- `EIVValidationRegistry.sol` — 核心合约（公证处的"存档柜"）
- `scripts/deploy.js` — 部署脚本（把公证处"建起来"）

### 4. eiv-docs（项目文档）📚

**类比：员工手册**

职责：
- 记录项目的设计决策
- 帮助新成员快速上手
- 作为 Hackathon 评审的参考材料

关键文件：
- `EIV-DOCS.md` — 完整项目文档
- `DESIGN.md` — 设计细节
- `ARCHITECTURE.md` — 本文件

---

## 数据流（详细版）

```
第 1 步：用户签署授权
         │
         ▼
   IntentSpec（JSON 格式）
   包含：目标合约、接收地址、金额上限、截止时间等
         │
         ▼
第 2 步：AI Agent 执行交易
         │
         ▼
   ExecutionTrace（交易记录）
   包含：实际调用了哪个合约、实际转了多少、实际发给了谁
         │
         ▼
第 3 步：EIV 验证引擎检查
         │
         ▼
   对比 IntentSpec 和 ExecutionTrace
   检查项：
   - 目标合约对不对？（A:Target）
   - 接收地址对不对？（B:Recipient）
   - 金额有没有超？（D:Amount）
   - 有没有过期？（F:Deadline）
   - 余额有没有残留？（G:Residual）
         │
         ▼
第 4 步：输出验证结果
         │
         ▼
   {
     "verdict": "PASS" 或 "FAIL",
     "violations": [...]
   }
         │
         ▼
第 5 步：上链存证（ERC-8004）
         │
         ▼
   写入 Sepolia 测试网的 ValidationRegistry 合约
```

---

## Violation 分类（违规类型）

| 类别 | 含义 | 生活类比 |
|------|------|---------|
| A:Target | 目标合约不对 | 你要转账给张三，AI 转给了李四 |
| B:Recipient | 接收地址不对 | 你要寄快递到北京，AI 寄到了上海 |
| C:Authorization | 授权被扩大 | 你只授权了 100 元，AI 花了 200 元 |
| D:Amount | 金额超限 | 你说了最多花 100，AI 花了 150 |
| E:Slippage | 滑点超限 | 你说了最多亏 5%，AI 亏了 10% |
| F:Deadline | 已过期 | 你说了 3 点前完成，AI 4 点才做 |
| G:Residual | 余额残留 | 你说了用完就关，AI 留了个"尾巴" |

---

## 为什么这样设计？

### 原则 1：确定性（Deterministic）

同一个输入，永远得到同一个输出。

**类比：** 1 + 1 永远等于 2，不会因为"今天心情好"变成 3。

### 原则 2：可替换接口（Replaceable Interface）

每个模块都通过"接口"连接，可以随时换实现。

**类比：** 你家的插座是标准的，你可以换台灯、换风扇，不用改电线。

### 原则 3：零依赖（Zero Dependencies）

eiv-core 不依赖任何第三方库，只用 Python 标准库。

**类比：** 你的手机不需要联网也能打电话——基础功能不依赖外部。
