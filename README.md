# 手术视频播放网页

> 静脉 PDT 治疗气管 RRP 博士论文配套手术演示视频在线播放页面

**Author:** Yufei  
**Created:** 2026-03-05

---

## 快速开始

### 1. 放入视频文件

将你的手术视频（MP4 格式，< 100MB）重命名为 `surgery.mp4`，放入 `videos/` 目录：

```
videos/surgery.mp4
```

> 如果视频文件名不同，请修改 `index.html` 中的 `<source src="videos/surgery.mp4">` 为实际文件名。

### 2. 本地预览

在项目根目录下运行：

```bash
python3 -m http.server 8080
```

然后在浏览器中访问：**http://localhost:8080**

> ⚠️ 直接双击打开 HTML 文件无法播放视频（浏览器跨域安全限制），必须通过 HTTP 服务器访问。

---

## 部署到 GitHub Pages（推荐，免费）

### 步骤

```bash
# 1. 初始化 Git 仓库
git init
git add .
git commit -m "Initial commit: surgical video player"

# 2. 在 GitHub 上创建一个新的仓库（如 surgical-video-pdt）

# 3. 推送到 GitHub
git remote add origin https://github.com/你的用户名/surgical-video-pdt.git
git branch -M main
git push -u origin main
```

然后在 GitHub 仓库页面：
1. 进入 **Settings** → **Pages**
2. Source 选择 **Deploy from a branch**
3. Branch 选择 **main**，目录选 **/ (root)**
4. 点击 **Save**

几分钟后即可通过以下地址访问：

```
https://你的用户名.github.io/surgical-video-pdt/
```

### 注意事项

- GitHub 单文件上限 100MB，视频必须压缩至此大小以内
- 仓库总大小建议不超过 1GB
- GitHub Pages 自带 HTTPS

---

## 备选：部署到 Linux 服务器（Nginx）

### 1. 上传文件

将整个项目目录上传到服务器，例如 `/var/www/surgical-video/`：

```bash
scp -r ./* user@your-server:/var/www/surgical-video/
```

### 2. Nginx 配置

```nginx
server {
    listen 80;
    server_name your-domain.com;

    root /var/www/surgical-video;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # 优化大视频文件传输
    location ~* \.mp4$ {
        mp4;
        mp4_buffer_size 1m;
        mp4_max_buffer_size 5m;
        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
    }

    # 静态资源缓存
    location ~* \.(html|css|js)$ {
        expires 7d;
        add_header Cache-Control "public, no-transform";
    }
}
```

```bash
# 测试并重载 Nginx
sudo nginx -t
sudo systemctl reload nginx
```

---

## 视频压缩建议

如果视频文件过大，可使用 FFmpeg 压缩：

```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset medium -acodec aac -b:a 128k videos/surgery.mp4
```

参数说明：
- `-crf 28`：压缩质量（18-28 范围，数值越大文件越小，画质越低）
- `-preset medium`：编码速度与压缩率的平衡
- 可调整 `-crf` 值使文件控制在 100MB 以内

---

## 技术栈

| 技术 | 用途 |
|------|------|
| HTML5 `<video>` | 视频播放 |
| [Plyr.js](https://plyr.io/) | 美化播放器 UI |
| CSS3 | 页面样式 |
| CDN (jsDelivr) | 外部依赖加载 |
