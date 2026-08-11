# NovaLink 技术资源导航站

NovaLink 是一个面向开发人员、技术研究者与内容创作者的轻量级外链资源聚合平台。该项目定位于对分散于网络各处的优质技术文档、视频教程、工具站点及社区资源进行系统性收录与分类导航，帮助用户快速定位所需信息，减少重复检索成本。NovaLink 不存储任何实体内容，仅提供结构化外链索引，适用于个人部署为起始页、团队内部知识导航、以及垂直领域资源站点的快速搭建。

目标用户包括：日常需要查阅大量技术资料的全栈工程师、运维人员、AI 应用开发者、视频内容制作者，以及对特定领域（如中文开源字幕、国产影视技术参数）有持续关注需求的进阶用户。通过清晰的目录分层与标签过滤，NovaLink 将原始链接资源转化为可维护、可扩展、可共享的知识导航体系。

## 功能概览

- **多级分类目录系统**：支持管理员后台动态增删改查资源分类，分类层级深度可达五级，满足从泛技术到细分专题的归档需求。
- **外链资源卡片展示**：每个资源以卡片形式呈现，包含标题、简短描述、标签集合、访问次数统计及最后校验时间，方便用户快速评估资源有效性。
- **全文模糊检索与标签过滤**：基于标题、描述、标签三字段的全文检索，配合多选标签过滤，实现精准定位。检索响应时间控制在 300 毫秒以内（数据量一万条级别）。
- **资源可用性自动巡检**：每日定时任务对已收录外链进行 HTTP 状态码检查，标记失效链接并邮件通知管理员，保证导航站资源健康度。
- **用户自定义收藏夹**：支持登录用户将常用资源加入个人收藏夹，并支持导入/导出为 JSON 格式，便于迁移与备份。
- **访问统计与热度排序**：记录每个资源的点击次数与最近访问时间，支持按热度、新增时间、字母序等多种排序方式，辅助用户发现高频优质内容。
- **响应式布局与深色模式**：前端界面基于 CSS Grid 与 Flexbox 实现自适应，兼容桌面端、平板与移动端；内置浅色/深色主题切换，适配不同使用环境。

## 应用场景

- **个人技术起始页**：开发者可将 NovaLink 部署为自己的浏览器新标签页，将日常高频访问的文档站、API 参考、论坛、代码仓库等统一收纳，每次打开即见全局，避免收藏栏杂乱。
- **团队内部知识导航**：技术团队可基于 NovaLink 搭建团队知识库入口，将内部 Wiki、CI/CD 流水线看板、日志系统、监控面板等内部链接按项目分组，并利用巡检功能确保各系统入口可用。
- **垂直领域资源站**：针对特定技术领域（如国产视频编解码参数查询、中文开源字幕社区、AI 模型权重站）构建主题导航，通过目录细分与标签体系，为领域新人提供完整的学习与工具链路指引。
- **活动与文档临时汇总**：在技术大会、黑客松或课程教学期间，可快速创建临时分类，将会议日程、演讲稿链接、代码示例仓库、在线协作白板等一次性资源集中展示，活动结束后一键归档或关闭。

## 快速开始

以下步骤假设您已具备基础的 Node.js 与 Git 环境。NovaLink 采用前后端分离架构，后端基于 Node.js + Express，前端使用 Vanilla JavaScript + CSS 构建，数据存储采用 SQLite 轻量级文件数据库，便于单机部署与迁移。

```bash
# 1. 克隆项目仓库
git clone https://github.com/novalink-dev/novalink-starter.git
cd novalink-starter

# 2. 安装依赖（包含后端服务与前端构建工具）
npm install

# 3. 初始化 SQLite 数据库结构与默认分类数据
npm run db:init

# 4. 启动开发服务器（默认监听端口 3000，同时提供前端静态文件与 REST API）
npm run dev
```

启动成功后，访问控制台输出提示的本地地址（通常为 http://localhost:3000 ）即可进入导航站首页。管理员后台入口为 /admin，默认管理员账号为 admin，密码为 novalink2026，首次登录后请立即修改密码。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用 nvm 管理多版本 |
| npm | 9.x 或以上 | 包管理器，随 Node.js 一同安装 |
| SQLite3 | 3.39 或以上 | 嵌入式数据库，系统级依赖需预先安装（开发环境已包含预编译二进制） |
| Git | 2.30 或以上 | 用于克隆仓库及后续版本更新拉取 |
| 系统内存 | 最低 512 MB，推荐 1 GB | 生产环境建议配备 1GB 以上内存以支撑巡检任务 |
| 磁盘空间 | 最低 200 MB | 主要用于存储数据库文件（约 50MB/万条记录）与静态资源 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/overview.md | 如何注册、收藏资源、使用检索与排序功能、切换主题 |
| 管理员手册 | /docs/admin-guide/category-management.md | 如何创建/编辑/删除分类、添加新资源链接、导入导出批量数据 |
| 开发指南 | /docs/developer-guide/api-reference.md | 后端 REST API 各端点说明、请求/响应格式、鉴权方式 |
| 部署运维 | /docs/ops-guide/deployment-options.md | 支持 Docker 部署、systemd 进程守护、Nginx 反向代理配置示例 |
| 设计说明 | /docs/design/architecture.md | 系统架构图、数据模型 ER 图、巡检任务调度设计、扩展性考量 |

## 资源列表

以下为本项目当前收录的全部外链资源，按内容主题划分为两大类别。所有链接均保留用户提供的原始格式，未做任何协议补全或域名规范化处理。

### 中文视频字幕与视听资源

<code>zhongwenzaixianzimumianfeigaoqing.org.cn</code>

<code>zaixianbofangzhongwenzimu.org.cn</code>

<code>zhongwenzimuzaixianmianfei.org.cn</code>

<code>yirenguochanzaixianshipin.org.cn</code>

<code>gaoqingshipinzaixianguankanw.org.cn</code>

<code>meinvshipinzaixianguankan.org.cn</code>

<code>jiujiumitaozaixianbofang.org.cn</code>

<code>yiquerzhongwenzimu.org.cn</code>

<code>zhongwenzimuzhifusiwang.org.cn</code>

<code>zhongwenzimushaofurenqi.org.cn</code>

## 项目结构

```
novalink-starter/
├── backend/                           # 后端服务源代码
│   ├── api/                           # REST API 路由定义
│   │   ├── auth.js                    # 登录、令牌刷新、登出接口
│   │   ├── resources.js               # 资源增删改查、检索、排序接口
│   │   ├── categories.js              # 分类树管理接口
│   │   └── health.js                  # 健康检查与版本信息接口
│   ├── models/                        # 数据模型层（SQLite 表结构映射）
│   │   ├── Resource.js                # 资源记录模型，包含校验逻辑
│   │   ├── Category.js                # 分类层级模型，支持路径枚举
│   │   ├── User.js                    # 用户模型，密码使用 bcrypt 哈希
│   │   └── AuditLog.js                # 操作审计日志模型
│   ├── services/                      # 业务逻辑层
│   │   ├── crawler.js                 # 链接可用性巡检服务（每日定时）
│   │   ├── search.js                  # 全文检索引擎（基于内存倒排索引）
│   │   └── stats.js                   # 点击统计与热度计算服务
│   ├── db/                            # 数据库相关
│   │   ├── init.sql                   # 初始化建表语句与默认分类种子数据
│   │   ├── migrations/                # 版本升级迁移脚本
│   │   └── nova.db                    # SQLite 数据库文件（生产环境）
│   └── server.js                      # Express 应用入口，中间件挂载与启动
├── frontend/                          # 前端静态资源
│   ├── index.html                     # 主页面模板，包含容器挂载点
│   ├── css/                           # 样式文件
│   │   ├── main.css                   # 全局基础样式与布局
│   │   ├── dark-theme.css             # 深色主题变量覆盖
│   │   └── components.css             # 卡片、导航栏、表单等组件样式
│   ├── js/                            # 前端逻辑
│   │   ├── app.js                     # 应用入口，路由监听与视图渲染
│   │   ├── api-client.js              # 封装 fetch 调用，统一错误处理
│   │   ├── store.js                   # 前端状态管理（分类树、资源列表、收藏）
│   │   └── renderers/                 # 各类卡片与列表渲染函数
│   └── assets/                        # 图片、字体等静态资源
├── config/                            # 全局配置文件
│   ├── default.json                   # 默认配置（端口、巡检间隔、分页大小）
│   ├── production.json                # 生产环境覆盖配置
│   └── custom.yaml                    # 用户自定义配置（可选，覆盖前两者）
├── scripts/                           # 辅助运维脚本
│   ├── backup-db.sh                   # 数据库每日备份脚本（配合 crontab）
│   ├── import-csv.js                  # 从 CSV 批量导入资源链接
│   └── export-json.js                 # 将全部资源导出为 JSON 格式
├── docs/                              # 完整文档目录（见上方文档导航章节）
├── tests/                             # 单元测试与集成测试
│   ├── unit/                          # 模型层与服务层的单元测试（Jest）
│   └── integration/                   # API 端到端测试（Supertest）
├── .env.example                       # 环境变量模板（JWT 密钥、管理员邮箱等）
├── docker-compose.yml                 # Docker Compose 编排文件（含数据库与后端）
├── Dockerfile                         # 基于 Alpine 的轻量级生产镜像构建文件
├── package.json                       # npm 项目配置，含依赖列表与脚本命令
└── README.md                          # 本文件
```

## 贡献指南

NovaLink 遵循开源社区协作模式，欢迎并鼓励各类贡献，包括但不限于新增资源收录、修复链接失效问题、改进界面交互、补充文档翻译、提交缺陷报告等。请参照以下步骤参与贡献：

1. 在 GitHub 上 Fork 本仓库，并将您的 Fork 克隆至本地开发环境。建议在 dev 分支基础上新建功能分支，分支命名遵循 feat/xxx 或 fix/xxx 格式。
2. 进行代码或文档修改时，请确保遵循项目 ESLint 规则（前端 JavaScript）与 Prettier 格式化规范。新增后端 API 需同步更新 /docs/developer-guide/api-reference.md 中的接口说明。若涉及数据库表结构变更，请同时在 /backend/db/migrations/ 下创建对应的迁移脚本。
3. 本地提交前运行 npm run test 确保所有单元测试及集成测试通过。新增功能应附带对应的测试用例。提交信息请使用简洁的英文描述，采用 Conventional Commits 规范（如 feat: add batch import from CSV）。
4. 将您的分支推送至个人 Fork，并在 GitHub 上向本仓库的 dev 分支发起 Pull Request。请在 PR 描述中清晰说明改动动机、实现方式及影响范围，关联相关 Issue（若有）。
5. 项目维护者将在两个工作日内进行 Code Review，可能会提出修改意见。合并后，您的贡献将会在下一版本发布时列入贡献者名单。

## 常见问题

**Q: 部署后访问首页正常，但点击任意资源链接跳转时提示“无法连接”，巡检日志显示状态码为 0 或超时，如何处理？**

A: 此问题通常源于目标站点对非浏览器 User-Agent 的请求返回异常，或目标站点本身存在网络隔离（如仅限内网访问）。请按以下步骤排查：首先检查后端服务所在主机的网络连通性，使用 curl -I 目标链接 手动测试；若主机访问正常而巡检失败，可在 /config/default.json 中修改巡检模块的 userAgent 字段，模拟主流浏览器标识；若目标站点为内网地址，请在巡检配置的 excludeDomains 中添加该域名，跳过自动检查。另外，部分站点会限制请求频率，可适当调大巡检间隔（默认 24 小时）避免触发风控。

**Q: 我想将 NovaLink 作为团队内部导航，但默认的 SQLite 数据库不支持并发写入，会不会成为瓶颈？**

A: SQLite 在默认配置下对并发写入有一定限制，但对于导航站这类读多写少（资源变更频率通常低于每日数次）的场景，完全够用。若团队规模超过 20 人且频繁进行批量导入/编辑操作，建议将数据库迁移至 PostgreSQL。项目已提供 /backend/models/ 下的抽象层，您只需修改 /config/default.json 中的 db.dialect 为 postgres，并配置对应的连接字符串即可。迁移前请运行 npm run db:dump 导出 SQLite 数据，再通过 pg_restore 导入。

**Q: 前端资源卡片中显示的“热度”数值是如何计算的，能否自定义权重？**

A: 热度值默认采用复合算法：热度 = 点击次数 * 0.6 + 近 7 天访问次数 * 0.3 + 收藏次数 * 0.1。该公式定义在 /backend/services/stats.js 中的 calculateHotScore 函数中。您可以根据实际需求修改各系数权重，甚至增加新的因子（如资源创建时间衰减因子）。修改后需要重启后端服务生效，历史热度数据会在每次点击或巡检时增量更新，无需重建全量。

## 许可证

MIT License。即允许任意个人或组织免费使用、复制、修改、合并、分发、再许可及销售本软件副本，但需在分发时保留原始版权声明与免责声明。本软件按“原样”提供，不提供任何明示或暗示的担保，包括但不限于适销性、特定用途适用性及非侵权性担保。详细条款请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
