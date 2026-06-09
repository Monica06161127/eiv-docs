# EIV 合约部署指南

## 前置知识

### 什么是"部署合约"？

**生活类比：** 你在区块链上"开一家店"。

- 区块链 = 一个巨大的商场
- 合约 = 你的店铺
- 部署 = 把店铺"建起来"
- 合约地址 = 你店铺的"门牌号"

### 为什么要部署到 Sepolia？

**Sepolia** 是以太坊的"测试网"：
- 用的是"假钱"（测试币），不花真钱
- 适合开发和测试
- 和主网行为完全一样

---

## 部署步骤

### 第 1 步：准备环境

```bash
cd eiv-contracts
npm install
```

### 第 2 步：配置环境变量

```bash
cp .env.example .env
```

填写 `.env` 文件：
```env
SEPOLIA_RPC_URL=https://rpc.sepolia.org
PRIVATE_KEY=your_private_key_here
ETHERSCAN_API_KEY=your_etherscan_api_key_here
```

**重要：** `PRIVATE_KEY` 绝对不要分享给别人！

### 第 3 步：编译合约

```bash
npm run compile
```

### 第 4 步：运行测试

```bash
npm test
```

### 第 5 步：部署到 Sepolia

```bash
npm run deploy:sepolia
```

**成功输出：**
```
EIVValidationRegistry deployed to: 0x1234...
```

**重要：** 记下这个地址！

### 第 6 步：配置 eiv-core

```bash
cd ../eiv-core
cp .env.example .env
```

在 `.env` 文件中填写：
```env
EIV_VALIDATION_REGISTRY_ADDRESS=0x1234...
```

---

## 已部署的合约

### Sepolia 测试网

| 合约 | 地址 | 状态 |
|------|------|------|
| Identity Registry | `0x8004A818BFB912233c491871b3d84c89A494BD9e` | ✅ 已部署 |
| Reputation Registry | `0x8004B663056A597Dffe9eCcC1965A193B7388713` | ✅ 已部署 |
| Validation Registry | 待部署 | ⏳ Week 4 |
