# NexusIndex

NexusIndex 是一个轻量级、可自托管的综合性技术资源导航与外部链接聚合系统。项目定位为个人开发者、技术团队及研究机构提供有序、可扩展的互联网资源分类管理方案，解决信息碎片化、书签分散、链接失效追踪困难等常见问题。系统核心功能包括链接分类存储、状态监控、标签检索与访问统计，可作为内部知识库入口或对外公开的垂直领域门户。

项目采用模块化设计，后端基于 Python FastAPI 构建，前端使用 Vue 3 组件化框架，数据存储层支持 SQLite 与 PostgreSQL，适配单机部署与容器化集群环境。整体架构注重数据可移植性与检索效率，内置链接有效性检查引擎与访问频次分析模块，便于运维者持续维护资源质量。

## 功能概览

- **多级分类管理**：支持用户自定义分类树，无限层级嵌套，每个资源可归属多个分类标签，便于构建精细化的导航体系。

- **链接状态监控**：系统后台定时执行 HTTP 探活任务，自动标记失效链接并生成告警日志，支持手动重新验证与状态重置。

- **全文检索引擎**：基于资源标题、描述、分类路径及自定义标签构建倒排索引，支持模糊匹配与布尔检索，响应时间低于 200 毫秒。

- **访问统计看板**：记录每个外部链接的点击次数、最后访问时间与来源 IP 聚合数据，提供趋势图表与热门资源排行。

- **导入导出机制**：支持标准书签 HTML 格式导入（兼容 Chrome/Firefox 导出），以及 JSON/CSV 格式的批量导出，便于数据迁移与备份。

- **用户权限分级**：内置管理员、编辑者、访客三级角色体系，编辑者可新增或修改资源，访客仅可浏览与检索，管理员拥有系统配置与用户管理权限。

- **API 开放接口**：提供 RESTful 风格的公共 API，支持第三方应用获取资源列表、分类树及状态信息，便于集成至其他平台或自动化脚本。

- **响应式界面适配**：前端页面针对桌面端与移动端分别优化，支持明暗主题切换，提供无障碍访问辅助功能（屏幕阅读器兼容）。

## 应用场景

- **技术团队内部知识库入口**：研发团队可将常用开发文档、API 参考、内网工具地址、代码仓库链接统一录入 NexusIndex，按项目或技术栈分类，新成员入职时可快速获取所有必要外部资源，减少询问与查找时间。

- **开源项目生态导航页**：开源项目维护者可使用 NexusIndex 搭建项目周边的生态导航站，集中陈列相关教程、社区论坛、扩展插件列表、贡献者博客等外链，为社区参与者提供清晰的信息入口，降低项目上手门槛。

- **学术研究资料汇编**：研究人员可将领域内预印本平台、数据集下载站、学术搜索引擎、机构知识库等链接分类整理，通过状态监控功能及时发现失效数据源，保证研究过程中引用的外部资源长期可访问。

- **个人书签管理与迁移中心**：个人开发者可将分散在多个浏览器的书签导出后统一导入 NexusIndex，通过分类与标签整理，配合全文检索快速定位历史收藏的资源，同时利用导出功能生成标准化书签文件同步至其他设备。

## 快速开始

以下步骤适用于开发环境快速启动，生产环境部署请参考官方文档中的容器化或系统服务配置章节。

```bash
# 克隆项目仓库
git clone https://github.com/nexus-index/nexusindex.git
cd nexusindex

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate  # Windows 请使用 venv\Scripts\activate

# 安装后端依赖与前端构建工具
pip install -r requirements.txt
npm install --prefix frontend

# 初始化数据库表结构与默认分类数据
python scripts/init_db.py

# 构建前端静态资源
npm run build --prefix frontend

# 启动开发服务器（默认监听 8000 端口）
python app/main.py
```

启动后访问本地 8000 端口即可进入系统首页，默认管理员账号为 admin，密码在首次启动时由初始化脚本生成并输出至控制台日志。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 后端运行环境，建议使用 3.11 版本以获得更好性能 |
| Node.js | 18.x 或 20.x LTS | 前端构建与开发服务器依赖，需包含 npm 包管理器 |
| SQLite | 3.35 及以上 | 默认内置数据库，用于单机部署；生产环境可换用 PostgreSQL |
| PostgreSQL | 14.x 及以上（可选） | 生产环境推荐使用，需启用 pg_trgm 扩展以支持中文全文检索 |
| Redis | 6.x 及以上（可选） | 用于缓存热点查询结果与会话存储，提升高并发场景响应速度 |
| Nginx | 1.20 及以上（可选） | 推荐作为反向代理服务器，处理静态文件缓存与负载均衡 |
| 系统内存 | 最低 512 MB | 建议 1 GB 以上；内存主要被 Python 进程与前端构建工具占用 |
| 磁盘空间 | 最低 200 MB | 初始安装占用约 150 MB，日志与数据库增长视数据量而定 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `/docs/user/quickstart.md` | 如何注册账号、添加第一条链接、创建分类以及设置标签？ |
| 管理员手册 | `/docs/admin/configuration.md` | 如何修改站点名称、调整监控频率、配置邮件告警与备份策略？ |
| 开发参考 | `/docs/dev/api_reference.md` | API 端点列表、请求与响应格式、鉴权方式及调用示例？ |
| 部署运维 | `/docs/deploy/docker_compose.md` | 如何使用 Docker Compose 一键启动全套服务栈（含 PostgreSQL + Redis + Nginx）？ |
| 数据迁移 | `/docs/deploy/migration.md` | 如何从 SQLite 迁移至 PostgreSQL，或从旧版本升级数据库 Schema？ |
| 故障排查 | `/docs/troubleshooting/common_issues.md` | 链接状态检查超时、前端资源加载失败、搜索无结果等常见问题如何解决？ |

## 资源列表

以下为 NexusIndex 项目收录的外部资源链接，按类别分组陈列。所有链接均以原始格式呈现，未做任何协议补全或域名改写。

**综合门户类**

<code>mimiseyingyuan.org.cn</code>

<code>qingqingcaoyuanyazhou.org.cn</code>

<code>jiuyimadou.org.cn</code>

**专业内容类**

<code>zhongwenzaixianyiqu.org.cn</code>

<code>yazhoutiantangse.org.cn</code>

<code>guochanyoucuyouhuang.org.cn</code>

**社区与交流类**

<code>yejiujiu.org.cn</code>

<code>madourenqi.org.cn</code>

<code>mengbaijiangzaixian.org.cn</code>

**综合精选类**

<code>jiujiuzhelidoushijingpin.org.cn</code>

## 项目结构

```
nexusindex/
├── app/                                # 后端主程序目录
│   ├── main.py                         # FastAPI 应用入口，注册路由与中间件
│   ├── config.py                       # 配置加载模块（环境变量、默认值、命令行参数）
│   ├── models/                         # 数据模型层（SQLAlchemy ORM 定义）
│   │   ├── __init__.py
│   │   ├── link.py                     # 链接资源表模型（标题、URL、分类外键、状态、点击量）
│   │   ├── category.py                 # 分类树表模型（名称、父级 ID、排序权重）
│   │   └── user.py                     # 用户与权限表模型（用户名、密码哈希、角色）
│   ├── services/                       # 业务逻辑服务层
│   │   ├── link_monitor.py             # 链接状态监控服务（异步 HTTP 探活、超时处理、重试机制）
│   │   ├── search_engine.py            # 全文检索引擎（构建倒排索引、查询解析、相关性排序）
│   │   └── stats_collector.py          # 访问统计收集器（记录点击、聚合日活、生成排行）
│   ├── api/                            # API 路由层
│   │   ├── v1/                         # 版本化 API 端点
│   │   │   ├── links.py                # 链接增删改查接口
│   │   │   ├── categories.py           # 分类管理接口
│   │   │   └── search.py               # 搜索接口
│   │   └── deps.py                     # 依赖注入（数据库会话、当前用户鉴权）
│   └── utils/                          # 工具函数库
│       ├── validators.py               # URL 格式校验、分类路径合法性检查
│       └── exporters.py                # 书签 HTML / JSON / CSV 导出生成器
├── frontend/                           # Vue 3 前端工程目录
│   ├── src/
│   │   ├── components/                 # 可复用 UI 组件（导航栏、分类树、链接卡片、搜索栏）
│   │   ├── views/                      # 页面级组件（首页、分类浏览、统计看板、管理后台）
│   │   ├── stores/                     # Pinia 状态管理（用户会话、分类缓存、搜索关键词）
│   │   └── router/                     # Vue Router 路由定义
│   ├── public/                         # 静态资源（favicon、站点图标、默认占位图）
│   └── package.json                    # 前端依赖清单与构建脚本
├── scripts/                            # 运维与开发辅助脚本
│   ├── init_db.py                      # 初始化数据库表与默认分类种子数据
│   ├── import_bookmarks.py             # 从 HTML 书签文件批量导入链接
│   └── backup_data.py                  # 定时备份数据库与配置文件的脚本
├── tests/                              # 单元测试与集成测试目录
│   ├── test_api/                       # API 端点测试（pytest + httpx）
│   └── test_services/                  # 业务逻辑层测试（监控引擎、搜索排序）
├── docs/                               # 完整项目文档（详见上方文档导航）
├── requirements.txt                    # Python 后端依赖（FastAPI、SQLAlchemy、httpx、alembic 等）
├── docker-compose.yml                  # 生产级容器编排配置（含 PostgreSQL、Redis、Nginx）
└── README.md                           # 本文件
```

## 贡献指南

NexusIndex 遵循开源社区协作规范，欢迎各类形式的贡献，包括但不限于新增功能、修复缺陷、完善文档、翻译界面及提供使用案例。

1. **提交 Issue 进行需求讨论**：在 GitHub Issues 页面新建议题，描述你发现的问题或希望新增的功能。请使用提供的模板填写，包含复现步骤、环境信息及预期行为，便于维护者快速响应。

2. **Fork 仓库并创建特性分支**：从主仓库 Fork 至个人账户，基于最新 main 分支创建以 `feature/` 或 `fix/` 为前缀的分支名，例如 `feature/add-ldap-auth`。请确保分支名称简洁描述改动内容。

3. **编写代码与测试用例**：遵循项目现有代码风格（Python 使用 PEP 8，Vue 使用 ESLint 配置）。新增功能需包含对应的单元测试，确保测试覆盖率不低于 80%。所有公共 API 与核心函数须添加 docstring 或注释。

4. **提交 Pull Request 并描述变更**：推送分支至个人仓库后，向主仓库 main 分支发起 Pull Request。PR 描述中请关联相关 Issue 编号，逐项列出改动点，并附上本地测试通过的截图或日志。维护者会在 3 个工作日内进行 Review。

5. **签署开发者原创声明**：首次贡献时需在 PR 评论中确认代码为本人原创且同意采用 MIT 许可证发布。若引用第三方代码，需在 PR 中明确标注来源与许可证兼容性。

## 常见问题

**问：链接状态监控显示超时或拒绝连接，但浏览器可以正常访问，如何调整检测参数？**

答：状态监控服务默认使用 5 秒超时和 3 次重试策略，且禁止跟随重定向。部分网站可能因防火墙规则、地区限制或反爬机制对非浏览器 User-Agent 返回异常状态。您可以在系统配置页面（管理员权限）调整 `MONITOR_TIMEOUT`、`MONITOR_RETRIES` 以及 `MONITOR_USER_AGENT` 参数。若需完全跳过特定域名的监控，可在链接编辑页面勾选“禁用监控”选项。

**问：导入 Chrome 导出的书签 HTML 文件时部分链接丢失分类信息，如何处理？**

答：Chrome 书签导出文件中的分类层级以 DL/DT 结构存储，但不同浏览器版本可能存在细微差异。导入脚本默认按一级文件夹作为分类名，若文件夹为空或包含特殊字符可能导致分类创建失败。建议导入前检查 HTML 文件中的文件夹名称是否包含系统不允许的字符（如 `/`、`\`、`#`）。您也可以使用 CSV 模板批量导入，该方式支持手动指定分类路径，容错性更高。若导入后仍有遗漏，可查看 `logs/import_errors.log` 文件获取详细错误行信息。

**问：全文搜索对中文分词效果不佳，单字搜索返回结果不准确，有何优化建议？**

答：SQLite 内置的 FTS5 扩展默认使用简单分词器，对中文支持有限。若部署于生产环境，我们强烈建议切换至 PostgreSQL 并启用 `zhparser` 或 `jieba` 中文分词扩展，可在配置文件中将 `SEARCH_ENGINE` 设为 `postgres_zh` 并重启服务。对于已存在的 SQLite 部署，可通过在搜索词前后添加双引号进行短语精确匹配，或使用 `+` 与 `-` 符号强制包含/排除特定关键词，这些运算符可改善搜索结果的相关性排序。

## 许可证

MIT License

Copyright (c) 2026 NexusIndex Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
