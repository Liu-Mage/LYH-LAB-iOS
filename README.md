# LYH LAB 项目采购管理 · iOS v0.1.1 源码交接

请完整解压。ZIP 内的根目录就是可作为 GitHub 仓库根目录的工程，不是可安装包。

| 内容 | 位置 / 说明 |
| --- | --- |
| 原生 SwiftUI | `LYHLab/LYHLabApp.swift`、`Models.swift`，原始 Swift 源文件保留 |
| Xcode 工程 | `LYHLab.xcodeproj`（含共享 LYHLab scheme）、构建设置及生成 Info.plist 配置 |
| 原生资源 | `LYHLab/Assets.xcassets`（已加入 Resources）、`Design/AppIcon.svg` 可编辑图标源 |
| 网站 API | `LYHLab/API.swift`：现有 HTTPS API、会话和 CSRF、项目、采购、报表；不替换证书验证 |
| 依赖 | SwiftUI / Foundation / Combine / UniformTypeIdentifiers 均为 Apple SDK 自带；本原生 target 无 SwiftPM 或 CocoaPods 依赖，无需 Package.resolved。iOS 最低 16.0。 |
| N1 原实现 | `References/N1-Web`：独立 Web Bluetooth 驱动、DM / QR 页面、样张、生成脚本、原始依赖配置和第三方许可证 |
| Windows 打包试验 | `README-WINDOWS-SIDESTORE.md` 和 `.github/workflows/ios-unsigned.yml` |
| 校验 | `verify_source.py`、`Tests/ModelsSmoke.swift`、`SHA256SUMS.txt` |

## 特别说明
- N1 相关源文件供后续移植，**没有接入 iOS target，不是已可用的 iOS 蓝牙打印驱动**。现有 Web Bluetooth 实现不能直接在普通 iPhone Safari 使用；SideStore 也不会让网页驱动变成 CoreBluetooth。DM 样张是演示，只能用于验证，不能写入正式库存。
- N1 Web 预构建页面在 `dist/`，无运行时安装步骤；JS 驱动、二维码及 ZXing JS/WASM 连同许可和版本来源已保留。若重新生成样张，脚本需要 Python 和 Pillow、numpy、qrcode、zxing-cpp（原说明 DM 生成用 3.1.1），以及脚本使用的字体；不属于 iOS 构建依赖。为避免传播部署配置，包内不含诊断站托管配置；仅省略内部自测结果并在两个非执行性文档中去除内部路径或设备序列，不改打印/扫码代码或许可证。
- 本包不含 Apple 密码、网站密码、签名证书、私钥、配对文件、生产数据库或正式采购记录。公开版不含生产网站/API 地址，登录时由本人填写 HTTPS 根地址。已按本次授权准备公开源码；本地输入的账号、会话、生产数据与签名材料仍不得上传。
- Linux 已运行结构和 N1 软件脚本检查；未运行 Xcode、GitHub Actions、SideStore 或 iPhone 验收。CI 产物若成功，也需要在用户设备上依法签名后再尝试安装。
