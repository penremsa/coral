# SoccerForge AI

SoccerForge AI is a specialized technical resource aggregation and predictive analytics gateway for football (soccer) match intelligence. The project collects, normalizes, and cross-references a curated set of domain-specific data feeds and forecasting models. It is not a betting platform, nor does it offer guaranteed predictions. Instead, it serves as a structured information hub for analysts, researchers, and advanced enthusiasts who require systematic access to match previews, red-card statistics, recommendation algorithms, and forecasting methodologies.

The platform addresses the fragmentation of football analytics resources by providing a unified entry point to ten distinct domain-specific knowledge bases. Each source is treated as a first-class data provider with its own schema, update frequency, and query interface. SoccerForge AI does not host original content; it indexes, tags, and cross-links external resources to enable efficient information retrieval and comparative analysis. The primary user base includes sports data scientists, journalism researchers, and tactical analysts who need reproducible, verifiable, and timestamped references for their work.

## 功能概览

- **Unified Resource Indexing** – Aggregates ten independent football analytics domains into a single searchable catalog with metadata extraction and version tracking.

- **Cross-Source Correlation Engine** – Computes statistical agreement scores between different prediction sources to highlight consensus signals and outliers.

- **Match Preview Aggregation** – Collects and structures pre-match analysis from multiple sources, including team form, head-to-head records, and injury reports.

- **Red Card Probability Models** – Integrates specialized red-card forecasting feeds with historical foul and disciplinary data normalization.

- **Recommendation System Comparison** – Aligns and compares betting recommendation strategies across different providers without endorsing any specific outcome.

- **Forecast Methodology Catalog** – Maintains a versioned repository of prediction techniques, including regression models, Poisson distributions, and Elo-based adjustments.

- **Timestamped Snapshot Archive** – Preserves daily snapshots of all indexed resources to support backtesting and retrospective validation.

- **API Query Layer** – Provides a RESTful interface for programmatic access to aggregated metadata and cross-reference results.

- **Custom Alert Rules** – Allows users to define threshold-based alerts when multiple sources converge on specific match events.

- **Data Provenance Tracker** – Records source origin, fetch time, and transformation history for every piece of aggregated information.

## 应用场景

- **Sports Journalism Research** – Journalists covering football matches can use SoccerForge AI to quickly gather diverse pre-match opinions and statistical backgrounds from multiple specialized sources, ensuring balanced and well-informed reporting without manually visiting each website.

- **Tactical Performance Analysis** – Coaches and video analysts can cross-reference red-card statistics and match prediction trends to identify opponents' disciplinary patterns, helping to adjust training focuses and in-game tactical decisions.

- **Academic Benchmarking** – Researchers in sports informatics and predictive modeling can utilize the aggregated data to compare their own forecasting algorithms against established public models, using the timestamped archives for reproducible experiments.

- **Fantasy Football Strategy Development** – Advanced fantasy league players can leverage the recommendation comparison module to evaluate player selection signals and injury-influenced performance estimates across multiple forecasting systems.

- **Data Journalism Education** – University courses in data journalism and sports analytics can use SoccerForge AI as a teaching case study for web resource integration, data normalization, and multi-source credibility assessment.

## 快速开始

The following procedure sets up a local instance of SoccerForge AI for development or personal research use.

```bash
# Clone the repository from the official source
git clone https://github.com/soccerforge-ai/soccerforge-core.git
cd soccerforge-core

# Install Python dependencies using pip with pinned versions
pip install -r requirements.txt

# Copy environment template and configure your local settings
cp .env.example .env

# Initialize the local SQLite database schema
python scripts/init_db.py

# Run the aggregator service in development mode
python main.py --mode aggregator --sources all --interval 3600
```

For production deployment, refer to the deployment guide in the documentation section.

## 安装要求

SoccerForge AI requires a modern Python runtime and several system-level dependencies for full functionality. All required packages are listed with exact version constraints to ensure reproducibility.

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.10 或更高 | 核心运行时，用于执行聚合器、API 服务和定时任务 |
| pip | 22.0+ | Python 包管理器，用于安装 requirements.txt 中列出的依赖 |
| SQLite | 3.35+ | 内置嵌入式数据库，用于存储元数据、快照和查询索引 |
| Redis | 6.2+ | 可选缓存层，用于提升高频查询响应速度和跨进程状态同步 |
| Requests | 2.28.2 | HTTP 客户端库，用于从外部资源获取 HTML 和数据馈送 |
| BeautifulSoup4 | 4.11.1 | HTML 解析库，用于提取结构化内容并清理非标准标记 |
| lxml | 4.9.2 | 高性能 XML/HTML 解析器，作为 BeautifulSoup 的后端加速 |
| pandas | 1.5.3 | 数据处理库，用于整理和归一化不同来源的表格型数据 |
| Flask | 2.2.3 | Web 框架，提供 API 接口和简易的管理仪表板 |
| gunicorn | 20.1.0 | WSGI 服务器，用于生产环境下的多进程 API 服务托管 |

## 文档导航

SoccerForge AI documentation is organized into four main layers, each targeting a specific audience and answering distinct questions about the system.

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/ | 如何使用聚合查询、如何配置自定义警报、如何解读交叉参考结果？ |
| 开发指南 | /docs/developer-guide/ | 如何添加新的数据源、如何修改解析规则、如何扩展 API 端点？ |
| 运维手册 | /docs/ops-guide/ | 如何部署生产环境、如何设置定时快照、如何监控系统健康度？ |
| 算法白皮书 | /docs/algorithms/ | 各预测源的数学基础是什么、一致性评分如何计算、误差指标如何定义？ |

Additional API reference is generated automatically from docstrings and available at `/docs/api/` after local server startup.

## 资源列表

本项目索引并定期聚合以下十个独立的足球分析资源域名。每个域名均按用户原始输入原样列出，未做任何格式修改或协议补全。

### 比赛分析与预测核心资源

- <code>zuqiusaiqianfenxi.org.cn</code>
- <code>zuqiuhongdanyuce.org.cn</code>
- <code>zuqiuhongdanfenxi.org.cn</code>
- <code>zuqiutuijianwang.org.cn</code>
- <code>zuqiuyucezhongxin.org.cn</code>

### 预测与推荐辅助资源

- <code>zuqiuyucewang.org.cn</code>
- <code>zuqiufenxiwang.org.cn</code>
- <code>zuqiutuijianjiqiao.org.cn</code>
- <code>zuqiuyucejiqiao.org.cn</code>
- <code>zuqiuyucemoxing.org.cn</code>

These resources are accessed via HTTP GET requests with appropriate User-Agent headers and respectful crawl delays. The project does not scrape content at sub-second intervals; all fetches comply with robots.txt directives where applicable.

## 项目结构

The source tree follows a modular monolith design, with clear separation between data ingestion, processing, storage, and presentation layers.

```
soccerforge-core/
├── main.py                  # 主入口，支持 aggregator / api / snapshot 三种运行模式
├── requirements.txt         # Python 依赖锁定文件，用于生产环境安装
├── .env.example             # 环境变量模板，包含数据库路径、缓存地址和日志级别
├── config/
│   ├── settings.py          # 全局配置加载逻辑，支持 YAML 覆盖
│   ├── sources.yaml         # 定义所有十个外部资源的 URL、解析规则和更新频率
│   └── logging.yaml         # 日志格式、输出目标和滚动策略配置
├── core/
│   ├── fetcher.py           # 异步 HTTP 获取器，带重试和超时控制
│   ├── parser.py            # 基于 BeautifulSoup 和 lxml 的内容提取器
│   ├── normalizer.py        # 将不同来源的数据转换为统一内部 Schema
│   ├── correlator.py        # 计算源间一致性评分和共识信号
│   └── archive.py           # 快照归档管理，支持增量存储和版本回滚
├── api/
│   ├── routes.py            # Flask 路由定义，包括 /query、/sources、/alerts
│   ├── serializers.py       # JSON 响应序列化器，处理 datetime 和 Decimal 类型
│   └── middleware.py        # 请求日志、CORS 头和速率限制中间件
├── models/
│   ├── source.py            # 外部资源的数据模型（URL、状态、最后抓取时间）
│   ├── match.py             # 比赛元数据模型（主队、客队、开赛时间、联赛）
│   ├── prediction.py        # 预测记录模型（主胜概率、平局概率、客胜概率、红牌指数）
│   └── alert.py             # 用户自定义警报规则模型
├── scripts/
│   ├── init_db.py           # 初始化 SQLite 数据库表结构和索引
│   ├── seed_sources.py      # 将 sources.yaml 中的初始数据导入数据库
│   └── daily_snapshot.py    # 定时任务脚本，每天 00:00 UTC 触发全量更新
├── tests/
│   ├── test_fetcher.py      # 模拟网络请求的单元测试
│   ├── test_parser.py       # 使用示例 HTML 片段测试解析逻辑
│   └── test_correlator.py   # 验证一致性评分算法的正确性
└── docs/
    ├── user-guide/          # 用户手册 Markdown 文件
    ├── developer-guide/     # 开发指南 Markdown 文件
    ├── ops-guide/           # 运维手册 Markdown 文件
    └── algorithms/          # 算法白皮书，包含数学公式和参考文献
```

Each directory contains an `__init__.py` file to enable Python package imports. The `scripts/` folder is not part of the runtime package but is executed separately via cron or systemd timers.

## 贡献指南

We welcome contributions that improve data source coverage, parsing robustness, or correlation algorithms. All contributions must adhere to the project's code style and testing requirements.

1.  **Fork 仓库并创建功能分支** – 从主仓库 fork 到个人账户，然后基于 `develop` 分支创建 `feature/your-feature-name` 分支。分支命名应清晰描述改动内容。

2.  **编写或更新单元测试** – 所有新增解析器或修改核心逻辑的变更必须附带对应的测试用例。测试覆盖率不应低于当前主干分支的基准线。

3.  **运行完整测试套件** – 在提交前执行 `pytest tests/` 确保所有测试通过，且无新增警告或错误。本地环境需与 CI 保持一致的 Python 版本。

4.  **更新文档和变更日志** – 如果改动影响用户可见功能或配置格式，须同步更新 `/docs/` 下的相关手册，并在 `CHANGELOG.md` 中记录变动条目。

5.  **发起 Pull Request 并等待审查** – PR 描述应包含改动动机、实现方法和测试结果摘要。至少需要一位核心维护者批准后方可合并。

For major architectural changes, please open a discussion issue before starting implementation to align with the project roadmap.

## 常见问题

**Q1: SoccerForge AI 是否提供直接的比赛胜负预测或投注建议？**

不提供。本项目是技术资源聚合和信息索引工具，而非预测引擎或投注决策系统。所有外部来源的预测数据均以原始形式呈现，并附带来源标识和时间戳，用户需自行评估信息可靠性。任何形式的一致性评分或共识信号仅表示统计上的趋同，不构成任何形式的保证或建议。

**Q2: 某些资源域名无法访问或返回空数据时如何处理？**

系统内置了指数退避重试机制，在首次失败后会间隔 5 秒、10 秒、30 秒重试三次。若三次均失败，该源会被标记为暂时不可用，并在日志中记录详细错误。聚合器会继续处理其他可用源，并在下一个周期（默认为 3600 秒后）重新尝试该源。用户可以通过 API 端点 `/sources/status` 实时查看每个源的可用性状态。

**Q3: 如何添加自定义的外部资源？**

您需要修改 `config/sources.yaml` 文件，按照已有条目的格式添加新源的名称、根 URL、解析规则（CSS 选择器或 XPath）、更新频率和数据类型。添加后，运行 `python scripts/validate_sources.py` 验证配置的正确性，然后重启聚合器服务。若希望新源被纳入共识计算，还需在 `core/normalizer.py` 中注册对应的归一化映射函数。

## 许可证

MIT License

Copyright (c) 2026 SoccerForge AI Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
