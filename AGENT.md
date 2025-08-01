# AGENT.md

本文件为AI助手提供关于Sink项目的指导。

## 项目概述

Sink是一个使用Nuxt 3和Cloudflare Workers构建的URL缩短服务。它提供分析、实时跟踪和现代化的Web界面。

## 核心技术

- **前端**: Nuxt 3, Vue 3, TypeScript, Tailwind CSS, shadcn/ui
- **后端**: Cloudflare Workers, H3 (Nitro)
- **数据库**: Cloudflare KV
- **分析**: Cloudflare Analytics Engine
- **部署**: Cloudflare Pages/Workers

## 项目结构

```txt
Sink/
├── app/                     # Nuxt 3应用程序
│   ├── components/          # Vue组件
│   ├── pages/              # 基于文件的路由
│   ├── layouts/            # 布局组件
│   ├── utils/              # 工具函数
│   └── middleware/         # 路由中间件
├── server/                  # 服务器端API
│   ├── api/                # API端点
│   ├── middleware/         # 服务器中间件
│   └── utils/              # 服务器工具
├── public/                 # 静态资源
├── schemas/                # TypeScript模式
├── tests/                  # 测试文件
└── docs/                   # 文档
```

## 开发命令

- `pnpm dev` - 启动开发服务器
- `pnpm build` - 构建生产版本
- `pnpm preview` - 预览生产构建
- `pnpm test` - 运行测试
- `pnpm lint` - 运行ESLint

## 主要规范

### 代码风格

- 所有新代码使用TypeScript
- 遵循Vue 3 Composition API模式
- 组件名称使用PascalCase
- 变量和函数使用camelCase
- CSS类使用kebab-case

### API结构

- RESTful端点在`/server/api/`
- 在`/schemas/`中使用Zod进行模式验证
- 实现适当的错误处理
- 使用Cloudflare环境变量进行配置

### 数据库

- 使用Cloudflare KV

### 测试

- 使用Vitest进行单元测试
- 测试文件应与源文件共同位置
- 使用`/tests/utils.ts`中的现有测试工具

## 环境变量

需要了解的关键环境变量：

- `NUXT_CF_ACCOUNT_ID` - Cloudflare账户ID
- `NUXT_CF_API_TOKEN` - Cloudflare API令牌
- `NUXT_DATASET` - Analytics引擎ID
- `NUXT_SITE_TOKEN` - 站点管理令牌

## 常见任务

### 添加新的API端点

1. 在`/server/api/`中创建具有适当HTTP方法的文件
2. 在`/schemas/`中添加Zod模式验证
3. 在`/tests/api/`中添加测试
4. 如需要，更新文档

### 添加新组件

1. 使用`/app/components/ui/`中的现有UI组件
2. 遵循已建立的组件模式
3. 为props添加TypeScript接口
4. 如适用，考虑添加到storybook

## 安全指南

- 永远不要提交密钥或API密钥
- 使用环境变量进行敏感配置
- 使用Zod模式验证所有用户输入
- 在API端点实施速率限制
- 遵循OWASP的Web安全指南

## 性能考虑

- 在适当的地方使用Cloudflare的边缘缓存
- 通过使用动态导入最小化打包大小
- 优化图片和资源
- 使用现有分析进行监控

## 故障排除

- 查看Cloudflare仪表板获取worker日志
- 使用`wrangler tail`获取实时日志
- 验证环境变量是否正确设置

## 部署

- 预发布：推送到`main`分支时自动进行
- 生产：通过Cloudflare仪表板手动触发
- 使用`wrangler deploy`进行手动部署
