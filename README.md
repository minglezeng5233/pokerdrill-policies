# HolyGTO Policies Site — GitHub Pages 部署指南

> 这是一个**完全静态**的政策站点，可一键部署到 GitHub Pages（永久免费）或 Cloudflare Pages。

## 📁 文件结构

```
holygto-policies-site/
├── index.html              # 法律中心入口（中英导航）
├── README.md               # 本文件
├── assets/
│   └── style.css           # 暗色赛博风（金桃 + 赛博蓝）
├── en/
│   ├── privacy.html        # English Privacy Policy（v1.0.130+ LLM/IAP 已纳入）
│   ├── terms.html          # English Terms of Service
│   └── delete-account.html # Account Deletion Form (Google Play required)
└── zh/
    ├── privacy.html        # 中文隐私政策
    ├── terms.html          # 中文服务条款
    └── delete-account.html # 中文删除账号
```

---

## 🚀 部署方案 A：GitHub Pages（推荐 / 5 分钟搞定）

### Step 1：创建仓库
```bash
# 1. 在 GitHub 网页端创建一个新公开仓库，名字: holygto-policies
#    (用户：minglezeng5233)

# 2. 本地初始化
cd docs/holygto-policies-site
git init
git add .
git commit -m "Initial: HolyGTO v1.0.136 policy site"
git branch -M main
git remote add origin https://github.com/minglezeng5233/holygto-policies.git
git push -u origin main
```

### Step 2：开启 Pages
1. 进 GitHub 仓库 → **Settings** → **Pages**
2. Source 选 **Deploy from a branch**
3. Branch 选 **main / (root)** → **Save**
4. 1-2 分钟后访问：

```
✅ 法律中心:        https://minglezeng5233.github.io/holygto-policies/
✅ 英文隐私政策:    https://minglezeng5233.github.io/holygto-policies/en/privacy.html
✅ 英文服务条款:    https://minglezeng5233.github.io/holygto-policies/en/terms.html
✅ 英文删除账号:    https://minglezeng5233.github.io/holygto-policies/en/delete-account.html
✅ 中文隐私政策:    https://minglezeng5233.github.io/holygto-policies/zh/privacy.html
✅ 中文服务条款:    https://minglezeng5233.github.io/holygto-policies/zh/terms.html
✅ 中文删除账号:    https://minglezeng5233.github.io/holygto-policies/zh/delete-account.html
```

**这些链接立即可用于 Play Console 提交**，无需买域名。

---

## 🌐 部署方案 B：Cloudflare Pages + 自有域名（专业）

### 前提：买域名 holygto.app
- 推荐 [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/)：约 \$11/年，无加价
- 或 [Namecheap](https://www.namecheap.com/)：首年 \$2，续费 \$13

### Step 1：连接 Cloudflare Pages
1. 登录 [Cloudflare](https://dash.cloudflare.com) → Workers & Pages → Create → **Pages** → Connect to Git
2. 选择你的 `holygto-policies` 仓库
3. 构建设置：
   - Framework preset: **None**
   - Build command: 留空
   - Build output directory: `/`
4. **Save and Deploy** → 几秒后给个 `holygto-policies.pages.dev` 临时域名

### Step 2：绑定 holygto.app
1. Pages 项目 → **Custom domains** → **Set up a custom domain**
2. 输入 `www.holygto.app`（推荐 www）→ 自动添加 CNAME → 1 分钟生效
3. （可选）再加 `holygto.app` 裸域，自动 301 到 www

### Step 3：最终 URL
```
✅ 法律中心:        https://www.holygto.app/
✅ 英文隐私政策:    https://www.holygto.app/en/privacy.html
✅ 英文删除账号:    https://www.holygto.app/en/delete-account.html
✅ 中文隐私政策:    https://www.holygto.app/zh/privacy.html
（其他类推）
```

### Step 4：（可选）干净 URL 美化
在仓库根目录加 `_redirects` 文件：
```
/privacy        /en/privacy.html        302
/terms          /en/terms.html          302
/delete-account /en/delete-account.html 302
/隐私政策       /zh/privacy.html        302
```
让 `holygto.app/privacy` 自动跳到 `/en/privacy.html`，对 Google Play 表单填写更清爽。

---

## ✅ Play Console 填写时直接用的 URL

| Play Console 字段 | 推荐填的 URL（域名版） | 临时备选（GitHub Pages 版） |
|---|---|---|
| Privacy policy URL | `https://www.holygto.app/en/privacy.html` | `https://minglezeng5233.github.io/holygto-policies/en/privacy.html` |
| Account deletion URL（Data safety） | `https://www.holygto.app/en/delete-account.html` | `https://minglezeng5233.github.io/holygto-policies/en/delete-account.html` |
| Terms of service（可选 in-app） | `https://www.holygto.app/en/terms.html` | `https://minglezeng5233.github.io/holygto-policies/en/terms.html` |

---

## 🔄 更新流程

任何政策变更后：
1. 直接编辑对应 `.html` 文件
2. 改顶部 `<p class="meta">` 里的"Last Updated"日期
3. `git add . && git commit -m "Update privacy policy: <reason>" && git push`
4. GitHub Pages / Cloudflare Pages 1-2 分钟自动重新部署

**不要忘记**：v1.0.137+ 引入新数据收集时（如崩溃报告 SDK），同步更新 privacy.html 第 1.3 节。

---

## ⚖️ 内容合规校验清单

| 项 | 状态 |
|---|---|
| 中英文版本完全对应 | ✅ |
| Last Updated 日期一致 | ✅ 2026-04-28 |
| 包含 18+ 受众声明 | ✅ |
| 明确"非真钱赌博"声明 | ✅（见 Terms 第 2.2 节） |
| GDPR / CCPA / PIPL 三大法域提及 | ✅ |
| Google Play / OpenAI / Vultr 第三方披露 | ✅ |
| 删除账号流程含可操作邮件链接 | ✅ |
| 数据保留期表格 | ✅ |
| 联系邮箱可点击 | ✅ |

---

## 📝 已知后续工作

- [ ] **必做**：买域名 `holygto.app` 并绑定（避免审核员看到 `github.io` 觉得不正规）
- [ ] **可选**：加一个简单的 GitHub Issue Template 让用户也能在 Issue 区申请删除
- [ ] **可选**：加多语言切换器（顶部按钮 EN / 中文）
- [ ] **可选**：在 HolyGTO App 内 `app/legal/privacy.tsx` 同步加链接到本站点
