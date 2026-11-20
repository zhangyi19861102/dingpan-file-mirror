# 海外软件下载渠道（GitHub 备用镜像）

## 方案要点
- 钉盘（国内主渠道）原样不动，不做任何改动；历史版本全部留在钉盘。
- GitHub 作为海外独立下载渠道：同一仓库、同一 Release（当前 `v1.1`），三个软件各占自己的附件名，互不干扰。
- **附件只增不删**：同一个 Release 里可以并存同一软件的多个历史版本，文件名自带版本号。
- 发布页按**版本号匹配**决定「海外通道」按钮是否点亮：GitHub 上有这个版本的包 → 按钮可点、直达该文件；没传 → 按钮灰色，提示先用钉盘。这样既不会 404，也能让老版本继续可下载。
- 网页地址固定不变，客户下载到的文件名就是附件原名。

## 仓库信息
- Owner：`zhangyi19861102`
- 仓库名：`dingpan-file-mirror`
- 仓库地址：https://github.com/zhangyi19861102/dingpan-file-mirror
- 网页（GitHub Pages）：https://zhangyi19861102.github.io/dingpan-file-mirror/

## 命名规则（决定按钮能不能点亮）

| 软件 | 附件名格式 | 示例 |
|---|---|---|
| ACC 切割中心 | `ACC_setup_<版本>.exe` | `ACC_setup_1.2.1.2Beta5.exe` |
| 汉邦输出中心 | `Han-Bond-Print-System_<版本>.exe` | `Han-Bond-Print-System_1.0.0.1Beta2.exe` |
| Kimo 企业版 | 原始名（含版本号即可，中文会被 GitHub 去掉） | `kimo-.26-9-3.rar` |
| Kimo 字体包 | 固定名 | `kimo-fonts.rar` |

版本号是匹配的唯一依据：文件名里必须能解析出与发布页一致的版本串
（`1.2.1.2Beta5`、`1.0.0.1Beta2`、`26-9-3`）。

## 当前 Release v1.1 现存附件

| 上传文件名 | 对应软件 | 版本/日期 | 大小 |
|---|---|---|---|
| `ACC_setup_1.2.1.2Beta5.exe` | ACC 切割中心 | 1.2.1.2 Beta05 | 182.1 MB |
| `Han-Bond-Print-System_1.0.0.1Beta2.exe` | 汉邦输出中心 | 1.0.0.1 Beta2 | 64.9 MB |
| `kimo-.26-9-3.rar` | Kimo 企业版 | 26-9-3（2026-09-03） | 155.8 MB |
| `kimo-fonts.rar` | Kimo 字体包（可选） | — | 42.4 MB |

## 发版流程（四个软件同一套）

1. 钉盘上传新版（国内渠道不变）。
2. 把新包放进 `inbox\`，双击 `一键归档.bat`：按类别归档到 `release-assets\`（除字体包外都保留带版本号的名字）并生成本次清单。
3. GitHub 上把 `release-assets\` 里的文件传到 Release `v1.1`——**新版本直接上传，不要去删旧版本**。
4. 双击 `刷新海外通道.bat`：读取 GitHub 上全部附件，按版本号刷新三个发布页的数据（`releases.json` / `releases.js`），并列出哪些版本已点亮。
5. 部署：
   - 输出中心：`publish_to_github.py` 推到 GitHub Pages（`hboc/` 子目录）。
   - ACC / Kimo：在 WorkBuddy 里点一次部署。
6. 把版本号追加到 `RELEASES.md`。

> 输出中心也可以全自动：`hboc_sync.py sync` 会从钉盘拉最新版并按 `Han-Bond-Print-System_<版本>.exe` 上传（旧版本不删）。

## 网页匹配规则（关键字）
- 含 `ACC` → ACC 切割中心
- 含 `hboc` / `han-bond` / `print system` / `输出中心` → 汉邦输出中心
- 含 `字体` / `font` → Kimo 字体包（固定名 `kimo-fonts.rar`）
- 含 `kimo` → Kimo 企业版

## 网页锚点定位
网页支持锚点，进入后自动高亮并滚动定位到对应条目，**文件名本身就是下载直链**，点击文件名即可直接下载：

| 锚点 | 定位条目 |
|---|---|
| `#acc` | ACC Cutting Center Controller |
| `#hboc` | Han-Bond Print System |
| `#kimo` | Kimo Enterprise（kimo 主程序） |
| `#fonts` | Kimo Font Pack（字体包） |

发布页的「海外通道」按主包 `#kimo`、字体包 `#fonts` 分别跳转，用户点进去即看到对应文件被选中。
不带锚点时四个条目全部平铺显示。

## 注意事项
- 普通仓库分支单文件上限 100MB；百兆级安装包必须放 Release（单附件上限 2GB）。
- 不要把安装包直接提交到 main 分支；main 分支只放 `index.html`。
- Release 附件会随版本累积，建议保留最近 10 个左右的版本，旧的再清理（清理后对应页面按钮自动变灰，不会 404）。
- 国内访问 GitHub 较慢属正常，本渠道面向海外用户；国内继续走钉盘。
