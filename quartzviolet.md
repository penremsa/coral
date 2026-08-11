# LinkHub 技术资源导航站

LinkHub 是一个面向开发者与技术爱好者的外链资源聚合平台，专注于收集、分类与展示高质量的外部技术文档、社区工具与实时数据面板。本项目不直接提供数据内容，而是通过严格的链接筛选与分类体系，帮助用户快速定位所需信息源，降低信息检索成本。

项目目标用户包括运维工程师、全栈开发者、技术决策者以及科研人员。LinkHub 通过统一的入口，将分散在多个域名下的赛事数据、比分播报、实时排名等外部资源进行整合，并提供轻量级的本地代理与链接可用性检测机制，确保用户始终能够访问有效的目标地址。本项目适用于需要频繁查阅外部数据源但不愿记忆大量 URL 的技术团队，也适合作为内部知识库的外链前置层。

## 功能概览

- **外链分类管理**：按数据来源、内容类型、更新频率对收录的 URL 进行标签化分类，支持多维度筛选。
- **链接可用性检测**：定时对已收录的外链发送 HEAD 请求，自动标记不可用链接，并在前端界面高亮警告。
- **本地缓存代理**：为高频访问的外链提供只读缓存副本，减少目标服务器压力并提升响应速度。
- **访问统计看板**：记录每个外链的点击次数、最近访问时间与响应耗时，辅助分析资源热度。
- **自定义标签系统**：允许用户为任意链接添加自定义标签，便于个人或团队级别的二次组织。
- **导入导出功能**：支持批量导入用户自有的 URL 列表（JSON/CSV 格式），并支持导出为 Markdown 表格或 HTML 书签文件。
- **只读镜像模式**：针对部分响应缓慢的站点，生成纯文本结构的只读镜像页面，保留核心数据字段。
- **RSS 订阅生成**：为分类列表生成 RSS 订阅源，允许用户通过阅读器获取新增外链通知。

## 应用场景

**运维监控数据聚合**：运维团队可将多个赛事比分、实时排名类外链统一收录至 LinkHub，通过可用性检测面板快速确认各数据源的健康状态，替代人工逐一点击验证。

**技术调研资源整理**：开发者在进行竞品分析或技术选型时，可将搜集到的参考文档、API 文档、社区讨论帖等外链存入 LinkHub，利用标签与分类功能建立个人知识索引库。

**内部知识库外链前置层**：企业内部的 Confluence 或 Wiki 系统可通过 iframe 嵌入 LinkHub 的分类视图，使团队成员无需离开内网环境即可查阅经审核的外部数据源列表。

**教育培训资源导航**：讲师或培训师可将课程涉及的延伸阅读链接、在线工具、实验平台等收录至 LinkHub，学员通过统一入口访问，避免因输入错误 URL 导致的学习中断。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，假定已安装 Git 与 Node.js 18+。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/linkhub.git

# 进入项目目录
cd linkhub

# 安装依赖（使用 npm）
npm install

# 配置环境变量（复制示例配置）
cp .env.example .env

# 初始化本地数据库（SQLite）
npm run migrate

# 启动开发服务器（默认端口 3000）
npm run dev
```

生产环境部署建议使用 `npm run build` 构建静态文件，然后通过 `npm start` 启动生产服务。若使用 Docker，可执行 `docker build -t linkhub . && docker run -p 3000:3000 linkhub`。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用 nvm 管理版本 |
| npm | 9.x 或 10.x | 包管理器，用于安装依赖与执行脚本 |
| SQLite3 | 3.38+ | 嵌入式数据库，用于存储链接元数据与访问日志 |
| Git | 2.30+ | 版本控制工具，用于克隆仓库与拉取更新 |
| curl / wget | 任意现代版本 | 用于可用性检测脚本（外部依赖） |
| crond / systemd-timer | 任意版本 | 可选，用于定时执行检测任务 |
| 浏览器 | 支持 ES2022 的现代浏览器 | 前端界面运行环境（Chrome / Firefox / Edge 等） |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | `/docs/user-guide/classification.md` | 如何创建自定义分类？标签与分类的区别是什么？ |
| 用户手册 | `/docs/user-guide/import-export.md` | 支持哪些导入格式？导出时能否保留自定义标签？ |
| 运维手册 | `/docs/ops/health-check.md` | 可用性检测的频率如何配置？检测超时时间如何调整？ |
| 运维手册 | `/docs/ops/cache-strategy.md` | 本地缓存代理的存储路径在哪？缓存过期策略是什么？ |
| 开发指南 | `/docs/dev/api-endpoints.md` | 后端提供了哪些 RESTful 接口？如何新增一个外链？ |
| 开发指南 | `/docs/dev/frontend-structure.md` | 前端组件目录结构是怎样的？状态管理使用什么方案？ |
| 部署参考 | `/docs/deploy/docker-compose.yml` | 如何使用 Docker Compose 一键部署全套服务？ |
| 部署参考 | `/docs/deploy/reverse-proxy.md` | 如何配置 Nginx 作为反向代理并启用 HTTPS？ |

## 资源列表

本列表按内容主题进行分组，所有 URL 均来自用户原始数据，未作任何修改。

赛事比分类
- <code>leisuzuqiubisaijieguo.org.cn</code>
- <code>leisuzuqiusaichengjieguo.org.cn</code>
- <code>jiebaozuqiusaichengjieguo.org.cn</code>

体育数据平台类
- <code>pptiyubifensaicheng.org.cn</code>
- <code>pptiyusaichengjieguo.org.cn</code>
- <code>hupuzuqiusaichengjieguo.org.cn</code>

综合体育资讯类
- <code>wangyitiyubisaijieguo.org.cn</code>
- <code>xijiasaichengjieguo.org.cn</code>
- <code>dejiabisaijieguo.org.cn</code>
- <code>ouguanbisaijieguo.org.cn</code>

## 项目结构

```
linkhub/
├── backend/                         # 后端服务（Node.js + Express）
│   ├── controllers/                 # 控制器层，处理请求与响应
│   │   ├── linkController.js        # 链接增删改查逻辑
│   │   └── healthController.js      # 可用性检测与状态报告
│   ├── models/                      # 数据模型（SQLite ORM）
│   │   ├── Link.js                  # 链接实体模型（含标签、分类、点击量）
│   │   └── Log.js                   # 访问日志与检测记录模型
│   ├── routes/                      # 路由定义
│   │   ├── api.js                   # RESTful API 路由聚合
│   │   └── webhook.js               # 外部检测回调路由
│   ├── services/                    # 核心业务服务
│   │   ├── fetcher.js               # 外链内容抓取与缓存服务
│   │   ├── checker.js               # 可用性检测调度服务
│   │   └── rssGenerator.js          # RSS 订阅源生成服务
│   └── utils/                       # 工具函数
│       ├── urlValidator.js          # URL 格式校验与规范化
│       └── logger.js                # 结构化日志工具（JSON 格式）
├── frontend/                        # 前端界面（Vue 3 + Vite）
│   ├── src/
│   │   ├── components/              # 可复用 Vue 组件
│   │   │   ├── LinkTable.vue        # 链接列表表格组件（含排序与筛选）
│   │   │   ├── TagFilter.vue        # 标签筛选侧边栏组件
│   │   │   └── HealthBadge.vue      # 可用性状态徽章组件
│   │   ├── views/                   # 页面级视图
│   │   │   ├── Dashboard.vue        # 总览看板（统计卡片与趋势图）
│   │   │   └── CategoryView.vue     # 分类详情页
│   │   ├── stores/                  # Pinia 状态管理
│   │   │   ├── linkStore.js         # 链接数据与筛选状态
│   │   │   └── uiStore.js           # 界面布局与主题状态
│   │   └── assets/                  # 静态资源（CSS、图片、字体）
│   └── index.html                   # 入口 HTML
├── scripts/                         # 运维与工具脚本
│   ├── migrate.js                   # 数据库迁移脚本（建表与种子数据）
│   ├── healthCheck.js               # 独立运行的可用性检测脚本（可被 crond 调用）
│   └── exportMarkdown.js            # 将链接数据导出为 Markdown 表格的工具
├── config/                          # 配置文件目录
│   ├── default.json                 # 默认配置（端口、检测间隔、缓存大小）
│   └── custom.json                  # 用户自定义配置（覆盖默认值）
├── docs/                            # 完整文档（详见文档导航章节）
├── tests/                           # 单元测试与集成测试
│   ├── unit/                        # 服务层与工具函数单元测试（Jest）
│   └── integration/                 # API 路由与数据库集成测试（Supertest）
├── .env.example                     # 环境变量示例（JWT 密钥、检测超时等）
├── docker-compose.yml               # Docker Compose 编排文件
├── Dockerfile                       # 生产环境容器镜像构建文件
├── package.json                     # npm 项目清单与依赖声明
└── README.md                        # 本文件
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库，并 clone 到本地开发环境。创建新分支时请使用 `feature/` 或 `fix/` 前缀，命名应简要描述改动内容，例如 `feature/add-import-csv`。

2. 运行 `npm install` 安装所有依赖，并执行 `npm run migrate` 初始化本地测试数据库。建议在 `.env` 文件中将 `NODE_ENV` 设置为 `development` 以启用调试日志。

3. 编写代码或文档时，请遵循项目现有的 ESLint 与 Prettier 配置（可在 `package.json` 中查看具体规则）。所有新增功能必须附带至少一个单元测试用例，测试文件放置于 `tests/unit/` 或 `tests/integration/` 目录下。

4. 完成本地开发后，运行 `npm run test` 确保所有测试通过，运行 `npm run build` 确认前端构建无报错。提交前请执行 `npm run lint` 自动修复代码风格问题。

5. 发起 Pull Request 至主仓库的 `main` 分支，请在 PR 描述中明确说明改动目的、影响范围以及是否涉及数据库迁移或配置变更。PR 通过 CI 检查且至少获得一名维护者批准后即可合并。

## 常见问题

**问：可用性检测会频繁访问目标站点，是否会对目标服务器造成压力？**

答：检测请求为轻量级 HEAD 请求，不下载响应体，且默认检测间隔为 30 分钟，每个目标 URL 单次检测仅消耗极少量连接资源。用户可在 `config/custom.json` 中调整 `checkInterval` 参数（单位分钟）或完全禁用自动检测，改用手动触发。

**问：本地缓存代理是否存储完整页面内容？存储期限是多久？**

答：缓存代理仅存储响应状态码、响应头（不含 Cookie）以及前 2KB 的响应体文本，用于快速预览和可用性判断。完整页面内容不会被持久化存储。缓存条目默认有效期 24 小时，超时后自动清除。用户可在配置文件中调整 `cacheTTL` 参数修改有效期。

**问：如何迁移已收录的链接数据到另一台服务器？**

答：使用内置的导出功能，在界面中点击“导出全部”即可生成包含所有链接字段（标题、URL、标签、分类、备注）的 JSON 文件。在新服务器上启动 LinkHub 后，通过“批量导入”功能上传该 JSON 文件，系统会自动校验 URL 格式并跳过重复项。若需迁移数据库文件，可直接复制 `data/linkhub.sqlite` 文件至新服务器的相同相对路径。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
