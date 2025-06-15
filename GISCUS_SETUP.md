# Giscus评论系统配置指南

Giscus是基于GitHub Discussions的评论系统，免费且无需额外服务器。

## 步骤1：启用GitHub Discussions

1. 进入你的GitHub仓库
2. 点击 **Settings** 标签
3. 向下滚动到 **Features** 区域
4. 勾选 **Discussions** 选项

## 步骤2：获取Giscus配置

1. 访问 [https://giscus.app](https://giscus.app)
2. 在 **Repository** 字段填入：`你的用户名/你的仓库名`
   - 例如：`johnsmith/my-blog`
3. 选择 **Discussion Category**：推荐选择 **General**
4. 其他设置保持默认

## 步骤3：复制生成的配置

网站会生成类似这样的配置：

```yaml
giscus:
  repo: johnsmith/my-blog
  repo_id: R_kgDOH1234567  # 你的实际ID
  category: General
  category_id: DIC_kwDOH1234567  # 你的实际ID
```

## 步骤4：更新_config.yml

将获取的配置填入你的`_config.yml`文件：

```yaml
comments:
  provider: giscus
  giscus:
    repo: 你的用户名/你的仓库名
    repo_id: "从giscus.app获取的ID"
    category: General
    category_id: "从giscus.app获取的ID"
    mapping: pathname
    strict: 0
    input_position: bottom
    lang: en
    reactions_enabled: 1
```

## 故障排除

如果评论系统不显示：

1. 确认仓库是公开的
2. 确认已安装Giscus GitHub App
3. 确认Discussions功能已启用
4. 检查repo_id和category_id是否正确

## 安全说明

- Giscus使用GitHub OAuth，访客需要GitHub账号才能评论
- 所有评论数据存储在GitHub Discussions中
- 你可以在GitHub仓库的Discussions标签中管理评论 