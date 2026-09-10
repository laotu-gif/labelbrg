# labelbrg-site

LabelBridge 主站静态源文件（酒标采购合伙人 / 定位英文站）。

## 目录
- `index.html` — 单页网站（hero / 服务 / 优势 / 流程 / 市场 / FAQ / CTA）
- `favicon.svg` — 撕角标签图标
- `og-image.png` — 1200×630 社交分享图

## 部署
推荐用 Vercel（与 aisenlabel.com 同平台），DNS 留在阿里云解析，无需 ICP 备案。

1. 把仓库推送到 GitHub：
   ```bash
   git init
   git add .
   git commit -m "feat: initial site"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/labelbrg-site.git
   git push -u origin main
   ```
2. 登录 https://vercel.com → Add New Project → Import `labelbrg-site` 仓库 → Deploy
   - Framework Preset: Other
   - Build Command: 留空
   - Output Directory: 留空（默认根目录）
3. Vercel 部署完成后：Project → Settings → Domains
   - 添加 `labelbrg.com`（apex）
   - 添加 `www.labelbrg.com`
   - Vercel 会给出该项目的精确解析记录
4. 去阿里云解析控制台（dns.aliyun.com）：
   - **删除**原 `labelbrg.com` 与 `www` 的两条 CNAME 记录（指向 workbuddy.link 的）
   - **新增** `labelbrg.com` A 记录：`@ A 76.76.21.21`（若 Vercel 卡片显示 216.198.79.1 等其他值，以卡片为准）
   - **新增** `www.labelbrg.com` CNAME：`www CNAME cname.vercel-dns.com`（若 Vercel 卡片显示项目专用值如 `xxx.vercel-dns-017.com`，以卡片为准）
5. 回 Vercel 点 Verify → 几分钟后状态变 Valid Configuration → 自动签发 HTTPS 证书。
6. 在 Vercel Domains 列表里把 `labelbrg.com` 设为 Primary（与 canonical 一致，www 自动跳 apex）。

## 本地预览
直接用浏览器打开 `index.html` 即可；或 `python3 -m http.server 8080`。

## 修改后重新上线
```bash
git add .
git commit -m "update"
git push
```
Vercel 自动部署到 labelbrg.com。
