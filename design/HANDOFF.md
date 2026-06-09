# EIV 项目交接文档

## 项目当前状态

**阶段：Walking Skeleton 完成 ✅**

已完成：
- ✅ 核心验证引擎（predicates.py）— 23/23 测试通过
- ✅ HTTP API（api.py）— 可以接收验证请求
- ✅ 前端 Dashboard（eiv-dashboard）— 基础 UI 完成
- ✅ 链上合约（eiv-contracts）— 已部署到 Sepolia
- ✅ Mock 数据模式 — 前端可独立开发

未完成：
- ❌ 真实链上数据接入（需要 RpcChainAdapter）
- ❌ 真实签名验证（需要 EIP-712 + ecrecover）
- ❌ 真实上链存证（需要写入 ValidationRegistry）

---

## 团队分工

| 成员 | 负责模块 | 当前任务 | 下一步 |
|------|---------|---------|--------|
| John | eiv-core + eiv-contracts | 核心引擎 + 合约开发 | 实现 RpcChainAdapter |
| Kieran | eiv-dashboard | 前端 UI + Mock 模式 | 对接真实 API |
| Luvia | eiv-docs + 协调 | 文档整理 + 团队协调 | 补全文档 + Demo Day 准备 |

---

## 关键文件说明

### eiv-core（验证引擎）

| 文件 | 作用 | 能改吗？ |
|------|------|---------|
| `predicates.py` | 核心判定逻辑 | ❌ 冻结，不要动 |
| `schema.py` | 数据结构定义 | ⚠️ 谨慎修改 |
| `service.py` | 编排流程 | ⚠️ 谨慎修改 |
| `api.py` | HTTP 接口 | ✅ 可以改 |
| `selftest.py` | 测试 | ✅ 可以改 |

### eiv-dashboard（前端）

| 文件 | 作用 | 能改吗？ |
|------|------|---------|
| `index.html` | 页面结构 | ✅ 可以改 |
| `style.css` | 样式 | ✅ 可以改 |
| `app.js` | 逻辑 | ✅ 可以改 |

---

## 下一步计划

### Week 4 目标

1. **John**：实现 RpcChainAdapter，从 Sepolia 真实获取交易数据
2. **Kieran**：Dashboard 对接真实 API，展示真实验证结果
3. **Luvia**：准备 Demo Day 演示材料

### Demo Day 演示流程

```
1. 展示 Dashboard 界面
2. 提交一个验证请求
3. 展示 PASS 的结果（绿色）
4. 提交一个有问题的验证请求
5. 展示 FAIL 的结果（红色 + 违规详情）
6. 展示链上存证记录
```

---

## 紧急联系

- 技术问题 → John
- 前端问题 → Kieran
- 协调问题 → Luvia
- 合约问题 → John

---

## 常见问题

### Q: 怎么跑起来？
```bash
# 终端 1：启动后端
cd eiv-core && python -m eiv.api

# 终端 2：打开前端
cd eiv-dashboard && open index.html
```

### Q: 怎么跑测试？
```bash
cd eiv-core && python -m eiv.selftest
```

### Q: 代码出问题了怎么办？
1. 先跑 `python -m eiv.selftest` 看测试是否通过
2. 检查 `.env` 文件是否配置正确
3. 找 John
