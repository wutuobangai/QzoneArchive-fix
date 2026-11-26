# QzoneArchive 修复版（QQ 空间记忆找回工具）

> 最后核查：2026-11-26。本次核对仓库说明与原有失效警告；未登录 QQ、未恢复归档或重新验证接口，工具仍按已失效、暂停下载处理。

> **先说明：这个 QQ 空间归档工具已经失效，暂停下载。** 请先看保留的失效说明，不要继续下载安装。
>
> 下方修复记录和能力说明保留为历史记录，不表示工具已恢复可用。
>
> 我是阿浩。我们现在做三件事：[AI 中转站＋直接使用](https://wutuobangai.com)；[帮你开通 ChatGPT、Claude、Gemini、Grok 会员](https://wutuobangai.top)；[AI 课程](https://forms.wutuobangai.com)——在筹备七天以内的集训，带做生意的人把 AI 用起来。
>
> 想看看我们现在做的东西，可以先拿这些免费资料：[AI 实战资料站](https://cal.wutuobangai.com)，看 AI 怎么分工、怎么验收；[中文视频提示词库](https://wutuobangai.top/opus55-video-prompts.html)，挑效果、拿提示词；[3D 动画导演资料](https://github.com/wutuobangai/3d-director/blob/main/README.zh-CN.md)，看小城动画示例、镜头与灯光做法。它们各有用途，都不是 QQ 空间找回工具；用 AI 生成内容所需的账号、环境与费用另算。
>
> 有问题，到 [会员开通站](https://wutuobangai.top) 的微信入口找服务台或阿浩。


> [!WARNING]
> **已失效，暂停下载（2026-11-20）**：2026 年 9 月中旬起，QQ 空间接口有变化，本工具获取动态时返回 HTTP 501，已经拿不到数据（见 #1 #2）。上游 QzoneArchive 已于 2026-09-04 停止维护。在找到可靠办法之前，请不要再下载安装包。


>
>

> 基于 [Gaoshu705/QzoneArchive](https://github.com/Gaoshu705/QzoneArchive)（GPLv3）。本仓库只做两处修复并提供 Windows / macOS 安装包，其余代码与上游 `main` 一致（基线 `269c30f`，2026-08-28）。请优先支持上游作者。

## 修了什么（2026-08-29）

1. **登录过期不再被当成坏页**：QQ 登录态过期时接口返回 `-3000 请先登录`，上游的「永久错误」名单没有这句 → 重试 6 次 → 再被当成坏页记跳过项、往后瞎探。修复版直接提示「登录失效，请重新扫码，进度已保存」。（`src-tauri/src/qzone.rs`）
2. **断点游标有效期 10 分钟 → 24 小时**：登录被踢后重新扫码往往超过 10 分钟，原版会从第一页重走一遍（去重不丢数据但白耗一小时）。（`src-tauri/src/archive.rs`）

两处改动共 42 行，附单元测试（`cargo test` 29/29）。


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
