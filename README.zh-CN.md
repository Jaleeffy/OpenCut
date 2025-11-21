<table width="100%">
  <tr>
    <td align="left" width="120">
      <img src="apps/web/public/logo.png" alt="OpenCut Logo" width="100" />
    </td>
    <td align="right">
      <h1>OpenCut</span></h1>
      <h3 style="margin-top: -10px;">免费、开源的视频编辑器，支持网页、桌面和移动端</h3>
    </td>
  </tr>
</table>

[English](README.md) | 简体中文

## 为什么选择 OpenCut？

- **隐私保护**：您的视频始终保存在本地设备上
- **功能免费**：CapCut 的基础功能现在都需要付费，我们提供免费替代方案
- **简单易用**：用户需要易于使用的编辑器 - CapCut 证明了这一点

## 功能特性

- 基于时间轴的编辑
- 多轨道支持
- 实时预览
- 无水印、无订阅
- 分析服务由 [Databuddy](https://www.databuddy.cc?utm_source=opencut) 提供，100% 匿名且无侵入性
- 博客由 [Marble](https://marblecms.com?utm_source=opencut) 提供支持，无头 CMS

## 项目结构

- `apps/web/` – 主要的 Next.js Web 应用
- `src/components/` – UI 和编辑器组件
- `src/hooks/` – 自定义 React Hooks
- `src/lib/` – 工具函数和 API 逻辑
- `src/stores/` – 状态管理（Zustand 等）
- `src/types/` – TypeScript 类型定义

## 快速开始

### 前置要求

在开始之前，请确保您的系统已安装以下软件：

- [Node.js](https://nodejs.org/en/)（v18 或更高版本）
- [Bun](https://bun.sh/docs/installation)
  （`npm` 的替代方案）
- [Docker](https://docs.docker.com/get-docker/) 和 [Docker Compose](https://docs.docker.com/compose/install/)

> **注意：** Docker 是可选的，但对于运行本地数据库和 Redis 服务是必需的。如果您只是运行前端或想为前端功能做贡献，可以跳过 Docker 设置。如果您已经按照下面 [设置](#设置) 中的步骤操作，就可以开始了！

### 设置

1. Fork 本仓库
2. 将您的 fork 克隆到本地
3. 进入 web 应用目录：`cd apps/web`
4. 复制 `.env.example` 为 `.env.local`：

   ```bash
   # Unix/Linux/Mac
   cp .env.example .env.local

   # Windows 命令提示符
   copy .env.example .env.local

   # Windows PowerShell
   Copy-Item .env.example .env.local
   ```

5. 安装依赖：`bun install`
6. 启动开发服务器：`bun dev`

## 开发环境设置

### 本地开发

1. 启动数据库和 Redis 服务：

   ```bash
   # 从项目根目录
   docker-compose up -d
   ```

2. 进入 web 应用目录：

   ```bash
   cd apps/web
   ```

3. 复制 `.env.example` 为 `.env.local`：

   ```bash
   # Unix/Linux/Mac
   cp .env.example .env.local

   # Windows 命令提示符
   copy .env.example .env.local

   # Windows PowerShell
   Copy-Item .env.example .env.local
   ```

4. 在 `.env.local` 中配置必需的环境变量：

   **必需变量：**

   ```bash
   # 数据库（与 docker-compose.yaml 配置一致）
   DATABASE_URL="postgresql://opencut:opencutthegoat@localhost:5432/opencut"

   # 为 Better Auth 生成安全密钥
   BETTER_AUTH_SECRET="your-generated-secret-here"
   BETTER_AUTH_URL="http://localhost:3000"

   # Redis（与 docker-compose.yaml 配置一致）
   UPSTASH_REDIS_REST_URL="http://localhost:8079"
   UPSTASH_REDIS_REST_TOKEN="example_token"

   # Marble 博客
   MARBLE_WORKSPACE_KEY=cm6ytuq9x0000i803v0isidst # 示例组织密钥
   NEXT_PUBLIC_MARBLE_API_URL=https://api.marblecms.com

   # 开发环境
   NODE_ENV="development"
   ```

   **生成 BETTER_AUTH_SECRET：**

   ```bash
   # Unix/Linux/Mac
   openssl rand -base64 32

   # Windows PowerShell（简单方法）
   [System.Web.Security.Membership]::GeneratePassword(32, 0)

   # 跨平台（使用 Node.js）
   node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"

   # 或使用在线生成器：https://generate-secret.vercel.app/32
   ```

5. 运行数据库迁移：`bun run db:migrate`（在 apps/web 目录内）
6. 启动开发服务器：`bun run dev`（在 apps/web 目录内）

应用程序将在 [http://localhost:3000](http://localhost:3000) 上运行。

## 贡献指南

我们欢迎贡献！虽然我们正在积极开发和重构某些区域，但仍有很多有效贡献的机会。

**🎯 重点领域：** 时间轴功能、项目管理、性能优化、bug 修复以及预览面板之外的 UI 改进。

**⚠️ 暂时避免：** 预览面板增强功能（字体、贴纸、效果）和导出功能 - 我们正在使用新的二进制渲染方法重构这些功能。

查看我们的 [贡献指南](.github/CONTRIBUTING.md) 了解详细的设置说明、开发指南和完整的重点领域指导。

**贡献者快速入门：**

- Fork 仓库并克隆到本地
- 按照 CONTRIBUTING.md 中的设置说明操作
- 创建功能分支并提交 PR

## 赞助商

感谢 [Vercel](https://vercel.com?utm_source=github-opencut&utm_campaign=oss) 对开源软件的支持。

<a href="https://vercel.com/oss">
  <img alt="Vercel OSS Program" src="https://vercel.com/oss/program-badge.svg" />
</a>

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FOpenCut-app%2FOpenCut&project-name=opencut&repository-name=opencut)

## 许可证

[MIT LICENSE](LICENSE)

---

![Star History Chart](https://api.star-history.com/svg?repos=opencut-app/opencut&type=Date)
