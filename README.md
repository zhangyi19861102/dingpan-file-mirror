# 海外软件下载渠道（GitHub 备用镜像）

## 方案要点
- 钉盘（国内主渠道）原样不动，不做任何改动；历史版本全部留在钉盘。
- GitHub 作为海外独立下载渠道，只放两个软件的**最新版** + Kimo 字体包。
- 安装包放在 **GitHub Release**，网页用 `releases/latest/download/文件名` 固定链接；只要每次发版附件文件名不变，下载链接永久不变，网页无需改动。

## 仓库信息
- Owner：`zhangyi19861102`
- 仓库名：`dingpan-file-mirror`
- 仓库地址：https://github.com/zhangyi19861102/dingpan-file-mirror
- 网页（GitHub Pages）：https://zhangyi19861102.github.io/dingpan-file-mirror/

## Release 固定附件清单（本次最新版）

本地已在 `release-assets\` 目录按固定文件名备好，直接上传即可：

| 固定附件名 | 来源文件（钉盘备份） | 版本/日期 | 大小 |
|---|---|---|---|
| `ACC_setup.exe` | `ACC_setup_1.2.1.1Beta6.exe` | ACC 1.2.1.1 Beta6 | 182.04 MB |
| `kimo-enterprise.rar` | `kimo-企业版26-9-3.rar` | Kimo 26-9-3（2026-09-03） | 155.80 MB |
| `kimo-fonts.rar` | `kimo字体安装程序.rar` | Kimo 字体包（配套，可选） | 42.39 MB |

> 三个副本已与源文件做过 MD5 校验，一致无损。

## 固定下载链接（releases/latest，永久不变）
```
https://github.com/zhangyi19861102/dingpan-file-mirror/releases/latest/download/ACC_setup.exe
https://github.com/zhangyi19861102/dingpan-file-mirror/releases/latest/download/kimo-enterprise.rar
https://github.com/zhangyi19861102/dingpan-file-mirror/releases/latest/download/kimo-fonts.rar
```
- 附件文件名必须与 `/download/` 后面的名称**完全一致**（大小写敏感）。
- 若更换文件名，网页 `index.html` 链接与 Release 附件名必须同时改。

## 首次部署步骤
1. 仓库根目录上传 `index.html`。
2. 仓库右侧 **Releases → Create a new release**：
   - Tag：`v1.0`
   - Title：`Software v1.0`
   - 把 `release-assets\` 里三个文件拖拽到附件区，保持固定文件名不变。
   - **不要勾选** Pre-release（预发布），否则 `latest` 不识别。
   - Publish release。
3. 仓库 **Settings → Pages**：Source 选 `Deploy from a branch`，Branch 选 `main` / `(root)`，Save。
4. 等待 1–3 分钟，打开 Pages 地址，验证三个按钮都能正常下载。

## 后续更新流程（链接不变）
1. 钉盘上传新版（国内渠道不变）。
2. GitHub 新建 Release（Tag：v1.1 / v1.2 …）。
3. 上传**同名**新版文件（`ACC_setup.exe` / `kimo-enterprise.rar` / `kimo-fonts.rar`），Publish release。
4. `latest` 自动指向最新版，网页和下载链接无需改动。

## 注意事项
- 普通仓库分支单文件上限 100MB；百兆级安装包必须放 Release（单附件上限 2GB）。
- 不要把安装包直接提交到 main 分支；main 分支只放 `index.html`。
- 历史版本不上传 GitHub，继续保留在钉盘。
- 国内访问 GitHub 较慢属正常，本渠道面向海外用户；国内继续走钉盘。
- 若某个 Release 忘记上传同名文件，对应 `latest` 链接会 404。
