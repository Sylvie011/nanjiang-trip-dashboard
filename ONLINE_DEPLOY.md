# 南疆网页上线说明

这个目录已经是可上线的静态网站：

- `nanjiang-trip-dashboard.html`：网页本体
- `nanjiang-hero.png`：页面横幅图
- `data/status.json`：机票和天气监控数据

上线后，网页会每60秒自动读取一次 `data/status.json`。只要后台监控任务更新这个文件，所有打开链接的人都会看到新状态。

## GitHub Pages 上线步骤

1. 打开 GitHub，新建一个公开仓库，例如 `nanjiang-trip-dashboard`。
2. 在仓库首页点 `Add file` → `Upload files`。
3. 上传这个目录里的以下内容：
   - `index.html`
   - `nanjiang-trip-dashboard.html`
   - `nanjiang-hero.png`
   - `ONLINE_DEPLOY.md`
   - 整个 `data` 文件夹
4. 点 `Commit changes`。
5. 进入仓库 `Settings` → `Pages`。
6. `Build and deployment` 选择：
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/root`
7. 保存后等待1-3分钟，GitHub 会生成一个公开链接，通常长这样：
   `https://你的用户名.github.io/nanjiang-trip-dashboard/`

朋友打开这个链接就能看到网页。

## 真正实时监控还需要什么

天气可以接天气 API 定时更新 `data/status.json`。

机票价格需要接入可靠航班/OTA数据源，或由浏览器自动化监控携程/飞猪/去哪儿的结果页后写入 `data/status.json`。由于机票价格、余票、行李和退改规则都很动态，建议使用你实际购买平台的数据源，并确认平台允许自动查询。

## 如何更新实时状态

GitHub Pages 会展示仓库里的 `data/status.json`。以后每次监控发现变化，只要更新并提交这个文件，网页上所有人会在最多60秒后看到新内容。

如果手动更新：

1. 打开仓库里的 `data/status.json`。
2. 点右上角铅笔图标编辑。
3. 修改 `updatedAt`、机票价格、天气风险或摘要。
4. 点 `Commit changes`。

如果自动更新：

- 可以用 GitHub Actions 定时任务更新 `data/status.json`。
- 天气可接入天气 API。
- 机票建议先确定数据来源，再做自动化，避免价格和余票不准确。

## 当前状态

当前网页已经支持实时展示，但 `status.json` 仍是初始监控结果。要让朋友看到真正实时变化，需要完成线上托管和后台数据更新任务。
