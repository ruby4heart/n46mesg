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
- OpenAI API Key 仅保存在当前浏览器本机

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

## OpenAI OCR / 翻译

页面内的「图片识别翻译」功能会：

1. 读取你上传的截图
2. 在浏览器中压缩成 JPEG
3. 调用 OpenAI Responses API
4. 输出识别原文和中文翻译
5. 一键填入消息内容框

默认模型是：

```text
gpt-5-mini
```

API Key 会保存在浏览器 `localStorage`，不会写进仓库，也不会上传到 Cloudflare。请求会直接从你的浏览器发送给 OpenAI。

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
