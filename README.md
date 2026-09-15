# jiaoman-releases

「胶漫」的**发布产物仓**（只放安装包与版本清单，源码不在这里）。

源码仓库是私有的；这个仓公开，是为了让应用能通过 CDN 直接读取版本信息 —— 应用里因此不需要、也不应该内置任何 GitHub token。

## 文件说明

| 文件 | 用途 |
| --- | --- |
| `version.json` | 版本清单：`versionCode` / `versionName` / `apk` / `sha256` / `size` / `notes` |
| `apk/JiaoMan-<版本>-release.apk` | 正式签名安装包（保留最近 3 个版本） |

## 应用侧读取顺序

1. `https://cdn.jsdelivr.net/gh/sd8288288/jiaoman-releases@main/version.json`（首选）
2. `https://ghproxy.net/https://raw.githubusercontent.com/sd8288288/jiaoman-releases/main/version.json`
3. `https://ghfast.top/...`
4. `https://gh-proxy.com/...`

APK 同样按以上镜像顺序下载，下载后校验 `sha256`，安装前再比对签名。

## 发布方式

在源码仓执行：

```powershell
powershell -File tools\publish-release.ps1 -Notes "本次更新说明"
```

不要手改本仓的文件 —— 都由脚本生成，手改会导致 sha256 与清单不一致、应用拒绝安装。
