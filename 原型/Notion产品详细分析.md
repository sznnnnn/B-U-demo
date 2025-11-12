# Notion 产品详细设计分析

> 基于 Notion 应用界面（非官网）的深度设计系统分析  
> 适用于前端开发参考的设计规范文档  
> 版本：v1.0 | 最后更新：2025-11

---

## 目录

1. [产品概览](#产品概览)
2. [整体布局系统](#整体布局系统)
3. [左侧边栏设计](#左侧边栏设计)
4. [主内容区域](#主内容区域)
5. [顶部导航栏](#顶部导航栏)
6. [文档编辑界面](#文档编辑界面)
7. [色彩系统](#色彩系统)
8. [字体排版系统](#字体排版系统)
9. [间距与布局](#间距与布局)
10. [组件设计规范](#组件设计规范)
11. [交互状态与动画](#交互状态与动画)
12. [微动效详细分析](#微动效详细分析)
13. [交互细节深度分析](#交互细节深度分析)
14. [图标系统](#图标系统)
15. [响应式设计](#响应式设计)
16. [可访问性设计](#可访问性设计)

---

## 产品概览

### 设计理念

Notion 的核心设计理念是**"内容优先"**（Content First），所有设计决策都围绕如何让用户专注于内容创作：

- **极简主义**：去除不必要的装饰，界面干净清爽
- **中性色调**：以白色和灰色为主，避免视觉干扰
- **块状编辑**：内容以块（Block）为单位，灵活组合
- **即时反馈**：所有操作都有即时的视觉反馈
- **一致性**：统一的交互模式和视觉语言

### 界面结构

```
┌─────────────────────────────────────────────────────────┐
│  [左侧边栏]          │  [顶部导航栏]                    │
│  - Logo/用户信息     │  - 面包屑导航                   │
│  - 快速访问          │  - 页面操作按钮                 │
│  - 共享空间          │  - 分享/收藏/更多               │
│  - 私有页面          │                                 │
│  - 设置/市场/回收站  │  [主内容区域]                   │
│                      │  - 页面标题                     │
│                      │  - 内容块编辑区                 │
│                      │  - 滚动条                       │
└─────────────────────────────────────────────────────────┘
```

---

## 整体布局系统

### 布局结构

#### 1. 左侧边栏（Sidebar）
- **宽度**：固定 `240px`
- **位置**：固定定位（Fixed），始终可见
- **背景色**：`#FFFFFF`（白色）
- **边框**：右侧 `1px solid #E8E7E5`
- **高度**：`100vh`（全屏高度）
- **滚动**：内容超出时内部滚动

#### 2. 主内容区域（Main Content）
- **左边距**：`240px`（为侧边栏留出空间）
- **最大宽度**：`1200px`（居中显示）
- **左右边距**：
  - 大屏（>1280px）：`96px`
  - 中屏（768px-1280px）：`48px`
  - 小屏（<768px）：`24px`
- **顶部边距**：`0px`（紧贴顶部）
- **背景色**：`#FFFFFF`

#### 3. 顶部导航栏（Top Bar）
- **高度**：`45px`
- **位置**：固定在主内容区域顶部
- **背景色**：`#FFFFFF`
- **边框**：底部 `1px solid #E8E7E5`（可选）
- **内边距**：水平 `16px`，垂直 `8px`

---

## 左侧边栏设计

### 结构层次

```
┌─────────────────────────┐
│ [用户头像] zn s's Notion │ ← 用户信息区
├─────────────────────────┤
│ [Search Icon] Search               │
│ [Home Icon] Home                 │ ← 快速访问区
│ [Calendar Icon] Meetings             │
│ [AI Icon] Notion AI            │
│ [Inbox Icon] Inbox                │
├─────────────────────────┤
│ Shared                  │ ← 分组标题
│ + Start collaborating   │
├─────────────────────────┤
│ Private                 │ ← 分组标题
│ [Document Icon] Getting Started      │
│ [Note Icon] Quick Note           │ ← 页面列表
│ [Database Icon] SEEA                 │
│ ...                     │
├─────────────────────────┤
│ [Settings Icon] Settings             │ ← 底部功能区
│ [Marketplace Icon] Marketplace          │
│ [Trash Icon] Trash                │
│ [图标行]                │
└─────────────────────────┘
```

### 详细规范

#### 1. 用户信息区（顶部）

```css
.user-info-section {
  padding: 16px 12px;
  border-bottom: 1px solid #E8E7E5;
  margin-bottom: 8px;
}

.user-avatar {
  width: 24px;
  height: 24px;
  border-radius: 4px;
  background: #6B4DFF; /* 紫色背景 */
  color: #FFFFFF;
  font-size: 12px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-right: 8px;
}

.user-name {
  font-size: 14px;
  font-weight: 500;
  color: #37352F;
  display: inline-block;
}
```

**尺寸规范**：
- 头像：`24px × 24px`
- 圆角：`4px`
- 用户名字号：`14px`
- 字重：`500`
- 内边距：`16px 12px`

#### 2. 快速访问区（Quick Access）

```css
.quick-access-item {
  height: 28px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  color: #787774;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  transition: background-color 0.15s ease;
  margin-bottom: 2px;
}

.quick-access-item:hover {
  background: rgba(0, 0, 0, 0.03);
}

.quick-access-item.active {
  background: rgba(0, 0, 0, 0.05);
  color: #37352F;
  font-weight: 500;
}

.quick-access-icon {
  width: 16px;
  height: 16px;
  color: #787774;
  flex-shrink: 0;
}
```

**尺寸规范**：
- 菜单项高度：`28px`
- 内边距：`4px 8px`
- 圆角：`4px`
- 图标尺寸：`16px × 16px`
- 图标与文字间距：`8px`
- 菜单项间距：`2px`
- 字号：`14px`

#### 3. 分组标题（Section Header）

```css
.section-header {
  font-size: 12px;
  font-weight: 600;
  color: #9B9A97;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 8px 12px 4px;
  margin-top: 16px;
  margin-bottom: 4px;
}

.section-header:first-child {
  margin-top: 0;
}
```

**尺寸规范**：
- 字号：`12px`
- 字重：`600`
- 颜色：`#9B9A97`
- 内边距：`8px 12px 4px`
- 上边距：`16px`（第一个分组为 `0`）
- 下边距：`4px`
- 字母间距：`0.5px`
- 文本转换：`uppercase`

#### 4. 页面列表项（Page Item）

```css
.page-item {
  height: 28px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  color: #37352F;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  transition: background-color 0.15s ease;
  margin-bottom: 2px;
  position: relative;
}

.page-item:hover {
  background: rgba(0, 0, 0, 0.03);
}

.page-item.active {
  background: rgba(0, 0, 0, 0.05);
  font-weight: 500;
}

.page-item-icon {
  width: 16px;
  height: 16px;
  color: #787774;
  flex-shrink: 0;
}

.page-item-title {
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

**尺寸规范**：
- 高度：`28px`
- 内边距：`4px 8px`
- 圆角：`4px`
- 字号：`14px`
- 图标尺寸：`16px × 16px`
- 图标与文字间距：`8px`
- 菜单项间距：`2px`

**交互状态**：
- **默认**：文字 `#37352F`，背景透明
- **悬停**：背景 `rgba(0, 0, 0, 0.03)`
- **激活**：背景 `rgba(0, 0, 0, 0.05)`，字重 `500`

#### 5. 底部功能区

```css
.bottom-actions {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 8px 12px;
  border-top: 1px solid #E8E7E5;
  background: #FFFFFF;
}

.bottom-action-item {
  height: 28px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  color: #787774;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  transition: background-color 0.15s ease;
  margin-bottom: 2px;
}

.bottom-action-item:hover {
  background: rgba(0, 0, 0, 0.03);
}
```

---

## 主内容区域

### 页面结构

```
┌─────────────────────────────────────────┐
│ [顶部导航栏]                             │
├─────────────────────────────────────────┤
│ [页面操作提示]                           │
│ + Add icon  + Add cover  + Add comment  │
│                                          │
│ [页面标题]                               │
│ Professional Social Practice Report...   │
│                                          │
│ [内容块区域]                             │
│ Introduction paragraph...                │
│                                          │
│ Section 1: Overview...                  │
│ Content paragraph...                    │
│                                          │
│ Section 2: My Professional...           │
│ Content paragraph...                     │
│                                          │
│ [滚动条]                                 │
└─────────────────────────────────────────┘
```

### 页面操作提示区

```css
.page-actions-hint {
  display: flex;
  gap: 16px;
  padding: 8px 0;
  margin-bottom: 8px;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.page-actions-hint:hover,
.page-actions-hint:focus-within {
  opacity: 1;
}

.page-action-hint-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 14px;
  color: #787774;
  cursor: pointer;
  padding: 4px 8px;
  border-radius: 4px;
  transition: background-color 0.15s ease;
}

.page-action-hint-item:hover {
  background: rgba(0, 0, 0, 0.03);
  color: #37352F;
}

.page-action-hint-icon {
  width: 14px;
  height: 14px;
  color: #787774;
}
```

**尺寸规范**：
- 提示项间距：`16px`
- 图标尺寸：`14px × 14px`
- 图标与文字间距：`6px`
- 字号：`14px`
- 内边距：`4px 8px`
- 圆角：`4px`

### 页面标题

```css
.page-title {
  font-size: 40px;
  font-weight: 700;
  color: #37352F;
  line-height: 1.2;
  margin: 0;
  padding: 4px 2px;
  border-radius: 3px;
  min-height: 1.5em;
  outline: none;
}

.page-title:hover,
.page-title:focus {
  background: rgba(0, 0, 0, 0.03);
}

.page-title[contenteditable="true"]:empty::before {
  content: "Untitled";
  color: #9B9A97;
}
```

**尺寸规范**：
- 字号：`40px`
- 字重：`700`
- 行高：`1.2`
- 颜色：`#37352F`
- 内边距：`4px 2px`
- 圆角：`3px`

---

## 🧭 顶部导航栏

### 结构

```
┌─────────────────────────────────────────────────────────┐
│ < > [Home Icon] [面包屑]  [Lock Icon] Private ▼  Edited 2y ago  [Star Icon] ⋯ │
└─────────────────────────────────────────────────────────┘
```

### 面包屑导航

```css
.breadcrumb-nav {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 14px;
  color: #787774;
  flex: 1;
}

.breadcrumb-item {
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.15s ease;
}

.breadcrumb-item:hover {
  background: rgba(0, 0, 0, 0.03);
  color: #37352F;
}

.breadcrumb-icon {
  width: 16px;
  height: 16px;
  color: #787774;
}

.breadcrumb-separator {
  color: #9B9A97;
  margin: 0 4px;
}
```

**尺寸规范**：
- 高度：`45px`
- 内边距：水平 `16px`，垂直 `8px`
- 字号：`14px`
- 图标尺寸：`16px × 16px`
- 项目间距：`4px`

### 导航按钮

```css
.nav-button {
  width: 28px;
  height: 28px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.15s ease;
  color: #787774;
}

.nav-button:hover {
  background: rgba(0, 0, 0, 0.03);
  color: #37352F;
}

.nav-button:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
```

### 页面操作按钮

```css
.page-action-button {
  height: 28px;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 14px;
  color: #37352F;
  background: transparent;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 6px;
  transition: background-color 0.15s ease;
}

.page-action-button:hover {
  background: rgba(0, 0, 0, 0.03);
}

.page-action-icon {
  width: 16px;
  height: 16px;
  color: #787774;
}
```

---

## 文档编辑界面

### 内容块（Block）系统

Notion 的核心是块状编辑系统，每个内容块都是独立的编辑单元。

#### 块的基本结构

```css
.content-block {
  padding: 3px 2px;
  border-radius: 3px;
  margin: 1px 0;
  position: relative;
  transition: background-color 0.15s ease;
}

.content-block:hover {
  background: rgba(0, 0, 0, 0.03);
}

.content-block:focus-within {
  background: rgba(0, 0, 0, 0.03);
}

.content-block[contenteditable="true"] {
  outline: none;
  min-height: 1.5em;
}
```

#### 块类型规范

##### 1. 段落（Paragraph）

```css
.block-paragraph {
  font-size: 16px;
  line-height: 1.6;
  color: #37352F;
  margin: 0;
  padding: 3px 2px;
}

.block-paragraph[contenteditable="true"]:empty::before {
  content: "Type '/' for commands";
  color: #9B9A97;
  pointer-events: none;
}
```

**尺寸规范**：
- 字号：`16px`
- 行高：`1.6`
- 颜色：`#37352F`
- 内边距：`3px 2px`
- 圆角：`3px`

##### 2. 标题（Heading）

```css
.block-heading-1 {
  font-size: 30px;
  font-weight: 700;
  line-height: 1.2;
  color: #37352F;
  margin: 2em 0 4px;
  padding: 3px 2px;
}

.block-heading-2 {
  font-size: 24px;
  font-weight: 600;
  line-height: 1.3;
  color: #37352F;
  margin: 1.4em 0 1px;
  padding: 3px 2px;
}

.block-heading-3 {
  font-size: 20px;
  font-weight: 600;
  line-height: 1.3;
  color: #37352F;
  margin: 1em 0 1px;
  padding: 3px 2px;
}
```

**尺寸规范**：
- H1：`30px`，字重 `700`，上边距 `2em`
- H2：`24px`，字重 `600`，上边距 `1.4em`
- H3：`20px`，字重 `600`，上边距 `1em`

##### 3. 列表（List）

```css
.block-bulleted-list,
.block-numbered-list {
  padding-left: 24px;
  margin: 1px 0;
}

.block-list-item {
  font-size: 16px;
  line-height: 1.6;
  color: #37352F;
  padding: 3px 2px;
  position: relative;
}

.block-bulleted-list .block-list-item::before {
  content: "•";
  position: absolute;
  left: -20px;
  color: #787774;
  font-size: 18px;
}

.block-numbered-list {
  counter-reset: list-counter;
}

.block-numbered-list .block-list-item {
  counter-increment: list-counter;
}

.block-numbered-list .block-list-item::before {
  content: counter(list-counter) ".";
  position: absolute;
  left: -20px;
  color: #787774;
  font-size: 16px;
}
```

**尺寸规范**：
- 左内边距：`24px`
- 列表标记位置：`-20px`
- 字号：`16px`
- 行高：`1.6`

##### 4. 引用（Quote）

```css
.block-quote {
  border-left: 3px solid #E8E7E5;
  padding-left: 14px;
  margin: 6px 0;
  font-size: 16px;
  line-height: 1.6;
  color: #37352F;
  font-style: italic;
}
```

**尺寸规范**：
- 左边框：`3px solid #E8E7E5`
- 左内边距：`14px`
- 字号：`16px`
- 行高：`1.6`

##### 5. 代码块（Code Block）

```css
.block-code {
  background: #F7F6F3;
  border: 1px solid #E8E7E5;
  border-radius: 3px;
  padding: 16px;
  margin: 4px 0;
  font-family: "SF Mono", Monaco, "Cascadia Code", "Roboto Mono", Consolas, "Courier New", monospace;
  font-size: 14px;
  line-height: 1.5;
  color: #37352F;
  overflow-x: auto;
}
```

**尺寸规范**：
- 背景：`#F7F6F3`
- 边框：`1px solid #E8E7E5`
- 圆角：`3px`
- 内边距：`16px`
- 字号：`14px`
- 字体：等宽字体

### 块操作菜单

当鼠标悬停在块上时，左侧会出现操作按钮：

```css
.block-control {
  position: absolute;
  left: -24px;
  top: 0;
  width: 20px;
  height: 20px;
  display: none;
  align-items: center;
  justify-content: center;
  border-radius: 3px;
  cursor: grab;
  color: #9B9A97;
  transition: all 0.15s ease;
}

.content-block:hover .block-control {
  display: flex;
}

.block-control:hover {
  background: rgba(0, 0, 0, 0.06);
  color: #37352F;
}

.block-control:active {
  cursor: grabbing;
}
```

---

## 色彩系统

### 主色调

#### 文字颜色

```css
/* 主文字色 */
--text-primary: #37352F;      /* 标题、正文 */
--text-secondary: #787774;    /* 辅助文字、图标 */
--text-tertiary: #9B9A97;      /* 占位符、禁用状态 */
--text-quaternary: #C4C2BE;   /* 极次要文字 */

/* 对比度检查 */
/* #37352F on #FFFFFF: 10.8:1 (优秀) */
/* #787774 on #FFFFFF: 4.9:1 (通过) */
/* #9B9A97 on #FFFFFF: 3.2:1 (仅大文字通过) */
```

#### 背景颜色

```css
/* 主背景 */
--bg-primary: #FFFFFF;        /* 主背景、卡片 */
--bg-secondary: #F7F6F3;      /* 侧边栏、代码块背景 */
--bg-tertiary: #FAFAF9;       /* 输入框背景 */
--bg-hover: rgba(0, 0, 0, 0.03);  /* 悬停背景 */
--bg-active: rgba(0, 0, 0, 0.05); /* 激活背景 */
```

#### 边框颜色

```css
/* 边框色 */
--border-default: #E8E7E5;     /* 默认边框 */
--border-hover: #DDDBD8;      /* 悬停边框 */
--border-focus: #2383E2;      /* 焦点边框（蓝色） */
```

#### 品牌色

```css
/* 品牌色 */
--brand-purple: #6B4DFF;       /* 用户头像背景 */
--brand-blue: #2383E2;         /* 链接、焦点 */
```

### 语义颜色

```css
/* 红色 - 错误/删除 */
--red-bg: #FFE2DD;
--red-text: #D44C47;
--red-border: #D44C47;

/* 黄色 - 警告/待办 */
--yellow-bg: #FFF7E0;
--yellow-text: #CB912F;
--yellow-border: #CB912F;

/* 绿色 - 成功/完成 */
--green-bg: #DDF5E7;
--green-text: #448361;
--green-border: #448361;

/* 蓝色 - 信息 */
--blue-bg: #E5F2FF;
--blue-text: #2383E2;
--blue-border: #2383E2;
```

### 颜色使用规范

1. **主文字**：用于标题、正文、重要信息
2. **次要文字**：用于辅助信息、图标、时间戳
3. **三级文字**：用于占位符、禁用状态（仅用于大文字）
4. **悬停背景**：所有可交互元素的悬停状态
5. **激活背景**：当前选中/激活的元素

---

## 字体排版系统

### 字体族

```css
font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, 
             "Segoe UI", Helvetica, "Apple Color Emoji", 
             Arial, sans-serif, "Segoe UI Emoji", 
             "Segoe UI Symbol";
```

**说明**：
- 优先使用系统字体栈
- 跨平台一致性
- 支持 Emoji 显示

### 字号系统

| 名称 | 尺寸 | Rem | 用途 | 行高 |
|------|------|-----|------|------|
| xs | 12px | 0.75rem | 时间戳、徽章、分组标题 | 1.4 |
| sm | 14px | 0.875rem | 导航菜单、按钮、辅助文字 | 1.5 |
| base | 16px | 1rem | 正文、段落、列表 | 1.6 |
| lg | 20px | 1.25rem | H3 标题 | 1.3 |
| xl | 24px | 1.5rem | H2 标题 | 1.3 |
| 2xl | 30px | 1.875rem | H1 标题 | 1.2 |
| 3xl | 40px | 2.5rem | 页面标题 | 1.2 |
| 4xl | 48px | 3rem | Hero 标题 | 1.1 |

### 字重系统

```css
--font-regular: 400;   /* 正文、默认 */
--font-medium: 500;    /* 按钮、激活项、强调 */
--font-semibold: 600;  /* 标题、分组标题 */
--font-bold: 700;      /* 大标题、重要强调 */
```

### 行高系统

```css
--leading-tight: 1.1;    /* 大标题 */
--leading-snug: 1.2;     /* 标题 */
--leading-normal: 1.5;   /* 正文 */
--leading-relaxed: 1.6;  /* 长文本阅读 */
```

### 字间距

```css
--letter-spacing-tight: -0.02em;  /* 大标题 */
--letter-spacing-normal: 0;       /* 默认 */
--letter-spacing-wide: 0.5px;     /* 分组标题（大写） */
```

---

## 间距与布局

### 间距系统（基于 4px）

| Token | 值 | Rem | 用途 |
|-------|-----|-----|------|
| space-1 | 4px | 0.25rem | 紧密元素间距 |
| space-2 | 8px | 0.5rem | 图标与文字、小间距 |
| space-3 | 12px | 0.75rem | 卡片内元素 |
| space-4 | 16px | 1rem | 标准间距、卡片内边距 |
| space-6 | 24px | 1.5rem | 区块间距 |
| space-8 | 32px | 2rem | 大区块间距 |
| space-10 | 40px | 2.5rem | 页面顶部间距 |
| space-12 | 48px | 3rem | Section 间距 |
| space-16 | 64px | 4rem | 大 Section 间距 |
| space-20 | 80px | 5rem | 页面级间距 |

### 布局规范

#### 侧边栏布局

```css
.sidebar {
  width: 240px;
  padding: 16px 12px;
}

.sidebar-section {
  margin-top: 16px;
}

.sidebar-section:first-child {
  margin-top: 0;
}

.sidebar-item {
  height: 28px;
  padding: 4px 8px;
  margin-bottom: 2px;
}
```

#### 主内容布局

```css
.main-content {
  margin-left: 240px;
  max-width: 1200px;
  padding: 0 96px; /* 大屏 */
}

@media (max-width: 1280px) {
  .main-content {
    padding: 0 48px; /* 中屏 */
  }
}

@media (max-width: 768px) {
  .main-content {
    padding: 0 24px; /* 小屏 */
  }
}
```

#### 内容块间距

```css
.content-block {
  margin: 1px 0; /* 块之间最小间距 */
}

.content-block.heading {
  margin-top: 1em; /* 标题上边距 */
  margin-bottom: 4px; /* 标题下边距 */
}
```

---

## 组件设计规范

### 按钮（Button）

#### Primary Button

```css
.btn-primary {
  height: 32px;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  background: #37352F;
  color: #FFFFFF;
  border: none;
  cursor: pointer;
  transition: all 0.15s ease;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
}

.btn-primary:hover {
  background: #2E2C27;
}

.btn-primary:active {
  background: #252320;
  transform: translateY(1px);
}

.btn-primary:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  pointer-events: none;
}
```

#### Secondary Button

```css
.btn-secondary {
  height: 32px;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  background: transparent;
  color: #37352F;
  border: 1px solid #E8E7E5;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-secondary:hover {
  background: rgba(0, 0, 0, 0.03);
  border-color: #DDDBD8;
}
```

#### Text Button

```css
.btn-text {
  height: 28px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 400;
  background: transparent;
  color: #37352F;
  border: none;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-text:hover {
  background: rgba(0, 0, 0, 0.03);
}
```

### 输入框（Input）

```css
.input {
  height: 32px;
  padding: 6px 12px;
  border-radius: 4px;
  border: 1px solid #E8E7E5;
  background: #FAFAF9;
  font-size: 14px;
  color: #37352F;
  transition: all 0.15s ease;
  outline: none;
}

.input::placeholder {
  color: #9B9A97;
}

.input:hover {
  border-color: #DDDBD8;
  background: #FFFFFF;
}

.input:focus {
  border-color: #2383E2;
  background: #FFFFFF;
  box-shadow: 0 0 0 2px rgba(35, 131, 226, 0.1);
}
```

### 卡片（Card）

```css
.card {
  background: #FFFFFF;
  border: 1px solid #E8E7E5;
  border-radius: 6px;
  padding: 16px;
  transition: all 0.2s ease;
}

.card:hover {
  border-color: #DDDBD8;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
}
```

### 徽章（Badge）

```css
.badge {
  display: inline-flex;
  align-items: center;
  height: 20px;
  padding: 4px 8px;
  border-radius: 10px;
  font-size: 12px;
  font-weight: 500;
  background: #E8E7E5;
  color: #787774;
}

.badge-primary {
  background: #2383E2;
  color: #FFFFFF;
}
```

### 分割线（Divider）

```css
.divider {
  height: 1px;
  background: #E8E7E5;
  border: none;
  margin: 16px 0;
}
```

---

## 交互状态与动画

### 过渡动画

```css
/* 快速交互（按钮点击、悬停） */
--transition-fast: all 0.15s ease;

/* 标准交互（卡片悬停、菜单展开） */
--transition-base: all 0.2s ease;

/* 缓慢交互（页面切换、模态框） */
--transition-slow: all 0.3s ease;
```

### 悬停效果

```css
/* 通用悬停背景 */
.hover-effect {
  transition: background-color 0.15s ease;
}

.hover-effect:hover {
  background: rgba(0, 0, 0, 0.03);
}

/* 卡片悬停 */
.card-hover {
  transition: all 0.2s ease;
}

.card-hover:hover {
  border-color: #DDDBD8;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
  transform: translateY(-1px);
}
```

### 焦点状态

```css
/* 输入框焦点 */
.input:focus {
  outline: none;
  border-color: #2383E2;
  box-shadow: 0 0 0 2px rgba(35, 131, 226, 0.1);
}

/* 按钮焦点（键盘导航） */
.button:focus-visible {
  outline: 2px solid #2383E2;
  outline-offset: 2px;
}
```

### 激活状态

```css
/* 导航项激活 */
.nav-item.active {
  background: rgba(0, 0, 0, 0.05);
  color: #37352F;
  font-weight: 500;
}

/* 按钮激活 */
.button:active {
  transform: translateY(1px);
  box-shadow: none;
}
```

### 加载状态

```css
.loading {
  opacity: 0.6;
  pointer-events: none;
  position: relative;
}

.loading::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 16px;
  height: 16px;
  margin: -8px 0 0 -8px;
  border: 2px solid #E8E7E5;
  border-top-color: #2383E2;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

---

## 微动效详细分析

### 微动效设计原则

Notion 的微动效设计遵循以下核心原则：

1. **即时反馈**：所有交互都有即时的视觉反馈（< 100ms）
2. **自然流畅**：使用缓动函数（easing）模拟物理运动
3. **适度克制**：动画时长适中，不干扰用户操作
4. **性能优先**：优先使用 CSS transform 和 opacity，避免触发重排重绘

### 动画时长系统

```css
/* 极快（即时反馈） */
--duration-instant: 0ms;      /* 无动画 */
--duration-immediate: 50ms;   /* 即时反馈 */
--duration-fast: 100ms;       /* 快速交互 */
--duration-base: 150ms;        /* 标准交互 */
--duration-slow: 200ms;        /* 缓慢交互 */
--duration-slower: 300ms;      /* 更慢交互 */
```

**使用场景**：
- **50ms**：颜色变化、透明度变化
- **100ms**：悬停背景、图标颜色
- **150ms**：按钮点击、菜单项悬停
- **200ms**：卡片悬停、下拉菜单展开
- **300ms**：页面切换、模态框出现

### 缓动函数（Easing Functions）

```css
/* 标准缓动 */
--ease-standard: cubic-bezier(0.4, 0.0, 0.2, 1);
/* 进入缓动（加速） */
--ease-in: cubic-bezier(0.4, 0.0, 1, 1);
/* 退出缓动（减速） */
--ease-out: cubic-bezier(0.0, 0.0, 0.2, 1);
/* 进入退出缓动（先加速后减速） */
--ease-in-out: cubic-bezier(0.4, 0.0, 0.2, 1);
/* 线性 */
--ease-linear: linear;
```

### 具体微动效分析

#### 1. 侧边栏菜单项悬停

**触发时机**：鼠标移入菜单项

**动画效果**：
```css
.nav-item {
  transition: background-color 0.15s cubic-bezier(0.4, 0.0, 0.2, 1),
              color 0.15s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.nav-item:hover {
  background-color: rgba(0, 0, 0, 0.03);
  color: #37352F;
}
```

**细节分析**：
- **时长**：`150ms`（快速响应）
- **缓动**：`cubic-bezier(0.4, 0.0, 0.2, 1)`（标准缓动）
- **变化属性**：背景色、文字颜色
- **视觉感受**：平滑、自然

#### 2. 内容块悬停显示操作按钮

**触发时机**：鼠标移入内容块

**动画效果**：
```css
.block-control {
  opacity: 0;
  transform: translateX(-4px);
  transition: opacity 0.15s cubic-bezier(0.4, 0.0, 0.2, 1),
              transform 0.15s cubic-bezier(0.4, 0.0, 0.2, 1);
  pointer-events: none;
}

.content-block:hover .block-control {
  opacity: 1;
  transform: translateX(0);
  pointer-events: auto;
}
```

**细节分析**：
- **时长**：`150ms`
- **缓动**：标准缓动
- **变化属性**：透明度、位移
- **初始状态**：透明度 0，向左偏移 4px
- **结束状态**：透明度 1，位置归零
- **视觉感受**：从左侧淡入滑出

#### 3. 按钮点击反馈

**触发时机**：鼠标按下按钮

**动画效果**：
```css
.btn-primary {
  transition: background-color 0.15s cubic-bezier(0.4, 0.0, 0.2, 1),
              transform 0.1s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.btn-primary:active {
  background-color: #252320;
  transform: translateY(1px) scale(0.98);
}
```

**细节分析**：
- **背景色变化**：`150ms`
- **位移/缩放**：`100ms`（更快）
- **位移距离**：向下 `1px`
- **缩放比例**：`0.98`（轻微缩小）
- **视觉感受**：按下感，有物理反馈

#### 4. 输入框焦点状态

**触发时机**：输入框获得焦点

**动画效果**：
```css
.input {
  transition: border-color 0.15s cubic-bezier(0.4, 0.0, 0.2, 1),
              background-color 0.15s cubic-bezier(0.4, 0.0, 0.2, 1),
              box-shadow 0.15s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.input:focus {
  border-color: #2383E2;
  background-color: #FFFFFF;
  box-shadow: 0 0 0 2px rgba(35, 131, 226, 0.1);
}
```

**细节分析**：
- **时长**：`150ms`
- **变化属性**：边框颜色、背景色、阴影
- **阴影效果**：蓝色光晕，2px 扩散
- **视觉感受**：清晰的焦点指示

#### 5. 卡片悬停提升

**触发时机**：鼠标移入卡片

**动画效果**：
```css
.card {
  transition: transform 0.2s cubic-bezier(0.4, 0.0, 0.2, 1),
              box-shadow 0.2s cubic-bezier(0.4, 0.0, 0.2, 1),
              border-color 0.2s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  border-color: #DDDBD8;
}
```

**细节分析**：
- **时长**：`200ms`（稍慢，更优雅）
- **位移距离**：向上 `2px`
- **阴影变化**：从无到有，增强层次感
- **视觉感受**：卡片"浮起"，有深度感

#### 6. 下拉菜单展开/收起

**触发时机**：点击触发按钮

**动画效果**：
```css
.dropdown-menu {
  opacity: 0;
  transform: translateY(-8px) scale(0.95);
  transition: opacity 0.2s cubic-bezier(0.4, 0.0, 0.2, 1),
              transform 0.2s cubic-bezier(0.4, 0.0, 0.2, 1);
  pointer-events: none;
}

.dropdown-menu.open {
  opacity: 1;
  transform: translateY(0) scale(1);
  pointer-events: auto;
}
```

**细节分析**：
- **时长**：`200ms`
- **初始状态**：透明度 0，向上偏移 8px，缩放 0.95
- **结束状态**：透明度 1，位置归零，缩放 1
- **视觉感受**：从上方淡入并放大

#### 7. 页面切换过渡

**触发时机**：切换页面

**动画效果**：
```css
.page {
  opacity: 0;
  transform: translateX(8px);
  transition: opacity 0.3s cubic-bezier(0.4, 0.0, 0.2, 1),
              transform 0.3s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.page.active {
  opacity: 1;
  transform: translateX(0);
}
```

**细节分析**：
- **时长**：`300ms`（较慢，不干扰阅读）
- **初始状态**：透明度 0，向右偏移 8px
- **结束状态**：透明度 1，位置归零
- **视觉感受**：从右侧淡入滑入

#### 8. 内容块拖拽反馈

**触发时机**：开始拖拽内容块

**动画效果**：
```css
.content-block.dragging {
  opacity: 0.5;
  transform: rotate(2deg) scale(0.98);
  transition: opacity 0.1s ease,
              transform 0.1s ease;
  cursor: grabbing;
}

.content-block.drag-over {
  border-top: 2px solid #2383E2;
  margin-top: 4px;
}
```

**细节分析**：
- **拖拽中**：透明度 0.5，轻微旋转和缩放
- **拖拽目标**：蓝色上边框，增加上边距
- **视觉感受**：清晰的拖拽状态指示

#### 9. 加载状态动画

**触发时机**：数据加载中

**动画效果**：
```css
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-spinner {
  width: 16px;
  height: 16px;
  border: 2px solid #E8E7E5;
  border-top-color: #2383E2;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}
```

**细节分析**：
- **时长**：`600ms`（一圈）
- **缓动**：`linear`（匀速）
- **视觉感受**：流畅的旋转，不卡顿

#### 10. 文本选择动画

**触发时机**：选择文本

**动画效果**：
```css
::selection {
  background: rgba(35, 131, 226, 0.2);
  color: #37352F;
  transition: background-color 0.1s ease;
}
```

**细节分析**：
- **时长**：`100ms`（快速）
- **背景色**：半透明蓝色
- **视觉感受**：清晰的选中状态

### 性能优化技巧

#### 1. 使用 transform 和 opacity

```css
/* 好：使用 transform（GPU 加速） */
.element {
  transform: translateY(-2px);
  transition: transform 0.2s ease;
}

/* 差：使用 top/left（触发重排） */
.element {
  top: -2px;
  transition: top 0.2s ease;
}
```

#### 2. 使用 will-change 提示浏览器

```css
.element {
  will-change: transform, opacity;
}

.element:hover {
  transform: translateY(-2px);
}
```

#### 3. 减少动画元素数量

- 避免同时动画过多元素
- 使用 `transform: translateZ(0)` 开启硬件加速

#### 4. 使用 requestAnimationFrame

```javascript
function animate() {
  // 动画逻辑
  requestAnimationFrame(animate);
}
animate();
```

---

## 交互细节深度分析

### 交互设计原则

1. **即时反馈**：所有操作都有即时视觉反馈
2. **可预测性**：交互行为符合用户预期
3. **容错性**：提供撤销、重做等容错机制
4. **一致性**：相同操作在不同场景下表现一致
5. **渐进式披露**：复杂功能逐步展示

### 具体交互细节

#### 1. 侧边栏菜单项交互

**交互流程**：
1. **默认状态**：文字颜色 `#787774`，背景透明
2. **悬停状态**：背景变为 `rgba(0, 0, 0, 0.03)`，文字颜色 `#37352F`
3. **激活状态**：背景 `rgba(0, 0, 0, 0.05)`，文字颜色 `#37352F`，字重 `500`

**细节要点**：
- 悬停和激活状态有明确的视觉区分
- 激活状态背景更深，字重更重
- 过渡动画 `150ms`，流畅自然

**代码实现**：
```css
.nav-item {
  height: 28px;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  color: #787774;
  background: transparent;
  cursor: pointer;
  transition: all 0.15s cubic-bezier(0.4, 0.0, 0.2, 1);
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 2px;
}

.nav-item:hover {
  background: rgba(0, 0, 0, 0.03);
  color: #37352F;
}

.nav-item.active {
  background: rgba(0, 0, 0, 0.05);
  color: #37352F;
  font-weight: 500;
}
```

#### 2. 内容块编辑交互

**交互流程**：
1. **默认状态**：内容块正常显示
2. **悬停状态**：背景变为 `rgba(0, 0, 0, 0.03)`，左侧显示操作按钮
3. **聚焦状态**：背景保持，光标显示
4. **编辑状态**：内容可编辑，实时保存

**细节要点**：
- 悬停时显示操作按钮（拖拽、删除等）
- 聚焦时有清晰的视觉反馈
- 编辑时背景色变化，提示可编辑状态

**代码实现**：
```css
.content-block {
  padding: 3px 2px;
  border-radius: 3px;
  margin: 1px 0;
  position: relative;
  transition: background-color 0.15s ease;
}

.content-block:hover {
  background: rgba(0, 0, 0, 0.03);
}

.content-block:focus-within {
  background: rgba(0, 0, 0, 0.03);
  outline: none;
}

.content-block[contenteditable="true"]:focus {
  background: rgba(0, 0, 0, 0.03);
}

.block-control {
  position: absolute;
  left: -24px;
  top: 0;
  width: 20px;
  height: 20px;
  opacity: 0;
  transform: translateX(-4px);
  transition: opacity 0.15s ease,
              transform 0.15s ease;
  pointer-events: none;
}

.content-block:hover .block-control {
  opacity: 1;
  transform: translateX(0);
  pointer-events: auto;
}
```

#### 3. 按钮交互细节

**交互流程**：
1. **默认状态**：正常显示
2. **悬停状态**：背景色加深，轻微上移
3. **按下状态**：背景色更深，向下位移 1px，轻微缩放
4. **释放状态**：恢复悬停状态

**细节要点**：
- 按下时有明显的物理反馈
- 位移和缩放同时进行，增强真实感
- 过渡时间短（100ms），响应迅速

**代码实现**：
```css
.btn-primary {
  height: 32px;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  background: #37352F;
  color: #FFFFFF;
  border: none;
  cursor: pointer;
  transition: background-color 0.15s ease,
              transform 0.1s ease;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-primary:hover {
  background: #2E2C27;
  transform: translateY(-1px);
}

.btn-primary:active {
  background: #252320;
  transform: translateY(1px) scale(0.98);
}
```

#### 4. 输入框交互细节

**交互流程**：
1. **默认状态**：浅灰背景 `#FAFAF9`，灰色边框
2. **悬停状态**：白色背景，边框颜色加深
3. **聚焦状态**：蓝色边框，蓝色光晕，白色背景
4. **输入状态**：保持聚焦样式，实时验证

**细节要点**：
- 悬停时背景变白，提示可交互
- 聚焦时有明显的蓝色光晕
- 光晕使用 `box-shadow`，不占用布局空间

**代码实现**：
```css
.input {
  height: 32px;
  padding: 6px 12px;
  border-radius: 4px;
  border: 1px solid #E8E7E5;
  background: #FAFAF9;
  font-size: 14px;
  color: #37352F;
  transition: all 0.15s ease;
  outline: none;
}

.input:hover {
  border-color: #DDDBD8;
  background: #FFFFFF;
}

.input:focus {
  border-color: #2383E2;
  background: #FFFFFF;
  box-shadow: 0 0 0 2px rgba(35, 131, 226, 0.1);
}
```

#### 5. 下拉菜单交互细节

**交互流程**：
1. **触发**：点击按钮或悬停
2. **展开**：从上方淡入滑下，缩放从 0.95 到 1
3. **悬停**：菜单项背景变化
4. **选择**：点击菜单项，菜单关闭
5. **关闭**：淡出并上移

**细节要点**：
- 展开动画从上方开始，符合下拉逻辑
- 缩放效果增强层次感
- 关闭动画与展开相反

**代码实现**：
```css
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  min-width: 200px;
  background: #FFFFFF;
  border: 1px solid #E8E7E5;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  opacity: 0;
  transform: translateY(-8px) scale(0.95);
  transition: opacity 0.2s ease,
              transform 0.2s ease;
  pointer-events: none;
  z-index: 1000;
}

.dropdown-menu.open {
  opacity: 1;
  transform: translateY(0) scale(1);
  pointer-events: auto;
}

.dropdown-item {
  padding: 8px 12px;
  font-size: 14px;
  color: #37352F;
  cursor: pointer;
  transition: background-color 0.15s ease;
}

.dropdown-item:hover {
  background: rgba(0, 0, 0, 0.03);
}
```

#### 6. 拖拽交互细节

**交互流程**：
1. **准备**：鼠标移到可拖拽元素上，光标变为 `grab`
2. **开始**：按下鼠标，光标变为 `grabbing`，元素半透明
3. **拖拽**：元素跟随鼠标移动，显示拖拽预览
4. **目标**：拖到目标位置，显示插入指示线
5. **放置**：释放鼠标，元素插入新位置

**细节要点**：
- 拖拽时元素半透明，不影响视线
- 目标位置有清晰的插入指示
- 拖拽预览使用 `transform`，性能好

**代码实现**：
```css
.draggable-item {
  cursor: grab;
  transition: opacity 0.1s ease,
              transform 0.1s ease;
}

.draggable-item:active {
  cursor: grabbing;
}

.draggable-item.dragging {
  opacity: 0.5;
  transform: rotate(2deg) scale(0.98);
}

.drag-target {
  position: relative;
}

.drag-target::before {
  content: "";
  position: absolute;
  top: -2px;
  left: 0;
  right: 0;
  height: 2px;
  background: #2383E2;
  opacity: 0;
  transition: opacity 0.15s ease;
}

.drag-target.drag-over::before {
  opacity: 1;
}
```

#### 7. 页面切换交互细节

**交互流程**：
1. **触发**：点击导航项或面包屑
2. **过渡**：当前页面淡出，新页面从右侧淡入
3. **完成**：新页面完全显示

**细节要点**：
- 使用淡入淡出，不干扰阅读
- 新页面从右侧滑入，符合阅读习惯
- 过渡时间适中（300ms），不感觉慢

**代码实现**：
```css
.page {
  opacity: 0;
  transform: translateX(8px);
  transition: opacity 0.3s cubic-bezier(0.4, 0.0, 0.2, 1),
              transform 0.3s cubic-bezier(0.4, 0.0, 0.2, 1);
  pointer-events: none;
}

.page.active {
  opacity: 1;
  transform: translateX(0);
  pointer-events: auto;
}
```

#### 8. 搜索交互细节

**交互流程**：
1. **触发**：点击搜索图标或快捷键（Cmd/Ctrl + K）
2. **展开**：搜索框从顶部滑下
3. **输入**：实时显示搜索结果
4. **选择**：键盘导航或鼠标点击
5. **关闭**：点击外部或按 ESC

**细节要点**：
- 快捷键支持，提高效率
- 实时搜索，即时反馈
- 键盘导航支持，无障碍

**代码实现**：
```css
.search-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(4px);
  opacity: 0;
  transition: opacity 0.2s ease;
  pointer-events: none;
  z-index: 1000;
}

.search-overlay.open {
  opacity: 1;
  pointer-events: auto;
}

.search-box {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%) translateY(-20px);
  width: 600px;
  max-width: 90%;
  background: #FFFFFF;
  border: 1px solid #E8E7E5;
  border-radius: 8px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  opacity: 0;
  transition: opacity 0.2s ease,
              transform 0.2s ease;
}

.search-overlay.open .search-box {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
```

#### 9. 工具提示（Tooltip）交互细节

**交互流程**：
1. **触发**：鼠标悬停在元素上
2. **延迟**：等待 200ms（避免误触发）
3. **显示**：淡入并向上滑出
4. **保持**：鼠标在元素上时保持显示
5. **隐藏**：鼠标移出后淡出

**细节要点**：
- 延迟显示，避免干扰
- 淡入滑出，自然流畅
- 位置智能调整，不超出视口

**代码实现**：
```css
.tooltip {
  position: absolute;
  padding: 6px 10px;
  background: #37352F;
  color: #FFFFFF;
  font-size: 12px;
  border-radius: 4px;
  opacity: 0;
  transform: translateY(-4px);
  transition: opacity 0.2s ease,
              transform 0.2s ease;
  pointer-events: none;
  z-index: 10000;
  white-space: nowrap;
}

.tooltip-trigger:hover .tooltip {
  opacity: 1;
  transform: translateY(0);
  transition-delay: 0.2s;
}
```

#### 10. 加载状态交互细节

**交互流程**：
1. **触发**：开始加载数据
2. **显示**：显示加载指示器
3. **动画**：旋转动画持续
4. **完成**：数据加载完成，淡出加载指示器

**细节要点**：
- 加载指示器清晰可见
- 旋转动画流畅不卡顿
- 加载完成后平滑过渡

**代码实现**：
```css
.loading-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(2px);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.2s ease;
  pointer-events: none;
  z-index: 100;
}

.loading-overlay.active {
  opacity: 1;
  pointer-events: auto;
}

.loading-spinner {
  width: 24px;
  height: 24px;
  border: 3px solid #E8E7E5;
  border-top-color: #2383E2;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}
```

### 交互反馈总结

| 交互类型 | 反馈方式 | 时长 | 缓动函数 |
|---------|---------|------|---------|
| 悬停 | 背景色变化 | 150ms | cubic-bezier(0.4, 0.0, 0.2, 1) |
| 点击 | 位移 + 缩放 | 100ms | cubic-bezier(0.4, 0.0, 0.2, 1) |
| 聚焦 | 边框 + 光晕 | 150ms | cubic-bezier(0.4, 0.0, 0.2, 1) |
| 展开 | 淡入 + 滑入 | 200ms | cubic-bezier(0.4, 0.0, 0.2, 1) |
| 切换 | 淡入淡出 | 300ms | cubic-bezier(0.4, 0.0, 0.2, 1) |
| 拖拽 | 透明度 + 变换 | 100ms | ease |
| 加载 | 旋转动画 | 600ms | linear |

---

## 图标系统

### 图标尺寸

```css
--icon-xs: 12px;   /* 行内小图标 */
--icon-sm: 14px;   /* 提示图标 */
--icon-base: 16px; /* 标准图标（菜单、按钮） */
--icon-lg: 20px;   /* 大图标 */
--icon-xl: 24px;   /* 特大图标 */
```

### 图标颜色

```css
/* 默认状态 */
.icon {
  color: #787774;
  width: 16px;
  height: 16px;
}

/* 悬停状态 */
.icon:hover {
  color: #37352F;
}

/* 激活状态 */
.icon.active {
  color: #37352F;
}

/* 禁用状态 */
.icon:disabled {
  color: #9B9A97;
  opacity: 0.5;
}
```

### 图标使用规范

1. **统一尺寸**：同一层级使用相同尺寸
2. **统一风格**：使用线条图标（Line Icons）
3. **统一颜色**：遵循颜色系统
4. **对齐方式**：与文字垂直居中对齐

---

## 响应式设计

### 断点系统

```css
/* 移动设备 */
@media (max-width: 640px) {
  /* sm */
  .sidebar {
    transform: translateX(-100%);
  }
  
  .main-content {
    margin-left: 0;
    padding: 0 16px;
  }
}

/* 平板 */
@media (min-width: 641px) and (max-width: 1024px) {
  /* md */
  .main-content {
    padding: 0 48px;
  }
}

/* 桌面 */
@media (min-width: 1025px) {
  /* lg */
  .main-content {
    padding: 0 96px;
  }
}

/* 大屏桌面 */
@media (min-width: 1280px) {
  /* xl */
  .main-content {
    max-width: 1200px;
  }
}
```

### 移动端适配

1. **侧边栏**：默认隐藏，通过按钮切换
2. **内容区域**：全宽显示，减少左右边距
3. **字体大小**：适当缩小，保持可读性
4. **触摸目标**：至少 `44px × 44px`

---

## 可访问性设计

### 对比度要求

- **正文文字（14px+）**：至少 `4.5:1`
- **大文字（18px+ 或 14px bold+）**：至少 `3:1`
- **UI 组件**：至少 `3:1`

### 键盘导航

```css
/* 所有可交互元素支持键盘导航 */
.interactive-element:focus-visible {
  outline: 2px solid #2383E2;
  outline-offset: 2px;
}

/* Tab 顺序 */
.interactive-element {
  tabindex: 0;
}

.interactive-element:disabled {
  tabindex: -1;
}
```

### 屏幕阅读器支持

```html
<!-- 使用语义化 HTML -->
<nav aria-label="Main navigation">
  <button aria-label="Toggle sidebar">☰</button>
</nav>

<!-- 提供替代文本 -->
<img src="icon.svg" alt="Settings" aria-hidden="true" />

<!-- 状态提示 -->
<div role="status" aria-live="polite">
  Page saved
</div>
```

### 动画偏好

```css
/* 尊重用户的动画偏好设置 */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 设计原则总结

### 1. 内容优先（Content First）
- 所有设计决策都围绕内容展开
- 减少视觉干扰，突出内容本身
- 提供充足的留白空间

### 2. 一致性（Consistency）
- 统一的间距系统（4px 基准）
- 统一的圆角（3px/4px/6px）
- 统一的交互反馈（0.15s-0.2s 过渡）
- 统一的颜色系统

### 3. 简洁性（Simplicity）
- 使用中性色调为主
- 避免过度装饰
- 保持界面清爽

### 4. 可访问性（Accessibility）
- 确保文字对比度符合 WCAG AA 标准
- 提供清晰的焦点状态
- 支持键盘导航
- 尊重用户的动画偏好

### 5. 响应式（Responsive）
- 移动优先设计
- 灵活的布局系统
- 自适应的组件尺寸

---

## 实施建议

### 1. CSS 变量系统

```css
:root {
  /* 文字颜色 */
  --text-primary: #37352F;
  --text-secondary: #787774;
  --text-tertiary: #9B9A97;
  
  /* 背景颜色 */
  --bg-primary: #FFFFFF;
  --bg-secondary: #F7F6F3;
  --bg-hover: rgba(0, 0, 0, 0.03);
  --bg-active: rgba(0, 0, 0, 0.05);
  
  /* 边框颜色 */
  --border-default: #E8E7E5;
  --border-hover: #DDDBD8;
  
  /* 间距系统 */
  --space-1: 4px;
  --space-2: 8px;
  --space-4: 16px;
  --space-8: 32px;
  
  /* 圆角 */
  --radius-sm: 3px;
  --radius-base: 4px;
  --radius-md: 6px;
  
  /* 过渡 */
  --transition-fast: all 0.15s ease;
  --transition-base: all 0.2s ease;
}
```

### 2. 组件库结构

```
components/
├── Button/
│   ├── Button.tsx
│   ├── Button.module.css
│   └── Button.stories.tsx
├── Input/
├── Card/
├── Navigation/
└── ...
```

### 3. 设计 Token

建议使用 JSON 格式存储设计 Token，便于跨平台使用：

```json
{
  "colors": {
    "text": {
      "primary": "#37352F",
      "secondary": "#787774",
      "tertiary": "#9B9A97"
    },
    "background": {
      "primary": "#FFFFFF",
      "secondary": "#F7F6F3"
    }
  },
  "spacing": {
    "1": "4px",
    "2": "8px",
    "4": "16px"
  }
}
```

---

## 细节补充

### 滚动条样式

```css
/* Webkit 浏览器 */
::-webkit-scrollbar {
  width: 10px;
  height: 10px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: #E8E7E5;
  border-radius: 5px;
}

::-webkit-scrollbar-thumb:hover {
  background: #DDDBD8;
}
```

### 选择文本样式

```css
::selection {
  background: rgba(35, 131, 226, 0.2);
  color: #37352F;
}
```

### 占位符样式

```css
::placeholder {
  color: #9B9A97;
  opacity: 1;
}
```

---

## 参考资源

- **Notion 官方应用**：直接观察和学习
- **设计系统文档**：建立和维护设计系统文档
- **组件库**：使用 Storybook 等工具管理组件
- **设计工具**：Figma/Sketch 中建立设计系统

---

**文档版本**: v1.0  
**最后更新**: 2025-11  
**基于**: Notion 应用界面深度分析  
**适用场景**: 前端开发参考、设计系统建立

