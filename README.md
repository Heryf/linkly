# Simple-Navigation-Station
个人使用，AI编写，小白常用软件收录

# 简约导航网站 - 开发文档

## 📋 项目简介
极简导航网站，支持本地存储管理，界面美观，兼容IE浏览器。

---

## ✨ 核心功能

### 用户端
- **搜索框**：支持自定义搜索引擎和宽度
- **分类卡片**：网格布局（3-8列可调）
- **链接管理**：图标自动识别、描述信息
- **响应式**：适配手机/平板/电脑

### 管理端
- **管理员登录**：密码保护（默认：admin）
- **编辑模式**：
  - 添加/删除/重命名分类
  - 添加/编辑/删除链接
  - 智能识别网站图标（favicon.ico）
- **全局设置**：
  - 布局调整（列数、图标大小）
  - **自定义壁纸**（上传本地或URL）
  - 网站信息配置
  - 数据导入导出（JSON）

---

## 🎨 设计要点

### 视觉风格
- **毛玻璃效果**：`backdrop-filter: blur(16px)`
- **配色**：主色 #409EFF（蓝）
- **默认壁纸**：优美风景图（Unsplash）

### 交互设计
- **右下角悬浮菜单**：
  - 未登录：显示"管理员登录"
  - 已登录：全局设置/编辑模式/退出
  - 点击展开，再次点击收起

- **编辑按钮**：
  - 分类右上角：重命名/删除
  - 链接右上角：蓝色圆形编辑按钮
  - 底部虚线框：添加新分类

---

## 💻 技术实现

### 技术栈
- HTML5 + CSS3 (Flexbox)
- JavaScript (ES5 - 兼容IE)
- FontAwesome 4.7
- LocalStorage 存储

### 核心数据结构
```javascript
var appData = {
    password: 'admin',
    bgUrl: '壁纸URL',
    layout: { cols: 5, iconSize: 32 },
    search: { engine: '百度URL', width: 500 },
    categories: [
        {
            title: '分类名',
            links: [
                { name: '网站名', url: '...', icon: '...', desc: '...' }
            ]
        }
    ]
};
```

### 关键功能
1. **智能识别图标**：
   ```javascript
   var faviconUrl = protocol + '//' + hostname + '/favicon.ico';
   ```

2. **壁纸上传**：
   - FileReader 转 Base64
   - 限制 2MB
   - 保存到 LocalStorage

3. **菜单切换**：
   - 使用 classList.add/remove('show')
   - 避免默认 display 设置

---

## 🐛 已知问题与解决

| 问题 | 解决方案 |
|------|----------|
| 点击编辑按钮同时跳转链接 | `event.stopPropagation(); event.preventDefault();` |
| 菜单点击后立即消失 | 使用 class 控制，操作后手动关闭 |
| 壁纸占用存储过大 | 限制2MB，建议使用外部URL |

---

## 📝 使用指南

### 首次使用
1. 打开 `index.html`
2. 点击右下角按钮 → 管理员登录（密码：admin）
3. 开启"编辑模式"

### 添加链接
1. 点击分类右上角"➕ 添加链接"
2. 输入网址 → 点击"识别"自动获取图标
3. 填写名称和描述 → 保存

### 更换壁纸
1. 全局设置 → 背景壁纸
2. 上传本地图片 或 输入URL
3. 预览 → 保存（所有访问者可见）

### 数据备份
- **导出**：下载 JSON 文件
- **导入**：上传 JSON 文件（覆盖当前数据）

---

## 🚀 优化建议

### 短期优化
- [ ] 支持多个搜索引擎切换
- [ ] 链接拖拽排序
- [ ] 操作提示（Toast）
- [ ] 暗黑模式

### 长期优化
- [ ] 云端同步（需后端）
- [ ] 访问统计
- [ ] 链接失效检测
- [ ] IndexedDB 代替 LocalStorage

---

## 📦 部署方式

### 本地使用
直接双击 `index.html`

### GitHub Pages
1. 创建仓库并上传文件
2. 启用 GitHub Pages
3. 访问 `https://用户名.github.io/仓库名`

### Vercel/Netlify
连接 GitHub 仓库自动部署

---

## 🔧 兼容性

- ✅ IE10+
- ✅ Chrome/Firefox/Edge
- ✅ 手机浏览器
- ✅ 360/UC等精简浏览器

---

**版本：v1.0.0** | **许可：MIT**
