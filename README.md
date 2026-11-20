# 海外软件下载渠道（GitHub 备用镜像）

## 方案要点
- 钉盘（国内主渠道）原样不动，不做任何改动；历史版本全部留在钉盘。
- GitHub 作为海外独立下载渠道，只放三个软件的**最新版** + Kimo 字体包。
- 安装包放在 **GitHub Release**，附件保留带版本号的原始文件名；网页打开时自动读取最新 Release，按文件名关键字匹配对应软件并填充下载地址。网页地址不变，客户下载到的文件名即为附件原名。
- 三个软件共用 **同一个仓库、同一个 Release**（当前 tag `v1.1`），互不干扰：ACC 主包、输出中心主包、Kimo 主包、Kimo 字体包各占一个附件名。

## 仓库信息
- Owner：`zhangyi19861102`
- 仓库名：`dingpan-file-mirror`
- 仓库地址：https://github.com/zhangyi19861102/dingpan-file-mirror
- 网页（GitHub Pages）：https://zhangyi19861102.github.io/dingpan-file-mirror/

## 当前最新版（Release v1.1 现存附件）

| 上传文件名 | 对应软件 | 版本/日期 | 大小 |
|---|---|---|---|
| `ACC_setup_1.2.1.2Beta0.exe` | ACC 切割中心 | 1.2.1.2 Beta0 | 182.0 MB |
| `hboc-setup.exe` | 汉邦输出中心 | 1.0.0.1 Beta2 | 64.9 MB |
| `kimo-.26-9-3.rar` | Kimo 企业版 | 26-9-3（2026-09-03） | 155.8 MB |
| `kimo-fonts.rar` | Kimo 字体包（可选） | — | 42.4 MB |

> 输出中心用**固定名** `hboc-setup.exe`（与 ACC/Kimo 保留原名不同）：它由 `hboc_sync.py` 每次从钉盘最新版覆盖上传，页面直链因此不会随版本改名而漂移。

## 后续更新流程
- **输出中心**：不需要手工归档。在 `D:\workbuddy存储路径\2026-11-12-09-26-24\hboc-release-page\` 下依次跑 `hboc_sync.py sync`（钉盘 → 数据 + 自动覆盖上传 `hboc-setup.exe`）→ `verify` → `publish_to_github.py`（推发布页到仓库 `hboc/` 子目录）。
- **ACC / Kimo**：继续用本工具手工归档 + 在 GitHub 上建 Release，或改用各自项目的同步脚本。
1. 钉盘上传新版（国内渠道不变）。
2. 把新包放进本工具 `inbox\`，双击 `一键归档.bat`，脚本按类别归档原名到 `release-assets\` 并生成清单。
3. GitHub 新建 Release（Tag：v1.1 / v1.2 …），把 `release-assets\` 里的原名文件上传，Publish release。
4. 网页自动指向最新版，网页地址和按钮无需改动；按清单把版本号追加到 `RELEASES.md`。

## 网页匹配规则（关键字）
- 含 `ACC` → ACC 切割中心
- 含 `hboc` / `han-bond` / `print system` / `输出中心` → 汉邦输出中心
- 含 `字体` / `font` → Kimo 字体包（固定名 `kimo-fonts.rar`）
- 含 `kimo` → Kimo 企业版（保留版本号原名）

## 网页锚点定位（2026-11-14 新增，2026-11-20 扩充）
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
- 历史版本不上传 GitHub，继续保留在钉盘。
- 国内访问 GitHub 较慢属正常，本渠道面向海外用户；国内继续走钉盘。
- 网页依赖公开 API 读取最新版本；API 不可用时按钮回退到兜底固定名链接。
