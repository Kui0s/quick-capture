# 快速记录

语音速记 + AI 润色 → Obsidian。单 HTML 文件 PWA，Android 手机使用。

## 功能
- 语音输入（中文，实时显示）
- AI 自动润色（Claude API，保留原意，修正错别字，分段整理）
- 一键保存到 Obsidian（URI Scheme → Web Share → 剪贴板 三级降级）
- 最近记录历史（本地 10 条）
- 离线可用（Service Worker 缓存）

## 文件
- `index.html` — 主应用（HTML + CSS + JS 全部内联）
- `manifest.json` — PWA 清单
- `sw.js` — Service Worker（离线缓存）

## 部署（GitHub Pages）

1. 创建 GitHub 仓库，上传这 3 个文件
2. 仓库 Settings → Pages → Source 选 "Deploy from a branch" → 选 main 分支 → Save
3. 等 1-2 分钟，访问 `https://你的用户名.github.io/仓库名/`
4. 手机 Chrome 打开该地址 → 菜单 → "添加到主屏幕"

## 手机使用

1. 主屏幕点击"快速记录"图标
2. 首次使用：填入 API Key 和 Obsidian 库名
3. 点击麦克风按钮 → 开始说话
4. 说完点击停止按钮
5. AI 自动润色 → 查看结果
6. 点击"保存到 Obsidian"

## 技术细节
- 语音识别：Web Speech API（`webkitSpeechRecognition`），需要网络
- AI 润色：直接浏览器调用 Claude API（`claude-sonnet-4-20250514`）
- API Key 存储在 localStorage，仅发送到 api.anthropic.com
- Android Chrome `continuous: true` 有自动停止问题，已用 `onend` 自动重启解决
