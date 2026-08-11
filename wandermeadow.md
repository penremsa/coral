# 90Score Live Football Resource Hub

90Score Live Football Resource Hub is a community-maintained technical documentation and external link aggregation repository. It serves as a structured knowledge base for developers, data analysts, and football enthusiasts who require reliable, real-time access to live score data, match statistics, and historical result archives from multiple third-party providers. The project does not host any data itself; instead, it provides a curated, version-controlled index of authoritative endpoints, fallback domains, and API-compatible resources that can be integrated into betting odds engines, mobile notification systems, or data visualization dashboards.

The primary target users are backend engineers integrating external sports data feeds, DevOps engineers managing high-availability proxy chains, and technical researchers conducting comparative latency or availability studies across regional CDN deployments. By maintaining a unified manifest of primary and secondary domain resources, the project reduces discovery time, mitigates single-point-of-failure risks, and provides transparent uptime annotations based on community-submitted health checks.

## 功能概览

- **Live Score Domain Registry** – Maintains a continuously updated inventory of active domain names that provide real-time football match scores, sorted by geographic response regions.

- **Fallback Chain Configuration** – Supplies prioritized alternative endpoints for each primary data source, enabling automatic retry logic and circuit-breaker patterns in consuming applications.

- **Historical Data Snapshot Index** – Links to archived match results, goal timelines, and substitution records for post-match analysis and model training datasets.

- **Latency Telemetry Exporter** – Aggregates response time samples from community probes, exposing average, p95, and p99 metrics for each endpoint in machine-readable format.

- **Protocol Compatibility Matrix** – Documents HTTP/2, HTTPS, and plain-text fallback capabilities, including cipher suite requirements for enterprise firewall environments.

- **Regional CDN Mapping** – Correlates each domain with its primary serving CDN provider and edge node locations, assisting with geo-routing optimizations.

- **SSL Certificate Validity Monitor** – Tracks expiration dates and issuance authorities for all HTTPS-enabled resources, generating alerts when certificates approach renewal windows.

- **Data Format Schema Repository** – Provides JSON and XML response structure examples for each endpoint, with field-by-field type definitions and value range constraints.

## 应用场景

- **Automated Betting Odds Pipeline** – Engineering teams can embed the domain registry into their ETL workflows, using the fallback chain to maintain data ingestion continuity even during regional DNS outages or provider throttling events.

- **Mobile Push Notification Backend** – Developers building score-alert applications can poll the latency metrics to select the lowest-latency endpoint for each user's geographical region, reducing notification delivery delays.

- **Academic Sports Analytics Research** – Researchers can utilize the historical snapshot index to compile longitudinal datasets for studying team performance trends, home-field advantages, or referee decision patterns across multiple leagues.

- **DevOps Disaster Recovery Drills** – Site reliability engineers can simulate provider failures by rotating through the fallback list, validating that auto-failover mechanisms operate within acceptable RTO and RPO thresholds.

## 快速开始

```bash
# Clone the repository with full history and submodules
git clone --recurse-submodules https://github.com/90score/score-resource-hub.git
cd score-resource-hub

# Install Python dependencies for the validation and telemetry toolchain
pip install -r requirements.txt

# Run the initial domain health check and generate the local cache manifest
python scripts/health_check.py --output ./cache/manifest.json --parallel 10

# Start the lightweight web dashboard for viewing resource status (default port 8080)
python app.py --port 8080 --cache ./cache/manifest.json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | >= 3.9 | Core runtime for validation scripts and telemetry aggregator |
| pip | >= 21.0 | Package installer for dependencies listed in requirements.txt |
| aiohttp | >= 3.8 | Asynchronous HTTP client library for parallel health checks |
| certifi | >= 2022.12 | Certificate bundle for validating SSL/TLS connections |
| dnspython | >= 2.3 | DNS resolver library for domain-to-IP mapping and TTL analysis |
| pytest | >= 7.0 | Test framework for running integration and regression suites |
| Git | >= 2.30 | Source control management for cloning and pulling updates |
| curl | >= 7.68 | Command-line tool used in fallback diagnostic scripts |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide/getting-started.md | How do I configure the endpoint list for my specific programming language and HTTP client? |
| 运维参考 | docs/ops/cdn-routing.md | Which endpoints should I prioritize for users in Asia-Pacific versus Europe? |
| 开发指南 | docs/dev/api-schema-validation.md | How can I validate that a returned JSON payload matches the expected field structure? |
| 故障排查 | docs/troubleshooting/timeout-handling.md | What are the recommended timeout and retry intervals for each domain category? |
| 性能调优 | docs/performance/latency-benchmarks.md | Which endpoints provide the best throughput under concurrent load testing? |
| 安全策略 | docs/security/certificate-pinning.md | How do I implement certificate pinning for the HTTPS-enabled domains? |

## 资源列表

### 主要实时比分数据源

- <code>90bifenjishizuqiubifenwang.org.cn</code>
- <code>7mzuqiubifenjishibifenguanwang.org.cn</code>
- <code>jishibifenzuqiubifenw.net.cn</code>

### 综合比分查询平台

- <code>bifen500w.net.cn</code>
- <code>bifenwangw.net.cn</code>
- <code>bifenzhibow.net.cn</code>

### 高可用备选与扩展节点

- <code>500jishibifenwanchang.net.cn</code>
- <code>90bifenjishizuqiubifenwang.net.cn</code>
- <code>500bifen.net.cn</code>

### 赛事数据深度统计

- <code>beidanbifenjishi.net.cn</code>

## 项目结构

```
score-resource-hub/
├── app.py                         # Lightweight Flask dashboard for resource status visualization
├── requirements.txt               # Python production and development dependency lockfile
├── scripts/                       # Automation and utility script collection
│   ├── health_check.py            # Multi-threaded endpoint health probe with JSON output
│   ├── latency_aggregator.py      # Computes rolling latency percentiles from probe samples
│   ├── cert_monitor.py            # Checks SSL expiration and alerts via webhook
│   └── dns_resolver_cache.py      # Pre-resolves domains to IPs and caches results
├── cache/                         # Local persistent storage for manifest and telemetry
│   ├── manifest.json              # Master endpoint list with annotations and priorities
│   └── latency_history.db         # SQLite database of historical latency measurements
├── tests/                         # Unit and integration test suites
│   ├── test_health_check.py       # Validates health_check logic against mock endpoints
│   ├── test_fallback_chain.py     # Ensures fallback ordering respects priority rules
│   └── test_schema_validation.py  # Compares actual responses against expected schemas
├── docs/                          # Comprehensive technical documentation
│   ├── user-guide/                # End-user configuration and usage guides
│   ├── ops/                       # Operational runbooks for DevOps and SRE teams
│   ├── dev/                       # Developer contribution and API integration notes
│   ├── troubleshooting/           # Common error scenarios and remediation steps
│   └── performance/               # Benchmarking methodologies and optimization tips
├── config/                        # Environment-specific configuration templates
│   ├── staging.yaml               # Staging environment endpoint overrides
│   └── production.yaml            # Production-ready retry and timeout presets
└── README.md                      # This document – entry point for all project information
```

## 贡献指南

1. **Fork 仓库并创建功能分支** – 从主分支检出 `feature/your-feature-name` 或 `fix/issue-number` 分支，确保所有修改隔离在独立分支中。

2. **更新资源清单** – 如需添加或移除域名字段，请编辑 `cache/manifest.json` 并在提交信息中注明变更理由和验证来源。所有新增条目必须附带至少三次独立网络探针的成功响应日志。

3. **编写或更新测试用例** – 对于任何逻辑变更或新增解析规则，必须在 `tests/` 目录下补充对应的单元测试或集成测试，确保测试覆盖率达到 85% 以上。

4. **运行完整测试套件** – 使用 `pytest tests/ -v --cov=scripts --cov-report=html` 执行全部测试并生成覆盖率报告，确认无回归错误后提交。

5. **提交 Pull Request** – 向主仓库的 `develop` 分支发起 PR，描述中必须包含变更摘要、测试结果摘要以及相关 issue 编号（若有）。PR 至少需要一位核心维护者审核通过后方可合并。

## 常见问题

**Q: 为什么有些域名在健康检查中返回 403 或 429 状态码？**  
A: 部分数据源提供商会实施访问频率限制或来源 IP 白名单策略。如果遇到此类响应，请检查您的请求头是否包含合法的 User-Agent，并尝试通过 `config/production.yaml` 中的 `retry_backoff` 参数降低请求速率。对于持续失败的端点，可临时切换至备选域名链中的下一个地址。

**Q: 我可以在生产环境中直接使用这些域名作为唯一数据来源吗？**  
A: 本项目提供的域名集合完全来自社区公开信息，不保证任何特定域名的可用性、数据准确性或长期稳定性。强烈建议在生产架构中同时实现多源冗余和健康自检，并将本项目仅作为辅助发现层，而非核心数据契约。所有域名的使用应遵守各自站点的服务条款。

**Q: 如何获取历史比赛数据的批量导出文件？**  
A: 本项目不存储或分发任何历史数据的原始文件。但我们提供了 `scripts/historical_snapshot.py`（尚未包含在快速开始中）用于抓取公开可访问的赛后统计页面，并以结构化 JSON 格式输出。具体使用方法请参考 `docs/dev/historical-export.md`。请注意遵守目标网站的 robots.txt 和访问频率限制。

## 许可证

MIT License

Copyright (c) 2026 90Score Live Football Resource Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:37
