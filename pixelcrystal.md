# ResourceHub

ResourceHub 是一个面向技术内容创作者、开源文档维护者以及互联网资源管理者的技术资源导航与外部链接聚合系统。该项目旨在解决技术文档中外部链接分散、失效、难以追踪的问题，通过结构化的链接管理与分类视图，帮助团队和个人高效维护项目文档中的引用资源。目标用户包括开源项目维护者、技术博客作者、文档工程师以及需要系统化管理外链资源的开发团队。

## 功能概览

- **链接分类管理**：支持按技术领域、资源类型、使用场景对链接进行多级分类，便于快速定位和批量操作。
- **链接健康检查**：定时检测外部链接的可访问性，自动标记失效链接并生成报告，减少文档中的死链数量。
- **结构化导出**：支持将链接列表导出为 Markdown、JSON、CSV 等格式，方便集成到文档流水线或静态站点生成器中。
- **标签与检索系统**：为每条链接添加自定义标签，支持全文检索与标签筛选，提升大规模链接库的查找效率。
- **访问统计看板**：记录链接被点击的次数、来源页面与时间分布，辅助评估资源的实际使用价值。
- **权限与审核流程**：支持多用户环境下的链接提交、审核、发布流程，适合团队协作场景下的资源管理。
- **API 接口支持**：提供 RESTful API 用于链接的增删改查及状态查询，便于与其他自动化工具或脚本集成。

## 应用场景

1. **开源项目文档站维护**：开源项目通常引用大量第三方库、教程、规范文档等外部资源。ResourceHub 可帮助维护者集中管理这些引用，定期检查有效性，并在版本发布前生成完整的资源清单。

2. **技术博客与知识库构建**：技术作者在撰写文章时常需要引用多篇参考文献或工具站点。使用 ResourceHub 可将所有外链统一存储并分类，写作时仅需插入链接 ID，避免重复输入长 URL，同时便于文章迁移时批量更新。

3. **团队内部技术雷达管理**：企业技术团队可借助 ResourceHub 建立内部技术资源库，收录常用开发工具、云服务控制台、内部文档系统、监控面板等入口，结合健康检查功能及时发现服务地址变更。

4. **离线文档资源打包**：对于需要生成离线版本的技术手册或培训材料，ResourceHub 支持导出完整的链接清单及元数据，配合脚本可批量预取页面快照或检查资源可用性，保障离线内容的完整性。

5. **合规审计与链接追溯**：在金融、医疗等受监管行业中，对外部引用有严格的合规要求。ResourceHub 的审核日志和版本历史功能可完整记录链接的添加、修改和删除操作，满足审计追溯需求。

## 快速开始

以下步骤指导您在本地环境快速启动 ResourceHub 服务。

```bash
# 1. 克隆代码仓库
git clone https://github.com/resourcehub/resourcehub.git
cd resourcehub

# 2. 安装依赖（使用 Python 虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化配置与数据库
cp .env.example .env
# 编辑 .env 文件，设置数据库连接等必要参数
python scripts/init_db.py

# 4. 运行开发服务器
python app.py --host 0.0.0.0 --port 8080
```

访问 `http://localhost:8080` 即可进入管理控制台。默认管理员账号为 `admin@resourcehub.local`，初始密码在首次启动时由初始化脚本输出至控制台日志，请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 - 3.12 | 核心运行环境，推荐使用 3.11 以获得最佳性能 |
| PostgreSQL | 14.x 及以上 | 主数据库，用于存储链接元数据、用户信息及操作日志 |
| Redis | 7.x 及以上 | 缓存与任务队列后端，用于健康检查异步任务及会话存储 |
| Node.js | 20.x LTS | 仅用于前端资源构建，生产环境若使用预构建静态文件可省略 |
| Nginx | 1.24.x 及以上 | 生产环境推荐反向代理服务器，用于静态资源服务与负载均衡 |
| Docker / Docker Compose | 最新稳定版 | 可选，用于容器化部署，开发环境可快速拉起全部依赖服务 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user/quick-start.md` | 如何安装部署、配置管理员账户、添加第一批链接 |
| 用户手册 | `/docs/user/link-management.md` | 如何批量导入/导出链接、设置分类标签、启用健康检查 |
| 开发指南 | `/docs/dev/api-reference.md` | REST API 的端点列表、请求/响应格式、认证方式 |
| 开发指南 | `/docs/dev/contributing.md` | 代码风格、提交规范、测试流程、PR 审核标准 |
| 运维手册 | `/docs/ops/monitoring.md` | 如何配置 Prometheus 指标采集、日志轮转、备份恢复策略 |
| 架构设计 | `/docs/architecture/data-model.md` | 数据库 ER 图、缓存策略、异步任务队列的设计原理 |

## 资源列表

本项目的资源导航模块收录了以下外部链接，按类别组织以便查阅。

技术参考与开发社区

<code>91shaofu.org.cn</code>

<code>97renqi.org.cn</code>

<code>jiujiulunli.org.cn</code>

设计素材与视觉资源

<code>zhongwenzimuzhifusiwa.org.cn</code>

<code>zhongwenzimumeinv.org.cn</code>

<code>meinvwangzhan.org.cn</code>

<code>oumeirenqi.org.cn</code>

多媒体与娱乐内容

<code>chengrenjuchang.org.cn</code>

<code>chengrenwuyejuchang.org.cn</code>

<code>siwazhongwenzimu.org.cn</code>

## 项目结构

```
resourcehub/
├── app/                             # 主应用目录
│   ├── api/                         # REST API 路由与控制器
│   │   ├── v1/                      # API v1 版本实现
│   │   │   ├── links.py             # 链接 CRUD 接口
│   │   │   ├── categories.py        # 分类管理接口
│   │   │   ├── checks.py            # 健康检查触发与结果查询
│   │   │   └── auth.py              # 认证与令牌接口
│   │   └── __init__.py
│   ├── models/                      # 数据库模型定义 (SQLAlchemy ORM)
│   │   ├── link.py                  # 链接实体模型
│   │   ├── user.py                  # 用户与角色模型
│   │   ├── check_record.py          # 健康检查历史记录
│   │   └── tag.py                   # 标签模型及关联表
│   ├── services/                    # 业务逻辑层
│   │   ├── link_service.py          # 链接管理核心逻辑
│   │   ├── check_service.py         # 异步健康检查调度与执行
│   │   ├── export_service.py        # 链接导出为多种格式
│   │   └── stats_service.py         # 点击统计与聚合计算
│   ├── templates/                   # Jinja2 服务端模板 (管理后台界面)
│   │   ├── dashboard.html           # 总览看板
│   │   ├── link_list.html           # 链接列表与搜索
│   │   └── link_edit.html           # 链接新增/编辑表单
│   └── static/                      # 编译后的前端静态资源 (CSS, JS, 图片)
├── scripts/                         # 辅助脚本与工具
│   ├── init_db.py                   # 数据库初始化与种子数据填充
│   ├── migrate_legacy.py            # 从旧版链接管理系统迁移数据
│   └── export_snapshot.py           # 定时导出全量链接快照
├── tests/                           # 单元测试与集成测试
│   ├── unit/                        # 各模块单元测试
│   └── integration/                 # API 与数据库集成测试
├── docs/                            # 项目文档 (见上方文档导航)
├── docker/                          # Docker 容器化部署相关文件
│   ├── Dockerfile                   # 主应用镜像构建文件
│   └── docker-compose.yml           # 全栈服务编排 (app + postgres + redis)
├── config/                          # 配置文件目录
│   ├── settings.py                  # 基础配置类
│   ├── development.py               # 开发环境配置
│   ├── production.py                # 生产环境配置
│   └── testing.py                   # 测试环境配置
├── logs/                            # 日志文件存储目录 (运行时生成)
├── requirements.txt                 # Python 依赖清单
├── pyproject.toml                   # 项目元数据与构建工具配置 (PEP 621)
├── .env.example                     # 环境变量模板文件
└── README.md                        # 本文件
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于代码、文档、测试用例和问题反馈。请遵循以下步骤参与本项目开发。

1.  **提交 Issue 或 Discussion**：在开始实质性工作前，请先在 GitHub Issues 中描述您发现的问题或希望新增的功能，或在 Discussions 中提出设计想法，避免重复劳动或方向偏差。
2.  **派生 (Fork) 仓库并创建分支**：从主仓库派生代码到您的个人账户下，然后基于 `main` 分支创建一个新的功能分支，分支命名建议使用 `feature/描述` 或 `fix/描述` 格式。
3.  **编写代码与测试**：确保您的代码遵循项目代码风格 (PEP 8 + Black 格式化)，并为新增或修改的逻辑编写相应的单元测试，保证测试覆盖率为不低于 85%。
4.  **签署开发者原创声明 (DCO)**：提交 Pull Request 前，请确保每个提交均包含 `Signed-off-by` 信息 (可使用 `git commit -s` 自动添加)，以表示您同意开发者原创声明 (Developer Certificate of Origin)。
5.  **发起 Pull Request (PR)**：向主仓库的 `main` 分支发起 PR，清晰描述变更内容、关联 Issue 编号以及测试结果摘要。PR 需要至少一位项目维护者审核批准后方可合并。

## 常见问题

**问：健康检查任务会消耗大量网络带宽或影响源站性能吗？**

答：健康检查采用 HEAD 请求优先策略，仅获取响应头信息而不下载完整页面内容，单次请求数据量极小。检查频率默认为每 24 小时一次，且支持用户自定义检查间隔和超时时间。对于大规模链接集，系统内置了指数退避重试和并发控制机制，避免对源站造成突发压力。您也可以手动将特定域名加入白名单以跳过检查。

**问：如果我要迁移到其他数据库（如 MySQL 或 SQLite），需要做什么修改？**

答：项目使用 SQLAlchemy ORM，理论上支持所有主流关系型数据库。您只需在 `.env` 文件中修改 `DATABASE_URL` 连接字符串为对应的驱动和地址即可。但请注意，部分高级功能（如 JSONB 字段的查询、全文检索）在不同数据库中的实现存在差异，若使用 SQLite 可能会损失部分性能优化特性。生产环境强烈推荐使用 PostgreSQL。

**问：如何备份我管理的所有链接数据？**

答：您可以通过两种方式进行备份。其一是使用 PostgreSQL 原生的 pg_dump 工具进行完整数据库备份，这也是推荐的方式；其二是使用项目内置的导出功能，在管理后台点击“导出全部”按钮，系统将生成包含所有链接及其元数据的 JSON 或 CSV 文件。此外，您也可以设置定时任务调用 `scripts/export_snapshot.py` 脚本，实现自动化的定期快照备份。

## 许可证

本项目采用 MIT 许可证。您可以自由地使用、修改、分发本软件，包括用于商业目的，但需保留原始版权声明和免责声明。详见项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:38
