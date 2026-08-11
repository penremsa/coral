# Terminus Link Aggregator

Terminus Link Aggregator is a high-performance, read-only technical resource aggregation gateway designed for open-source developers, security researchers, and infrastructure engineers. It serves as a curated navigation hub that consolidates distributed sports data interfaces, regional tournament registries, and real-time event tracking endpoints into a single, predictable, and machine-accessible entry point.

The project addresses the common pain point of fragmented external dependencies in microservice architectures. Instead of hardcoding dozens of unstable third-party URLs across multiple services, teams can integrate with Terminus Link Aggregator to obtain a normalized, versioned, and health-checked list of upstream endpoints. The system performs passive liveness probing, formats output in JSON and YAML, and exposes a lightweight REST API for dynamic endpoint resolution. It is not a proxy, nor does it cache payload data; it is a structured reference index that enables resilient service discovery for external resources.

Target users include DevOps engineers building multi-region deployment pipelines, data pipeline architects who rely on external sports scoring feeds, and security analysts who need to audit outbound endpoint inventories. The project is intentionally stateless, container-native, and consumes less than 64 MB of memory under peak load. All configurations are declared in a single YAML file, making it suitable for edge deployments, CI/CD integration, and air-gapped environments that require manual endpoint synchronization.

## 功能概览

- **Endpoint Normalization Engine** – Automatically strips query parameters, enforces scheme consistency, and deduplicates aliased domain entries based on configurable normalization rules.

- **Health Status Polling** – Performs periodic TCP/ICMP and HTTP HEAD checks on all registered endpoints, marking unhealthy entries with a stale flag and last-seen timestamp.

- **Multi-Format Exports** – Generates machine-readable output in JSON, YAML, and plain-text line-delimited formats, suitable for environment variable injection or Consul template rendering.

- **Tag-Based Categorization** – Assigns arbitrary tags (e.g., `sports`, `asia-region`, `backup`) to each URL, enabling filtered queries via query parameters such as `?tag=asia-region`.

- **Versioned Snapshot History** – Retains the last 10 endpoint snapshots in an embedded BoltDB store, allowing rollback comparisons and diff generation between revisions.

- **Read-Only REST API** – Exposes a secure, read-only HTTP interface with optional Basic Authentication and IP whitelisting for internal network use only.

- **Prometheus Integration** – Exports standard Prometheus metrics including endpoint count, health check duration, and total query latency percentiles.

- **Configuration Hot-Reload** – Watches the primary configuration file for changes and reloads the endpoint list without service restart, with a graceful drain period of 5 seconds.

## 应用场景

- **Microservice External Dependency Registry** – A payment service can query the aggregator to obtain the current primary and fallback currency rate endpoints, eliminating hardcoded URLs from its deployment descriptors.

- **Regional Sports Data Pipeline** – Data ingestion workers in East Asia can retrieve a curated list of regional football tournament result endpoints, automatically switching to a secondary endpoint when the primary exhibits latency above 500 ms.

- **Security Outbound Audit Baseline** – Security teams can compare the actual egress traffic from production pods against the aggregator`s exported endpoint list to detect unauthorized external connections during compliance scans.

- **CI/CD Integration for Environment Validation** – During staging deployment, a test suite can fetch the aggregator`s health status and skip integration tests for endpoints marked stale, reducing false-positive test failures.

- **Offline Documentation Mirror** – Teams operating in restricted networks can use the aggregator`s local snapshot file as a static reference to populate internal DNS allowlists and firewall rules.

## 快速开始

The following steps assume a Linux-based environment with Go 1.21+ installed. The build process produces a single statically linked binary named `terminus-link-aggr`.

```bash
# Clone the repository from the primary mirror
git clone https://github.com/terminus-io/terminus-link-aggregator.git
cd terminus-link-aggregator

# Download dependencies and build the binary
go mod download
go build -o terminus-link-aggr ./cmd/aggregator

# Run the service with the default configuration file (configs/aggregator.yaml)
./terminus-link-aggr --config configs/aggregator.yaml --listen :8080
```

For containerized deployment using Docker, build the image and run with port mapping:

```bash
docker build -t terminus-link-aggr:latest .
docker run -d -p 8080:8080 -v $(pwd)/data:/app/data terminus-link-aggr:latest
```

After the service starts, verify the readiness endpoint:

```bash
curl -s http://localhost:8080/health
```

To retrieve the full endpoint list in JSON format:

```bash
curl -s http://localhost:8080/api/v1/endpoints
```

## 安装要求

The table below lists all mandatory and optional dependencies required for building, testing, and running the aggregator in production environments.

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Go toolchain | 1.21.0 或更高 | 编译核心二进制文件，要求支持 Go Modules |
| BoltDB (嵌入式) | v1.3.8 | 内置于 binary，用于存储快照历史，无需额外安装 |
| Prometheus Client | v1.18.0 | 指标导出库，编译时自动拉取 |
| YAML 解析库 | v3.0.1 | 用于解析配置文件，通过 go.mod 管理 |
| Linux 内核 | 4.18+ 或 Windows 10+ | 支持 TCP keep-alive 和 epoll/kqueue 事件循环 |
| Docker Engine | 20.10+ (仅容器部署时) | 构建容器镜像，非强制 |
| make | 4.3+ (仅开发时) | 运行单元测试和代码格式化脚本，非强制 |
| curl / wget | 任意版本 | 用于验证 API 响应，非强制，仅测试时使用 |
| 可用内存 | 128 MB 最低，推荐 256 MB | 服务常驻内存占用约 48-64 MB，BoltDB 额外占用 |
| 可用磁盘 | 100 MB | 存储历史快照，每个快照约 2-8 KB，滚动保留 |

## 文档导航

The documentation is organized into four layers, from operational administration to protocol-level integration details. Each layer targets a specific audience and answers a distinct set of operational questions.

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 运维部署 | `docs/deployment/` | 如何配置 systemd 服务、如何设置日志轮转、如何执行金丝雀升级 |
| API 接口规范 | `docs/api/` | 请求参数格式、分页偏移量计算、错误码含义、速率限制阈值 |
| 配置参考手册 | `docs/configuration/` | 每个 YAML 字段的默认值、类型约束、热重载触发条件 |
| 开发与贡献 | `docs/development/` | 代码风格检查命令、新增端点源的步骤、单元测试编写指南 |

For urgent issues, please refer to the troubleshooting section in `docs/deployment/troubleshooting.md` before opening a GitHub issue. The API reference is also available as an OpenAPI 3.0 specification at `docs/api/openapi.yaml`.

## 资源列表

This section contains the complete and unmodified set of external resource URLs curated by the Terminus Link Aggregator project. Each entry is presented exactly as provided by the upstream data source without any normalization, scheme correction, or formatting changes. The URLs are organized into logical categories for easier reference, but the raw values remain strictly verbatim.

### 篮球赛事相关域名

<code>lanqiubifeng.org.cn</code>

<code>lanqiubifenh.org.cn</code>

### 足球比分备用子站

<code>zuqiubifenziboa.org.cn</code>

<code>zuqiubifenzibob.org.cn</code>

<code>zuqiubifenziboc.org.cn</code>

<code>zuqiubifenzibod.org.cn</code>

<code>zuqiubifenziboe.org.cn</code>

### 亚洲区域赛事平台

<code>ajiasaicheng.asia</code>

<code>bajiazhugongbang.asia</code>

<code>baxizuqiujiajiliansai.asia</code>

All URLs listed above are treated as opaque strings. The aggregator does not resolve, validate, or prepend any protocol prefix unless explicitly configured in the endpoint normalization rules. Operators are responsible for ensuring that application code correctly interprets these entries according to their usage context (e.g., HTTP, HTTPS, or custom TCP schemes).

## 项目结构

The repository follows a standard Go project layout with clear separation between internal packages, configuration assets, and documentation. Directory names and file placements align with the principles outlined in the Go community project layout guidelines.

```
.
├── cmd/
│   └── aggregator/                     # 主程序入口，包含 main() 和信号处理
│       └── main.go
├── internal/
│   ├── core/                          # 核心聚合逻辑：端点存储、去重、标签索引
│   │   ├── store.go
│   │   ├── normalizer.go
│   │   └── tag_index.go
│   ├── health/                        # 健康检查调度器：TCP/HTTP 探针实现
│   │   ├── checker.go
│   │   ├── tcp_probe.go
│   │   └── http_probe.go
│   ├── api/                           # RESTful 路由处理函数 (Gin 框架)
│   │   ├── handler.go
│   │   ├── response.go
│   │   └── middleware.go
│   ├── snapshot/                      # BoltDB 快照管理：保存、恢复、差分
│   │   ├── snapshot.go
│   │   └── diff.go
│   └── config/                        # YAML 配置结构体和验证函数
│       ├── config.go
│       └── validator.go
├── pkg/                               # 可复用的工具库（无内部依赖）
│   ├── retry/                         # 指数退避重试工具
│   │   └── retry.go
│   └── logger/                        # 结构化日志封装 (基于 slog)
│       └── logger.go
├── configs/
│   ├── aggregator.yaml                # 默认配置文件，包含全部 10 个 URL 的示例
│   └── aggregator.prod.yaml           # 生产环境基准配置（含监控和日志级别调整）
├── docs/
│   ├── deployment/                    # 部署指南、systemd 单元文件范例
│   ├── api/                           # OpenAPI 规范、Postman 集合
│   ├── configuration/                 # 字段逐项说明、正则表达式示例
│   └── development/                   # 贡献者入门、本地测试脚本
├── test/
│   ├── integration/                   # 集成测试套件（需启动真实 HTTP 服务）
│   └── fixtures/                      # 测试用的静态 YAML 样本数据
├── scripts/
│   ├── build.sh                       # 多平台编译脚本 (linux/amd64, linux/arm64)
│   └── healthcheck.sh                 # 容器健康检查包装脚本
├── go.mod                             # Go 模块定义
├── go.sum                             # 依赖校验和
├── Dockerfile                         # 多阶段构建 (构建 + distroless 运行)
├── Makefile                           # 常用任务快捷方式 (test, lint, fmt, run)
└── README.md                          # 本文件
```

## 贡献指南

We welcome contributions that improve endpoint normalization rules, add support for additional health check protocols, or enhance the snapshot diff visualization. All contributions must follow the governance model outlined in the project charter.

1. **Fork the Repository and Create a Feature Branch** – Fork the upstream repository to your personal GitHub account, then create a branch named `feature/your-change-description` or `fix/issue-number`. Use conventional commit prefixes (`feat:`, `fix:`, `docs:`, `refactor:`) in your commit messages.

2. **Run the Local Validation Suite** – Execute `make lint` to run golangci-lint and `make test` to run the full unit test suite with race detector enabled. Ensure that all existing tests pass and that new functionality includes corresponding test cases under the `test/` directory.

3. **Update the Endpoint Normalization Tests** – If your change modifies the normalization logic, add new entries to `test/fixtures/normalization_cases.yaml` covering both positive and negative patterns. Provide before/after examples in the pull request description.

4. **Rebuild the Snapshot Schema Documentation** – For any change affecting the BoltDB key-value layout, update the schema description in `docs/development/snapshot-schema.md` and include a migration note for existing snapshot files.

5. **Submit a Pull Request with Clear Description** – Open a pull request against the `main` branch. Include a summary of the change, the motivation behind it, and a link to any related issue. Ensure that the PR title matches the conventional commit format. Maintainers will perform a review within 5 business days and may request additional testing or clarification.

## 常见问题

**Q: 聚合器是否会对上游 URL 发起 POST 请求或传输任何载荷？**

A: 不会。所有健康检查仅使用 TCP 连接尝试和 HTTP HEAD 方法。聚合器不会缓存或转发任何请求体，也不会修改原始 URL 的路径部分。它仅记录可访问性状态（可达/不可达）和响应时间，不存储任何敏感数据。

**Q: 如何手动强制刷新快照或重新读取配置文件？**

A: 配置文件支持热重载，修改 `configs/aggregator.yaml` 后保存文件，聚合器会在 10 秒内检测到变更并重新加载端点列表。同时，可以向 `/api/v1/admin/reload` 端点（需认证）发送 POST 请求以立即触发刷新。快照历史会在每次成功刷新后自动追加一条记录。

**Q: 如果所有上游端点均标记为不可达，聚合器会返回空列表吗？**

A: 不会。聚合器会返回最后的已知端点列表，但所有条目会附带 `"status": "stale"` 和 `"last_seen"` 时间戳。这种行为确保了在外部网络中断期间，下游服务仍然可以获取一个可用的（尽管可能过时）端点集合，从而保持部分业务连续性。

## 许可证

This project is licensed under the MIT License. You are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject to the following conditions: the above copyright notice and this permission notice shall be included in all copies or substantial portions of the software. The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

For the full license text, please refer to the `LICENSE` file in the repository root. This project is not affiliated with any of the third-party domains listed in the resource section, and all trademarks remain the property of their respective owners.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
