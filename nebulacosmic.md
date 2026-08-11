# Resource Navigator

Resource Navigator is a high-performance, stateless technical resource aggregation and navigation system designed for developers, researchers, and IT professionals who need to maintain a curated collection of external references, documentation hubs, and specialized content repositories. The project addresses the fundamental challenge of managing and presenting large volumes of external URLs in a structured, maintainable, and rapidly accessible format, eliminating the friction associated with scattered bookmarks and unstructured reference lists.

Targeting system administrators, DevOps engineers, and technical team leads, Resource Navigator provides a lightweight, Markdown-driven cataloging solution that integrates seamlessly with existing documentation pipelines. It transforms raw URL collections into semantically organized navigation structures, complete with dependency resolution, environment requirement validation, and automated health checking for external endpoints. The platform is built for extensibility, allowing teams to customize categorization logic, apply access control rules, and generate static site outputs for offline distribution.

## 功能概览

- **Hierarchical Resource Classification** – Organizes URLs into multi-level taxonomies with tag-based filtering and full-text search across titles, descriptions, and metadata fields.

- **Automated Link Health Monitoring** – Performs periodic HEAD and GET requests to validate endpoint availability, automatically flagging broken or redirected links with timestamped status logs.

- **Markdown-Driven Configuration** – All resource definitions, categories, and metadata are stored in human-readable Markdown files, enabling version control integration and peer review workflows.

- **Static Site Generation Engine** – Produces fully self-contained HTML output with responsive design, suitable for deployment on any static hosting service or local file system.

- **Access Control and Visibility Rules** – Supports role-based visibility (public, team-only, restricted) with configurable override policies per category or individual resource entry.

- **Dependency and Compatibility Matrix** – Automatically parses and displays system requirements, browser compatibility, and API version dependencies for each listed external resource.

- **Custom Metadata Schemas** – Allows defining custom fields per resource type, such as API rate limits, authentication requirements, or geographic availability zones.

- **Audit Logging and Change Tracking** – Records every modification to the resource database, including who made the change and when, with optional webhook integration for external notification systems.

## 应用场景

- **Technical Documentation Portals** – Project maintainers use Resource Navigator to curate external reference links, API documentation sites, and community forum threads, ensuring that contributors can quickly locate authoritative sources without sifting through outdated bookmarks.

- **Enterprise Knowledge Bases** – Internal teams deploy the system to centralize links to internal dashboards, monitoring tools, logging interfaces, and runbook repositories, applying visibility rules to restrict sensitive URLs to authorized personnel only.

- **Academic Research Repositories** – Researchers compile collections of datasets, preprint servers, institutional repositories, and subject-specific databases, using the custom metadata feature to tag entries by discipline, publication date, or access restrictions.

- **DevOps Toolchain Registries** – Platform engineering teams maintain registries of CI/CD tools, container registries, monitoring endpoints, and infrastructure APIs, with health monitoring alerts that notify on-call staff when critical endpoints become unreachable.

- **Regional Content Categorization** – Organizations operating in multiple jurisdictions organize resources by geographical region, regulatory domain, or language group, leveraging the hierarchical classification to provide localized navigation views for different user segments.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/your-org/resource-navigator.git
cd resource-navigator

# Install dependencies using pip for Python-based reference implementation
pip install -r requirements.txt

# Initialize the default resource database from example configuration
python scripts/init_db.py --sample-data

# Run the static site generator to produce output in ./dist directory
python build.py --input ./resources --output ./dist --watch

# Start the local development server on port 8080
python -m http.server --directory ./dist 8080
```

For production deployment, refer to the deployment guide in the documentation section. The system supports Docker-based builds and can be integrated with GitHub Actions or GitLab CI for automated regeneration on every commit.

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 或更高 | 核心解释器，用于运行构建脚本和 CLI 工具 |
| Markdown Parser | 3.3.0+ | 用于解析资源配置文件，支持扩展语法 |
| Requests Library | 2.25.0+ | 处理 HTTP 健康检查请求，支持超时和重试策略 |
| PyYAML | 5.4.0+ | 可选，用于 YAML 格式的元数据补充（兼容模式） |
| Git | 2.20.0+ | 用于版本控制集成和变更历史追溯（生产环境推荐） |
| Docker Engine | 20.10.0+ | 可选容器化部署方案，包含完整运行环境 |
| Node.js | 14.x 或更高 | 仅前端开发模式需要，用于实时预览和热重载 |
| Nginx / Apache | 任意稳定版本 | 生产静态文件服务器，支持 gzip 压缩和缓存头配置 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | /docs/getting-started.md | 如何从零开始部署实例、定义第一个资源类别、添加初始 URL 条目 |
| 配置参考 | /docs/configuration.md | 所有配置文件结构、环境变量、命令行参数及自定义元数据 schema 定义 |
| 架构设计 | /docs/architecture.md | 系统组件图、数据流、扩展点设计及性能调优建议 |
| 运维手册 | /docs/operations.md | 健康检查调度策略、日志聚合、备份恢复及监控告警配置 |
| API 接口 | /docs/api.md | 提供 RESTful 风格的只读查询接口，供外部系统集成使用 |
| 迁移指南 | /docs/migration.md | 从旧版本或第三方书签系统导入数据的步骤及兼容性说明 |

## 资源列表

### 综合信息门户类别

- <code>shufuzipai.org.cn</code>
- <code>yazhouchuanmei.org.cn</code>

### 传媒与内容聚合类别

- <code>zhongwenzimuzhongchu.org.cn</code>
- <code>chunshuifuli.org.cn</code>

### 娱乐与兴趣社区类别

- <code>daxiangjiaojiu.org.cn</code>
- <code>langrenzonghewang.org.cn</code>
- <code>oumeirihandiyiye.org.cn</code>

### 精品内容与专项站点类别

- <code>xiangjiaojiujiujingpinririzaoyeyezao.org.cn</code>
- <code>zhongwenzaixianyiquerqu.org.cn</code>
- <code>yazhouwuyejuchang.org.cn</code>

## 项目结构

```
resource-navigator/
├── build.py                     # 主构建脚本，调用解析器和生成器
├── requirements.txt             # Python 依赖清单
├── Dockerfile                   # 容器化构建定义，基于 Alpine Linux
├── .env.example                 # 环境变量模板，包含健康检查间隔和缓存参数
├── resources/                   # 资源定义目录，所有 Markdown 配置存放于此
│   ├── categories/              # 类别定义，每文件定义一种分类层级
│   │   ├── tech.yaml            # 技术类别的层级规则和图标映射
│   │   ├── media.yaml           # 媒体类别的过滤标签和排序权重
│   │   └── regional.yaml        # 区域性类别的地理标签和时区关联
│   ├── entries/                 # 单个资源条目，每个 URL 对应一个 .md 文件
│   │   ├── shufuzipai.md        # 包含标题、描述、标签、健康检查阈值
│   │   ├── yazhouchuanmei.md    # 含自定义元数据和访问限制标记
│   │   └── ...                  # 其余条目遵循相同结构
│   └── schemas/                 # 自定义元数据 JSON Schema 定义
│       ├── default.json         # 全局默认字段验证规则
│       └── custom.json          # 针对特定类别的扩展字段
├── src/                         # 核心 Python 源码
│   ├── parser.py                # Markdown/YAML 解析器，生成中间抽象语法树
│   ├── validator.py             # 链接健康验证引擎，支持并发检查和重试
│   ├── generator.py             # 静态 HTML 生成器，使用 Jinja2 模板引擎
│   ├── watcher.py               # 文件系统监听器，用于开发模式自动重建
│   └── utils/                   # 工具函数集合
│       ├── http.py              # HTTP 客户端封装，包含超时和代理支持
│       ├── logger.py            # 结构化日志记录，支持 JSON 格式输出
│       └── cache.py             # LRU 缓存实现，减少重复验证请求
├── templates/                   # Jinja2 HTML 模板，控制输出样式和布局
│   ├── base.html                # 基础骨架，包含 Bootstrap 和自定义 CSS
│   ├── index.html               # 首页类别网格视图
│   ├── detail.html              # 单个资源详情页，显示所有元数据和状态
│   └── partials/                # 可复用的模板组件，如导航栏和页脚
├── static/                      # 静态资源文件，构建时复制到输出目录
│   ├── css/                     # 自定义样式表，采用响应式移动优先设计
│   ├── js/                      # 前端交互脚本，含搜索过滤和状态轮询
│   └── fonts/                   # 可选的图标字体和排版资源
├── tests/                       # 单元测试和集成测试套件，覆盖所有核心模块
│   ├── test_parser.py           # 解析器正确性测试，含边界条件
│   ├── test_validator.py        # 健康检查模拟测试，使用 mock 网络请求
│   └── fixtures/                # 测试数据样本，模拟真实资源配置
├── docs/                        # 完整项目文档，包含 API 参考和运维指南
│   ├── getting-started.md
│   ├── configuration.md
│   ├── architecture.md
│   ├── operations.md
│   ├── api.md
│   └── migration.md
└── scripts/                     # 辅助脚本，用于数据迁移和批量操作
    ├── init_db.py               # 初始化数据库文件或生成示例配置
    ├── import_bookmarks.py      # 从 HTML 书签导出文件批量导入
    └── health_check.py          # 独立运行的全面端点扫描器，输出 CSV 报告
```

## 贡献指南

1. 从 GitHub 仓库复刻项目并创建功能分支，分支命名遵循 `feature/` 或 `fix/` 前缀规范。确保本地开发环境满足安装要求表格中的所有依赖版本。

2. 在 `resources/entries/` 目录下添加或修改资源条目文件，严格遵守 Markdown 格式规范。每个条目必须包含 `title`、`url`、`description` 和 `tags` 字段。新增类别时需在 `resources/categories/` 中定义对应的 YAML 规则。

3. 执行本地构建验证：运行 `python build.py --strict` 进行完整构建，该命令会启用所有校验器并生成详细的构建日志。确保所有链接健康检查通过（允许配置重试次数）。

4. 编写或更新单元测试以覆盖所改动的代码或配置逻辑。测试覆盖率不得低于 85%。使用 `pytest` 运行完整测试套件，确保无回归错误。

5. 提交 Pull Request 至主仓库的 `main` 分支，PR 描述中应包含变更类型、影响范围及测试结果摘要。项目维护者将进行代码审查和配置一致性检查，通过后合并。

## 常见问题

**问：系统如何处理目标 URL 的变更或重定向？**

答：健康检查模块在每次构建时执行 HEAD 请求，并记录 HTTP 状态码。对于 301/302 重定向，系统会跟踪最终目标并更新内部记录，同时在日志中标记原始 URL 为重定向状态。管理员可以配置重定向跟踪的最大深度（默认 5 跳）。如果目标 URL 持续返回 4xx 或 5xx 状态，系统将在连续三次失败后将该条目标记为“异常”，并在生成 HTML 时高亮显示。管理员可通过运行 `scripts/health_check.py --report` 获取所有异常条目的汇总报告。

**问：是否支持多语言界面和资源描述？**

答：核心系统界面语言通过模板中的 i18n 机制支持，当前提供中文和英文两种语言包，可通过环境变量 `LANGUAGE` 切换。资源条目的描述字段支持在 Markdown 文件中使用 `description_zh` 和 `description_en` 双重字段，系统会根据当前界面语言自动选择合适的描述展示。若未提供特定语言版本，则回退到默认的 `description` 字段。

**问：如何备份和迁移现有的资源数据库到另一台服务器？**

答：由于所有资源配置均以纯文本 Markdown 文件存储，备份和迁移只需复制整个 `resources/` 目录及其子目录。若使用了可选的 SQLite 缓存数据库（用于加速频繁查询），则需额外备份 `cache.db` 文件。迁移到新服务器时，建议先执行 `python build.py --clean-cache` 重置缓存，然后使用 `python scripts/import_bookmarks.py --validate` 重新校验所有条目，确保新环境中的网络访问策略与旧环境一致。对于自动化部署，推荐使用 Docker 镜像并挂载配置目录卷，实现配置与运行环境的完全分离。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
