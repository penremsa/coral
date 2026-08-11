# SkyLink Resource Aggregator

SkyLink Resource Aggregator is a lightweight, community-driven metadata indexing platform designed for technical researchers, digital archivists, and content curation engineers. It addresses the core challenge of discovering, organizing, and accessing distributed multimedia metadata across specialized domain name spaces. The system does not host, store, or transmit any copyrighted content; it solely indexes public metadata, availability status, and structural attributes of third-party resources. This project targets system administrators, data pipeline developers, and academic researchers who require reproducible, auditable, and machine-readable resource catalogs for large-scale web metadata analysis.

The aggregator operates as a deterministic metadata fetcher that validates domain responses, extracts HTTP headers, records TLS certificate fingerprints, and preserves WHOIS registration snapshots. It is built for reliability, transparency, and operational simplicity, enabling users to maintain local mirrors of resource availability dashboards without external dependencies. SkyLink is not a search engine nor a proxy; it is a governance tool for understanding the lifecycle of ephemeral web properties.

## 功能概览

- **Deterministic Domain Probing** – Issues HTTP/HTTPS GET requests with configurable timeouts and user-agent rotation, recording response codes, content-length, and server signatures.

- **Metadata Snapshot Storage** – Saves probe results into versioned JSONL files indexed by ISO 8601 timestamps, supporting incremental daily updates.

- **Availability Trend Analysis** – Computes uptime percentages, average response latency, and certificate validity windows over configurable rolling windows (7d, 30d, 90d).

- **WHOIS Data Archival** – Performs WHOIS queries on each domain, extracting registrar, creation date, expiration date, and name server records for lifecycle tracking.

- **TLS Fingerprint Logging** – Captures X.509 certificate serial numbers, issuer DN, subject DN, and SHA-256 fingerprints for change detection.

- **Export Adapters** – Provides CSV, Prometheus metrics exposition, and SQLite output formats for integration with external monitoring stacks.

- **Configuration Hot-Reload** – Supports runtime adjustment of probe intervals, concurrency limits, and target domain lists via a YAML configuration file.

- **Health Check Endpoint** – Exposes an internal HTTP `/health` endpoint returning aggregate status, last run timestamp, and failure counts.

## 应用场景

- **Academic Research on Domain Name Stability** – Researchers can utilize the aggregator to study registration patterns, expiration cycles, and TLS adoption rates among specialized top-level domains. The deterministic probe logs provide primary data for longitudinal studies on web resource persistence.

- **Enterprise IT Asset Inventory** – Security teams can deploy SkyLink to continuously verify the availability of external resource domains referenced in internal documentation, automatically alerting when a domain becomes unresolvable or returns unexpected HTTP statuses.

- **Data Pipeline Monitoring** – ETL engineers can integrate the aggregator's Prometheus endpoint into their Grafana dashboards to track the health of upstream metadata sources, reducing manual checks and improving pipeline observability.

- **Forensic Analysis of Resource Mobility** – Digital forensics analysts can replay historical snapshot logs to correlate domain availability changes with external events, supporting incident response investigations.

- **Compliance and Policy Enforcement** – Compliance officers can use the exported SQLite database to generate audit reports verifying that all external resource references remain operational and correctly configured.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/skylink-io/aggregator.git
cd aggregator

# Install Python dependencies (requires Python 3.9+)
pip install -r requirements.txt

# Copy example configuration
cp config/aggregator.example.yaml config/aggregator.yaml

# Edit config/aggregator.yaml to adjust probe targets and intervals
nano config/aggregator.yaml

# Run the metadata aggregator
python -m skylink.main --config config/aggregator.yaml --once

# For continuous operation (daemon mode)
python -m skylink.main --config config/aggregator.yaml --daemon
```

## 安装要求

| 依赖 | 必需 | 说明 |
|---|---|---|
| Python 3.9.0 or higher | 是 | 核心运行环境，需要支持 asyncio 和 dataclasses |
| aiohttp 3.8.0+ | 是 | 异步 HTTP 客户端，用于并发域名探测 |
| python-whois 0.7.0+ | 是 | WHOIS 查询库，需要系统安装 whois 命令行工具 |
| cryptography 38.0.0+ | 是 | TLS 证书指纹提取和验证 |
| pyyaml 6.0+ | 是 | 配置文件解析和环境变量替换 |
| prometheus-client 0.15.0+ | 否 | 仅当启用 Prometheus 导出适配器时需要 |
| sqlite3 (system package) | 否 | 仅当使用 SQLite 输出插件时需要 |
| tzdata 2022.0+ | 是 | 时区规范化支持 |
| dnspython 2.2.0+ | 是 | DNS 解析辅助和 A/AAAA 记录缓存 |
| certifi 2022.0.0+ | 是 | TLS 证书验证根证书捆绑包 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | `docs/user-guide/configuration.md` | 如何配置探测间隔、超时、并发数以及目标域名列表？ |
| 用户指南 | `docs/user-guide/output-formats.md` | 支持的导出格式有哪些？如何切换 JSONL、CSV、SQLite？ |
| 运维手册 | `docs/operations/deployment.md` | 如何以 systemd 服务或容器方式部署生产环境实例？ |
| 运维手册 | `docs/operations/monitoring.md` | 如何解读健康检查端点，以及如何设置 Prometheus 告警规则？ |
| 开发者文档 | `docs/development/architecture.md` | 核心模块（prober、storage、exporter）的职责和交互流程是什么？ |
| 开发者文档 | `docs/development/testing.md` | 如何运行单元测试、集成测试以及模拟外部依赖？ |
| 参考手册 | `docs/reference/api.md` | 内部 REST API 端点详情，包括 `/health` 和 `/metrics` 的返回结构。 |

## 资源列表

本项目的资源索引涵盖与域名运营状态、内容可用性及访问质量相关的公共信息源。以下 URL 为外部参考链接，用于扩展元数据上下文或人工复核用途。

**域名状态监测目标**

<code>guochangaoqingshipinzaixian.org.cn</code>

<code>guochangaoqingshipinguankan.org.cn</code>

<code>rimanzaixianmianfeiguankan.org.cn</code>

<code>zhongwenzimumianfeibofang.org.cn</code>

**内容访问相关资源**

<code>zaixianzimumianfeiguankan.org.cn</code>

<code>zaixianzimuguankanmianfei.org.cn</code>

<code>zaixianzimugaoqingdianshiju.org.cn</code>

<code>mianfeishipinwangzhanzaixianguankan.org.cn</code>

**多语言内容索引**

<code>rihanzaixianmianfeishipinw.org.cn</code>

<code>oumeizaixianmianfeishipinw.org.cn</code>

## 项目结构

```
skylink/
├── aggregator.yaml               # 主配置文件（环境变量替换支持）
├── requirements.txt              # Python 依赖声明（固定版本）
├── setup.py                      # 打包脚本，支持 pip install -e .
├── README.md                     # 项目说明文档
├── LICENSE                       # MIT 许可证文本
│
├── config/                       # 配置模板和默认值
│   ├── aggregator.example.yaml   # 带注释的完整配置样例
│   └── logging.conf              # Python logging 配置（JSON 格式）
│
├── skylink/                      # 核心源码目录
│   ├── __init__.py               # 包初始化，定义 __version__
│   ├── main.py                   # 入口点：解析命令行、加载配置、调度探测器
│   ├── prober/                   # 探测引擎模块
│   │   ├── __init__.py
│   │   ├── http.py               # aiohttp 异步请求封装，带重试和超时
│   │   ├── tls.py                # 证书链提取与指纹计算
│   │   └── whois.py              # 同步 whois 查询包装器（线程池执行）
│   ├── storage/                  # 存储后端模块
│   │   ├── __init__.py
│   │   ├── jsonl_writer.py       # 按日期分区的 JSONL 写入器
│   │   ├── csv_exporter.py       # 聚合 CSV 导出（可配置字段）
│   │   └── sqlite_repo.py        # SQLite 持久化仓库（迁移管理）
│   ├── exporter/                 # 指标导出模块
│   │   ├── __init__.py
│   │   ├── prometheus.py         # 生成 Prometheus 指标文本格式
│   │   └── health.py             # 内部健康状态聚合器
│   ├── utils/                    # 工具函数
│   │   ├── __init__.py
│   │   ├── net.py                # DNS 解析缓存、IP 验证
│   │   └── time.py               # 时区感知时间戳生成器
│   └── scheduler/                # 调度模块（基于 asyncio 轮询）
│       ├── __init__.py
│       └── daemon.py             # 循环调度器，支持优雅关闭
│
├── tests/                        # 测试套件
│   ├── unit/                     # 单元测试（覆盖 prober、storage）
│   ├── integration/              # 集成测试（需要网络访问）
│   └── fixtures/                 # 模拟响应数据（JSON 存根）
│
└── scripts/                      # 运维辅助脚本
    ├── docker-entrypoint.sh      # 容器启动脚本
    └── backup-snapshots.sh       # 定期归档历史快照到 S3 兼容存储
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** – 从 `main` 分支创建新的分支，命名规范为 `feature/` 或 `fix/` 后跟简要描述（例如 `feature/add-retry-backoff`）。确保分支名称简洁且自解释。

2.  **编写或更新单元测试** – 所有新增或修改的代码必须包含相应的单元测试，测试覆盖率不应低于 85%。使用 `pytest` 运行测试套件，并确保本地所有测试通过后再提交。

3.  **遵循代码风格规范** – 提交前运行 `black` 和 `isort` 进行代码格式化，使用 `flake8` 检查风格警告。所有公共函数和类必须包含 Google 风格的 docstring 注释。

4.  **更新文档和示例配置** – 如果更改影响了配置参数、输出格式或命令行接口，必须同步更新 `docs/` 目录下对应的用户指南，并修改 `config/aggregator.example.yaml` 以反映新字段。

5.  **提交 Pull Request 并填写模板** – 在 PR 描述中明确列出变更类型（新增特性、修复缺陷、文档改进）、测试结果摘要以及是否影响现有部署。至少需要一名维护者审核通过后方可合并。

## 常见问题

**问：SkyLink 是否会缓存或存储任何媒体文件内容？**

答：不会。SkyLink 仅记录 HTTP 响应元数据（状态码、头部、内容长度）和 TLS 证书信息。它不下载响应体（即 `aiohttp` 的 `read()` 方法不会被调用），也不保存任何音频、视频或文本内容。所有存储的数据均为公开可得的非内容元数据，符合数据最小化原则。

**问：如何处理域名解析失败或 WHOIS 查询超时？**

答：探测引擎内置了指数退避重试策略（初始延迟 1 秒，最大重试 3 次）。对于 WHOIS 查询，单独设置 10 秒超时，并使用线程池隔离以避免阻塞事件循环。若所有重试均失败，该域名会被标记为 `UNREACHABLE` 状态，并在存储记录中保留失败原因字段，便于后续人工检查。用户可以配置 `failure_threshold` 参数，当连续失败次数超过阈值时触发告警。

**问：是否可以自定义探测的目标域名列表，而无需修改代码？**

答：可以。所有目标域名均在 `config/aggregator.yaml` 文件的 `targets` 列表字段中定义。该字段支持环境变量替换，例如可以使用 `targets: ${SKYLINK_TARGETS:["example.com"]}` 从环境变量读取。配置更改后无需重启整个服务，主进程会监听配置文件变更信号（SIGHUP）并执行热重载。

## 许可证

MIT License

Copyright (c) 2026 SkyLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
