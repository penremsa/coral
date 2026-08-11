# TechNav Resource Aggregator

TechNav is a specialized technical resource navigation and aggregation system designed for developers, researchers, and IT professionals who need to efficiently organize, categorize, and access distributed online resources across multiple domains. The project addresses the common challenge of managing disparate reference materials, documentation sites, and data sources by providing a unified indexing layer with version-aware tracking capabilities.

Targeting system architects, DevOps engineers, and technical documentation maintainers, TechNav solves the problem of resource drift and link rot by implementing a structured metadata framework that preserves original resource identifiers while enabling semantic search, dependency mapping, and availability monitoring. The system operates as a static site generator with dynamic health-check middleware, ensuring that all indexed resources remain accessible and correctly categorized over time.

## 功能概览

- **Resource Indexing Engine** - Automated crawling and metadata extraction from user-submitted URLs with support for bulk import operations and duplicate detection.

- **Category-Based Taxonomy System** - Dynamic classification of resources into user-defined taxonomies with support for multi-tagging and hierarchical category trees.

- **Health Monitoring Dashboard** - Periodic availability checking for all indexed resources with latency tracking, SSL certificate validation, and response code logging.

- **Versioned Snapshot Management** - Historical record keeping for resource state changes, including content hash comparison and diff generation for HTML-based resources.

- **Search and Filter Pipeline** - Full-text search across resource titles, descriptions, and custom metadata fields with faceted filtering by category, status, and update timestamp.

- **Export and Integration APIs** - RESTful endpoints for resource list retrieval in JSON, CSV, and XML formats, with webhook support for external system integration.

- **Access Control and Team Collaboration** - Role-based permission system allowing multiple maintainers to manage resource collections with audit logging for all modifications.

## 应用场景

- **Technical Documentation Consolidation** - A development team maintaining multiple microservices can use TechNav to aggregate API documentation, deployment guides, and internal wikis from various subdomains into a single searchable interface, reducing the time spent hunting for correct reference materials.

- **Competitive Intelligence Monitoring** - Market researchers tracking financial or sports data feeds can configure TechNav to monitor specific URL endpoints for content changes, receiving automated alerts when underlying data structures or presentation formats are modified.

- **Academic Reference Management** - Researchers compiling bibliographic resources and online datasets can leverage the system's metadata annotation features to tag resources by project, research domain, or data type, facilitating collaborative literature reviews.

- **Infrastructure Asset Tracking** - Platform engineering teams can maintain an inventory of internal tooling dashboards, monitoring endpoints, and logging interfaces, with automated health checks that proactively notify teams of service degradations.

## 快速开始

```bash
# Step 1: Clone the repository
git clone https://github.com/technav/technav-core.git
cd technav-core

# Step 2: Install dependencies using Poetry
poetry install --no-dev
poetry build

# Step 3: Configure environment variables
cp .env.example .env
# Edit .env with your database connection string and admin credentials

# Step 4: Initialize database schema
alembic upgrade head

# Step 5: Import sample resource list
python scripts/import_urls.py --source resources.txt

# Step 6: Start the development server
python -m technav.server --host 0.0.0.0 --port 8080

# For production deployment with Gunicorn
gunicorn -w 4 -b 0.0.0.0:8080 technav.wsgi:application
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|----------|------|
| Python | 3.10 - 3.12 | 核心运行时环境，使用 asyncio 事件循环处理并发任务 |
| PostgreSQL | 15.x 及以上 | 主数据存储，使用 JSONB 类型存储灵活的资源元数据 |
| Redis | 7.0.x 及以上 | 缓存层和分布式锁管理，用于健康检查任务的去重和状态暂存 |
| Poetry | 1.5.x 及以上 | Python 依赖管理和打包工具，维护虚拟环境隔离 |
| Node.js | 20.x LTS | 前端资源构建工具链依赖，仅开发环境需要 |
| Nginx | 1.24.x 及以上 | 生产环境反向代理和静态资源服务（推荐配置） |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|------|----------|------------|
| 用户指南 | <code>/docs/user-guide/</code> | 如何使用资源索引、搜索过滤、个人收藏和标签管理功能 |
| 管理员手册 | <code>/docs/admin-handbook/</code> | 如何执行批量导入、配置健康检查策略、管理用户权限和审计日志 |
| API 参考 | <code>/docs/api-reference/</code> | 各 REST 端点的请求/响应格式、认证方式、分页参数和错误码定义 |
| 部署运维 | <code>/docs/deployment/</code> | 生产环境架构设计、高可用配置、备份恢复策略和性能调优参数 |
| 开发贡献 | <code>/docs/contributing/</code> | 代码风格规范、测试框架使用、提交信息格式和 PR 审核流程 |
| 架构设计 | <code>/docs/architecture/</code> | 系统模块划分、数据流设计、扩展点定义和第三方集成模式 |

## 资源列表

本批次收录的资源（第 239/455 批）覆盖了特定主题领域的多个数据源节点，所有条目均保持原始格式原样存档。

体育数据类

<code>bifenwangc.org.cn</code>

<code>500bifena.org.cn</code>

<code>500bifenb.org.cn</code>

<code>500bifenc.org.cn</code>

赛事统计类

<code>jiebaobifena.org.cn</code>

<code>jiebaobifenb.org.cn</code>

<code>jiebaobifenc.org.cn</code>

实时比分类

<code>zuqiujishibifend.org.cn</code>

<code>zuqiujishibifene.org.cn</code>

<code>zuqiujishibifenf.org.cn</code>

## 项目结构

```
technav-core/
├── technav/                          # 主应用包目录
│   ├── __init__.py                   # 包初始化，暴露核心工厂函数
│   ├── server.py                     # ASGI 应用入口，启动配置和中间件栈
│   ├── settings.py                   # 分层配置管理（开发/测试/生产环境）
│   ├── models/                       # SQLAlchemy ORM 实体定义
│   │   ├── resource.py               # Resource 实体：URL、标题、描述、分类
│   │   ├── category.py               # 分类树实体，支持无限级嵌套
│   │   ├── health_log.py             # 健康检查历史记录实体
│   │   └── user.py                   # 用户账户和角色权限实体
│   ├── services/                     # 业务逻辑层
│   │   ├── indexer.py                # 资源索引服务：爬取、解析、元数据提取
│   │   ├── health_checker.py         # 异步健康检查调度器
│   │   ├── search.py                 # 全文检索引擎和过滤查询构建器
│   │   └── exporter.py               # 资源导出服务（JSON/CSV/XML 格式）
│   ├── api/                          # RESTful API 路由层
│   │   ├── v1/                       # API 版本 1 路由注册
│   │   │   ├── resources.py          # CRUD 端点、批量导入、搜索
│   │   │   ├── categories.py         # 分类管理端点
│   │   │   └── health.py             # 健康检查状态和手动触发端点
│   │   └── middleware.py             # 认证、日志记录和错误处理中间件
│   ├── core/                         # 核心工具库和基础设施
│   │   ├── database.py               # 数据库连接池和会话管理
│   │   ├── cache.py                  # Redis 缓存抽象层
│   │   ├── http_client.py            # 异步 HTTP 客户端（超时/重试/代理）
│   │   └── validators.py             # URL 格式验证和规范化工具
│   ├── templates/                    # 服务端渲染模板（管理后台）
│   │   ├── dashboard.html            # 监控面板模板
│   │   └── resource_list.html        # 资源列表展示模板
│   └── static/                       # 前端静态资源（CSS/JS/图标）
├── scripts/                          # 运维和开发辅助脚本
│   ├── import_urls.py                # 批量导入 URL 数据的命令行工具
│   ├── export_snapshot.py            # 导出当前全部资源快照
│   └── migration_helper.py           # 数据库迁移辅助脚本
├── tests/                            # 单元测试和集成测试
│   ├── unit/                         # 单元测试（服务层和工具函数）
│   ├── integration/                  # 集成测试（API 端点和数据库交互）
│   └── conftest.py                   # Pytest 共享 fixture 配置
├── docs/                             # 完整项目文档（见文档导航表格）
├── .env.example                      # 环境变量配置模板
├── Dockerfile                        # 多阶段构建 Docker 镜像文件
├── docker-compose.yml                # 本地开发环境编排（PostgreSQL + Redis）
├── pyproject.toml                    # Poetry 依赖声明和项目元数据
├── alembic.ini                       # 数据库迁移工具配置
├── nginx.conf                        # 生产环境 Nginx 参考配置
└── README.md                         # 本文档
```

## 贡献指南

1.  **Issue 跟踪与讨论**
    在提交任何代码变更之前，请先在 GitHub Issues 中查找是否存在相关的讨论或已报告的问题。若无现成 issue，请新建一个，清晰描述您希望解决的问题或希望增加的功能特性，并等待项目维护者的确认和反馈。

2.  **分支管理与开发流程**
    从 <code>main</code> 分支派生一个新的功能分支，命名格式为 <code>feature/简短描述</code> 或 <code>fix/问题编号</code>。所有开发工作在此分支进行，确保每次提交均通过单元测试和代码风格检查。

3.  **代码规范与测试要求**
    遵循 PEP 8 代码风格，使用 Black 和 isort 进行自动格式化。新增功能或修复必须附带对应的单元测试，测试覆盖率不得低于 85%。运行 <code>pytest</code> 命令确保全部测试通过后方可提交。

4.  **提交信息与拉取请求**
    提交信息采用约定式提交格式：<code>type(scope): subject</code>，例如 <code>feat(indexer): add retry mechanism for failed crawls</code>。完成开发后，向 <code>main</code> 分支发起拉取请求，并在 PR 描述中引用相关的 issue 编号，简述实现方案和测试结果。

5.  **文档同步更新**
    任何涉及用户界面、API 行为或配置方式的变更，必须同步更新 <code>/docs/</code> 目录下的对应文档文件。文档使用 Markdown 格式编写，确保示例代码可执行且参数说明准确无误。

## 常见问题

**Q: 系统如何处理目标资源不可访问或响应超时的情况？**

健康检查服务采用指数退避重试策略，首次失败后分别在 5 秒、15 秒、45 秒后进行三次重试。若全部重试均失败，资源状态标记为 <code>unreachable</code>，并在管理面板中高亮显示。系统同时记录失败原因（如 DNS 解析失败、连接超时、SSL 证书错误、HTTP 状态码异常），便于运维人员排查。用户可手动触发即时检查以验证恢复状态。

**Q: 如何导入包含数千个 URL 的批量数据？**

推荐使用 <code>scripts/import_urls.py</code> 脚本，支持从纯文本文件（每行一个 URL）、CSV 文件（需包含 <code>url</code> 和 <code>title</code> 列）或 JSON 数组格式导入。对于大规模导入（超过 5000 条），建议启用 <code>--bulk</code> 模式，该模式使用 PostgreSQL 的 <code>COPY</code> 命令进行批量插入，性能提升约 20 倍。导入完成后系统会自动触发一次轻量级的元数据补全扫描。

**Q: 前端界面是否支持自定义品牌标识和主题颜色？**

是的。系统在 <code>technav/static/css/</code> 目录下提供了 <code>_variables.css</code> 文件，其中定义了全部 CSS 自定义属性（颜色、字体、间距、边框半径）。管理员可修改此文件或通过管理后台的“外观设置”页面在线调整主色、强调色和导航栏样式，无需重新构建前端资源。所有自定义配置存储在数据库的 <code>site_config</code> 表中，并缓存在 Redis 中以减少读取开销。

## 许可证

MIT License

Copyright (c) 2026 TechNav Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
