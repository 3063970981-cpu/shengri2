# A Little Wish For You · 黄相焓的21岁生日贺卡

实际项目使用 Vite + React + Motion for React + CSS，蛋糕、数字蜡烛、火焰与烟雾由 SVG/CSS 分层绘制，无图片依赖。

## 本地预览

安装 Node.js 22.12+（推荐 24 LTS），在此文件所在的 birthday-card 目录打开终端：

```sh
npm install
npm run dev
```

打开终端显示的地址（通常 http://localhost:5173）。可用同一 Wi-Fi 的手机访问终端的 Network 地址。

生产构建与预览：

```sh
npm run build
npm run preview
```

不要双击 index.html；请通过上面的本地服务打开。

## 背景音乐（已添加）

已将用户提供的生日快乐八音盒 MP3 放到：

```
public/audio/happy-birthday.mp3
```

音乐文件已包含在源码与构建产物中。网页会实际请求并校验 MP3 文件头；日后移除文件或服务器返回 HTML 时会显示“音乐素材待准备”。

首次点击 OPEN YOUR CARD 后才尝试播放，700ms 淡入到 0.35 音量，循环播放；切换场景、许愿、重新播放均不重建音频。右上角按钮支持淡出暂停与淡入恢复。浏览器阻止播放时会提示手动重试。素材检查尚未完成时打开贺卡，可在检查完成后点击音乐按钮开始。

## 修改文案

所有主要文案集中在 src/config.js。样式在 src/style.css，交互在 src/main.jsx。

## 互动顺序

1. 打开贺卡：CSS 3D 翻开书页、蛋糕升起，约 1.9 秒后可点蜡烛。
2. 点击数字蜡烛附近的透明大按钮，或下方提示按钮：锁定重复操作，火焰 0.5 秒内倾斜熄灭，同时飘起烟雾。
3. 熄灭后约 1 秒弹出许愿卡。
4. 点击“我许好愿啦 ♡”：显示完整祝福，播放一次纸屑与星星庆祝。
5. 最后祝福信右下角的小紫星，连续点击三次（相邻点击间隔不超过 1.4 秒）打开彩蛋。
6. “重新播放”会重置贺卡与彩蛋，音乐保持原状态。

支持键盘操作、弹窗焦点、手机竖屏和 prefers-reduced-motion；减少动画时停用持续漂浮与纸屑，缩短翻页、蛋糕升起和火焰动画。

## 发布到 Vercel

方式一：把本目录内容上传到自己的 GitHub 仓库，在 Vercel 选择 Add New → Project 并导入仓库。若上传的是更大的上层目录，将 Root Directory 指向 birthday-card 所在目录。

- Framework Preset：Vite
- Build Command：npm run build
- Output Directory：dist
- Node.js：24.x（或受支持的 22.x）

确认音乐文件也提交到 public/audio，点击 Deploy。已附 vercel.json 预设构建信息。

方式二：在本目录执行 `npx vercel` 并按提示登录、部署，正式发布执行 `npx vercel --prod`。

官方说明：https://vercel.com/docs/frameworks/frontend/vite
Vite 部署说明：https://vite.dev/guide/static-deploy

无需后端、密钥或环境变量。本项目未代为发布，发布后可以把网址分享给收件人。


## Vercel 登录报 ByteString 错误时

如果 Windows 电脑名称含中文，Vercel CLI 的登录请求可能报 ByteString 错误。已附 vercel-helper.cjs，仅对当前工具进程使用英文设备名称，不修改 Windows 设置。

在项目目录运行：

```powershell
node .\vercel-helper.cjs login
```

完成浏览器登录授权后，再运行：

```powershell
node .\vercel-helper.cjs --prod
```
