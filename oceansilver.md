# VidiLink Aggregator

VidiLink Aggregator 是一个面向技术内容创作者与资源管理者的轻量级外链聚合与导航系统。该项目定位于中小型技术团队、个人知识库维护者以及内容聚合站点运营方，用于解决多源资源分散、链接管理混乱、访问入口不统一的问题。通过结构化的链接分类、状态监控与快速访问面板，VidiLink Aggregator 帮助用户将大量外部资源整合为可维护、可分享、可嵌入的导航页面，并支持多批次、多标签的资源编排。

目标用户包括：开源项目文档维护者、技术博客作者、在线教育内容整理者、企业内部知识库管理员以及需要频繁引用外部链接的研发团队。项目本身不存储或代理任何外部内容，仅作为链接的元数据管理工具，确保合规性与轻量化。

## 功能概览

- **批量链接导入与分类**：支持通过 JSON 或 YAML 配置文件批量导入外部链接，并按主题、区域、语言或批次自动打标分类，便于后续检索与展示。

- **实时可用性检测**：内置 HTTP 状态检查模块，可定时探测每个链接的访问状态（200/404/超时等），并在管理面板中以颜色标识异常链接，降低维护成本。

- **自定义导航页生成**：根据分类与标签动态生成响应式 HTML 导航页面，支持明暗主题切换、搜索过滤与自定义 Logo 占位，可直接部署为静态站点。

- **访问统计与点击追踪**：集成轻量级点击日志记录，统计每个链接的点击次数、最后访问时间与来源 IP 聚合（匿名化处理），为内容热度分析提供数据支撑。

- **多用户协作编辑**：提供基于角色的访问控制（管理员/编辑者/只读），允许多名成员共同维护链接库，并记录操作审计日志。

- **数据导入导出**：支持 CSV、JSON、Markdown 列表三种格式的链接数据导入导出，方便与其他工具（如 Notion、Airtable）进行数据交换。

- **定时备份与快照**：每日自动备份全量链接数据至指定存储路径，支持手动创建快照，便于回滚至历史版本。

## 应用场景

1. **技术文档站点外链管理**：开源项目文档中常需引用外部依赖、教程或参考链接，维护人员可使用 VidiLink Aggregator 统一管理这些外链，并生成独立的“资源导航”页面嵌入文档站点，确保链接始终保持最新且可访问。

2. **在线课程资源汇总**：教育机构或独立讲师在制作技术课程时，需要为学生提供大量延伸阅读材料。通过本系统可按周次或模块分类整理链接，生成专属课程资源页，学生可一键访问所有推荐资料。

3. **企业内部知识库增强**：企业内部的 Confluence 或 Wiki 中散落着众多团队收藏的常用工具、内部系统入口与第三方服务地址。VidiLink Aggregator 可作为统一入口层，对内部链接进行健康监控与权限管理，减少“死链”投诉。

4. **开源项目 README 资源编排**：开源项目维护者可将项目依赖的社区资源、姊妹项目、文档站等链接托管至本系统，再通过 API 动态拉取生成 README 中的资源列表，避免每次更新均需提交代码仓库。

5. **个人书签替代方案**：技术爱好者可用本系统替代浏览器内置书签管理，实现跨设备、跨浏览器的统一收藏夹，并附带标签检索与状态提醒功能。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，要求已安装 Git 与 Node.js 18+。

```bash
# 1. 克隆项目仓库
git clone https://github.com/vidilink/aggregator.git
cd aggregator

# 2. 安装项目依赖
npm install

# 3. 复制环境配置文件并修改数据库连接等参数
cp .env.example .env

# 4. 执行数据库迁移与初始数据种子
npm run migrate
npm run seed

# 5. 启动开发服务器（默认监听 3000 端口）
npm run dev
```

访问 `http://localhost:3000` 即可进入管理控制台，默认管理员账号为 `admin@vidilink.local`，密码为 `admin123`（首次登录请立即修改）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用官方二进制或 nvm 安装 |
| npm | 9.x 或 10.x | 包管理器，随 Node.js 一同安装 |
| PostgreSQL | 14.x 或 15.x | 主数据库，用于存储链接元数据、用户信息及审计日志 |
| Redis | 7.x | 缓存与会话存储，用于提升高频查询性能及分布式锁 |
| Nginx | 1.24+ | 生产环境推荐作为反向代理，处理静态资源与负载均衡 |
| Git | 2.30+ | 用于克隆仓库及版本管理 |
| PM2 | 5.x | 生产环境进程守护（可选，但强烈推荐） |
| Docker | 20.10+ | 若使用容器化部署方式，则需要 Docker 与 Docker Compose |
| OpenSSL | 3.x | 用于生成密钥对与证书管理（本地开发默认使用自签名） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | `docs/getting-started.md` | 如何在一小时内完成首次部署并导入第一批链接？ |
| 配置参考 | `docs/configuration.md` | 环境变量、分类规则、检测频率、邮件通知等如何配置？ |
| API 手册 | `docs/api-reference.md` | 如何通过 REST API 进行链接的增删改查、批量操作与状态查询？ |
| 部署指南 | `docs/deployment.md` | 生产环境如何配置 Nginx、SSL、数据库连接池与日志轮转？ |
| 扩展开发 | `docs/extension.md` | 如何编写自定义检测插件或添加新的导入导出格式支持？ |
| 运维手册 | `docs/operations.md` | 如何进行数据备份、迁移、性能调优与故障排查？ |
| 设计说明 | `docs/design.md` | 系统架构图、数据模型 ER 图以及核心技术选型决策记录？ |

## 资源列表

### 技术文档与开发参考

- <code>guochangaoqingshipinzaixian.org.cn</code>
- <code>guochangaoqingshipinguankan.org.cn</code>
- <code>rimanzaixianmianfeiguankan.org.cn</code>
- <code>zhongwenzimumianfeibofang.org.cn</code>
- <code>zaixianzimumianfeiguankan.org.cn</code>
- <code>zaixianzimuguankanmianfei.org.cn</code>
- <code>zaixianzimugaoqingdianshiju.org.cn</code>
- <code>mianfeishipinwangzhanzaixianguankan.org.cn</code>
- <code>rihanzaixianmianfeishipinw.org.cn</code>
- <code>oumeizaixianmianfeishipinw.org.cn</code>

上述列表为项目预置示例链接，用户可根据实际需要替换或增删。所有链接均以原始字符串形式存储，不做任何协议补全或域名规范化处理，以确保数据的原始性与可控性。

## 项目结构

```
aggregator/
├── src/                           # 核心源代码目录
│   ├── api/                       # REST API 路由与控制器
│   │   ├── v1/                    # API 版本 1 实现
│   │   │   ├── links.js           # 链接 CRUD 与批量操作端点
│   │   │   ├── categories.js      # 分类管理端点
│   │   │   ├── health.js          # 健康检查与状态探测端点
│   │   │   └── stats.js           # 点击统计与聚合查询端点
│   │   └── middleware/            # 认证、日志、限流等中间件
│   ├── core/                      # 核心业务逻辑层
│   │   ├── detector/              # 链接可用性检测引擎
│   │   │   ├── http-checker.js    # HTTP 状态码与超时检测
│   │   │   └── scheduler.js       # 定时任务调度器（基于 node-cron）
│   │   ├── importer/              # 数据导入导出模块
│   │   │   ├── json-parser.js
│   │   │   ├── csv-transformer.js
│   │   │   └── md-list-generator.js
│   │   └── auth/                  # 认证与权限管理（JWT + RBAC）
│   ├── models/                    # 数据模型（ORM 映射）
│   │   ├── Link.js                # 链接表模型
│   │   ├── User.js                # 用户表模型
│   │   ├── Category.js            # 分类表模型
│   │   └── AuditLog.js            # 审计日志表模型
│   ├── services/                  # 外部服务集成层
│   │   ├── cache.js               # Redis 缓存封装
│   │   ├── mailer.js              # 邮件通知服务（告警与周报）
│   │   └── backup.js              # 自动备份与快照管理
│   ├── views/                     # 前端导航页模板（EJS + Tailwind）
│   │   ├── layouts/               # 基础布局模板
│   │   ├── partials/              # 可复用组件（链接卡片、搜索框、分页）
│   │   └── pages/                 # 完整页面（首页、分类视图、管理后台）
│   └── utils/                     # 工具函数集
│       ├── logger.js              # 结构化日志（基于 winston）
│       ├── validator.js           # 输入校验（URL 格式、分类名等）
│       └── config-loader.js       # 多环境配置加载器
├── config/                        # 配置文件目录
│   ├── default.yaml               # 默认配置（端口、检测间隔、缓存时间）
│   ├── production.yaml            # 生产环境覆盖配置
│   └── development.yaml           # 开发环境覆盖配置
├── migrations/                    # 数据库迁移脚本（Knex.js）
│   ├── 20250101000001_initial_schema.js
│   ├── 20250115000002_add_user_roles.js
│   └── 20250201000003_create_audit_logs.js
├── seeders/                       # 初始测试数据种子
│   └── dev-seed.js                # 开发环境默认链接与用户
├── docs/                          # 完整文档（见文档导航章节）
├── tests/                         # 单元测试与集成测试（Jest + Supertest）
│   ├── unit/
│   └── integration/
├── public/                        # 静态资源（CSS、JS、图片占位）
│   ├── css/
│   ├── js/
│   └── images/
├── scripts/                       # 运维辅助脚本
│   ├── backup.sh                  # 手动备份脚本
│   └── health-check.sh            # 外部健康探测脚本
├── docker-compose.yml             # 容器化编排（PostgreSQL + Redis + App）
├── Dockerfile                     # 生产环境镜像构建文件
├── .env.example                   # 环境变量示例
├── package.json                   # 项目依赖与脚本定义
├── package-lock.json              # 依赖锁定文件
├── README.md                      # 本文件
└── LICENSE                        # MIT 许可证文本
```

## 贡献指南

我们欢迎各类形式的贡献，包括但不限于功能建议、缺陷报告、代码提交与文档改进。为确保协作流畅，请遵循以下步骤：

1. **查阅议题与项目看板**：访问 GitHub Issues 页面查看现存任务，确认无重复工作后再行提交。对于新功能或较大改动，建议先创建议题进行讨论，避免方向偏差。

2. **派生仓库并创建功能分支**：将主仓库 Fork 至个人账户，然后基于 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的分支名称，例如 `feature/add-telegram-notifier`。

3. **编写测试与遵守编码规范**：所有新增功能必须附带对应的单元测试或集成测试；代码需通过 ESLint 与 Prettier 检查，并确保原有测试用例全部通过。提交前请运行 `npm run lint` 与 `npm test`。

4. **提交清晰的信息与拉取请求**：提交信息应遵循 Conventional Commits 格式（如 `feat: add batch delete endpoint`），并推送到派生仓库。然后向主仓库的 `main` 分支发起 Pull Request，在描述中关联相关议题并简述改动内容与测试结论。

5. **接受代码审查与迭代**：项目维护者将审查您的 PR，可能提出修改建议。请积极回应并及时更新分支，直至合并。合并后您的贡献将出现在下一版本的发布说明中。

## 常见问题

**问：系统支持同时管理多少个链接？是否有性能瓶颈？**

答：在默认配置（PostgreSQL 15 + Redis 7）下，单实例可稳定管理 5 万至 10 万个链接，检测引擎采用异步并发控制，每轮全量检测完成时间取决于网络延迟与超时设置。若链接数量超过 10 万，建议分片部署或调整检测频率为每周一次，同时可启用只读副本分担查询压力。项目本身无硬性数量上限，但建议定期清理无效链接以保持数据质量。

**问：如何迁移已有书签或链接数据到本系统？**

答：我们提供三种迁移路径。第一，通过 CSV 模板导入，模板格式在管理后台“导入”页面下载；第二，若您使用浏览器导出的 HTML 书签文件，可使用社区提供的转换脚本（位于 `scripts/convert-bookmark.js`）将其转为 JSON 格式再导入；第三，对于 Notion 或 Airtable 用户，可先导出为 CSV，再使用我们提供的映射配置完成字段对应。详细操作请参阅文档中的“数据迁移指南”。

**问：部署后无法访问外部链接检测功能，可能是什么原因？**

答：通常是由于网络策略或代理配置导致。请检查以下三点：第一，确保服务器可以出站访问公网，且防火墙未屏蔽出站 80/443 端口；第二，若服务器位于内网且需通过代理访问外网，请在 `.env` 中设置 `HTTP_PROXY` 与 `HTTPS_PROXY` 环境变量；第三，部分站点可能屏蔽非浏览器 User-Agent 请求，您可以在配置中修改检测器的 `userAgent` 字段为常见浏览器标识。如仍无法解决，可查看日志文件 `logs/error.log` 中的详细报错信息。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括商业用途。完整的许可证文本请参阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
