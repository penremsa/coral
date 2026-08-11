# Hyperlink Atlas

Hyperlink Atlas is a curated, high-performance technical resource aggregation and navigation system. It is designed for developers, data analysts, and technical researchers who require reliable, up-to-date external links to specialized data sources. The project does not host or generate data; instead, it provides a structured, version-controlled, and machine-readable index of external URLs, organized by category, with metadata for validation and accessibility. The primary goal is to eliminate link rot, reduce search friction, and offer a centralized, verified starting point for accessing niche or dynamic web resources. Target users include automation engineers building scrapers, analysts requiring consistent data entry points, and open-source projects that depend on external reference data.

The system operates as a static site generator and a command-line interface tool. It validates each linked resource for HTTP response status, content-type, and response time, generating a health report. This ensures that every URL in the index is not only syntactically correct but also semantically accessible at the time of the last check. The project emphasizes transparency, reproducibility, and ease of integration, making it suitable for both interactive browsing and automated CI/CD pipelines.

## 功能概览

- **结构化资源索引** – 提供按领域和用途分类的链接集合，采用 YAML 和 JSON 双格式存储，便于程序解析。
- **自动健康检查** – 每日定时验证所有链接的可达性，记录状态码、响应时间和重定向链，生成可视化报告。
- **命令行交互工具** – 提供 `hl-atlas check`、`hl-atlas list`、`hl-atlas export` 等子命令，支持过滤、排序和格式转换。
- **静态导航站点生成** – 基于模板引擎生成响应式 HTML 页面，包含搜索、分类筛选和链接状态徽章，适合内网部署。
- **变更追踪与审计日志** – 记录每次资源列表的增删改操作，支持回滚和差异对比，满足合规需求。
- **自定义标签与注解** – 允许用户为每个链接添加键值对元数据，如维护者、更新频率、数据格式等，增强可管理性。
- **多格式导出** – 支持将索引导出为 CSV、Markdown 表格、RSS 订阅源和 Prometheus 指标格式，适配不同消费端。

## 应用场景

- **数据采集管道初始化** – 数据工程师可在 ETL 流程中通过 Hyperlink Atlas 获取最新源地址，避免因链接变更导致任务失败。系统提供的健康检查接口可作为前置断言，确保采集前所有源站可用。
- **研究文献参考管理** – 学术团队可维护特定领域的资源集合，通过注解字段标注数据来源、更新时间及使用限制，便于协作审阅和成果溯源。
- **企业内部导航门户** – 企业可将 Hyperlink Atlas 部署为内部技术资源门户，聚合各团队常用的 API 文档、监控面板和内部工具地址，搭配权限分级视图。
- **开源项目依赖外链验证** – 开源项目维护者可将该项目集成至 CI 流程，自动检测文档或配置文件中的外部链接是否失效，提前发现断裂引用。

## 快速开始

以下指令适用于 Linux 和 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 克隆仓库
git clone https://github.com/hyperlink-atlas/hyperlink-atlas.git
cd hyperlink-atlas

# 安装依赖（使用 pip 和 npm）
pip install -r requirements.txt
npm install --global @hyperlink-atlas/cli

# 初始化配置并运行首次健康检查
hl-atlas init --config ./config.yaml
hl-atlas check --all --output report.json

# 生成静态站点
hl-atlas build --source ./data/index.yaml --dest ./public
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 或更高 | 用于核心检查引擎和数据处理，推荐使用 3.11 |
| Node.js | 18.x 或 20.x LTS | 用于 CLI 工具和前端构建，需包含 npm |
| Git | 2.30 以上 | 用于版本管理和贡献流程，支持子模块 |
| YAML 解析库 (PyYAML) | 6.0.1 | Python 环境下的 YAML 读写依赖 |
| HTTPX | 0.27.0 | 异步 HTTP 客户端，用于并发健康检查 |
| Jinja2 | 3.1.2 | 模板引擎，用于生成静态 HTML 页面 |
| Pytest | 8.0.0 (可选) | 单元测试框架，仅在开发环境中需要 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何安装、配置、运行检查以及定制索引？ |
| 开发者指南 | `/docs/developer-guide/` | 如何扩展检查器、添加新数据源或提交补丁？ |
| API 参考 | `/docs/api-reference/` | 各模块和命令行接口的详细参数说明？ |
| 运维手册 | `/docs/operations/` | 如何部署、监控、备份及故障恢复？ |

## 资源列表

### 足球比分与赛事结果类

- <code>jingcaizuqisaichengjieguo.org.cn</code>
- <code>jiebaozuqiubifenjishibifenshoujiban.net.cn</code>
- <code>qiutanzuqiubifenwang.net.cn</code>
- <code>qiutanzuqiubifenshoujiwang.net.cn</code>
- <code>qiutanzuqiujishibifenshoujiban.net.cn</code>
- <code>jiebaozuqiubifenguanwang.org.cn</code>

### 综合比分数据类

- <code>500jingcaizuqiubifen.org.cn</code>
- <code>500bifenwanzhengban.org.cn</code>
- <code>500zuqiubifenwanzhengban.org.cn</code>
- <code>500zuqiuwanzhengbifen.org.cn</code>

## 项目结构

```
hyperlink-atlas/
├── src/                           # 核心源代码目录
│   ├── checker/                   # 健康检查模块，包含 HTTP 验证器
│   │   ├── async_client.py        # 异步请求池与超时控制
│   │   └── reporter.py            # 生成 JSON/HTML 格式报告
│   ├── cli/                       # 命令行接口实现
│   │   ├── main.py                # 入口解析与子命令路由
│   │   └── commands/              # 各子命令具体逻辑 (check, build, list)
│   ├── index/                     # 资源索引解析和管理
│   │   ├── loader.py              # 读取 YAML/JSON 并校验格式
│   │   └── validator.py           # 强制字段及类型检查
│   └── web/                       # 静态站点生成器
│       ├── templates/             # Jinja2 模板文件 (.html)
│       └── assets/                # CSS、JavaScript、图标资源
├── data/                          # 数据存储目录
│   ├── index.yaml                 # 主资源索引文件 (用户可编辑)
│   ├── snapshots/                 # 历史健康检查快照 (按日期归档)
│   └── audit.log                  # 资源变更操作日志
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 模块级测试
│   └── integration/               # 端到端测试 (含模拟网络)
├── docs/                          # 完整文档，含 markdown 和图片
├── scripts/                       # 辅助脚本 (初始化、备份、迁移)
├── config.yaml.example            # 配置模板 (含超时、重试、通知)
├── requirements.txt               # Python 生产依赖列表
├── package.json                   # Node.js 项目元数据和构建脚本
├── Makefile                       # 常用任务快捷方式 (install, test, build)
└── README.md                      # 本文件
```

## 贡献指南

1.  **问题报告与建议** – 使用 GitHub Issues 提交 bug 或功能请求，请附上复现步骤、日志片段或预期行为描述。对于链接失效报告，建议提供 `hl-atlas check --url <URL>` 的输出。
2.  **分支开发流程** – 从 `main` 签出新的特性分支，命名遵循 `feat/` 或 `fix/` 前缀。提交信息需符合 Conventional Commits 规范，确保变更历史清晰。
3.  **测试覆盖** – 所有新增或修改的检查器逻辑必须附带对应的单元测试，位于 `tests/unit/` 目录。运行 `pytest` 确保全部测试通过且覆盖率不低于 85%。
4.  **文档同步** – 若修改了命令行参数或配置项，需同步更新 `docs/user-guide/` 中的对应章节，并运行 `make docs` 检查渲染效果。
5.  **拉取请求** – 提交 PR 前请进行自我审查，确保无调试代码、无关文件或格式问题。PR 描述需清晰说明变更动机、实现方式和影响范围。

## 常见问题

**问：健康检查是否会过度请求目标服务器，导致我的 IP 被封禁？**

答：项目默认采用指数退避策略，并发数限制为 5，且每 10 秒启动一轮检查，避免突发流量。用户可在 `config.yaml` 中调整 `max_concurrent` 和 `delay_between_requests` 参数。对于敏感目标，建议配置 `robots_policy` 尊重目标站的爬虫协议，或手动设置检查频率为每日一次。

**问：如何导入我自己的链接集合，而不使用默认的索引文件？**

答：您可以使用 `hl-atlas import --format csv --path my_links.csv` 命令将 CSV 文件转换为项目内部格式，并合并至 `data/index.yaml`。支持格式包括 CSV、JSON 和纯文本列表。导入时会自动执行去重和格式校验，并提供冲突报告供人工确认。

**问：静态站点生成后，如何添加身份验证或访问控制？**

答：本项目生成的站点是纯静态 HTML，本身不包含认证机制。推荐使用 Web 服务器层（如 Nginx 的 basic_auth 或 OAuth2 代理）或部署在内部网络环境。对于企业级需求，可基于 `src/web/` 模块二次开发，集成 JWT 或 LDAP 验证逻辑，但需注意这会偏离上游设计。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
