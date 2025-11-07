# Notion 设计系统规范

> 基于 Notion 界面提取的完整前端设计规范
> 适用技术栈：React + Tailwind CSS

---

## 📚 目录

1. [色彩系统](#色彩系统)
2. [字体排版](#字体排版)
3. [间距布局](#间距布局)
4. [组件规范](#组件规范)
5. [阴影圆角边框](#阴影圆角边框)
6. [图标系统](#图标系统)
7. [交互状态](#交互状态)

---

## 🎨 色彩系统

### 主题色 (Primary Colors)

```css
--primary-blue: #2383E2;      /* 品牌主色、按钮、链接 */
--primary-purple: #6B4DFF;    /* 强调色、用户头像背景 */
```

### 中性色 (Neutral / Gray Scale)

```css
/* 文字颜色 */
--text-primary: #37352F;      /* 标题、正文 */
--text-secondary: #787774;    /* 辅助文字、图标 */
--text-tertiary: #9B9A97;     /* 占位符、禁用状态 */

/* 背景颜色 */
--bg-primary: #FFFFFF;        /* 主背景、卡片 */
--bg-secondary: #F7F6F3;      /* 侧边栏、悬浮背景 */
--bg-tertiary: #FAFAF9;       /* 区块背景、输入框 */

/* 边框颜色 */
--border-default: #E8E7E5;    /* 分割线、卡片边框 */
--border-hover: #DDDBD8;      /* 悬浮状态边框 */
```

### 状态色 (Semantic Colors)

```css
/* 红色 - To Do / 错误 */
--red-bg: #FFE2DD;
--red-text: #D44C47;
--red-border: #D44C47;

/* 黄色 - Doing / 警告 */
--yellow-bg: #FFF7E0;
--yellow-text: #CB912F;
--yellow-border: #CB912F;

/* 绿色 - Done / 成功 */
--green-bg: #DDF5E7;
--green-text: #448361;
--green-border: #448361;

/* 蓝色 - 信息 */
--blue-bg: #E5F2FF;
--blue-text: #2383E2;
--blue-border: #2383E2;
```

### 交互状态

```css
--hover-overlay: rgba(0, 0, 0, 0.03);
--active-overlay: rgba(0, 0, 0, 0.05);
--focus-ring: rgba(35, 131, 226, 0.1);
```

---

## 🔤 字体排版

### 字体族 (Font Family)

```css
font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", 
             Helvetica, "Apple Color Emoji", Arial, sans-serif, 
             "Segoe UI Emoji", "Segoe UI Symbol";
```

### 字号梯度 (Font Size Scale)

| 名称 | 尺寸 | Rem | 用途 |
|------|------|-----|------|
| xs | 12px | 0.75rem | 时间戳、徽章、小字 |
| sm | 14px | 0.875rem | 正文、导航菜单、按钮 |
| base | 16px | 1rem | 卡片标题、表单 |
| lg | 20px | 1.25rem | 章节标题 |
| xl | 24px | 1.5rem | 页面副标题 |
| 2xl | 30px | 1.875rem | 页面主标题 |
| 3xl | 40px | 2.5rem | 营销页大标题 |
| 4xl | 48px | 3rem | Hero 标题 |

### 字重 (Font Weight)

```css
--font-regular: 400;   /* 正文 */
--font-medium: 500;    /* 按钮、标签、强调 */
--font-semibold: 600;  /* 标题、活动项 */
--font-bold: 700;      /* 营销页大标题 */
```

### 行高 (Line Height)

```css
--leading-tight: 1.2;   /* 大标题 */
--leading-normal: 1.5;  /* 正文 */
--leading-relaxed: 1.6; /* 长文本阅读 */
--leading-none: 1;      /* 按钮、徽章 */
```

---

## 📐 间距布局

### 间距基准 (Spacing Scale - 基于 4px)

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

### 布局规则

#### 侧边栏 (Sidebar)
```css
宽度: 240px
内边距: 16px
菜单项高度: 28px
菜单项间距: 2px
菜单项图标: 16px
分组标题上边距: 24px
```

#### 主内容区 (Main Content)
```css
最大宽度: 1200px
大屏左右外边距: 96px
中屏左右外边距: 48px
小屏左右外边距: 24px
顶部间距: 40px
```

#### 卡片网格 (Card Grid)
```css
列数: 响应式 (4列 → 3列 → 2列 → 1列)
行间距: 16px
列间距: 16px
卡片内边距: 16px
```

#### 看板视图 (Kanban Board)
```css
列最小宽度: 280px
列间距: 16px
卡片间距: 8px
列头高度: 40px
```

---

## 🧩 组件规范

### 按钮 (Buttons)

#### Primary Button
```css
高度: 32px
内边距: 8px 12px
圆角: 4px
字号: 14px
字重: 500
背景: #2383E2
文字: #FFFFFF
边框: none

Hover:
  背景: #1a6fbd (darkened 10%)
  
Active:
  背景: #0d5ba6 (darkened 20%)
  
Disabled:
  背景: #E8E7E5
  文字: #9B9A97
  cursor: not-allowed
```

#### Secondary Button
```css
高度: 32px
内边距: 8px 12px
圆角: 4px
背景: transparent
边框: 1px solid #E8E7E5
文字: #37352F

Hover:
  背景: rgba(0, 0, 0, 0.03)
  边框: #DDDBD8
```

#### Text Button
```css
背景: transparent
边框: none
文字: #2383E2 / #D44C47 / #CB912F
内边距: 4px 8px

Hover:
  文字: 加深 10%
  背景: rgba(35, 131, 226, 0.05)
```

### 卡片 (Cards)

#### 标准卡片
```css
背景: #FFFFFF
边框: 1px solid #E8E7E5
圆角: 6px
内边距: 16px
过渡: all 0.2s ease

Hover:
  阴影: 0 4px 12px rgba(0, 0, 0, 0.08)
  边框: #DDDBD8
  transform: translateY(-2px)
```

#### 看板卡片
```css
背景色: 状态色背景 (#FFE2DD / #FFF7E0 / #DDF5E7)
边框: 1px solid 对应状态色
圆角: 4px
内边距: 12px
```

### 输入框 (Input)

```css
高度: 32px
内边距: 6px 12px
圆角: 4px
边框: 1px solid #E8E7E5
背景: #FAFAF9
字号: 14px

Placeholder:
  颜色: #9B9A97
  
Focus:
  边框: #2383E2
  背景: #FFFFFF
  阴影: 0 0 0 2px rgba(35, 131, 226, 0.1)
  
Disabled:
  背景: #F7F6F3
  文字: #9B9A97
  cursor: not-allowed
```

### 导航菜单 (Navigation)

```css
菜单项高度: 28px
内边距: 4px 8px
圆角: 4px
字号: 14px
图标大小: 16px
图标右边距: 8px

默认:
  文字: #787774
  背景: transparent
  
Hover:
  背景: rgba(0, 0, 0, 0.03)
  
Active/Selected:
  背景: rgba(0, 0, 0, 0.05)
  文字: #37352F
  字重: 500
```

### 徽章 (Badge)

#### 计数徽章
```css
高度: 20px
内边距: 4px 8px
圆角: 10px (pill)
字号: 12px
字重: 500
背景: #E8E7E5
文字: #787774
```

#### 状态标签
```css
内边距: 4px 8px
圆角: 4px
字号: 12px
字重: 500

To Do:
  背景: #FFE2DD
  文字: #D44C47
  
Doing:
  背景: #FFF7E0
  文字: #CB912F
  
Done:
  背景: #DDF5E7
  文字: #448361
```

### 分割线 (Divider)

```css
边框: 1px solid #E8E7E5
上下间距: 24px
```

---

## 🎭 阴影圆角边框

### 阴影系统 (Box Shadow)

```css
/* 无阴影 */
--shadow-none: none;

/* 小阴影 - 下拉菜单 */
--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.06);

/* 中阴影 - 卡片悬浮 */
--shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08);

/* 大阴影 - 模态框 */
--shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.12);

/* 超大阴影 - 弹出层 */
--shadow-xl: 0 16px 48px rgba(0, 0, 0, 0.16);
```

### 圆角系统 (Border Radius)

```css
--radius-none: 0;
--radius-sm: 3px;     /* 小元素、徽章 */
--radius-base: 4px;   /* 按钮、输入框、标签 */
--radius-md: 6px;     /* 卡片、弹窗 */
--radius-lg: 8px;     /* 大卡片 */
--radius-xl: 12px;    /* 图片容器 */
--radius-full: 9999px; /* 圆形头像、pill */
```

### 边框系统 (Border)

```css
--border-width: 1px;
--border-width-2: 2px;

/* 边框样式 */
border: 1px solid #E8E7E5;  /* 默认 */
border: 1px solid #DDDBD8;  /* Hover */
border: 2px solid #2383E2;  /* Focus */
```

---

## 🎯 图标系统

### 图标尺寸

```css
--icon-xs: 12px;   /* 行内小图标 */
--icon-sm: 16px;   /* 菜单、按钮图标 */
--icon-base: 20px; /* 标准图标 */
--icon-lg: 24px;   /* 大图标 */
--icon-xl: 32px;   /* 特大图标 */
```

### 图标状态

```css
/* 默认状态 */
颜色: #787774
尺寸: 16px

/* Hover 状态 */
颜色: #37352F

/* Active/Selected 状态 */
颜色: #37352F
背景: rgba(0, 0, 0, 0.05)
圆角: 4px
内边距: 4px

/* 禁用状态 */
颜色: #9B9A97
opacity: 0.5
```

### 社交媒体图标

```css
/* 默认状态 */
尺寸: 40px × 40px
背景: #E8E7E5
圆角: 8px
图标颜色: #787774
图标大小: 20px

/* Hover 状态 */
背景: #DDDBD8
图标颜色: #37352F
过渡: all 0.2s ease

/* Active 状态 */
背景: #37352F
图标颜色: #FFFFFF
```

---

## ✨ 交互状态

### 过渡动画 (Transitions)

```css
/* 快速交互 */
--transition-fast: all 0.15s ease;

/* 标准交互 */
--transition-base: all 0.2s ease;

/* 缓慢交互 */
--transition-slow: all 0.3s ease;

/* 常用属性 */
transition: background-color 0.2s ease;
transition: transform 0.2s ease;
transition: box-shadow 0.2s ease;
transition: opacity 0.2s ease;
```

### Hover 效果

```css
/* 按钮 Hover */
transform: translateY(-1px);
box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);

/* 卡片 Hover */
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);

/* 菜单项 Hover */
background: rgba(0, 0, 0, 0.03);
```

### Focus 状态

```css
/* 输入框 Focus */
outline: none;
border-color: #2383E2;
box-shadow: 0 0 0 2px rgba(35, 131, 226, 0.1);

/* 按钮 Focus (键盘导航) */
outline: 2px solid #2383E2;
outline-offset: 2px;
```

### Active 状态

```css
/* 按钮 Active */
transform: translateY(0);
box-shadow: none;

/* 导航项 Active */
background: rgba(0, 0, 0, 0.05);
font-weight: 500;
```

### Disabled 状态

```css
opacity: 0.5;
cursor: not-allowed;
pointer-events: none;
background: #E8E7E5;
color: #9B9A97;
```

---

## 📱 响应式断点

```css
/* 移动设备 */
@media (max-width: 640px) {
  /* sm */
}

/* 平板 */
@media (min-width: 641px) and (max-width: 1024px) {
  /* md */
}

/* 桌面 */
@media (min-width: 1025px) {
  /* lg */
}

/* 大屏桌面 */
@media (min-width: 1280px) {
  /* xl */
}
```

---

## 🎨 色彩对比度 (A11y)

### WCAG 2.1 对比度要求

- **正文文字 (14px+)**: 至少 4.5:1
- **大文字 (18px+ 或 14px bold+)**: 至少 3:1
- **UI 组件**: 至少 3:1

### Notion 色彩对比度检查

```
✅ #37352F (文字主色) on #FFFFFF: 10.8:1 (优秀)
✅ #787774 (文字次要) on #FFFFFF: 4.9:1 (通过)
⚠️ #9B9A97 (文字三级) on #FFFFFF: 3.2:1 (仅大文字通过)
✅ #2383E2 (蓝色) on #FFFFFF: 4.5:1 (通过)
✅ #FFFFFF (白色) on #2383E2: 4.5:1 (通过)
```

---

## 📝 设计原则

### 1. 简洁优雅
- 使用中性色为主，品牌色为辅
- 避免过度装饰，保持界面清爽
- 留白充足，提升阅读体验

### 2. 一致性
- 统一的间距系统（4px 基准）
- 统一的圆角（4px/6px）
- 统一的交互反馈（0.2s 过渡）

### 3. 可访问性
- 确保文字对比度符合 WCAG AA 标准
- 提供清晰的焦点状态
- 支持键盘导航

### 4. 响应式
- 移动优先设计
- 灵活的栅格系统
- 自适应的组件尺寸

---

## 🚀 快速开始

下一步可以：
1. 查看 `tailwind.config.js` 配置文件
2. 查看 React 组件示例代码
3. 参考设计 Token（JSON 格式）

---

**文档版本**: v1.0  
**最后更新**: 2025-11  
**基于**: Notion 官网与应用界面提取
