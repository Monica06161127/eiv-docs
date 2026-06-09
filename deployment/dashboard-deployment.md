# EIV Dashboard 部署指南

## 本地运行（开发用）

### 方式 1：直接打开

```bash
cd eiv-dashboard
open index.html
```

### 方式 2：本地服务器

```bash
cd eiv-dashboard
python -m http.server 3000
```

访问 `http://localhost:3000`

---

## 部署到 GitHub Pages（免费）

### 步骤

1. 推送代码到 GitHub
2. 打开仓库 → Settings → Pages
3. Source 选择 `main` 分支
4. 保存，等 1-2 分钟

访问：`https://monica06161127.github.io/eiv-dashboard/`

---

## 部署到 Vercel（推荐）

### 步骤

1. 访问 https://vercel.com，用 GitHub 登录
2. 点击 New Project
3. 选择 eiv-dashboard 仓库
4. 点击 Deploy

访问：`https://eiv-dashboard.vercel.app`

---

## 连接 eiv-core API

Dashboard 默认连接 `http://127.0.0.1:8000`。

如需修改，编辑 `app.js`：
```javascript
const API_BASE = 'https://your-api-server.com';
```
