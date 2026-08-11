# HyperLink Navigator

HyperLink Navigator 是一个面向技术社区与内容创作者的轻量化外链资源聚合与导航系统。项目定位于为开发者、技术博主、科研工作者以及信息整理人员提供一套可自部署、可扩展的链接收藏与分类展示工具。其核心价值在于将分散、易失效的零散 URL 资源，通过结构化目录、标签系统与状态监控机制，转化为高可读性、高可维护性的内部知识库入口。

目标用户包括：需要维护团队技术文档导航的架构师、运营个人资讯站点的独立开发者、以及希望系统化管理学习路径的进阶学习者。HyperLink Navigator 不依赖任何重型前端框架，后端基于 Node.js 与 SQLite，兼顾单机部署与低资源消耗，同时提供 RESTful API 用于对接现有运维监控体系，解决传统书签工具无法批量导入、无法自定义元数据、无法检测链接可用性的长期痛点。

## 功能概览

- **多级目录分类管理**：支持无限层级的目录树创建，允许用户按技术栈、业务域或信息类型对链接进行精细化分组，便于大规模链接的有序沉淀。

- **链接元数据扩展**：每条链接记录可附加自定义标签、来源描述、维护人信息、更新频率与关联项目编号，满足企业级知识管理对可追溯性的要求。

- **批量导入与导出**：提供 CSV 与 JSON 格式的批量导入接口，支持从主流浏览器书签文件（HTML）解析链接，同时支持按目录筛选后的数据导出，便于备份或迁移。

- **链接可用性监控**：内置基于 node-fetch 的定时巡检任务，可配置检查间隔与超时阈值，对失效链接自动标记并生成异常报告，降低运维人工巡检成本。

- **全文检索与过滤**：针对链接标题、描述、标签及所属目录路径构建轻量级倒排索引，支持模糊搜索与多条件组合过滤，提升海量链接下的定位效率。

- **用户权限分级**：支持管理员、编辑者、访客三级权限体系，管理员可管理系统配置与用户账户，编辑者可增删改链接，访客仅拥有只读访问权限，适用于团队协作场景。

- **响应式前端面板**：提供基于 EJS 模板引擎的服务端渲染界面，在移动端与桌面端均能保持良好的布局自适应，无需额外安装客户端即可使用全部核心功能。

## 应用场景

- **技术团队内部文档导航**：开发团队可将日常使用的 CI/CD 工具链地址、日志平台、监控看板、代码仓库、设计稿链接统一收录至 HyperLink Navigator，按项目或微服务模块划分目录，新成员入职时即可通过该导航系统快速了解团队基础设施入口。

- **个人知识库外链管理**：研究人员或技术博主在阅读文献、追踪技术趋势时积累的大量外链，可通过本系统按主题（例如“分布式系统论文”、“Rust 生态库”、“前端性能优化案例”）分类存储，配合标签与检索功能，将零散书签转化为可复用的个人知识索引。

- **开源项目资源站聚合**：开源社区维护者可利用 HyperLink Navigator 搭建项目周边的生态导航页，集中展示官方文档、社区论坛、示例代码库、视频教程、第三方工具集成等资源，为贡献者与用户提供一站式入口，减少重复咨询。

- **运维监控告警联动**：运维团队可将内部监控面板、日志聚合平台、告警管理后台等链接按机房或可用区归类，并通过系统提供的 API 将链接状态推送到钉钉或 Slack 机器人，实现当监控链接不可达时的自动告警通知。

## 快速开始

以下步骤将帮助您在本地环境中快速启动 HyperLink Navigator 服务。执行环境要求为 Linux/macOS/WSL，已安装 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库至本地
git clone https://github.com/hyperlink-navigator/hln-core.git

# 进入项目根目录
cd hln-core

# 安装生产环境与开发环境依赖
npm install

# 初始化 SQLite 数据库表结构与默认配置项
npm run init-db

# 以开发模式启动服务，默认监听 3000 端口
npm run dev
```

启动成功后，在浏览器中访问 `http://localhost:3000` 即可进入导航面板首页。若需以生产模式运行，请使用 `npm start` 命令，并确保通过环境变量 `PORT` 与 `DB_PATH` 配置端口和数据库文件路径。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.17.0 或更高 | 运行时环境，推荐使用 LTS 版本，用于执行服务端 JavaScript 代码与依赖管理 |
| SQLite3 | 3.31.0 或更高 | 嵌入式关系型数据库，用于存储链接记录、目录树、用户信息及系统配置，无需额外部署服务进程 |
| npm | 9.0.0 或更高 | Node.js 包管理器，用于安装项目依赖及执行脚本命令 |
| 操作系统 | Linux (glibc 2.28+), macOS 11+, 或 Windows 10/11 (WSL2) | 支持主流 POSIX 兼容环境，Windows 用户建议通过 WSL2 获得最佳文件系统性能 |
| 网络环境 | 出方向 HTTPS 可达 | 用于链接可用性监控模块对外发起探测请求，需允许访问目标域名 443 与 80 端口 |
| 内存 | 最低 512 MB，推荐 1 GB 以上 | 服务运行内存占用与链接总数及巡检并发数相关，建议 10000 条链接以下配置 1 GB |
| 存储 | 至少 100 MB 可用空间 | 数据库文件及日志存储，实际占用随链接数量与巡检历史记录增长 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|----------|-----------|
| 用户手册 | `/docs/user-guide/getting-started.md` | 如何首次登录、创建目录、添加第一条链接以及理解界面各区域功能？ |
| 部署指南 | `/docs/admin/deployment-options.md` | 支持哪些部署方式（Docker、Systemd、PM2）？如何配置反向代理与 HTTPS 证书？ |
| API 参考 | `/docs/api/restful-endpoints.md` | 如何通过 REST API 批量导入链接、查询目录树或触发链路巡检？认证头如何传递？ |
| 运维调优 | `/docs/operations/tuning-and-monitoring.md` | 巡检任务如何调整并发数与超时阈值？日志级别如何动态修改？数据库增长过快如何优化？ |

## 资源列表

本节收录本项目外部依赖、参考文档、社区论坛及数据源等相关资源链接。所有链接均保持用户原始输入格式，未做任何协议、域名或路径改写。

**体育数据类资源**

- <code>qiutanzuqiubifenb.org.cn</code>
- <code>qiutanzuqiubifenc.org.cn</code>
- <code>lanqiubifena.org.cn</code>
- <code>lanqiubifenb.org.cn</code>
- <code>lanqiubifenc.org.cn</code>
- <code>qiutanbifena.org.cn</code>
- <code>qiutanbifenb.org.cn</code>
- <code>qiutanbifenc.org.cn</code>
- <code>bifenwanga.org.cn</code>
- <code>bifenwangb.org.cn</code>

## 项目结构

```
hln-core/
├── app/
│   ├── controllers/               # 路由控制器层，处理请求参数解析与响应封装
│   │   ├── linkController.js      # 链接增删改查及搜索逻辑
│   │   ├── categoryController.js  # 目录树结构与移动排序逻辑
│   │   └── monitorController.js   # 巡检任务触发与结果查询接口
│   ├── services/                  # 核心业务服务层，封装数据访问与外部调用
│   │   ├── linkService.js         # 链接元数据校验、标签解析与批量处理
│   │   ├── indexService.js        # 全文索引重建与关键词检索
│   │   └── probeService.js        # 基于 node-fetch 的链接可用性探测
│   ├── models/                    # 数据模型定义，对应 SQLite 表结构
│   │   ├── linkModel.js           # 链接记录模型（id, title, url, category_id, tags, status）
│   │   ├── categoryModel.js       # 目录模型（id, name, parent_id, sort_order）
│   │   └── userModel.js           # 用户账户与权限模型（id, username, password_hash, role）
│   └── utils/                     # 通用工具函数库
│       ├── logger.js              # 基于 winston 的日志封装，支持按日滚动
│       └── validator.js           # URL 格式校验与 sanitize 安全过滤
├── config/
│   ├── default.json               # 默认配置项（端口、数据库路径、巡检间隔）
│   └── production.json            # 生产环境覆盖配置（可设置日志级别、禁用调试接口）
├── public/                        # 前端静态资源目录
│   ├── css/                       # 基于 Tailwind CSS 的响应式样式表
│   ├── js/                        # 前端交互脚本（目录折叠、表单提交、实时搜索）
│   └── assets/                    # 图标与品牌相关图片资源
├── views/                         # EJS 服务端渲染模板
│   ├── layout.ejs                 # 全局布局模板，包含通用 head 与页脚
│   ├── dashboard.ejs              # 导航面板首页，展示目录树与最近访问链接
│   └── admin/                     # 管理后台相关页面（用户管理、系统配置）
├── tests/                         # 单元测试与集成测试用例
│   ├── unit/                      # 服务层与模型层独立测试
│   └── integration/               # API 端到端测试，使用 supertest 驱动
├── scripts/
│   ├── init-db.js                 # 初始化数据库表与默认管理员账户
│   └── seed-links.js              # 填充示例链接数据用于开发测试
├── .env.example                   # 环境变量示例文件，包含 JWT_SECRET 等敏感配置占位
├── package.json                   # 项目依赖清单与脚本入口定义
├── README.md                      # 项目总体介绍与快速入门（即本文档）
└── LICENSE                        # MIT 许可证全文
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于功能提议、缺陷报告、代码提交与文档完善。请遵循以下步骤参与项目开发：

1. **提交 Issue 讨论**：在 GitHub Issues 中搜索是否已有相关问题，若无则新建 Issue 并选择对应的模板（Bug 报告 / 功能请求 / 改进建议），详细描述当前行为与期望行为，并附上必要的环境信息与日志片段。

2. **分支开发流程**：从 `main` 分支拉取最新的代码，创建以 `feature/` 或 `fix/` 为前缀的短横线命名分支（例如 `feature/add-ldap-auth`）。本地开发时请确保通过所有现有单元测试，并为新增功能补充对应的测试用例。

3. **代码风格规范**：遵循 ESLint 配置（基于 Airbnb 风格指南），提交前运行 `npm run lint` 与 `npm run format` 自动修复缩进、引号与尾逗号问题。所有对外接口需附带 JSDoc 类型注释。

4. **提交信息格式**：采用 Conventional Commits 规范，提交信息首行使用 `<type>(<scope>): <subject>` 格式，其中 type 包括 feat、fix、docs、style、refactor、test、chore 等，scope 为可选的影响模块，subject 使用现在时祈使语气描述变更内容。

5. **发起 Pull Request**：将本地分支推送至远程仓库后，在 GitHub 中向 `main` 分支发起 Pull Request，PR 描述中需关联对应的 Issue 编号，并勾选自检清单（如通过 CI 检查、测试覆盖率无下降、文档已同步更新）。等待至少一位维护者进行 Code Review 后完成合并。

## 常见问题

**Q: 系统启动后提示数据库连接失败，如何排查？**

A: 请按以下顺序检查：首先确认 `DB_PATH` 环境变量或 `config/default.json` 中的数据库路径是否具有可写权限，尤其在 Linux 下需确保运行进程的用户对目录拥有读写权限。其次检查 SQLite3 原生模块是否在当前平台正确编译，可执行 `npm rebuild sqlite3` 重新构建。最后确认系统中是否存在其他进程占用数据库文件，SQLite 默认不支持并发写入，确保只有一个服务实例运行。若使用 Docker 部署，请确保挂载卷的宿主机目录权限正确映射。

**Q: 链接可用性巡检任务不执行或结果不更新，可能是什么原因？**

A: 首先检查 `config/default.json` 中 `monitor.interval` 参数是否为有效正整数（单位秒），并确认服务启动日志中是否打印 “Monitor scheduler started”。其次，巡检任务依赖出方向网络访问能力，请确保服务器防火墙未屏蔽对外 80 与 443 端口，且 DNS 解析正常。若目标链接为内网地址，需将 `monitor.allowPrivate` 配置项设为 true。最后，数据库中的 `links` 表需存在 `status` 和 `last_checked_at` 字段，若使用旧版数据库结构，请执行 `npm run migrate-latest` 进行模式升级。

**Q: 如何将现有浏览器书签批量导入到 HyperLink Navigator？**

A: 目前支持两种途径：第一，通过系统管理界面中的“导入书签”功能，上传从 Chrome 或 Firefox 导出的 HTML 书签文件（通常为 Netscape Bookmark 格式），系统将自动解析目录层级与链接标题；第二，若书签数量极大（超过 5000 条），建议使用命令行工具 `scripts/import-from-csv.js`，将书签整理为包含 `title, url, category_path, tags` 列的 CSV 文件，然后执行 `node scripts/import-from-csv.js --file ./bookmarks.csv` 完成导入。导入前请确认 CSV 文件使用 UTF-8 编码，且 URL 列格式合法，否则将跳过非法记录并在日志中输出警告。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
