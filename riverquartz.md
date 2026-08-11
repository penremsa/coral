# Terminus Navigator

Terminus Navigator 是一个面向技术调研、内容聚合与信息检索场景的轻量化外链导航与资源元数据索引系统。项目定位为技术团队、开源社区与个人研究者的外链汇总中间件，解决多源异构资源链接分散、状态不可见、分类模糊、复用困难等问题，提供结构化的链接资产托管与基础状态探测能力。

目标用户包括技术文档维护者、社区运营人员、渗透测试与情报分析方向的工程师，以及需要长期维护大量外链资源的项目管理者。Terminus Navigator 不提供内容代理、不修改原始资源、不规避访问策略，仅作为链接清单的版本化存储与可视化外壳，保持对被索引资源的最大尊重与最小干预。

## 功能概览

- **外链资产版本化管理** 支持对批量链接进行增删改查与变更记录追踪，每个链接条目可绑定标签、备注与状态标记。

- **批量链接状态探测** 通过可配置的超时与重试策略，对索引链接进行定期或按需的 HTTP 头探测，返回状态码归类与可达性摘要。

- **多级分类与标签系统** 支持无限层级目录与扁平标签双维度组织方式，适配不同使用习惯，分类树可导出为 JSON / YAML 结构。

- **链接元数据补充** 支持为每个链接手动填写或自动抓取页面标题、描述、语言、证书有效期等基础元数据，辅助快速筛选。

- **只读只写双模式访问** 提供公开只读视图用于展示已核准链接，以及认证写入模式用于批量导入、编辑与版本回滚。

- **全文与字段级检索** 基于链接 URL、标题、标签、备注内容进行快速模糊匹配，检索结果可排序并高亮匹配片段。

- **导入导出适配器** 内置对 CSV、JSON、Markdown 列表、纯文本换行列表的导入导出，便于与现有文档体系互操作。

## 应用场景

- **技术文档外链维护** 开源项目文档站中常引用大量外部依赖、教程、参考实现，Terminus Navigator 可作为独立外链仓库，通过 API 将链接列表嵌入文档站点，避免链接散落在多个 Markdown 文件中难以更新。

- **安全研究情报聚合** 威胁情报分析人员需要长期跟踪多个日志源、样本库、CVE 公告页面，项目支持对链接状态进行定时探测并记录状态变化趋势，辅助判断情报源可用性。

- **社区资源推荐墙** 技术社区或学习小组可利用公共只读视图搭建资源推荐页面，分类展示学习资料、工具站、视频资源等，运营人员通过后台批量更新链接，无需直接改动前端代码。

- **项目迁移外链审计** 在网站域名更换或 HTTPS 强制升级过程中，运维团队可将全部历史外链导入系统，通过状态探测与元数据抓取快速识别需要更新的链接，生成迁移审计报告。

## 快速开始

以下步骤适用于开发环境快速启动 Terminus Navigator 实例。

```bash
# 克隆项目仓库
git clone https://github.com/terminus-navigator/navigator.git
cd navigator

# 安装项目依赖（使用 npm，Node.js 18+）
npm install

# 复制环境变量示例文件并配置
cp .env.example .env

# 初始化本地 SQLite 数据库与默认分类数据
npm run init-db

# 以开发模式启动服务，默认监听 3000 端口
npm run dev
```

启动后访问 `http://localhost:3000` 进入只读视图，通过 `/admin` 路径进入管理界面，默认管理员账号为 `admin`，初始密码在首次启动时输出于控制台日志中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，建议使用官方预编译二进制或 nvm 管理 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖与执行脚本 |
| SQLite | 3.38 或更高 | 嵌入式数据库，用于存储链接元数据与分类树，无需额外安装 |
| 可用磁盘空间 | 至少 200 MB | 用于存放数据库文件、日志与缓存元数据 |
| 内存 | 最低 512 MB，推荐 1 GB | 运行服务与执行状态探测任务时的内存占用 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user/quick-start.md | 如何快速部署、登录、创建第一条链接记录与分类 |
| 用户手册 | /docs/user/import-export.md | 支持哪些导入导出格式，批量操作的具体步骤与字段映射 |
| 开发指南 | /docs/dev/api-reference.md | RESTful API 各端点的请求参数、响应结构与错误码 |
| 运维参考 | /docs/ops/health-check.md | 状态探测模块的配置项、超时调优与告警阈值设定 |

## 资源列表

以下为 Terminus Navigator 项目当前索引的外部资源链接汇总，按功能类别划分。所有链接均保留用户原始输入格式，不做任何协议补全或域名改写。

语言与字幕资源

<code>shipinzaixianmianfeiguankanw.org.cn</code>

<code>zhongwenzimurenqiwuma.org.cn</code>

<code>zhongchuzaixianzhongwenzimu.org.cn</code>

<code>youmazhongwenzimu.org.cn</code>

<code>zaixianguankanzhongwenzimu1.org.cn</code>

<code>zhongwenzimuzaixianmianfeikan1.org.cn</code>

<code>zhongwenzaixianzimumianfeigaoqing1.org.cn</code>

主题与分类内容

<code>nannvchuangshangdapuke.org.cn</code>

<code>xiaojirushuimitaozaixian.org.cn</code>

<code>guochanheisizaixianguankan.org.cn</code>

## 项目结构

```
navigator/
├── src/
│   ├── core/                         # 核心业务逻辑层
│   │   ├── link.service.js           # 链接增删改查、状态更新、标签关联
│   │   ├── category.service.js       # 分类树构建、移动、合并操作
│   │   └── probe.service.js          # 基于 node-fetch 的状态探测调度器
│   ├── api/                          # RESTful API 路由与控制器
│   │   ├── v1/                       # API 版本 v1 实现
│   │   │   ├── links.controller.js   # /api/v1/links 路由处理
│   │   │   └── categories.controller.js
│   │   └── middleware/               # 身份验证、日志、错误处理中间件
│   ├── db/                           # 数据库层
│   │   ├── migrations/               # SQLite 数据库迁移脚本（按版本号）
│   │   ├── seed/                     # 初始分类与示例链接数据
│   │   └── client.js                 # 数据库连接池与查询构建器封装
│   ├── ui/                           # 服务端渲染视图与静态资源
│   │   ├── public/                   # 前端 CSS、JavaScript、图标资源
│   │   ├── views/                    # EJS 模板，含只读列表与后台管理界面
│   │   └── components/               # 可复用的 UI 片段（分页、筛选栏）
│   └── utils/                        # 工具函数集
│       ├── validator.js              # URL 格式校验、域名黑名单过滤
│       ├── exporter.js               # JSON / CSV / Markdown 导出生成器
│       └── logger.js                 # 结构化日志，支持 JSON 与普通文本格式
├── config/                           # 环境配置文件与默认参数
│   ├── default.yaml                  # 默认超时、重试、分页大小配置
│   └── custom/                       # 用户自定义配置覆盖目录（不提交至 Git）
├── tests/                            # 单元测试与集成测试
│   ├── unit/                         # 针对 service 层与 util 层的单元测试
│   └── integration/                  # API 端到端测试与数据库状态校验
├── docs/                             # 用户文档与开发文档（详见文档导航）
├── scripts/                          # 辅助运维脚本
│   ├── init-db.sh                    # 初始化数据库与种子数据
│   └── batch-import.sh               # 从外部 CSV 批量导入链接
├── .env.example                      # 环境变量示例文件
├── package.json                      # npm 项目配置与依赖声明
├── README.md                         # 项目说明文档（当前文件）
└── LICENSE                           # MIT 许可证全文
```

## 贡献指南

Terminus Navigator 欢迎外部贡献者参与功能改进、文档完善与问题修复。请遵循以下步骤提交贡献：

1. 在 GitHub 上 Fork 本仓库至个人命名空间，并克隆至本地开发环境。建议在开发前阅读 `/docs/dev/development-setup.md` 了解本地调试配置。

2. 创建特性分支，分支命名采用 `feat/`、`fix/` 或 `docs/` 前缀，后跟简短描述，例如 `feat/add-batch-tag-edit`。避免在主分支上直接修改。

3. 实现功能或修复问题后，确保运行 `npm run test` 通过全部单元测试与集成测试，并补充新增功能对应的测试用例。若涉及 API 变更，同步更新 `/docs/dev/api-reference.md` 中的示例与字段说明。

4. 提交代码时遵循 Conventional Commits 规范，提交信息应清晰描述变更内容与动机。提交前执行 `npm run lint` 检查代码风格。

5. 通过 GitHub 发起 Pull Request 至主仓库的 `main` 分支，PR 描述中需说明变更背景、实现方式与测试覆盖情况。维护者将在 3 个工作日内进行 Review，并根据反馈进行修改直至合并。

## 常见问题

**Q：状态探测模块是否会频繁访问外部链接，导致被目标服务器封禁？**

A：探测模块默认采用礼貌爬取策略，并发请求数限制为 5，超时设为 10 秒，并遵守 robots.txt 的全局 Crawl-delay 指令。用户可在配置文件中调整 `probe.interval` 与 `probe.maxConcurrency` 参数。建议对大型链接列表使用分批探测模式，避免在短时窗口内产生大量请求。

**Q：是否可以完全离线运行 Terminus Navigator？**

A：核心链接管理与分类功能完全支持离线运行，无需外网访问。状态探测与元数据抓取功能需要访问目标链接所在网络，若网络受限可关闭探测模块或配置代理。数据库与前端 UI 均在本地运行，不依赖外部 CDN 资源，所有静态资源已内联至发布包中。

**Q：如何将现有 Markdown 文档中的链接列表批量迁移至系统？**

A：项目提供 `import:markdown` 脚本，可解析 Markdown 文件中的所有 `[text](url)` 与裸链接，自动提取 URL 并生成导入预备 CSV。用户随后可在管理界面中完成分类映射与标签补充。详细步骤请参考 `/docs/user/import-export.md` 中关于 Markdown 导入的章节。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
