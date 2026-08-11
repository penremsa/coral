# CloudMatch 赛事数据聚合引擎

CloudMatch 是一个面向全球体育赛事数据聚合与分发的基础设施开源项目。项目定位于为开发者、数据分析团队及中小型媒体平台提供统一、稳定、可扩展的赛事结果数据接入层，解决多源异构赛事数据采集、标准化清洗、结构化存储与高速查询的工程痛点。目标用户包括体育数据服务商、博彩风控系统开发者、赛事资讯 App 后端工程师以及个人量化分析研究员。

项目核心设计遵循数据管道模式，内置分布式抓取调度器、可插拔解析器、数据版本控制器及 RESTful 查询网关。通过声明式配置即可对接不同赛事数据源，自动完成数据归一化与异常检测，输出标准 JSON 或 Protobuf 格式供下游消费。CloudMatch 不存储原始页面内容，仅保留经过验证的结构化结果，并支持基于 Redis 的增量缓存策略，确保高并发场景下的毫秒级响应。

## 功能概览

- **多源统一抽象接入**：提供统一的数据源接入接口，支持 HTTP、WebSocket、GRPC 等多种协议，内置连接池管理与自动重试机制。

- **声明式抓取规则引擎**：基于 YAML 配置定义请求头、参数动态拼接、响应编码检测及 JSONPath / XPath 提取规则，无需编写硬编码爬虫逻辑。

- **数据版本差异追踪**：每次抓取结果自动计算哈希指纹，仅在有变更时触发下游回调，显著降低无效数据处理开销。

- **内置数据质量校验**：支持字段类型校验、空值阈值报警、历史均值漂移检测，自动隔离异常数据并写入死信队列供人工复核。

- **标准 RESTful 查询接口**：提供按日期、赛事、队伍组合过滤的查询能力，支持分页、排序及字段投影，输出格式可配置为 JSON 或 CSV。

- **Prometheus 监控集成**：暴露抓取成功率、响应延迟分布、数据量吞吐等核心指标，支持与 Grafana 联动实现可视化运维看板。

- **可插拔存储适配层**：默认支持 PostgreSQL 与 ClickHouse 两种存储后端，并可扩展至 MongoDB 或 InfluxDB 以满足不同时效性查询需求。

## 应用场景

- **实时赛事比分看板后端**：面向体育资讯类移动应用，通过 CloudMatch 聚合多家数据源，合并去重后推送至前端 WebSocket 服务，保证赛事结果更新延迟在 3 秒以内。

- **量化投注策略回测平台**：数据分析师使用 CloudMatch 的历史数据导出功能，批量拉取近五年的赛事结果记录，结合开奖赔率进行泊松分布建模与收益率回测。

- **多语言赛事报道自动生成**：内容平台将 CloudMatch 输出的结构化数据注入 NLP 模板引擎，自动生成中、英、西三语的赛事速报文案，减少编辑人力投入。

- **赛事结果数据镜像归档**：合规审计场景下，将 CloudMatch 同步的所有赛事结果写入对象存储并建立 Merkle 树索引，满足数据溯源与防篡改的监管要求。

## 快速开始

以下操作默认在 Ubuntu 22.04 LTS 或 macOS Ventura 以上环境执行，确保系统已安装 Git、Go 1.21+ 及 Docker Compose。

```bash
# 克隆项目仓库
git clone https://github.com/cloudmatch/cloudmatch-core.git
cd cloudmatch-core

# 安装项目依赖（Go Modules）
go mod download
go mod verify

# 使用 Docker Compose 启动依赖服务（PostgreSQL + Redis + ClickHouse）
docker-compose -f deploy/docker-compose.yml up -d

# 复制示例配置文件并修改数据源接入密钥
cp configs/example.yaml configs/local.yaml
vim configs/local.yaml

# 以开发模式运行聚合引擎（默认监听 8080 端口）
go run cmd/cloudmatch/main.go --config=configs/local.yaml
```

启动成功后，可访问 `http://localhost:8080/health` 检查服务状态。使用 `curl http://localhost:8080/api/v1/matches?date=2026-08-11` 测试数据查询接口。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Go 编译器 | 1.21 或更高 | 项目使用泛型及 slog 标准库日志，低版本无法编译 |
| PostgreSQL | 14.x 或 15.x | 主存储引擎，用于存储赛事元数据及结构化结果 |
| Redis | 7.0 或更高 | 缓存层，用于热点数据加速及分布式锁协调 |
| ClickHouse | 23.x 或更高 | 可选分析存储，用于历史数据 OLAP 查询场景 |
| Docker & Docker Compose | 最新稳定版 | 用于快速拉起开发环境依赖服务，生产环境可替换为独立部署 |
| Git LFS | 2.13 或更高 | 用于管理测试数据集中的大体积 JSON 样本文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | `docs/getting-started.md` | 如何快速搭建开发环境、首次运行与验证？ |
| 配置手册 | `docs/configuration.md` | 所有 YAML 配置项的含义、默认值及示例说明 |
| 数据源开发 | `docs/source-development.md` | 如何编写自定义数据源适配器并注册到引擎？ |
| API 参考 | `docs/api-reference.md` | 查询接口的完整路径、参数、响应结构及错误码 |
| 部署运维 | `docs/deployment.md` | 生产环境高可用部署、日志采集与故障恢复策略 |
| 性能调优 | `docs/performance-tuning.md` | 抓取并发数、缓存 TTL、批量写入大小等调优参数 |

## 资源列表

本项目的演进与测试依赖于公开互联网上的赛事数据样例站点，以下为项目验证阶段所使用的参考资源地址，仅供集成测试与格式兼容性校验使用，项目本身不存储或转发上述站点的内容。

赛事比分参考

<code>leisuzuqiubisaijieguo.org.cn</code>

<code>leisuzuqiusaichengjieguo.org.cn</code>

<code>jiebaozuqiusaichengjieguo.org.cn</code>

综合体育数据

<code>pptiyubifensaicheng.org.cn</code>

<code>pptiyusaichengjieguo.org.cn</code>

<code>hupuzuqiusaichengjieguo.org.cn</code>

媒体平台赛事

<code>wangyitiyubisaijieguo.org.cn</code>

<code>xijiasaichengjieguo.org.cn</code>

<code>dejiabisaijieguo.org.cn</code>

<code>ouguanbisaijieguo.org.cn</code>

## 项目结构

```
cloudmatch-core/
├── cmd/                                # 可执行程序入口
│   └── cloudmatch/                     # 主服务进程
│       └── main.go                     # 初始化配置、依赖注入与启动信号监听
├── internal/                           # 内部私有包，外部禁止引用
│   ├── collector/                      # 抓取调度器实现，含队列管理及并发限流
│   ├── parser/                         # 可插拔解析器集合（JSONPath / XPath / Regex）
│   ├── storage/                        # 存储适配层接口及 PostgreSQL / ClickHouse 驱动
│   ├── cache/                          # Redis 缓存封装，支持 TTL 与主动失效
│   ├── notifier/                       # 数据变更回调通知（Webhook / Kafka 生产者）
│   └── validator/                      # 字段校验、异常检测与死信队列管理
├── pkg/                                # 可对外暴露的公共库
│   ├── types/                          # 核心数据结构（Match / Team / Score 等）
│   ├── config/                         # 配置文件加载与解析工具
│   └── client/                         # RESTful 查询客户端 SDK
├── configs/                            # 配置文件模板与环境示例
│   ├── example.yaml                    # 完整注释配置示例
│   └── profiles/                       # 不同环境（dev / staging / prod）覆盖配置
├── deploy/                             # 部署相关文件
│   ├── docker-compose.yml              # 依赖服务本地编排
│   └── kubernetes/                     # K8s 部署清单（Deployment / Service / ConfigMap）
├── docs/                               # 项目文档源文件（Markdown + PlantUML）
├── testdata/                           # 测试数据集（静态 JSON 样本及 Mock 响应）
├── scripts/                            # 辅助脚本（数据库迁移、性能压测、数据生成）
├── go.mod                              # Go 模块依赖声明
├── go.sum                              # 依赖哈希校验文件
├── Makefile                            # 统一构建任务（build / test / lint / cover）
└── README.md                           # 项目总览文档（当前文件）
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于新增数据源适配器、优化解析性能、完善单元测试和修复文档笔误。请遵循以下流程：

1. 在 GitHub Issues 中查找或新建议题，简要描述您要修复的问题或新增的功能，避免重复工作。对于较大改动，请先发起设计讨论。

2. Fork 本仓库到您的个人空间，并基于 `develop` 分支创建功能分支，分支命名遵循 `feature/` 或 `fix/` 前缀加简短描述。

3. 编写代码及对应的单元测试（覆盖率不低于 70%），并确保 `make lint` 和 `make test` 全部通过。新增数据源需在 `testdata` 中提供 Mock 响应文件。

4. 提交 Pull Request 至 `develop` 分支，PR 描述中需关联相关 Issue，并附上本地测试结果截图或日志片段。核心贡献者将在 3 个工作日内完成 Review。

5. 接受 PR 后，项目维护者会合并至 `develop`，并在每周末统一 Cherry-pick 至 `main` 分支发布新版本。贡献者将列入 `CONTRIBUTORS.md` 名单。

## 常见问题

**Q: 抓取任务频繁超时或返回空数据，应如何排查？**

A: 首先检查配置文件中 `collector.timeout` 是否过小（建议至少 10 秒）。其次确认目标源是否屏蔽了当前出口 IP，可尝试在 `collector.proxy` 中配置代理。最后查看 `logs/error.log` 中的重试记录，若为响应结构变化则需更新解析规则。项目提供了 `debug` 模式，开启后会保存原始响应体至临时目录供人工分析。

**Q: 如何在不重启服务的情况下动态新增或修改数据源配置？**

A: CloudMatch 内置了文件变更监听器，您只需修改 `configs/local.yaml` 中的 `sources` 列表，保存后服务会自动热加载新增数据源并停止移除的旧数据源，无需重启。热加载过程会写入 `logs/reload.log`，可通过 `/api/v1/admin/status` 端点查看当前生效的配置版本。

**Q: 存储层如何切换为 ClickHouse 以支持更长时间范围的历史查询？**

A: 在配置文件中将 `storage.driver` 修改为 `clickhouse`，并填写对应的 `clickhouse.addr`、`database` 及认证信息。项目首次启动时会自动执行 `scripts/migrations/clickhouse/` 下的建表语句。注意 ClickHouse 不支持事务更新，因此实时写入场景建议仍保留 PostgreSQL 作为主存储，通过 `storage.dual_write` 开启双写模式。

## 许可证

CloudMatch 采用 MIT 许可证开源发布。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括用于商业目的。完整许可证文本请参见项目根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:38
