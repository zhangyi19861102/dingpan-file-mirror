# 海外软件下载渠道（GitHub 备用镜像）

## 方案要点
- 钉盘（国内主渠道）原样不动，不做任何改动；历史版本全部留在钉盘。
- GitHub 作为海外独立下载渠道，只放两个软件的**最新版** + Kimo 字体包。
- 安装包放在 **GitHub Release**，附件保留带版本号的原始文件名；网页打开时自动读取最新 Release，按文件名关键字匹配对应软件并填充下载地址。网页地址不变，客户下载到的文件名即为附件原名。

## 仓库信息
- Owner：`zhangyi19861102`
- 仓库名：`dingpan-file-mirror`
- 仓库地址：https://github.com/zhangyi19861102/dingpan-file-mirror
- 网页（GitHub Pages）：https://zhangyi19861102.github.io/dingpan-file-mirror/

## 本次最新版（release-assets\）

| 上传文件名（保留原名） | 版本/日期 | 大小 |
|---|---|---|
| `ACC_setup_1.2.1.1Beta6.exe` | ACC 1.2.1.1 Beta6 | 182.04 MB |
| `kimo-企业版26-9-3.rar` | Kimo 26-9-3（2026-09-03） | 155.80 MB |
| `kimo-fonts.rar` | Kimo 字体包（配套，可选） | 42.39 MB |

> 三个文件已与钉盘源文件做过 MD5 校验，一致无损。

## 后续更新流程
1. 钉盘上传新版（国内渠道不变）。
2. 把新包放进本工具 `inbox\`，双击 `一键归档.bat`，脚本按类别归档原名到 `release-assets\` 并生成清单。
3. GitHub 新建 Release（Tag：v1.1 / v1.2 …），把 `release-assets\` 里的原名文件上传，Publish release。
4. 网页自动指向最新版，网页地址和按钮无需改动；按清单把版本号追加到 `RELEASES.md`。

## 网页匹配规则（关键字）
- 含 `ACC` → ACC 切割中心
- 含 `ACC` → ACC 切割中心（保留版本号原名）
- 含 `字体` / `font` → Kimo 字体包（固定名 `kimo-fonts.rar`）
- 含 `kimo` → Kimo 企业版（保留版本号原名）

## 网页锚点定位（2026-11-14 新增）
网页支持锚点，进入后自动高亮并滚动定位到对应条目，**文件名本身就是下载直链**，点击文件名即可直接下载：

| 锚点 | 定位条目 |
|---|---|
| `#acc` | ACC Cutting Center Controller |
| `#kimo` | Kimo Enterprise（kimo 主程序） |
| `#fonts` | Kimo Font Pack（字体包） |

发布页的「海外通道」按主包 `#kimo`、字体包 `#fonts` 分别跳转，用户点进去即看到对应文件被选中。
不带锚点时三个条目全部平铺显示。

## 注意事项
- 普通仓库分支单文件上限 100MB；百兆级安装包必须放 Release（单附件上限 2GB）。
- 不要把安装包直接提交到 main 分支；main 分支只放 `index.html`。
- 历史版本不上传 GitHub，继续保留在钉盘。
- 国内访问 GitHub 较慢属正常，本渠道面向海外用户；国内继续走钉盘。
- 网页依赖公开 API 读取最新版本；API 不可用时按钮回退到兜底固定名链接。
