# 项目展示网站 Codebase 总结

## 项目概述

这是一个**学术研究项目展示网站模板**，基于静态HTML构建，适用于展示论文、研究成果等学术内容。项目设计现代化、响应式，并针对GitHub Pages部署进行了优化。

---

## 目录结构

```
展示网站/
├── .git/                          # Git版本控制
├── .nojekyll                      # GitHub Pages配置（禁用Jekyll）
├── README.md                      # 项目说明文档
├── CLAUDE.md                      # 本文件 - Codebase总结
├── index.html                     # 主HTML文件（入口点，521行）
└── static/                        # 静态资源目录
    ├── css/                       # 样式文件
    │   ├── bulma.min.css          # Bulma CSS框架
    │   ├── bulma-carousel.min.css # 轮播组件样式
    │   ├── bulma-slider.min.css   # 滑块组件样式
    │   ├── fontawesome.all.min.css# Font Awesome图标
    │   └── index.css              # 自定义样式（754行）
    ├── images/                    # 图片资源
    │   ├── carousel1-4.jpg        # 轮播图片
    │   └── favicon.ico            # 网站图标
    ├── js/                        # JavaScript文件
    │   ├── bulma-carousel.min.js  # 轮播控件
    │   ├── bulma-slider.min.js    # 滑块控件
    │   ├── fontawesome.all.min.js # 图标库
    │   └── index.js               # 自定义脚本（143行）
    ├── pdfs/                      # PDF资源
    │   └── sample.pdf             # 示例PDF
    └── videos/                    # 视频资源
        ├── banner_video.mp4       # 横幅视频
        └── carousel1-3.mp4        # 轮播视频
```

---

## 技术栈

### 前端框架和库
| 技术 | 版本 | 用途 |
|------|------|------|
| Bulma | 0.9.x | CSS框架，响应式布局 |
| jQuery | 3.5.1 | DOM操作（CDN引入） |
| bulmaCarousel | - | 图片/视频轮播组件 |
| bulmaSlider | - | 滑块控件组件 |
| Font Awesome | - | 图标库 |
| Academicons | - | 学术图标（CDN） |
| Google Fonts | Inter | 字体系统 |
| Adobe Embed API | - | PDF查看器 |

### 外部CDN依赖
- Google Fonts (Inter字体)
- jQuery (ajax.googleapis.com)
- Adobe Document Cloud (PDF查看器)
- Academicons (jsDelivr CDN)

---

## 主要页面组件

### index.html 结构（按顺序）

1. **Meta标签和SEO** (第3-180行)
   - Open Graph标签（社交分享）
   - Twitter卡片
   - 学术引文元标签（Google Scholar）
   - JSON-LD结构化数据

2. **固定UI元素** (第184-235行)
   - 滚动到顶部按钮
   - More Works下拉菜单

3. **Hero Section** (第238-314行)
   - 论文标题、作者列表
   - 机构和会议信息
   - 外部链接按钮组（PDF/GitHub/arXiv等）

4. **Teaser Video** (第318-333行)
   - 响应式横幅视频播放器

5. **Abstract Section** (第336-351行)
   - 摘要区域

6. **Image Carousel** (第355-392行)
   - 4张图片轮播（带描述）

7. **Video Presentation** (第398-415行)
   - YouTube嵌入视频

8. **Video Carousel** (第419-449行)
   - 3个视频轮播

9. **PDF Poster** (第457-469行)
   - 嵌入式PDF查看器

10. **BibTeX Citation** (第474-492行)
    - BibTeX引用代码块
    - 复制到剪贴板功能

11. **Footer** (第495-518行)
    - 模板归属信息

---

## 自定义样式系统 (index.css)

### CSS变量
```css
/* 主色系 */
--primary-color: #2563eb;     /* 蓝色 */
--primary-hover: #1d4ed8;     /* 深蓝 */
--accent-color: #0ea5e9;      /* 浅蓝 */

/* 文本色 */
--text-primary: #1e293b;      /* 深灰 */
--text-secondary: #64748b;    /* 中灰 */
--text-light: #94a3b8;        /* 浅灰 */

/* 背景 */
--background-primary: #ffffff;
--background-secondary: #f8fafc;
```

### 响应式断点
| 断点 | 宽度范围 | 说明 |
|------|----------|------|
| 全宽 | >1024px | 完整布局 |
| 平板 | 769-1024px | 调整Padding |
| 手机 | 481-768px | 堆栈按钮 |
| 超小屏 | <480px | 最小化设计 |

---

## JavaScript功能 (index.js)

| 功能 | 行号 | 说明 |
|------|------|------|
| More Works菜单 | 4-37 | 下拉菜单切换、Escape关闭、外部点击关闭 |
| BibTeX复制 | 40-73 | Clipboard API，带回退方案 |
| 滚动到顶部 | 75-91 | 滚动超300px显示按钮 |
| 视频自动播放 | 94-120 | IntersectionObserver实现视图触发播放 |
| 轮播初始化 | 122-142 | jQuery初始化Bulma轮播和滑块 |

---

## 性能优化

1. **资源加载策略**
   - 关键CSS同步加载
   - 非关键CSS异步加载（preload + onload）
   - JavaScript全部defer
   - 图片延迟加载（loading="lazy"）

2. **预连接优化**
   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   ```

3. **视频优化**
   - IntersectionObserver控制视频播放
   - 仅在视口内时播放

---

## SEO配置

- **标准Meta**: title, description, keywords, author
- **Open Graph**: Facebook/LinkedIn分享预览
- **Twitter卡片**: Twitter分享美化
- **学术引文**: citation_title, citation_author等
- **JSON-LD**: ScholarlyArticle, Organization结构化数据

---

## 开发指南

### 快速定制（需修改的位置）

README.md中标记了所有TODO位置：

1. **Meta信息** - 修改论文标题、作者、描述
2. **社交媒体缩略图** - 替换og:image URL
3. **内容** - 摘要、轮播标题和描述
4. **视频** - YouTube视频ID、本地视频文件
5. **资源** - 图片、PDF、favicon

### 部署

1. 修改内容后直接推送到GitHub
2. 启用GitHub Pages（Settings > Pages）
3. 选择分支和目录
4. `.nojekyll`文件确保正确处理

---

## 关键文件修改指南

| 需求 | 修改文件 | 位置 |
|------|----------|------|
| 更改颜色主题 | `static/css/index.css` | CSS变量区(1-24行) |
| 修改页面内容 | `index.html` | 对应section |
| 添加新功能 | `static/js/index.js` | 底部添加 |
| 更换资源 | `static/images/videos/pdfs/` | 替换文件 |
| SEO优化 | `index.html` | Meta标签区(3-180行) |

---

## 许可证

CC-BY-SA 4.0 - 基于Nerfies项目页面模板

---

## 文件统计

| 类别 | 数量 | 大小 |
|------|------|------|
| HTML | 1 | ~21KB |
| CSS | 5 | ~377KB |
| JavaScript | 6 | ~1.2MB |
| 图片 | 5 | ~1.3MB |
| 视频 | 4 | ~8MB |
| PDF | 1 | ~14KB |
| **总计** | **~23** | **~11MB** |
