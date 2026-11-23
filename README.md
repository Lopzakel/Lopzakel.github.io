# 毛祺浩 · 个人网站

一个计算机系大一学生的单页个人主页。手写 HTML、CSS、JavaScript，没有框架、没有构建步骤、没有外部依赖，下载下来直接打开就能看。

页面包含首屏、关于、教育与经历、项目、技能、联系方式六个部分，带浅色 / 深色主题、响应式布局和少量滚动动效。视觉上有深色个人资料卡、项目缩略图、经历徽章和技能图标，全部用 HTML/CSS 与内联 SVG 手绘，没有外部图片请求。

> 姓名、学校、年级、邮箱和 GitHub 已经按毛祺浩填写；**项目进度和技能等级仍需按真实情况确认**。发布前请按下面「改成你自己的」逐项核对。

## 快速开始

直接双击 `index.html` 就能看。

更推荐起一个本地服务器（剪贴板 API 在 `file://` 下行为不一致）：

```bash
python -m http.server 8000
# 打开 http://localhost:8000
```

没有 Python 的话，`npx serve .` 也可以。

## 文件结构

```text
personal-site/
├── index.html          页面结构与全部文案
├── styles.css          样式、主题变量、响应式断点
├── script.js           主题切换、滚动动效、导航高亮、复制邮箱、成都时间
├── assets/
│   └── favicon.svg     站点图标
└── README.md
```

所有资源都是相对路径，放在子目录（比如 GitHub Pages 的项目页）也能正常工作。

## 改成你自己的

### 1. 全局搜索替换

| 当前内容 | 说明 |
| --- | --- |
| `毛祺浩` / `Mao Qihao` / `MQH` | 姓名、英文名与字母标记，出现在标题、导航、首屏、资料卡、favicon |
| `四川传媒学院` | 学校。这里按官方校名写；如果你要写「四川传媒大学」，全局替换成那个 |
| `计算机系` | 专业与院系 |
| `大一`、`2030 届`、`2026.09`–`2030.06` | 年级、届别与学制 |
| `2027 暑期实习` | 求职状态，出现在首屏、资料卡和代码卡 |
| `hutao0806@qq.com` | 邮箱，出现在首屏、关于、联系区 |
| `成都` / `CHENGDU` | 城市与资料卡脚注 |
| `UE5 VR 开发` | 目前唯一的项目，按真实进度改 |

### 2. 首屏

- `index.html` 里的 `<title>`、`meta name="description"` 和 `og:*`：改标题与简介。
- `.hero__title` 里的姓名，以及下面的 `Mao Qihao — 计算机系学生`。
- `.hero__lede` 一段自我介绍；`.hero__meta` 三个标签（城市、学校年级、届别）。
- 右侧 `profile.js` 代码卡：改 `school`、`major`、`year`、`focus`、`stack`、`now`、`openTo`。注意保持 JS 对象语法，字符串用双引号。
- 两个按钮：`查看项目` 跳到 `#projects`；邮箱按钮的 `data-copy` 和可见文字都要改。

### 3. 关于

`#about` 里有三块：一句大字 statement、两段自我介绍、右侧深色资料卡 `.profile`。

资料卡顶部是 `PROFILE / 2026` 和「开放中」，中间是 `MQH` 字母徽章、姓名与专业，下面每行是：

```html
<div><dt>所在地</dt><dd>成都，中国</dd></div>
```

可以增删；「状态」那一行的圆点用了 `class="dot"`。条形码和 `CHENGDU · CN` 脚注也在同一块里。卡片的 1.2° 倾斜由 `.profile` 的 `rotate` 控制，悬停会摆正。

### 4. 经历

`#experience` 的 `.timeline`，每条结构如下，复制整条即可增加：

```html
<article class="timeline__item reveal">
  <div class="timeline__when">
    <time datetime="2026-09">2026.09</time> — <time datetime="2030-06">2030.06</time>
  </div>
  <div class="timeline__body">
    <h3>
      <span class="timeline__logo timeline__logo--school" aria-hidden="true">川</span>
      <span class="timeline__title">学校 / 公司 · 职位 <span class="tag tag--quiet">本科</span></span>
    </h3>
    <p class="timeline__meta">年级、技术栈或一句话说明</p>
    <p>做了什么，结果如何。有数字就写数字。</p>
    <ul class="chips">
      <li>课程 / 技术标签</li>
    </ul>
  </div>
</article>
```

没有的经历整条删掉；时间用 `<time datetime="YYYY-MM">` 更语义化。左侧的「川 / 自」是经历徽章，学校、公司、社团各一套颜色；换成你的字即可。不想要徽章时，删掉 `.timeline__logo`，再把 `.timeline__body` 的 `padding-left` 改成 `0`。

### 5. 项目

#projects 目前只有一个项目卡 .featured：左边文案，右边是 UE5 VR 头显的内联 SVG。要换成你自己的项目，改标题、描述、技术标签和链接；缩略图直接替换 <svg class="vr-art"> 的内容。没有项目时可删掉 .featured__visual，并把 .featured 的 grid-template-columns 改成 1fr。

项目链接目前指向 https://github.com/Lopzakel；有具体仓库后换成 repo 地址。
### 6. 技能

`#skills` 三栏：语言 &amp; 基础、工具 &amp; 环境、接下来。每行是：

```html
<li><span>名称</span><i aria-hidden="true"></i><em>熟练度</em></li>
```

按真实情况写，别写「精通」。三个分组标题前的图标是 `.skill-icon` 内联 SVG，纯装饰，可换可删。

### 7. 联系与页脚

- 联系区的邮箱链接和复制按钮。
- GitHub 链接已换成 `https://github.com/Lopzakel`；博客 / Bilibili 暂时删掉，需要时按同样格式加回。
- 页脚年份由脚本自动更新；「手写于成都」可以改成你想写的话。

### 8. 图标与分享信息

- `assets/favicon.svg`：当前是 `MQH` 字母块，换成自己的字母或图形，保持 `viewBox="0 0 64 64"` 即可。
- `<meta name="theme-color">` 以及 `script.js` 里 `applyTheme()` 的两个颜色值，和主题背景保持一致。
- 需要分享卡片时，加一条 `og:image` 指向 1200×630 的图片。

## 换配色和字体

设计变量集中在 `styles.css` 顶部：

```css
:root {
  --paper: #f4f1ea;
  --ink: #17160f;
  --accent: #cf4f22;
  --accent-text: #b04018;
  /* ... */
}

[data-theme="dark"] {
  --paper: #12110d;
  --ink: #f1ece0;
  --accent: #ff7141;
  /* ... */
}
```

- `--accent` 用于装饰、色块和高亮；`--accent-text` 用于小字和链接，改的时候注意对比度（正文至少 4.5:1）。
- `--paper`、`--paper-2`、`--card` 控制背景层次；`--ink`、`--ink-soft` 控制文字。
- 字体只用系统字体栈（`--sans`、`--mono`），不加载外部字体，所以没有网络请求。想换字体改这两个变量即可。
- 深色模式默认跟随系统，也可以点右上角手动切换，选择会存进 `localStorage`。

## 部署

### GitHub Pages

1. 新建仓库，把本目录的文件推到 `main` 分支根目录（`index.html` 要在根目录）。
2. 仓库 **Settings → Pages → Build and deployment**，Source 选 `Deploy from a branch`，分支选 `main`、目录选 `/ (root)`，保存。
3. 一两分钟后访问 `https://<用户名>.github.io/<仓库名>/`。
4. 如果仓库名是 `<用户名>.github.io`，地址就是 `https://<用户名>.github.io/`。

纯静态站点，不需要 Actions，也不需要 `.nojekyll`。

### Vercel / Netlify

- **Vercel**：导入仓库，Framework Preset 选 `Other`，Build Command 留空，Output Directory 填 `.`。
- **Netlify**：把整个文件夹拖到 Netlify Drop；或连接仓库，Build command 留空，Publish directory 填 `.`。

### 自己的服务器

把 `index.html`、`styles.css`、`script.js` 和 `assets/` 上传到任意静态目录，Nginx / Caddy 默认配置就能跑。

## 实现细节

- **无构建**：没有 npm、打包器或 CSS 框架，改完刷新即可。
- **视觉**：深色资料卡固定深色；项目缩略图、经历徽章和技能图标都是内联 SVG 或 CSS 绘制，没有外部图片请求。
- **主题**：`<head>` 里有一小段内联脚本，在首屏绘制前读取 `localStorage` 和系统偏好，避免深色模式闪白。
- **动效**：IntersectionObserver 做滚动出现；`prefers-reduced-motion: reduce` 下全部关闭。
- **响应式**：断点在 1024 / 900 / 720 / 520 / 380px，390px 和 320px 宽度下检查过布局。
- **无障碍**：跳到主内容链接、可见焦点样式、`aria-label`、`aria-current`、语义化标题层级；没有 JavaScript 时内容仍然可读。
- **时间**：页脚时间固定按 `Asia/Shanghai` 显示，不受访问者时区影响。

## 许可

随意修改和使用。邮箱、社交链接和项目进度仍是占位，发布前请替换成你自己的。
