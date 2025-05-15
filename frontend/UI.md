# 前端 UI 设计与实现文档

## 项目概述

这是一个使用现代技术栈构建的网站搜索引擎项目的前端部分。项目前端包含三个主要模块：

* administrator - 网站运营后台（供这个项目的管理员使用）
* user - 用户网站（供普通用户使用）
* manage - 网站管理员（供网站管理员使用，以便提交索引链接）

## 主要功能流程

1. 用户搜索流程：

   * 通过前端界面输入关键词
   * 前端将关键词通过 HTTP 请求发送至后端 API
   * 后端返回搜索结果，前端展示
   * 如果没有搜索结果，显示"没有搜到诶~要不换个关键词试试"
   
2. 前端与后端交互：

   * 使用 Next.js 框架提供简洁且响应式的用户界面
   * 搜索请求通过API发送至后端，获取相关搜索结果
   * 结果实时渲染，确保用户获得最新信息

## 项目标准

* 实现响应式布局和简约的UI设计
* 使用 Tailwind CSS 进行样式管理
* 搜索框在首页居中显示
* 统一简约的设计风格
* 确保代码安全性，避免漏洞
* 做好错误处理和用户反馈

## 初始化项目

使用以下命令初始化 Next.js 项目：

```bash
npx create-next-app@latest . --typescript --eslint --tailwind --app --turbo --no-src-dir --no-sourcemap --import-alias "@/*" --yes
```


## 项目结构

```text
frontend/
├─ app/
│  ├─ (auth)/           # 身份验证相关页面
│  │  ├─ login/
│  │  └─ register/
│  ├─ search/          # 搜索结果页面
│  ├─ page.tsx         # 首页
│  └─ layout.tsx       # 根布局
├─ components/         # 可重用组件
│  ├─ ui/             # 基础UI组件
│  └─ search/         # 搜索相关组件
├─ styles/            # 全局样式
└─ public/            # 静态资源
```

## 设计规范

### 颜色方案
- 主色调：#4285F4 (Google 蓝)
- 辅助色：
  - #DB4437 (红)
  - #F4B400 (黄)
  - #0F9D58 (绿)
- 背景色：#FFFFFF
- 文字颜色：
  - 主要文本：#202124
  - 次要文本：#5F6368
  - 链接文本：#1A0DAB

### 字体规范
```css
--font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
--font-size-base: 14px;
--font-size-lg: 16px;
--font-size-xl: 20px;
--line-height-base: 1.5;
```

### 间距规范
```css
--spacing-xs: 4px;
--spacing-sm: 8px;
--spacing-md: 16px;
--spacing-lg: 24px;
--spacing-xl: 32px;
```

## 页面设计

### 首页 (app/page.tsx)
- 设计风格：极简主义，参考 Google 首页
- 布局：
  - Logo 居中显示
  - 搜索框居中，宽度自适应
  - 搜索按钮和工具栏位于搜索框下方

样式示例：
```css
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: var(--spacing-xl);
}

.logo {
  margin-bottom: var(--spacing-xl);
  height: 92px;
  width: auto;
}

.search-container {
  width: 100%;
  max-width: 584px;
  margin: 0 auto;
}

.search-box {
  width: 100%;
  height: 44px;
  padding: 0 var(--spacing-md);
  border: 1px solid #dfe1e5;
  border-radius: 24px;
  outline: none;
  font-size: var(--font-size-base);
  transition: all 0.3s;
  box-shadow: none;
}

.search-box:hover {
  box-shadow: 0 1px 6px rgba(32,33,36,.28);
  border-color: rgba(223,225,229,0);
}

.search-box:focus {
  box-shadow: 0 1px 6px rgba(32,33,36,.28);
  border-color: rgba(223,225,229,0);
}

.buttons {
  display: flex;
  justify-content: center;
  gap: var(--spacing-md);
  margin-top: var(--spacing-lg);
}

.button {
  background-color: #f8f9fa;
  border: 1px solid #f8f9fa;
  border-radius: 4px;
  color: #3c4043;
  font-size: var(--font-size-base);
  padding: 0 16px;
  height: 36px;
  cursor: pointer;
  text-align: center;
  user-select: none;
}

.button:hover {
  border: 1px solid #dadce0;
  box-shadow: 0 1px 1px rgba(0,0,0,.1);
}
```

### 搜索结果页面 (app/search/page.tsx)
- 设计风格：清晰的信息层级
- 布局：
  - 顶部固定导航栏，包含 Logo 和搜索框
  - 左侧可能包含筛选选项
  - 主体内容区展示搜索结果

样式示例：
```css
.header {
  position: sticky;
  top: 0;
  background: white;
  border-bottom: 1px solid #ebebeb;
  padding: var(--spacing-sm) var(--spacing-xl);
  display: flex;
  align-items: center;
  gap: var(--spacing-xl);
}

.header-logo {
  height: 30px;
  width: auto;
}

.search-results {
  padding: var(--spacing-lg) var(--spacing-xl);
  max-width: 652px;
  margin: 0 auto;
}

.result-item {
  margin-bottom: var(--spacing-xl);
}

.result-title {
  font-size: var(--font-size-lg);
  color: #1a0dab;
  text-decoration: none;
  line-height: 1.3;
}

.result-url {
  color: #006621;
  font-size: var(--font-size-base);
  margin: var(--spacing-xs) 0;
}

.result-snippet {
  color: #545454;
  font-size: var(--font-size-base);
  line-height: 1.58;
}
```

## 响应式设计

通过 Tailwind CSS 的断点系统实现响应式布局：

```css
/* 移动端 */
@media (max-width: 640px) {
  .search-container {
    padding: 0 var(--spacing-md);
  }
  
  .header {
    flex-direction: column;
    padding: var(--spacing-sm);
  }
}

/* 平板 */
@media (min-width: 641px) and (max-width: 1024px) {
  .search-container {
    max-width: 90%;
  }
}

/* 桌面端 */
@media (min-width: 1025px) {
  .search-container {
    max-width: 584px;
  }
}
```

## 核心组件

### SearchBox 组件
```typescript
// components/search/SearchBox.tsx
interface SearchBoxProps {
  initialValue?: string;
  onSearch: (query: string) => void;
}

const SearchBox: React.FC<SearchBoxProps> = ({ initialValue = '', onSearch }) => {
  // 实现搜索框逻辑
};
```

### SearchResult 组件
```typescript
// components/search/SearchResult.tsx
interface SearchResultProps {
  title: string;
  url: string;
  snippet: string;
}

const SearchResult: React.FC<SearchResultProps> = ({ title, url, snippet }) => {
  // 实现搜索结果展示
};
```

## 性能优化

1. 图片优化

* 使用 Next.js Image 组件
* 合适的图片格式和尺寸
* 懒加载处理

2. 代码分割

* 路由级别的代码分割
* 动态导入大型组件

3. 缓存策略

* 静态资源缓存
* API 响应缓存

4. 性能监控

* 使用 Web Vitals 监控核心性能指标
* 分析并优化关键渲染路径

## 开发规范

1. 组件开发

* 遵循 React 最佳实践
* 使用 TypeScript 类型声明
* 组件职责单一

1. 样式管理

* 使用 Tailwind CSS 工具类
* 避免内联样式
* 保持一致的命名规范

1. 状态管理

* 使用 React Context 或其他状态管理工具
* 合理划分状态层级

1. 错误处理

* 实现错误边界
* 友好的错误提示界面

## 辅助工具

1. 开发工具

* VSCode
* ESLint 配置
* Prettier 配置

1. 调试工具

* React Developer Tools
* Chrome DevTools

1. 性能分析

* Lighthouse
* Web Vitals
