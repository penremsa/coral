# HydraLink 技术资源导航站

HydraLink 是一个面向开发人员、技术研究人员与互联网内容分析者的高密度外链聚合与分类管理工具。本项目定位于解决在复杂网络环境下对特定领域资源的高效检索、状态监控与结构化归档问题，适用于需要批量维护大量域名数据源、定期验证资源可用性以及进行内容类型初步判定的工程技术团队。HydraLink 不生产内容，不提供代理或翻墙服务，仅作为公开互联网资源的元数据索引系统运行，所有收录链接均来源于公开渠道。

## 功能概览

- **批量链接状态巡检**：自动对入库链接进行 HTTP/HTTPS 可访问性探测，记录响应码与响应时间，支持异常告警。
- **多维度分类标签体系**：允许用户为每个链接自定义标签，支持按语种、内容主题、站点类型等维度进行筛选。
- **结构化元数据提取**：对目标页面自动提取标题、描述、关键词及内容类型，辅助快速判断站点性质。
- **自定义监控频率**：可针对不同重要程度的链接设置独立扫描周期，最低支持每分钟一次。
- **历史快照对比**：记录每次巡检的页面摘要信息，支持差异对比，用于检测站点改版或内容变更。
- **开放 RESTful API**：所有核心功能均提供 JSON 接口，方便集成至第三方运维平台或数据中台。
- **数据导入导出**：支持 CSV/JSON 格式的批量链接导入与备份导出，便于团队协作与数据迁移。

## 应用场景

- **学术研究资源归档**：研究人员在开展网络语言学或区域文化传播研究时，可利用 HydraLink 对特定语种或主题的域名集合进行长期可用性跟踪，确保研究数据源的持续有效。
- **内容审核与分类辅助**：内容安全团队可将待审核的域名列表导入系统，利用元数据提取功能初步判定站点内容倾向，提高人工复审效率。
- **运维监控面板**：运维人员将业务依赖的第三方数据源链接纳入监控，通过 Dashboard 实时掌握各资源端口的健康状态，快速定位故障。
- **竞品信息收集**：市场分析团队对竞品相关域名进行定期快照对比，捕捉页面结构或运营内容的变化节奏，为决策提供间接依据。
- **个人书签管理升级**：开发者可将个人收藏的大量技术博客、文档站点、工具链接迁移至 HydraLink，利用标签和状态监控代替传统浏览器书签的混乱管理。

## 快速开始

以下步骤适用于 Linux / macOS 系统，Windows 用户建议使用 WSL2 环境。

```bash
# 1. 克隆项目仓库
git clone https://github.com/hydra-link/hydralink-core.git
cd hydralink-core

# 2. 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化配置文件与环境变量
cp .env.example .env
# 编辑 .env 文件，填入数据库连接信息与管理员邮箱

# 4. 执行数据库迁移
python manage.py migrate

# 5. 启动开发服务
python manage.py runserver --host 0.0.0.0 --port 8000
```

访问 `http://localhost:8000` 即可进入仪表板，默认管理员账号为 `admin@hydralink.local`，初始密码在首次启动时打印于终端日志中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 暂未完成兼容性测试 |
| PostgreSQL | 13.0 及以上 | 主要数据存储，用于存放链接元数据与巡检日志 |
| Redis | 6.2 及以上 | 缓存与任务队列后端，支撑异步巡检任务调度 |
| Node.js | 16.0 及以上 | 仅用于前端资产构建，后端运行不依赖 |
| Nginx | 1.18 及以上 | 生产环境推荐反向代理与静态资源服务 |
| Celery Worker | 5.2 及以上 | 作为独立进程执行周期性巡检任务，需与 Redis 配合 |
| Supervisor | 4.2 及以上 | 用于生产环境守护 Celery 与 Gunicorn 进程（非必需） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何注册、登录、添加链接、创建标签、查看巡检报告 |
| 运维指南 | `/docs/ops-guide/` | 如何部署生产环境、配置 SSL、调优巡检并发数、备份数据 |
| 开发者手册 | `/docs/dev-guide/` | API 鉴权方式、自定义巡检插件开发、数据库表结构说明 |
| 架构设计 | `/docs/architecture/` | 系统模块划分、消息队列流转逻辑、水平扩展方案 |
| 常见问题 | `/docs/faq/` | 巡检超时怎么办、如何排除特定链接、如何迁移至新服务器 |

## 资源列表

本导航站收录的公开互联网资源按内容主题划分为以下子类别，所有链接均保持用户原始输入格式原样呈现，未做任何协议补全或规范化处理。

**综合语种与内容类**

- <code>zhongwenrenqi.org.cn</code>
- <code>renqishaofu.org.cn</code>
- <code>rihanlunli.org.cn</code>

**多媒体与平台类**

- <code>bajiaoshipinapp.org.cn</code>
- <code>zhongwenzimusiwa.org.cn</code>
- <code>renqiyouma.org.cn</code>

**垂直领域与社区类**

- <code>xiaodiaowang.org.cn</code>
- <code>chengrenjingpin18.org.cn</code>
- <code>guoyuav.org.cn</code>
- <code>jiujiurenqi.org.cn</code>

以上链接均为公开互联网上存在的域名，HydraLink 仅将其作为数据源示例纳入测试集合，不代表项目方对其中内容的认可或背书。

## 项目结构

```
hydralink-core/
├── src/                            # 核心应用源码
│   ├── core/                       # 主配置模块（settings, urls, wsgi）
│   ├── apps/                       # 功能应用集合
│   │   ├── links/                  # 链接管理：增删改查、标签、分组
│   │   ├── probes/                 # 巡检引擎：异步请求、响应解析、超时处理
│   │   ├── alerts/                 # 告警模块：邮件/飞书/钉钉通知
│   │   ├── api/                    # RESTful API 视图与序列化器
│   │   └── users/                  # 用户认证与权限管理
│   ├── libs/                       # 通用工具库（自定义装饰器、中间件、缓存封装）
│   └── tasks/                      # Celery 任务定义（周期性巡检、数据清理）
├── tests/                          # 单元测试与集成测试用例
│   ├── unit/                       # 各模块独立测试
│   └── integration/                # 端到端流程测试（含 Mock 外部请求）
├── scripts/                        # 运维辅助脚本（数据迁移、批量导入、日志切割）
├── frontend/                       # 前端工程（Vue 3 + Vite）
│   ├── src/                        # 前端源码（组件、视图、状态管理）
│   └── dist/                       # 生产构建产物（由 CI 自动生成）
├── docs/                           # 完整项目文档（用户手册、运维指南、API 参考）
├── deploy/                         # 部署相关模板（docker-compose, nginx.conf, systemd 单元）
├── logs/                           # 日志存储目录（按日期滚动，保留 30 天）
├── .env.example                    # 环境变量配置模板
├── requirements.txt                # Python 生产依赖列表
├── requirements-dev.txt            # 开发与测试额外依赖
├── manage.py                       # Django 管理入口
├── pyproject.toml                  # 项目元数据与工具配置（black, isort, mypy）
└── README.md                       # 项目入口文档（本文件）
```

## 贡献指南

1. **提交 Issue 讨论**：在发起任何代码变更前，请先在 GitHub Issues 中描述您发现的问题或希望新增的功能，等待维护者确认方案可行性，避免无效劳动。
2. **Fork 并创建特性分支**：从主仓库 fork 代码后，基于 `develop` 分支创建您的特性分支，分支命名遵循 `feature/xxx` 或 `fix/xxx` 格式。
3. **编写测试与文档**：新增功能必须附带对应的单元测试或集成测试，并同步更新 `/docs` 下的相关文档页面，确保文档与代码保持一致。
4. **通过 CI 检查**：提交 Pull Request 前，请确保本地通过 `black`、`isort`、`mypy` 以及 `pytest` 全部检查，CI 流水线将自动执行这些校验。
5. **提交 Pull Request**：PR 标题须简明扼要描述变更内容，正文需链接对应的 Issue 编号，并勾选自查清单（测试通过、文档更新、无合并冲突）。

## 常见问题

**问：巡检任务频繁出现超时或连接拒绝，如何调整参数？**

答：请在 `/src/core/settings.py` 中修改 `PROBE_TIMEOUT`（默认 10 秒）和 `PROBE_RETRY`（默认 3 次）变量。对于网络环境较差的服务器，建议将超时增加至 30 秒，并开启 `PROBE_VERIFY_SSL=False` 以跳过证书验证（仅测试环境）。生产环境请确保目标链接在您的网络策略中是可访问的。

**问：如何将现有书签或 CSV 列表批量导入系统？**

答：您可以使用脚本 `scripts/bulk_import.py`，该脚本接受 CSV 文件路径作为参数，要求文件包含 `url`、`title`、`tags` 三列。执行示例：`python scripts/bulk_import.py --file ./my_bookmarks.csv --user admin@hydralink.local`。导入前建议先用 `--dry-run` 选项预览解析结果。

**问：系统支持分布式部署多台 Worker 并行巡检吗？**

答：支持。您只需将多台服务器连接至同一个 Redis 消息队列，并在每台机器上启动 Celery Worker 进程（使用相同的队列名称）。系统会自动将任务分发给空闲 Worker，但需注意避免多 Worker 对同一链接同时发起请求，目前版本未内置请求去重锁，建议在业务低峰期调度大批量任务。

## 许可证

本项目采用 MIT 许可证。您可以在遵守版权声明的前提下，自由使用、修改、分发本软件，包括商业用途。详细条款请参阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
