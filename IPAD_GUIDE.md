# 🍎 iPad 部署指南

本文档介绍如何将贪吃蛇游戏部署到 iPad 上游玩。

---

## 方法一：GitHub Pages（推荐）

**最简单的方式，无需任何工具**

### 步骤

1. 将代码推送到 GitHub 仓库
2. 进入仓库 **Settings** → **Pages**
3. Source 选择 **Deploy from a branch**
4. Branch 选择 **main**，目录选择 **/ (root)**
5. 点击 **Save**
6. 等待几分钟，访问 `https://你的用户名.github.io/仓库名/`

### 在 iPad 上添加到主屏幕

1. 用 Safari 打开游戏网址
2. 点击底部的「分享」按钮（方框带向上箭头）
3. 选择「添加到主屏幕」
4. 命名为「贪吃蛇」并添加

这样就可以像原生 App 一样从桌面启动游戏了！

---

## 方法二：本地服务器 + 局域网访问

**适合开发调试，不需要上传到服务器**

### Mac 端操作

```bash
# 进入项目目录
cd /Users/zhangtao/Sourcecode/github/snakeFood

# 启动简单的 HTTP 服务器（Python 3）
python3 -m http.server 8080

# 或者用 Node.js（需先安装）
npx serve -p 8080
```

### 查看 Mac 的 IP 地址

```bash
# 方法1：系统偏好设置 → 网络
# 方法2：终端运行
ipconfig getifaddr en0
```

假设显示 `192.168.1.100`

### iPad 端操作

1. 确保 iPad 和 Mac 连接同一个 Wi-Fi
2. 打开 Safari，访问 `http://192.168.1.100:8080`
3. 同上，可以「添加到主屏幕」

---

## 方法三：Pythonista（纯 iPad 方案）

**如果你有 Pythonista App，可以完全在 iPad 上运行**

1. 在 iPad 上安装 [Pythonista](https://apps.apple.com/app/pythonista-3/id1085978097)（付费 App，约 ¥68）
2. 将 `index.html` 内容复制到 Pythonista
3. 运行以下代码启动服务器：

```python
import http.server
import socketserver
import webbrowser
import os

PORT = 8080
os.chdir(os.path.expanduser('~/Documents'))

Handler = http.server.SimpleHTTPRequestHandler

with socketserver.TCPServer(("", PORT), Handler) as httpd:
    print(f"游戏运行在 http://localhost:{PORT}")
    webbrowser.open(f'http://localhost:{PORT}')
    httpd.serve_forever()
```

---

## 方法四：iCloud Drive + Scriptable

1. 安装 [Scriptable](https://apps.apple.com/app/scriptable/id1405459188)（免费）
2. 将 `index.html` 保存到 iCloud Drive 的 Scriptable 文件夹
3. 创建脚本加载 HTML

---

## 游戏控制方式

### iPad 触屏操作

| 操作 | 说明 |
|------|------|
| **滑动屏幕** | 控制蛇的方向（上下左右滑动） |
| **点击暂停按钮** | 暂停/继续游戏 |
| **点击难度按钮** | 选择慢/中/快三种速度 |

### 键盘操作（外接键盘）

| 按键 | 功能 |
|------|------|
| ↑ ↓ ← → 或 WASD | 控制方向 |
| **空格键** | 暂停/继续 |
| **ESC** | 暂停/继续 |

---

## 常见问题

### Q: 音效没有声音？

A: 首次打开游戏时需要点击「开始游戏」按钮来激活音频。这是 iOS Safari 的安全策略限制。

### Q: 游戏界面太小/太大？

A: 游戏已适配移动端，如果显示不正常，尝试：
- 横屏游玩
- 检查是否开启了 Safari 的「请求桌面网站」

### Q: 如何离线玩？

A: 使用方法一（GitHub Pages）+ 添加到主屏幕后，iOS 会缓存页面，可以短暂离线游玩。完全离线建议使用方法三（Pythonista）。

---

## 文件结构

```
snakeFood/
├── index.html      # 游戏主文件（包含 HTML + CSS + JS）
└── IPAD_GUIDE.md   # 本说明文档
```

游戏是纯前端实现，单个 `index.html` 文件即可运行，无需后端服务。
