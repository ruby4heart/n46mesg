# n46mesg

一个用于复刻消息截图排版的单页网页工具。它可以把成员消息按模板排版，并导出为 PNG 图片。

## 功能

- 文字、照片、视频三种消息模板
- 自定义成员名、头像、时间
- 多条消息排序、编辑、删除
- 上传照片或视频封面
- 视频消息播放按钮和「此视频无音频」标记
- 一键导出 PNG
- 图片 OCR + 日文转中文
- 从截图中提取消息时间并填入消息栏
- OpenAI / DeepSeek API Key 仅保存在当前浏览器本机

## 本地使用

直接打开 `index.html` 即可使用。

也可以启动本地静态服务：

```bash
python -m http.server 5173
```

然后访问：

```text
http://127.0.0.1:5173
```

## OCR / 翻译

页面内的「图片识别翻译」功能支持两种 API 服务：

- OpenAI：支持截图 OCR、时间提取、原文识别和中文翻译
- DeepSeek：支持把已识别或手动粘贴的原文翻译成中文

OpenAI 流程会：

1. 读取你上传的截图
2. 在浏览器中压缩成 JPEG
3. 调用 OpenAI Responses API
4. 输出识别时间、原文和中文翻译
5. 一键填入消息时间或消息内容框

DeepSeek 官方 API 当前按文本 Chat Completions 接口接入，本工具不会用 DeepSeek 直接识别图片。使用 DeepSeek 时，请先把日文原文粘贴到「原文」框，再点击翻译。

默认模型：

```text
OpenAI: gpt-5.4-mini
DeepSeek: deepseek-v4-flash
```

API Key 会保存在浏览器 `localStorage`，不会写进仓库，也不会上传到 Cloudflare。请求会直接从你的浏览器发送给所选 API 服务。

请不要把 API Key 写进 `index.html`，也不要提交到 GitHub。

## Cloudflare Pages 部署

这是纯静态网页，可以直接部署到 Cloudflare Pages。

推荐配置：

```text
Framework preset: None / Static HTML
Build command: exit 0
Build output directory: /
Root directory: /
Production branch: main
```

部署后访问 `*.pages.dev` 即可。

## 隐私提醒

- 不要把真实付费消息、偶像照片、视频封面提交到仓库
- 图片识别翻译会把上传的截图发送给 OpenAI API 处理
- API Key 本地保存只适合个人使用，不适合多人共用设备
- 如果要做公开多人使用版，建议改成 Cloudflare Worker / Pages Functions 代理，并把 Key 放进服务端环境变量

## 开发

项目目前只有一个静态文件：

```text
index.html
```

修改后可用浏览器直接打开验证。提交前建议至少检查：

```bash
git status
```
