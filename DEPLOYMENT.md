# Cloudflare Pages 部署指南

## 🚀 部署步骤

### 1. 准备工作

1. **推送代码到GitHub**：
   ```bash
   git add .
   git commit -m "Initial blog setup"
   git push origin main
   ```

2. **获取Cloudflare API Token**：
   - 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
   - 进入 "My Profile" > "API Tokens"
   - 创建自定义token，权限包括：
     - Zone:Zone:Read
     - Zone:Page Rules:Edit
     - Account:Cloudflare Pages:Edit

### 2. Cloudflare Pages 设置

1. **创建Pages项目**：
   - 进入 Cloudflare Dashboard > Pages
   - 点击 "Create a project"
   - 连接你的GitHub仓库
   - 选择你的博客仓库

2. **构建设置**：
   ```
   Framework preset: Jekyll
   Build command: npm run build && bundle exec jekyll build
   Build output directory: _site
   Root directory: (留空)
   ```

3. **环境变量**：
   ```
   RUBY_VERSION=3.2.0
   NODE_VERSION=18
   ```

### 3. GitHub Secrets 配置

在你的GitHub仓库设置中添加以下Secrets：

```
CLOUDFLARE_API_TOKEN=你的API Token
CLOUDFLARE_ACCOUNT_ID=你的Account ID
```

### 4. 自定义域名（可选）

1. 在Cloudflare Pages项目中点击 "Custom domains"
2. 添加你的域名
3. 按照提示配置DNS记录

## 🔧 优化建议

### 性能优化
- 启用Cloudflare的Auto Minify
- 使用Cloudflare Images优化图片
- 启用Brotli压缩

### SEO优化
- 配置Google Analytics
- 提交sitemap到Google Search Console
- 设置适当的缓存策略

### 安全设置
- 启用HTTPS（自动）
- 配置安全头部
- 设置适当的CSP策略

## 📊 监控和分析

1. **Cloudflare Analytics**：
   - 在 `_config.yml` 中配置 Cloudflare Web Analytics
   
2. **Google Analytics**：
   - 获取GA4跟踪ID
   - 在配置文件中添加

3. **性能监控**：
   - 使用Cloudflare的Real User Monitoring
   - 定期检查Core Web Vitals

## 🐛 常见问题

### 构建失败
- 检查Ruby和Node.js版本
- 确认所有依赖都在Gemfile和package.json中

### 样式问题
- 检查baseurl配置
- 确认CDN设置正确

### 评论系统
- 确保GitHub仓库开启Discussions
- 正确配置Giscus设置 