# AGENTS.md — 项目代理说明

## 项目概述

静脉给药 PDT 治疗气管 RRP 的手术演示视频播放网页，为博士论文配套的在线播放页面，便于审稿人、答辩委员及同行通过链接直接观看手术视频。

- **类型**：纯静态网页（HTML + CSS + JS），无需构建工具
- **播放器**：Plyr.js v3（jsDelivr CDN）
- **部署**：GitHub Pages（仓库：https://github.com/entpyf/PDT-video）
- **作者**：Yufei（潘宇飞），创建时间：2026-03-05

## 目录结构

```
视频网页/
├── index.html            # 主页面（Plyr.js 播放器、深色医学风格、响应式设计）
├── videos/
│   └── surgery.mp4       # 手术视频文件（MP4，<100MB，随仓库提交）
├── docs/
│   └── PROJECT_RULES.md  # 项目规则文档
├── README.md             # 项目简介
├── .gitignore            # Git 忽略规则
└── AGENTS.md             # 本文件
```

## 技术要点

| 项目 | 说明 |
|------|------|
| 字体 | Noto Serif SC + Noto Sans SC（Google Fonts CDN） |
| 播放器 | Plyr.js v3（jsDelivr CDN） |
| 风格 | 深色背景、青绿色点缀、医学编辑风格 |
| 视频 | 直接随仓库提交，<100MB（GitHub 允许） |

## 运行与部署

- **本地预览**：`python3 -m http.server 8080`
- **部署方案**：GitHub Pages 或 Nginx

## 开发规范

- 视频文件压缩至 100MB 以内，格式为 MP4（H.264 编码）
- 页面为纯静态文件，所有外部依赖通过 CDN 引入
- 脚本作者：Yufei，创建时间：2026-03-05
