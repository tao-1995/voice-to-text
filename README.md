# 猫咪语音转写

纯离线音频转汉字：导入音频文件或麦克风录音，本地识别为中文文本，可导出 txt 与 SRT 字幕。

**免费分享** · 获取来源：小红书 **VibeCoding西星（账号：6107975461）**

同一来源在程序内有三处标注，便于转发时核对出处：底部状态栏、关于页（程序名下方 + 来源渠道行 + 页脚）、首次启动提示。

状态：**V1.0.0 正式版已打包**（自包含 win-x64，安装后离线可用，目标机不要求安装 .NET 或 FFmpeg）。支持录音转写、文件转写（批量、可编辑、TXT/SRT 导出）、设置与关于四页。

下载产物在 `dist/CatStt-1.0.0/`（免解压目录）与 `dist/CatStt-1.0.0-portable.zip`（便携包），校验值见 `dist/SHA256SUMS.txt`，交付记录见 [docs/release.md](docs/release.md)。

环境与运行步骤见 [docs/environment.md](docs/environment.md)；分期进度与已确认事项见 [docs/progress.md](docs/progress.md)。

## 项目结构

- `src/CatStt.App/`：WPF 界面、页面与窗口；`Assets/Cats/` 猫咪素材（`icon-cat.png` 为程序图标，透明底 256×256）；`Assets/App/CatStt.ico` 为 exe 与窗口图标（多尺寸）。
- `src/CatStt.Core/`：纯领域层（分段模型、SRT 构建、导出、模型校验、配置）。
- `src/CatStt.Media/`：FFmpeg 解码、Silero VAD 分段、SenseVoice 识别、录音采集与转写流水线。
- `config/distribution.json`：免费与获取来源配置。打包时随包分发为 exe 同级的 `distribution.json`，状态栏、关于页、首次启动提示都从这里取文案，界面不硬编码渠道。
- `.envs/`：本项目 SDK、FFmpeg —— 均为指向工作区共享组件库 `components/` 的目录链接，实体只存一份；`.cache/`：开发依赖缓存（同为链接）。
- `build/`：构建输出与中间文件；`dist/`：交付包。

## 开发

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File "F:\AIProject\miniProgram\projects\voice-to-text\scripts\dev.ps1" -Action Build
```

其余动作：`Run`（开发运行）、`Check`（启动自检）、`M2Smoke` / `M3Smoke`（无人操作冒烟）、`UiShot`（四页截图到 `build/ui-*.png`）、`Transcribe -InputFile <wav>`。

打包：`scripts/publish.ps1 -Version 1.0.0`（`Publish` / `Zip` / `Dist` / `Verify` / `Clean`，默认 `All`）。打包产物中**不含 README**；随包附「使用说明」「获取来源说明」「LICENSE」「THIRD-PARTY-NOTICES」。
