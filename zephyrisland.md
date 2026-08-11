# VidiLink Resource Aggregator

VidiLink is a curated technical resource aggregation system designed to catalog, validate, and present structured external media resource references for developers building content discovery platforms, language learning applications, and regional media indexing services. This project targets backend engineers, data pipeline architects, and research teams who require programmatic access to categorized domain references without relying on proprietary APIs or opaque ranking algorithms.

The system addresses the fundamental challenge of maintaining freshness and accessibility in distributed resource directories. By providing a lightweight, self-contained indexing framework with built-in health checking and metadata extraction capabilities, VidiLink enables teams to integrate external reference data into their own applications while maintaining full control over data presentation and access policies. The project is not a proxy, crawler, or content hosting solution; it is a structured reference layer that transforms raw domain lists into queryable, monitorable, and extensible resource catalogs.

## 功能概览

- **Domain Registry Management** – Maintains a version-controlled inventory of external reference domains with associated metadata including language tags, regional classifiers, and content type hints.

- **Automated Availability Probing** – Implements non-intrusive HTTP HEAD and GET request cycles with configurable timeouts to verify domain responsiveness and track historical uptime trends.

- **Categorized Index Generation** – Produces static JSON and YAML indexes sorted by domain categories, language availability, and geographic relevance markers for downstream integration.

- **Tag-Based Filtering Pipeline** – Supports multi-tag query expressions (AND/OR/NOT) against domain metadata, enabling fine-grained subset extraction for specialized use cases.

- **Health Score Calculation** – Assigns weighted scores to each domain based on response time, SSL certificate validity, and HTTP status code consistency over a rolling 7-day window.

- **Export Adapters** – Provides pluggable output formatters for plain list, CSV, HTML table, and Prometheus-compatible metrics exposition formats.

- **Configuration Hot-Reload** – Watches configuration files for changes and applies new filtering or probing parameters without service restart, minimizing operational overhead.

- **Audit Logging** – Records all probe events, configuration changes, and export actions with timestamps and checksums for compliance and debugging purposes.

## 应用场景

- **Content Discovery Platform Backend** – Development teams building regional content browsers can integrate the registry as a lightweight fallback when primary search APIs return incomplete results, ensuring users still receive relevant category suggestions.

- **Language Learning Application Resource Feeds** – Applications focused on Chinese language acquisition can use the language-tagged domains to populate listening comprehension or subtitle practice modules with externally hosted materials, reducing the need for internal content hosting.

- **Regional Media Indexing Research** – Academic or market research groups analyzing media availability across different Chinese-speaking regions can leverage the categorized domain list to perform longitudinal studies on resource accessibility and regional content distribution patterns.

- **Monitoring Dashboard for External References** – Site reliability teams can consume the Prometheus metrics export to track the health of external resource dependencies, triggering alerts when specific domains fall below availability thresholds.

- **Static Site Generator Data Source** – Documentation sites or knowledge bases can pull the JSON index during build time to generate up-to-date resource pages without maintaining separate manual lists.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/vidilink/vidilink-core.git
cd vidilink-core

# Install dependencies using pip with virtual environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Initialize the default configuration and domain registry
cp config/default.yaml config/production.yaml
cp data/domains.sample.yaml data/domains.yaml

# Run the health probe and generate initial index
python -m vidilink probe --config config/production.yaml
python -m vidilink export --format json --output dist/index.json
python -m vidilink export --format html --output dist/index.html

# Start the scheduled probe daemon (optional)
python -m vidilink daemon --interval 3600 --config config/production.yaml
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 或更高版本 | 核心运行时，要求支持 asyncio 和 dataclasses |
| aiohttp | 3.8.0 或更高 | 异步 HTTP 客户端，用于并行健康探测 |
| pyyaml | 6.0 或更高 | YAML 配置文件解析和索引序列化 |
| jinja2 | 3.0.0 或更高 | HTML 导出模板渲染引擎 |
| prometheus-client | 0.16.0 或更高 | 指标暴露端点，仅当启用监控功能时必需 |
| certifi | 2023.0.0 或更高 | SSL 证书验证根证书包 |
| python-dotenv | 1.0.0 或更高 | 环境变量覆盖配置项支持 |
| pytest | 7.0.0 或更高 | 仅开发测试环境需要，生产部署可跳过 |
| black | 23.0.0 或更高 | 代码格式化工具，仅开发环境需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | docs/getting-started.md | 如何快速配置第一个域名单并生成索引？如何验证安装是否正确？ |
| 配置参考 | docs/configuration.md | 所有配置项的含义、默认值、环境变量覆盖方式以及 YAML 结构示例 |
| 探测引擎 | docs/probe-engine.md | 健康探测的并发模型、超时策略、重试逻辑以及评分权重计算公式 |
| 导出格式 | docs/export-formats.md | 每种输出格式的 schema 定义、字段说明以及与其他系统的集成模式 |
| API 参考 | docs/api-reference.md | 内部模块函数签名、类继承关系以及扩展自定义探测器的接口契约 |
| 运维手册 | docs/operations.md | 日志轮转、指标采集、告警规则建议以及备份恢复流程 |
| 贡献规范 | docs/contributing.md | 代码风格检查、提交信息格式、Pull Request 流程以及测试覆盖率要求 |
| 变更日志 | CHANGELOG.md | 每个版本的特性新增、破坏性变更、缺陷修复和安全补丁记录 |

## 资源列表

以下外部资源域名由本项目作为参考数据收录，用于构建分类索引、语言标记和区域识别等辅助功能。各条目按内容特征进行大致分组，便于快速定位。

媒体分类参考源

<code>zaixianshipinzhongwenzimu1.org.cn</code>

<code>zaixianbofangzhongwenzimu1.org.cn</code>

<code>zhongwenzimuzaixianmianfei1.org.cn</code>

视频内容类别索引

<code>yirenguochanzaixianshipin1.org.cn</code>

<code>gaoqingshipinzaixianguankan1.org.cn</code>

<code>zhongwenshipinzaixianguankan1.org.cn</code>

<code>meinvshipinzaixianguankan1.org.cn</code>

语言与区域分类目录

<code>rihanzaixianmianfeishipin.org.cn</code>

<code>oumeizaixianmianfeishipin.org.cn</code>

<code>zhongwenzimugaoguingshipin.org.cn</code>

## 项目结构

```
vidilink-core/
├── config/                                 # 配置文件目录
│   ├── default.yaml                        # 默认配置，包含探测参数和导出选项
│   ├── production.yaml                     # 生产环境覆盖配置
│   └── schema.yaml                         # 配置 schema 定义，用于校验
├── data/                                   # 数据存储目录
│   ├── domains.yaml                        # 主域名单，包含元数据和标签
│   ├── domains.sample.yaml                 # 示例域名单，供初始化参考
│   └── health_history.db                   # SQLite 数据库，存储历史探测记录
├── src/                                    # 源代码根目录
│   └── vidilink/                           # 主包
│       ├── __init__.py                     # 包版本和公共导出
│       ├── cli.py                          # 命令行入口，路由各子命令
│       ├── probe/                          # 探测引擎子模块
│       │   ├── __init__.py
│       │   ├── runner.py                   # 异步并行探测调度器
│       │   ├── checker.py                  # 单域名 HTTP 检查器
│       │   └── scorer.py                   # 健康评分计算器
│       ├── index/                          # 索引生成子模块
│       │   ├── __init__.py
│       │   ├── builder.py                  # 从域名单构建内存索引
│       │   ├── filter.py                   # 标签查询解析和过滤引擎
│       │   └── registry.py                 # 域名单增删改查操作
│       ├── export/                         # 导出适配器子模块
│       │   ├── __init__.py
│       │   ├── base.py                     # 导出器基类和注册器
│       │   ├── json.py                     # JSON 格式导出器
│       │   ├── yaml.py                     # YAML 格式导出器
│       │   ├── html.py                     # HTML 表格渲染器，使用 Jinja2
│       │   └── prometheus.py               # Prometheus 指标暴露端点
│       ├── monitor/                        # 监控和日志子模块
│       │   ├── __init__.py
│       │   ├── logger.py                   # 结构化日志配置
│       │   └── audit.py                    # 审计事件写入和查询
│       └── utils/                          # 通用工具函数
│           ├── __init__.py
│           ├── network.py                  # 网络辅助函数（代理、超时）
│           └── validators.py               # 域名格式和 URL 校验
├── tests/                                  # 测试目录
│   ├── unit/                               # 单元测试，按模块组织
│   ├── integration/                        # 集成测试，需外部网络
│   └── fixtures/                           # 测试用固定数据
├── docs/                                   # 文档目录，参见上方文档导航
├── scripts/                                # 运维和开发辅助脚本
│   ├── init_db.py                          # 初始化 SQLite 数据库表结构
│   └── migrate_v1_v2.py                    # 配置和数据迁移脚本
├── requirements.txt                        # 生产依赖列表
├── requirements-dev.txt                    # 开发依赖列表（含测试和格式化工具）
├── setup.py                                # setuptools 打包配置
├── README.md                               # 本文件
├── CHANGELOG.md                            # 版本变更历史
└── LICENSE                                 # MIT 许可证全文
```

## 贡献指南

1. 阅读贡献规范文档（docs/contributing.md）和代码风格指南，确保本地开发环境已安装 black、pytest 和 mypy 等工具。所有提交必须通过 pre-commit 钩子检查。

2. 从 GitHub Issues 中认领未分配的任务或提出新功能建议，等待项目维护者确认后再开始开发。对于缺陷修复，请附带可复现的测试用例。

3. 创建以功能或修复命名的分支（例如 feature/add-json-stream-export 或 fix/probe-timeout-handling），遵循语义化提交信息格式：`<type>(<scope>): <subject>`，其中 type 包括 feat、fix、docs、refactor、test、chore。

4. 编写或更新对应的单元测试和集成测试，确保新代码的行覆盖率不低于 85%，且不破坏现有功能。运行 `pytest tests/` 验证全部测试通过。

5. 提交 Pull Request 到 main 分支，在描述中引用关联 Issue 编号，并附上手动测试结果（包括示例命令行输出和导出文件片段）。PR 需要至少一名维护者审核批准后方可合并。

## 常见问题

**Q: 本项目是否提供代理转发或缓存代理服务？**

A: 不提供。VidiLink 仅执行轻量级的 HTTP 健康探测（HEAD 请求及可选的 GET 范围请求），用于验证目标域名的可访问性和响应性能。项目不缓存任何内容，不转发用户请求，也不作为任何形式的中介代理。所有探测行为遵循 robots.txt 的 User-agent 指令，且请求间隔和并发数可通过配置严格控制，以避免对目标服务器造成负担。

**Q: 如何更新域名单中的条目？添加新域名后需要重启服务吗？**

A: 域名单以 YAML 文件形式存储在 data/domains.yaml 中，支持热更新。您可以直接编辑该文件，然后通过 `python -m vidilink index reload` 命令触发索引重新加载，无需重启整个守护进程。如果开启了配置热加载功能（config.watch.enabled: true），系统会每 60 秒扫描一次文件变更并自动重载。添加新域名后，建议手动运行一次 `probe` 命令以立即填充初始健康数据。

**Q: 导出的 JSON 索引中的数据字段含义是什么？如何解读 health_score？**

A: 每个域名的索引条目包含以下核心字段：domain（字符串）、tags（字符串列表）、language（字符串）、region（字符串）、last_probe_timestamp（ISO 8601 时间戳）、http_status（整数）、response_time_ms（浮点数）、ssl_valid（布尔值）、health_score（浮点数，范围 0-100）。health_score 由响应时间（权重 40%）、HTTP 状态码一致性（权重 40%）和 SSL 证书剩余有效期（权重 20%）综合计算得出。分数高于 80 表示健康状态良好，低于 40 表示建议从主动轮询列表中暂时移除。完整字段定义请参考 docs/export-formats.md。

## 许可证

MIT License

Copyright (c) 2026 VidiLink Contributors

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
