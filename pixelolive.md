# 资源导航聚合系统

Resource Navigation Aggregator (RNA) 是一个面向技术内容创作者、数字档案管理员及研究人员的垂直领域资源索引平台。本项目不直接托管或分发任何第三方内容，而是提供结构化、可维护的外部资源引用目录，帮助用户快速定位特定主题的公开网络资源。系统核心定位为“只读型资源地图”，通过明确的分类标签与摘要信息，降低信息检索成本，适用于需要批量管理、审核或归档网络公开链接的工作流。

本项目的目标用户包括内容安全审核员、网络数据分析师、开源情报（OSINT）研究者以及合规性审查团队。系统内置了链接状态检测、访问频率统计与基础元数据提取模块，能够辅助用户判断外部资源的可用性与类别倾向，从而提升大规模链接库的运维效率。项目遵循最小化数据存储原则，不缓存任何外部资源内容，仅存储用户主动提交的 URL 与自定义标签。

## 功能概览

- **批量链接导入与解析**：支持通过 CSV、JSON 或纯文本行批量导入外部 URL，系统自动解析域名、路径层级与查询参数，并提取基础网络协议信息。

- **自定义分类标签系统**：允许用户为每个链接分配多级标签（如“地域-亚洲”“类别-影视”“属性-公开档案”），标签体系支持动态增删改，并基于标签组合生成筛选视图。

- **链接可达性健康检查**：内置异步 HTTP/HTTPS 探针，可配置超时与重试策略，定期检测每个链接的响应状态码、响应时间与重定向链，并将异常结果汇总至仪表盘。

- **访问日志与统计看板**：记录每个外部链接的点击次数、最后访问时间与引用来源（Referer），提供基于时间维度的热度趋势图，支持按域名聚合统计。

- **元数据自动补全**：对特定域名（如主流视频平台、文档分享站）尝试通过 Open Graph 协议或结构化数据标记抓取页面标题与描述，作为人工编辑的参考依据。

- **只读只写分离的权限模型**：支持多用户角色划分（管理员、编辑员、观察员），编辑员仅可管理链接元数据与标签，观察员仅拥有查询与导出权限。

- **全量数据导入导出接口**：提供 RESTful API 与命令行工具，支持将整个链接库导出为 JSON、XML 或 Markdown 表格格式，便于离线备份或迁移至其他系统。

## 应用场景

- **内容合规性批量复审**：企业合规团队可定期将待审核的外部资源链接导入系统，利用标签过滤与健康检查功能，优先处理失效或响应异常的链接，并生成审核报告用于存档。

- **学术研究参考文献整理**：研究人员在收集网络公开数据源时，可使用本系统建立带注释的链接目录，按地域、语种或主题分类，并共享给协作组成员，确保引用路径的可追溯性。

- **开源情报线索管理**：OSINT 分析师将分散在多个报告中的线索链接统一录入系统，通过访问日志追踪线索的活跃度，结合自定义标签标记置信度与情报来源，形成结构化的情报知识库。

- **网站迁移与重构辅助**：在进行网站改版或域名迁移时，运维团队可利用本系统的链接可达性检查功能，批量验证旧域名的重定向状态，识别需要更新的内部引用或外部依赖。

- **数字档案长期保存规划**：档案管理人员使用本系统监控外部引用链接的生命周期状态，对频繁失效的域名启动替代源查找流程，确保数字档案中的引用路径持续有效。

## 快速开始

以下步骤适用于在 Linux 服务器或本地开发环境（需预先安装 Git、Node.js 18+ 与 npm）中部署本项目。

```bash
# 克隆项目仓库
git clone https://github.com/example/resource-navigation-aggregator.git

# 进入项目目录
cd resource-navigation-aggregator

# 安装生产依赖
npm install --production

# 复制环境变量模板并修改数据库连接等配置
cp .env.example .env

# 执行数据库迁移脚本（使用 SQLite 或 PostgreSQL）
npm run migrate

# 启动服务，默认监听 3000 端口
npm start
```

访问 `http://localhost:3000` 即可进入系统首页。首次启动将自动创建默认管理员账户，初始密码可在启动日志中查看，请务必在首次登录后修改密码。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x LTS 或更高 | 运行时环境，建议使用 Active LTS 版本以保证稳定性 |
| npm | 9.x 或更高 | 包管理器，随 Node.js 一同安装 |
| SQLite | 3.35 或更高 | 默认内嵌数据库，适用于单机或小规模部署；生产环境可切换为 PostgreSQL |
| Redis | 7.0 或更高 | 可选依赖，用于会话存储与高频访问缓存；未安装时将降级为内存缓存 |
| Git | 2.30 或更高 | 用于版本克隆与后续增量更新 |
| 系统内存 | 最低 512 MB，推荐 2 GB | 数据库缓存与并发探针任务均占用内存，建议根据链接总数调整 |
| 磁盘空间 | 最低 200 MB | 用于存储数据库文件与日志，日志可按策略自动轮转 |
| 网络出口 | 允许出站 TCP 80/443 | 健康检查模块需要对外部链接发起 HTTP 请求，需确保防火墙放行 |
| 时区设置 | UTC+8 推荐 | 统计看板的时间聚合依赖系统时区，建议与运维团队统一 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何导入链接、分配标签、查看健康报告以及导出数据 |
| 管理员手册 | `/docs/admin-guide/` | 如何配置探针参数、管理用户权限、调整日志级别与执行数据库备份 |
| API 参考 | `/docs/api-reference/` | 所有 RESTful 接口的请求/响应格式、鉴权方式与状态码含义 |
| 部署指南 | `/docs/deployment/` | 使用 Docker Compose 或 Kubernetes 进行容器化部署的完整配置文件与说明 |
| 贡献者规范 | `/docs/contributing/` | 代码风格、提交信息格式、PR 审查流程与测试覆盖率要求 |
| 常见故障 | `/docs/troubleshooting/` | 探针超时、数据库锁定、内存溢出等常见问题的排查步骤与解决方案 |

## 资源列表

本系统作为资源导航聚合器，初始内置了一批公开可访问的外部链接作为演示数据集。这些链接按照内容主题进行初步分类，仅供系统功能演示与测试用途。用户可根据自身需求随时删除或替换以下链接。

影视与视频内容类

- <code>fengmanrenqishipin.org.cn</code>
- <code>rihanyoumadianying.org.cn</code>
- <code>lingleixiaoshuoshipin.org.cn</code>
- <code>oumeijiqingsetu.org.cn</code>

特定主题资源类

- <code>mitunjiujiujingpinjiujiujiujiu.org.cn</code>
- <code>dapukeyoutengyoujiao.org.cn</code>
- <code>zhongwenzimushunvrenqi.org.cn</code>

区域分类资源类

- <code>yazhoubiantailinglei.org.cn</code>
- <code>yazhouzipaisetu.org.cn</code>
- <code>seqiqiyazhou.org.cn</code>

## 项目结构

```
resource-navigation-aggregator/
├── src/
│   ├── core/                          # 核心业务逻辑模块
│   │   ├── link-parser.js             # URL 解析、归一化与域名提取
│   │   ├── tag-engine.js             # 标签增删改查与组合筛选逻辑
│   │   └── health-checker.js         # 异步探针调度、超时与重试策略
│   ├── api/                           # RESTful 接口路由与控制器
│   │   ├── v1/                        # API 版本 v1 路由定义
│   │   │   ├── links.js              # 链接 CRUD 与批量导入端点
│   │   │   ├── tags.js               # 标签管理端点
│   │   │   └── stats.js              # 统计与看板数据聚合端点
│   │   └── middleware/                # 鉴权、日志、限流与错误处理中间件
│   ├── db/                            # 数据库抽象层与迁移脚本
│   │   ├── models/                    # Sequelize 或 TypeORM 实体定义
│   │   ├── migrations/               # 版本化数据库迁移文件
│   │   └── seeders/                  # 初始演示数据填充脚本
│   ├── workers/                       # 后台任务队列（Bull 或 Agenda）
│   │   ├── probe-queue.js            # 链接健康检查任务队列定义
│   │   └── metadata-fetcher.js       # 元数据自动补全异步任务
│   └── utils/                         # 通用工具函数（日志、加密、验证）
│       ├── logger.js                  # Winston 日志封装
│       ├── validator.js              # 输入校验与安全过滤
│       └── exporter.js               # JSON/CSV/Markdown 导出生成器
├── config/                            # 环境配置文件（按 NODE_ENV 加载）
│   ├── default.json                   # 基础配置（端口、日志级别、探针默认参数）
│   ├── development.json               # 开发环境覆盖配置
│   └── production.json               # 生产环境覆盖配置（关闭调试、启用缓存）
├── docs/                              # 完整文档目录（与文档导航对应）
├── tests/                             # 单元测试与集成测试用例
│   ├── unit/                          # 独立函数与模块测试
│   └── integration/                   # API 与数据库交互测试
├── scripts/                           # 运维辅助脚本
│   ├── backup-db.sh                  # 数据库定时备份脚本
│   └── health-check-cli.js           # 命令行手动触发链接检查工具
├── .env.example                       # 环境变量模板（含数据库连接串、密钥占位）
├── docker-compose.yml                 # 含 Redis、PostgreSQL 的完整容器编排
├── Dockerfile                         # 基于 node:18-alpine 的生产镜像构建
├── package.json                       # npm 依赖声明与脚本命令
└── README.md                          # 本文件
```

## 贡献指南

1. **问题追踪与需求讨论**：请在 GitHub Issues 中搜索是否已有类似问题，若无则新建 Issue，并按照模板填写复现步骤、环境信息与期望行为。对于新功能建议，请详细说明应用场景与业务价值。

2. **派生仓库与分支开发**：将本仓库 Fork 至个人账户，并基于 `main` 分支创建功能分支（命名格式为 `feature/简短描述` 或 `fix/问题编号`）。禁止直接在 `main` 分支上进行修改。

3. **代码规范与测试覆盖**：提交代码前请运行 `npm run lint` 检查代码风格（基于 ESLint + Prettier），并确保新增或修改的功能包含对应的单元测试与集成测试，整体测试覆盖率不得低于 85%。

4. **提交信息格式**：遵循 Conventional Commits 规范（如 `feat: 添加批量导入进度条`、`fix: 修复探针超时导致的内存泄漏`、`docs: 更新部署指南中的 Redis 配置`），提交信息应清晰描述变更内容与影响范围。

5. **发起 Pull Request**：将功能分支推送至个人远程仓库后，向本仓库的 `main` 分支发起 Pull Request。PR 描述中需关联相关 Issue，并简要说明实现方案、测试结果与可能的破坏性变更。至少需要一位项目维护者批准后方可合并。

## 常见问题

**问：系统自带的健康检查是否会对外部网站造成压力或被视为攻击？**

答：健康检查模块采用指数退避重试策略，每个链接的检查间隔不小于 10 秒，且单次检查仅发起一次 HEAD 请求（若目标服务器支持），随后视情况回退至 GET 请求（仅获取响应头）。并发连接数默认限制为 5，可通过配置文件调整。请用户在使用前确保检查频率符合目标网站的服务条款，本系统不承担因过度频繁检查引发的任何责任。

**问：导入大量链接（超过 1 万条）时，系统性能是否会显著下降？**

答：系统在数据库层面对链接表与标签表建立了联合索引，且批量导入采用分批次提交（每批 500 条）的方式，避免事务过大导致锁表。健康检查任务采用队列机制，不会阻塞主线程。若链接数量超过 10 万条，建议将后端数据库切换为 PostgreSQL 并启用读写分离，同时增加 Redis 缓存命中率。实际性能瓶颈通常取决于网络 I/O 而非系统本身。

**问：能否将本系统用于商业目的或嵌入到其他产品中？**

答：本项目采用 MIT 许可证，允许免费使用、修改、分发和再授权，包括用于商业软件或专有项目。但需保留原始版权声明与许可证文本。本系统不附带任何担保，使用者需自行承担因依赖外部链接资源而产生的法律合规风险。

## 许可证

MIT License

Copyright (c) 2026 Resource Navigation Aggregator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
