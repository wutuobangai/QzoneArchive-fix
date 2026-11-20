# QzoneArchive 修复版（QQ 空间记忆找回工具）

> [!WARNING]
> **已失效，暂停下载（2026-11-20）**：2026 年 9 月中旬起，QQ 空间接口有变化，本工具获取动态时返回 HTTP 501，已经拿不到数据（见 #1 #2）。上游 QzoneArchive 已于 2026-09-04 停止维护。在找到可靠办法之前，请不要再下载安装包。


> ⭐ **推荐下载**：[Releases](https://github.com/wutuobangai/QzoneArchive-fix/releases/tag/v1.0.3-patch0829) 里以 `00-Recommended-` 开头的压缩包（安装包 + 中文图文教程，解压就能用）
>
> 🧑‍💻 **维护者 Happy AI · 阿浩**（抖音「跟着阿浩玩Ai」）｜官网 **[wutuobangai.top](https://wutuobangai.top/?utm_source=github&utm_medium=readme&utm_campaign=qzone-20260829)**：ChatGPT Plus / Pro · Claude · Gemini · Grok 会员正规充值，24 小时内交付，有售后｜[AI 免费知识库](https://wutuobangai.top/knowledge.html?utm_source=github&utm_medium=readme)（教程 / 工具 / 资料，不用登录）
> <br>**更多免费工具 · Happy AI**：QQ 空间资料找回来后，也可以试试 [Opus 5.5 中文视频提示词库](https://wutuobangai.top/opus55-video-prompts.html?utm_source=github&utm_medium=readme&utm_campaign=qzone-to-opus55)：在线看 927 条案例，看效果、一键复制。<br>产品广告、科普动画、歌词 MV，都能先挑一个喜欢的效果，再换成自己的内容。<br>[继续逛 AI 免费知识库 →](https://wutuobangai.top/knowledge.html?utm_source=github&utm_medium=readme&utm_campaign=qzone-more-free-tools)
>
> 💬 加阿浩微信（送一次 AI 诊断）：<br><img src="https://cdn.wutuobangai.com/tools/qzone/happyai-wechat-poster-20260923.png" width="320" alt="扫码加阿浩微信">

> 基于 [Gaoshu705/QzoneArchive](https://github.com/Gaoshu705/QzoneArchive)（GPLv3）。本仓库只做两处修复并提供 Windows / macOS 安装包，其余代码与上游 `main` 一致（基线 `269c30f`，2026-08-28）。请优先支持上游作者。

## 修了什么（2026-08-29）

1. **登录过期不再被当成坏页**：QQ 登录态过期时接口返回 `-3000 请先登录`，上游的「永久错误」名单没有这句 → 重试 6 次 → 再被当成坏页记跳过项、往后瞎探。修复版直接提示「登录失效，请重新扫码，进度已保存」。（`src-tauri/src/qzone.rs`）
2. **断点游标有效期 10 分钟 → 24 小时**：登录被踢后重新扫码往往超过 10 分钟，原版会从第一页重走一遍（去重不丢数据但白耗一小时）。（`src-tauri/src/archive.rs`）

两处改动共 42 行，附单元测试（`cargo test` 29/29）。

## 下载

- [Releases](https://github.com/wutuobangai/QzoneArchive-fix/releases/tag/v1.0.3-patch0829)：`QzoneArchive_1.0.3-patch0829_x64-setup.exe`（Windows）· `QzoneArchive_1.0.3-patch0829_universal.dmg`（macOS 通用）
- 使用教程与国内下载：https://wutuobangai.top/qzone-tool.html
- 版本号仍显示 1.0.3，辨认修复版请核对 Release 里的 SHA-256。macOS 包未签名，首次打开右键 → 打开。

## 能找回多远（实测两个号）

- 腾讯只保留最近约 6000 条互动记录。互动少的号能追到 2010 年；互动多的号老的会被顶掉，可能只到 2014 年。
- 没人点赞/评论过的动态找不回，这是接口机制。

## 自己编译

```bash
npm install
npx tauri build --bundles nsis            # Windows
npx tauri build --target universal-apple-darwin --bundles app,dmg   # macOS
```

## 协议与致谢

GPLv3，与上游一致。感谢 Gaoshu705 及贡献者。本仓库由 [灵极乌托邦 AI](https://wutuobangai.com) 维护，仅用于个人备份用途，与腾讯公司无关。
