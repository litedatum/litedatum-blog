# 🚀 发布前检查清单

## ✅ 必须完成的配置

### 1. 基础配置 (_config.yml)
- [ ] `url`: 修改为实际域名
- [ ] `github.username`: 填入GitHub用户名
- [ ] `social.name`: 填入真实姓名
- [ ] `social.email`: 填入联系邮箱
- [ ] `timezone`: 设置为 `America/New_York`
- [ ] `social.links`: 更新GitHub链接

### 2. 评论系统 (Giscus)
- [ ] 启用GitHub Discussions
- [ ] 访问 giscus.app 获取配置
- [ ] 填入 `repo_id` 和 `category_id`

### 3. GitHub Actions配置
- [ ] 修改 `.github/workflows/pages-deploy.yml` 中的 `projectName`
- [ ] 设置GitHub Secrets:
  - `CLOUDFLARE_API_TOKEN`
  - `CLOUDFLARE_ACCOUNT_ID`

### 4. 博客文章
- [ ] 所有文章的 `author` 字段改为真实姓名

## 🔧 推荐配置

### 5. 网站分析
- [ ] Cloudflare Web Analytics ID (推荐)
- [ ] 或者 Google Analytics 4 ID

### 6. SEO优化
- [ ] Google Search Console验证码
- [ ] 提交sitemap到搜索引擎

## 🧪 发布前测试

### 7. 本地测试
```bash
# 清理并重新构建
bundle exec jekyll clean
npm run build
bundle exec jekyll build

# 本地预览
bundle exec jekyll serve
```

### 8. 功能检查
- [ ] 网站能正常加载
- [ ] 所有页面链接正常
- [ ] 搜索功能工作
- [ ] 主题切换正常
- [ ] 移动端显示正常

### 9. 内容检查
- [ ] 所有文章显示正常
- [ ] 代码高亮正确
- [ ] 图片能正常显示
- [ ] meta标签信息正确

## 🌐 Cloudflare部署准备

### 10. Cloudflare Pages设置
- [ ] 创建Cloudflare Pages项目
- [ ] 项目名与GitHub Actions配置一致
- [ ] 构建设置：
  - Framework preset: Jekyll
  - Build command: `npm run build && bundle exec jekyll build`
  - Build output directory: `_site`

### 11. 环境变量 (Cloudflare)
- [ ] `RUBY_VERSION=3.2.0`
- [ ] `NODE_VERSION=18`

### 12. 域名设置 (可选)
- [ ] 添加自定义域名
- [ ] 配置DNS记录
- [ ] 启用HTTPS

## 🔒 安全检查

### 13. 敏感信息检查
- [ ] 没有硬编码的API密钥
- [ ] 没有暴露敏感配置
- [ ] GitHub Secrets正确设置

### 14. 权限检查
- [ ] 仓库设置正确
- [ ] GitHub Actions权限配置
- [ ] Cloudflare API Token权限最小化

## 📊 监控准备

### 15. 网站监控
- [ ] 设置Cloudflare Web Analytics
- [ ] 配置Uptime监控
- [ ] 设置错误报告

### 16. 性能优化
- [ ] 启用Cloudflare CDN
- [ ] 开启图片优化
- [ ] 启用Brotli压缩

## 🎯 发布后验证

### 17. 功能验证
- [ ] 网站在多个浏览器中正常显示
- [ ] 评论系统工作正常
- [ ] 搜索引擎能正常抓取
- [ ] 社交媒体分享功能正常

### 18. 性能验证
- [ ] 页面加载速度 < 3秒
- [ ] Core Web Vitals指标良好
- [ ] 移动端性能良好

---

## 🔧 快速配置脚本

创建你的配置文件：

1. 复制 `_config_template.yml` 为 `_config.yml`
2. 填入你的实际信息
3. 根据 `GISCUS_SETUP.md` 配置评论系统
4. 运行本地测试
5. 推送到GitHub触发部署

**记住**: 完成所有✅必须项后才能发布！ 