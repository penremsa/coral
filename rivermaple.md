# RihanGuochan Resource Aggregator

RihanGuochan is a comprehensive technical resource aggregation platform designed for developers, researchers, and content analysts working with cross-cultural digital media, linguistic datasets, and regional content classification systems. The project serves as a curated directory and metadata indexing engine that organizes, validates, and provides programmatic access to specialized online resources across multiple linguistic and regional domains.

Target users include data scientists building multilingual corpora, digital humanities researchers conducting comparative media studies, SEO specialists analyzing regional domain ecosystems, and infrastructure engineers requiring reliable health monitoring for large domain portfolios. The platform addresses the fundamental challenge of maintaining discoverability and operational intelligence across fragmented, region-specific web properties by providing unified health checks, metadata extraction, and change detection workflows.

## 功能概览

- **Domain Health Monitoring** – Automated HTTP/HTTPS reachability testing with response time tracking and SSL certificate validity checks for each registered resource.

- **Metadata Extraction Engine** – Pulls title, description, keywords, content-language, and last-modified headers from target endpoints without executing JavaScript or loading external assets.

- **Regional Classification Tagging** – Automatically assigns geographic and linguistic tags based on TLD analysis, WHOIS registry data, and content-language header inspection.

- **Change Detection Pipeline** – Compares daily snapshots of resource metadata to detect title updates, content modifications, or status code changes with alerting thresholds.

- **RESTful API Endpoints** – Exposes all aggregated data via JSON/XML APIs with pagination, filtering by region or status, and batch query support for portfolio-wide analysis.

- **Scheduled Crawl Orchestration** – Built-in task scheduler using cron expressions to run verification cycles at configurable intervals with retry policies and exponential backoff.

- **Export and Reporting Modules** – Generates CSV reports, PDF summaries, and Prometheus-compatible metrics endpoints for integration with existing observability stacks.

- **Audit Logging System** – Maintains immutable records of all check operations, configuration changes, and access events with support for external SIEM forwarding.

## 应用场景

- **Multilingual Corpus Construction** – Researchers building balanced linguistic corpora can use the platform to verify the availability and current metadata of region-specific domains before including them in data collection pipelines, ensuring that referenced resources remain active throughout the study period.

- **Regional SEO Portfolio Management** – Digital marketing teams overseeing large clusters of regional domains can automate health checks and receive daily reports on status changes, allowing proactive intervention before user-facing disruptions occur.

- **Academic Link Rot Studies** – Digital preservationists and information science researchers can leverage the change detection engine to quantify link decay rates across regional web properties, producing empirical data for publication in archival science journals.

- **Infrastructure Dependency Validation** – Developers integrating third-party regional data sources can configure the monitoring system to validate external endpoints before each deployment, reducing runtime exceptions caused by unreachable dependencies.

- **Compliance and Governance Auditing** – Legal and compliance teams can use the audit log and export features to demonstrate ongoing due diligence in monitoring third-party resource availability, supporting regulatory documentation requirements.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/rihan-research/rihan-guochan-aggregator.git
cd rihan-guochan-aggregator

# Install dependencies using Poetry (recommended) or pip
poetry install --no-dev
# Alternatively: pip install -r requirements.txt

# Copy environment configuration template
cp .env.example .env

# Edit .env to set your database connection and scheduler preferences
# DATABASE_URL=postgresql://user:password@localhost:5432/rihan_db
# SCHEDULER_ENABLED=true

# Run database migrations
alembic upgrade head

# Start the aggregation and monitoring service
python -m rihan_guochan.main --mode daemon

# Or run a one-time health check on all registered resources
python -m rihan_guochan.main --mode health-check --output json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.10 - 3.12 | 核心运行环境，推荐使用 pyenv 管理 |
| PostgreSQL | 14.x 或更高 | 主数据库，存储资源元数据和审计日志 |
| Redis | 7.x 或更高 | 缓存层和任务队列后端，用于调度器状态存储 |
| libssl-dev | 1.1.1 或更高 | SSL 证书验证和 HTTPS 请求所需的系统库 |
| curl | 7.68 或更高 | 用于健康检查的后备探测工具，提供 fallback 机制 |
| Poetry | 1.4.0 或更高 | 依赖管理和打包工具，建议使用官方安装脚本 |
| Alembic | 1.11 或更高 | 数据库迁移管理，已包含在项目依赖中 |
| Prometheus Client | 0.17 或更高 | 指标导出库，可选但推荐用于生产监控集成 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/ | 如何使用 API、配置调度器、导出报告、解读健康检查结果 |
| 运维指南 | /docs/operations/ | 如何部署高可用集群、备份数据库、配置日志轮转、升级版本 |
| 开发者文档 | /docs/developer/ | 如何扩展自定义检查器、添加新的资源解析器、贡献代码规范 |
| API 参考 | /docs/api/ | 所有 RESTful 端点的详细说明、请求示例、响应结构和错误码 |
| 架构设计 | /docs/architecture/ | 系统组件图、数据流说明、扩展性设计决策和性能调优参数 |
| 故障排查 | /docs/troubleshooting/ | 常见错误信息解析、日志分析方法、网络问题诊断步骤 |

## 资源列表

以下为平台第 279/455 批次收录的全部原始资源链接，按类别分组展示。所有链接均以原始格式原样列出，未做任何协议补全或域名规范化处理。

区域分类 - 东亚

<code>rihanguochanyiqu.org.cn</code>

<code>jingpinyiren.org.cn</code>

<code>hanguorouputuan.org.cn</code>

<code>yazhouribenguochan.org.cn</code>

区域分类 - 中文音译及人物

<code>oumeizhongwenzimujingpinrenqi.org.cn</code>

<code>tiantangyiren.org.cn</code>

<code>zhongwenzimuyiren.org.cn</code>

<code>yirenrihan.org.cn</code>

区域分类 - 其他专题

<code>zhongchushaofu.org.cn</code>

<code>tingtingyiquerqusanqu.org.cn</code>

## 项目结构

```
rihan-guochan-aggregator/
├── rihan_guochan/                      # 主应用包
│   ├── __init__.py
│   ├── main.py                         # 入口点：CLI 解析与模式路由
│   ├── core/                           # 核心业务逻辑层
│   │   ├── checker.py                  # HTTP 健康检查实现，含重试与超时控制
│   │   ├── metadata.py                 # 元数据提取器：标题、描述、语言标签
│   │   ├── scheduler.py                # 基于 APScheduler 的定时任务编排器
│   │   └── registry.py                 # 资源注册表管理：增删改查与状态持久化
│   ├── api/                            # RESTful API 实现层
│   │   ├── v1/                         # API 版本 1 端点
│   │   │   ├── resources.py            # /api/v1/resources CRUD 操作
│   │   │   ├── health.py               # /api/v1/health 聚合状态查询
│   │   │   └── reports.py              # /api/v1/reports 导出与生成
│   │   └── middleware/                 # 认证、限流、日志中间件
│   ├── models/                         # SQLAlchemy 数据模型
│   │   ├── resource.py                 # Resource 表：URL、状态、最后检查时间
│   │   ├── audit.py                    # AuditLog 表：操作记录与时间线
│   │   └── snapshot.py                 # Snapshot 表：每日元数据版本历史
│   ├── services/                       # 外部服务集成层
│   │   ├── whois.py                    # WHOIS 查询服务封装
│   │   ├── ssl_validator.py            # SSL 证书链验证与过期预警
│   │   └── exporter.py                 # CSV/JSON/PDF 导出服务
│   ├── utils/                          # 通用工具函数集
│   │   ├── network.py                  # 网络请求工具，含 User-Agent 轮转
│   │   ├── validators.py               # URL 规范化与域名格式校验
│   │   └── logging.py                  # 结构化日志配置与 Sentry 集成
│   └── config/                         # 配置管理
│       ├── settings.py                 # Pydantic 配置模型，从 .env 加载
│       └── logging.yaml                # Loguru 日志格式与输出级别定义
├── tests/                              # 单元测试与集成测试套件
│   ├── unit/                           # 各模块独立测试用例
│   └── integration/                    # 数据库与 API 端到端测试
├── scripts/                            # 运维与部署辅助脚本
│   ├── init_db.sql                     # 初始数据库 Schema 创建
│   └── seed_resources.py               # 批量导入资源列表的种子脚本
├── docs/                               # 文档目录（详见文档导航章节）
├── .env.example                        # 环境变量配置模板
├── pyproject.toml                      # Poetry 项目定义与依赖锁定
├── alembic.ini                         # 数据库迁移工具配置
└── README.md                           # 本文件
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于新增资源校验规则、优化元数据提取逻辑、完善文档以及报告问题。请遵循以下步骤参与本项目：

1.  **Fork 仓库并创建功能分支** – 从主仓库 Fork 代码后，使用 `git checkout -b feature/your-feature-name` 创建独立开发分支，避免在主分支上直接提交。

2.  **编写或修改代码并确保测试通过** – 所有新增功能必须包含对应的单元测试，测试覆盖率不得低于 85%。运行 `poetry run pytest` 确保全部测试用例通过，且无回归错误。

3.  **更新文档和变更日志** – 若您的修改影响用户可见的行为或 API 接口，请同步更新 `/docs` 下的相关文档，并在 `CHANGELOG.md` 中按 [Keep a Changelog](https://keepachangelog.com/) 格式记录变更。

4.  **提交 Pull Request 并描述变更内容** – 推送分支后，在主仓库发起 Pull Request，标题应简明扼要，描述栏需详细说明修改动机、实现方式以及测试情况。PR 至少需要一位维护者审核通过方可合并。

5.  **签署开发者原创声明** – 首次贡献时，需要在 PR 评论中明确声明您拥有所提交代码的版权，并同意将其按照 MIT 许可证进行授权。

## 常见问题

**问：平台如何处理目标资源返回的 301/302 重定向？**

系统默认跟随最多 5 次重定向，最终状态码和最终 URI 都会被记录。如果重定向链中出现循环，系统会中断并标记为 `REDIRECT_LOOP` 状态，同时保留最后已知的响应头信息。对于需要禁用重定向跟踪的场景，可在 API 请求中附加 `?follow_redirects=false` 参数。

**问：健康检查的轮询频率是否会造成目标服务器的负担？**

系统设计了自适应轮询策略。对于返回 `200 OK` 且响应时间低于 500ms 的资源，检查间隔为配置的基准周期（默认 24 小时）；对于频繁超时或返回 5xx 错误的资源，系统会自动将检查间隔延长至基准周期的 3 倍，避免在目标服务不稳定时增加额外负载。所有并发请求数可通过 `MAX_WORKERS` 环境变量限制。

**问：新增私有资源（非公开 URL）如何添加到平台？**

平台设计为仅索引可公开访问的资源。对于需要认证或内网访问的 URL，平台不提供凭证存储或自动登录功能。建议在监控配置中将这些资源标记为 `INTERNAL` 类型，并配合健康检查的 `--allow-private` 标志使用，此时系统仅验证网络可达性而不解析内容元数据。

## 许可证

MIT License

Copyright (c) 2026 Rihan Research Group

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:28
