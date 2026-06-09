# EIV Core API 文档

## 基础信息

- **地址**：`http://127.0.0.1:8000`（本地开发）
- **格式**：JSON
- **编码**：UTF-8

---

## 接口列表

### 1. 健康检查

**GET** `/healthz`

检查 API 是否正常运行。

**请求**：无需参数

**响应**：
```json
{
  "status": "ok"
}
```

**用途**：Dashboard 显示"连接状态指示灯"

---

### 2. 提交验证请求

**POST** `/submit`

提交一份授权和执行记录，让 EIV 验证。

**请求体**：
```json
{
  "intent": {
    "spec": {
      "target": "0x1234...",
      "recipient": "0xabcd...",
      "amount": "1000000",
      "deadline": 1700000000
    },
    "signer": "0xUser"
  },
  "tx_ref": "tx_001"
}
```

**字段说明**：

| 字段 | 类型 | 说明 | 生活类比 |
|------|------|------|---------|
| `intent.spec.target` | string | 目标合约地址 | 你要去哪家店 |
| `intent.spec.recipient` | string | 接收地址 | 你把钱给谁 |
| `intent.spec.amount` | string | 金额（uint256 字符串） | 给多少钱 |
| `intent.spec.deadline` | number | 截止时间（Unix 时间戳） | 最晚什么时候完成 |
| `intent.signer` | string | 签名者地址 | 谁签的授权 |
| `tx_ref` | string | 交易引用 ID | 这笔交易的"编号" |

**响应**：
```json
{
  "status": "accepted",
  "validation_id": "val_abc123"
}
```

---

### 3. 查看所有验证记录

**GET** `/results`

获取所有已验证的记录列表。

**请求**：无需参数

**响应**：
```json
{
  "results": [
    {
      "validation_id": "val_abc123",
      "tx_ref": "tx_001",
      "verdict": "PASS",
      "n_violations": 0
    },
    {
      "validation_id": "val_def456",
      "tx_ref": "tx_002",
      "verdict": "FAIL",
      "n_violations": 2
    }
  ]
}
```

---

### 4. 查看单条验证详情

**GET** `/results/{validation_id}`

获取某条验证记录的完整详情。

**路径参数**：
- `validation_id`：验证记录 ID（如 `val_abc123`）

**响应**：
```json
{
  "validation_id": "val_abc123",
  "tx_ref": "tx_001",
  "intent": {
    "spec": {
      "target": "0x1234...",
      "recipient": "0xabcd...",
      "amount": "1000000",
      "deadline": 1700000000
    },
    "signer": "0xUser"
  },
  "result": {
    "verdict": "PASS",
    "violations": []
  }
}
```

---

## 错误码

| HTTP 状态码 | 含义 | 常见原因 |
|------------|------|---------|
| 200 | 成功 | - |
| 400 | 请求格式错误 | JSON 格式不对、缺少必填字段 |
| 401 | 签名验证失败 | 授权签名无效 |
| 404 | 找不到记录 | validation_id 不存在 |
| 500 | 服务器内部错误 | 代码 bug |

---

## 使用示例

### 用 curl 测试

```bash
# 1. 健康检查
curl http://127.0.0.1:8000/healthz

# 2. 提交验证请求
curl -X POST http://127.0.0.1:8000/submit \
  -H "Content-Type: application/json" \
  -d '{
    "intent": {
      "spec": {
        "target": "0x1234",
        "recipient": "0xabcd",
        "amount": "1000000",
        "deadline": 1700000000
      },
      "signer": "0xUser"
    },
    "tx_ref": "tx_001"
  }'

# 3. 查看所有结果
curl http://127.0.0.1:8000/results

# 4. 查看单条详情
curl http://127.0.0.1:8000/results/val_abc123
```
