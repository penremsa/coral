# NovaLink 技术资源索引平台

NovaLink 是一个面向开发人员与技术研究者的外链资源聚合与导航系统，专注于收集、分类和展示高价值的技术参考站点、数据工具与实时信息接口。本项目不直接提供数据内容，而是通过结构化目录与可检索的资源映射，帮助技术团队在数据采集、实时比分监控、网络质量分析等场景下快速定位合适的外部服务端点。

项目定位为技术基础设施的辅助层，适用于需要频繁切换外部数据源、维护多环境配置、或构建聚合类信息产品的开发小组。通过集中管理分散的第三方资源，NovaLink 能够显著降低团队在接口发现与可用性验证上的重复劳动成本。

## 功能概览

- **按协议类型自动归类**：系统根据资源 URL 的协议特征（HTTP/HTTPS、WebSocket、FTP 等）自动划分到不同的访问通道，便于网络策略配置。

- **可用性被动检测**：集成轻量级心跳探测机制，定期对收录的域名进行 TCP 连通性检查，并在管理面板中标记异常状态。

- **标签化检索体系**：每个资源可附加多个功能标签（如 `realtime`、`historical`、`odds`、`cn_only`），支持多标签组合过滤。

- **版本化资源快照**：每次更新资源列表时自动生成时间戳快照，支持回滚到任意历史状态，方便排查外部接口变更引起的问题。

- **批量导入与导出**：支持 CSV 与 JSON 格式的批量资源录入，以及按筛选条件导出完整资源清单，便于与其他运维系统对接。

- **访问日志审计**：记录所有通过本平台发起的资源访问请求（脱敏），提供基础的调用频次统计与异常访问告警。

- **自定义健康检查脚本**：高级用户可为特定域名编写自定义探测脚本（Python/Shell），实现对业务层面可用性的精确监控。

- **只读只管、不代理**：明确声明本平台不提供数据缓存、代理转发或内容改写服务，所有外部请求由客户端直接发起，确保合规与透明。

## 应用场景

- **实时数据聚合类产品开发**：团队在构建体育数据看板或即时信息推送服务时，需要同时对接多个不同域名下的接口以保障冗余和容灾。NovaLink 的资源分类体系可以帮助快速筛选出符合协议和数据格式要求的候选域名，缩短调研周期。

- **网络质量区域对比测试**：运维人员可通过本平台列出的多个地域性域名（以 `.org.cn` 为特征），配合内部监控系统进行不同运营商线路下的 DNS 解析时延与 HTTP 首包时间对比，辅助 CDN 调度决策。

- **离线文档与资源归档**：技术写作人员或知识库管理员可以定期导出 NovaLink 的资源清单，结合备注字段中的描述信息，将其嵌入内部技术文档作为外部参考附录，保持文档与线上资源同步。

- **渗透测试与安全审计的允许列表管理**：安全团队在进行授权测试时，需要明确列出所有允许访问的外部域名，避免测试流量误触非授权目标。NovaLink 的资源导出功能可作为生成白名单配置文件的数据源。

- **新员工技术栈熟悉训练**：将 NovaLink 作为内部导航首页，新入职的开发人员可以快速了解团队常用的第三方服务提供商、数据接口风格以及域名命名规范，加速项目环境搭建。

## 快速开始

以下步骤将在本地环境中启动 NovaLink 索引服务，默认监听 8080 端口。请确保系统已安装 Git、Node.js（v18 及以上）与 npm。

```bash
# 克隆代码仓库
git clone https://github.com/novalink-dev/novalink-index.git

# 进入项目目录
cd novalink-index

# 安装项目依赖
npm install

# 复制环境变量模板并修改数据库连接等配置
cp .env.example .env

# 以开发模式启动服务，默认访问地址为 http://localhost:8080
npm run dev
```

启动后，系统会自动加载 `data/sources.json` 中的初始资源列表。如需加载本批次提供的完整资源，请使用管理后台的批量导入功能，或直接覆盖 `data/sources.json` 文件后重启服务。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | v18.17.0 或更高 | 运行时环境，推荐使用 LTS 版本 |
| npm | v9.0.0 或更高 | 包管理器，用于安装项目依赖 |
| PostgreSQL | v14.0 或更高 | 主数据库，存储资源元数据、标签和审计日志 |
| Redis | v7.0 或更高 | 缓存层，用于临时存储健康检查结果和会话数据 |
| Git | v2.30 或更高 | 版本控制，用于克隆仓库和管理配置变更 |
| 系统内存 | 至少 2GB 可用 | 保证 Node 进程和数据库缓存正常运行 |
| 磁盘空间 | 至少 10GB 可用 | 用于存储历史快照和访问日志（按日轮转） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 运维手册 | `/docs/operations/deployment.md` | 如何在生产环境中使用 Docker Compose 部署高可用实例？如何配置反向代理和 SSL 证书？ |
| API 参考 | `/docs/api/resources.md` | 外部系统如何通过 RESTful API 查询资源列表、获取单个资源详情以及触发手动健康检查？ |
| 数据模型 | `/docs/data/schema.md` | 资源表、标签表、快照表和日志表之间的关联关系如何？字段约束和索引策略是怎样的？ |
| 自定义探测 | `/docs/advanced/custom-check.md` | 如何为特定域名编写自定义健康检查脚本？脚本的输入输出规范是什么？ |
| 前端面板 | `/docs/ui/dashboard.md` | 管理面板中各个图表和列表的含义是什么？如何快速筛选出当前不可用的资源？ |
| 安全策略 | `/docs/security/audit-log.md` | 审计日志记录哪些字段？如何配置日志的远程发送和自动清理周期？ |

## 资源列表

本批次收录的外部资源共计 10 个域名，均属于体育数据与实时比分类目。按照域名主题特征划分为以下子类别，所有域名严格保持原始输入格式。

### 综合比分类

<code>qiutanbifen888.org.cn</code>

<code>tiqiuwang.org.cn</code>

### 篮球专项比分

<code>lanqiubifennbanba.org.cn</code>

### 足球即时比分（系列 A）

<code>zuqiujishibifena.org.cn</code>

<code>zuqiujishibifenb.org.cn</code>

<code>zuqiujishibifenc.org.cn</code>

### 足球即时比分（系列 B）

<code>tiqiuwanga.org.cn</code>

<code>tiqiuwangb.org.cn</code>

<code>tiqiuwangc.org.cn</code>

### 足球比分查询

<code>qiutanzuqiubifena.org.cn</code>

## 项目结构

```
novalink-index/
├── src/
│   ├── core/                     # 核心模块：应用初始化、依赖注入容器
│   ├── api/                      # RESTful API 路由层（资源、标签、快照、日志）
│   │   ├── v1/                   # API 版本 v1 的实现
│   │   └── middleware/           # 鉴权、限流、请求日志中间件
│   ├── services/                 # 业务逻辑层：资源管理、探测调度、快照服务
│   │   ├── resource.service.js
│   │   ├── health.service.js
│   │   └── snapshot.service.js
│   ├── repositories/             # 数据访问层：封装 PostgreSQL 与 Redis 操作
│   ├── workers/                  # 后台任务进程：定时健康检查、日志归档
│   ├── models/                   # 数据模型定义（Joi 校验 + Sequelize 映射）
│   ├── utils/                    # 工具函数：DNS 解析、URL 规范化、日期格式化
│   ├── config/                   # 配置文件加载与合并逻辑
│   └── app.js                    # 应用入口文件
├── data/
│   ├── sources.json              # 初始资源列表（JSON 格式）
│   └── snapshots/                # 历史资源快照存储目录
├── tests/
│   ├── unit/                     # 单元测试（Jest）
│   └── integration/              # 集成测试（含数据库与 API 联调）
├── docs/                         # 完整文档（见上方文档导航表格）
├── scripts/
│   ├── init-db.sql               # 数据库初始化脚本
│   └── seed-resources.js         # 批量导入资源命令行工具
├── .env.example                  # 环境变量配置模板
├── docker-compose.yml            # 本地开发与生产环境容器编排
├── Dockerfile                    # 多阶段构建镜像文件
├── package.json                  # npm 依赖清单与脚本命令
└── README.md                     # 本文件
```

## 贡献指南

1. **资源新增或更新建议**：若您发现某个外部资源已变更内容类型或永久下线，请通过 GitHub Issues 提交资源变更请求，并附上您验证时使用的测试命令或截图。核心团队会在两个工作日内复核并合并。

2. **代码贡献流程**：Fork 本仓库后，在 `develop` 分支上创建您的特性分支（命名格式为 `feature/功能简述`）。完成开发后提交 Pull Request 至 `develop` 分支，请确保所有单元测试通过且代码覆盖率不低于 80%。

3. **文档改进**：鼓励对文档中的拼写错误、示例代码不清晰或遗漏的配置项进行修正。文档修改无需提交单元测试，但需确保 Markdown 格式符合 `markdownlint` 规则。

4. **安全性报告**：如发现本平台自身存在安全漏洞（如未授权访问、注入风险等），请直接发送邮件至安全团队邮箱（见 `SECURITY.md`），不要公开提交 Issue，我们将按照标准漏洞处理流程响应。

5. **本地化与国际化**：欢迎为本项目添加多语言界面支持。请在 `locales/` 目录下新建对应语言 JSON 文件，并确保所有 UI 文本均通过 `i18n` 函数引用，而非硬编码。

## 常见问题

**问：NovaLink 是否会对列出的外部资源进行数据缓存或代理转发？**

答：不会。本项目严格遵循“只索引、不代理”的原则。所有列出的 URL 仅供用户自行访问，平台不会存储任何来自外部资源的数据内容，也不会修改请求或响应。用户客户端直接与目标域名建立连接，本平台仅提供资源元数据（如域名、标签、最后检测时间）。

**问：健康检查显示某个域名为不可用状态，但我的浏览器可以正常打开，是什么原因？**

答：健康检查模块默认使用 TCP 四次握手探测，仅验证目标 IP 的端口是否开放，并不模拟完整的 HTTP 请求。如果目标服务器配置了基于 User-Agent 或特定 Header 的访问限制，可能导致 TCP 连接成功但业务层无法正常响应。您可以为该域名配置自定义检查脚本（参考 `/docs/advanced/custom-check.md`），改用 `curl` 或 `wget` 模拟真实浏览器请求以获取准确状态。

**问：如何批量更新资源列表而不影响正在运行的服务？**

答：推荐使用快照恢复功能。首先在管理后台导出当前资源快照作为备份，然后通过 `POST /api/v1/resources/batch-import` 接口上传新的 CSV 或 JSON 文件，系统会自动生成新的版本快照。上传完成后，您可以在管理面板的“快照管理”中一键切换回任一历史版本，整个过程无需重启服务。

## 许可证

MIT License

Copyright (c) 2026 NovaLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:30
