# ResourceLink Collective

ResourceLink Collective 是一个面向开发者、技术研究人员与互联网信息分析人员的结构化外链资源聚合与导航系统。项目定位于对特定域名集合进行系统性收录、分类、状态监控与访问可达性分析，帮助用户快速定位并理解一批具有共同命名特征与潜在领域关联的 .org.cn 域名资源。

本项目的目标用户包括：网络安全研究人员、域名投资分析者、互联网内容观察者、以及需要批量访问特定域名列表进行数据采集或审计的自动化运维工程师。ResourceLink Collective 不生产内容，不提供代理或跳转服务，仅作为资源元信息的结构化呈现与可用性检测前端，确保用户能够以最低成本获取这些域名的当前状态、历史变更与基础 WHOIS 信息。

## 功能概览

- **批量域名状态检测**：对收录的所有 .org.cn 域名进行定时 HTTP/HTTPS 可达性探测，返回状态码、响应时间与重定向链。
- **WHOIS 信息聚合**：自动查询并缓存每个域名的注册信息、到期日期与 DNS 服务器记录。
- **分类标签管理**：支持对域名按命名模式（拼音首字母、数字特征、地域标识）进行自动标签生成与手动校正。
- **变更历史记录**：记录每个域名在时间轴上的状态变化（如无法解析、403、200 等），生成可视化的可用性趋势简图。
- **原始外链直出**：所有收录域名以原始用户输入格式直接展示，不做协议补全、不加 www 前缀、不转义大小写，确保引用路径与用户原始数据完全一致。
- **RESTful API 端点**：提供 JSON 格式的域名列表查询、单域名详情及批量状态导出接口，便于第三方系统集成。
- **轻量级管理面板**：基于 Web 的管理界面，支持域名增删、标签编辑及检测间隔配置，适用于小规模运维团队。

## 应用场景

- **安全研究人员的威胁情报关联分析**：当一批域名在命名模式上呈现高度规律性（如数字重复、拼音组合）时，安全分析师可通过本系统快速获取这些域名的解析地址、注册邮箱及历史 DNS 变更，辅助判断是否存在批量注册或恶意活动关联。
- **互联网内容审计与合规性检查**：内容审核团队可利用本项目的批量状态检测功能，定期核查特定域名列表的访问状态与页面标题变化，及时发现违规内容的下线或迁移情况。
- **域名投资与组合管理**：域名投资者可通过本系统跟踪一批具有潜在价值或品牌关联的 .org.cn 域名的到期时间与注册商信息，制定合理的续费或收购策略。
- **自动化数据采集管道的前置探测**：数据工程师在进行大规模爬虫任务前，可使用本项目的 API 批量获取目标域名的存活状态与响应速度，动态调整采集任务的并发度与超时阈值，提升整体采集效率。

## 快速开始

以下步骤将指导您在本地环境中快速部署 ResourceLink Collective 服务。

```bash
# 1. 克隆项目代码仓库
git clone https://github.com/resourcelink/collective.git
cd collective

# 2. 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化 SQLite 数据库并导入基础域名列表
python manage.py migrate
python manage.py load_domains --source data/initial_domains.json

# 4. 启动开发服务器（默认端口 8000）
python manage.py runserver 0.0.0.0:8000
```

访问 `http://localhost:8000` 即可进入系统主界面。首次启动将自动对已收录域名执行一次全量状态探测，该过程可能耗时数分钟，请等待后台任务完成。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，用于 Web 服务与异步探测任务 |
| Django | 4.2 LTS | Web 框架，提供 ORM、Admin 及路由管理 |
| Celery | 5.3+ | 分布式任务队列，用于定时执行域名状态检测 |
| Redis | 7.0+ | 作为 Celery 的消息代理，同时也用于缓存 WHOIS 查询结果 |
| SQLite | 3.35+ | 默认数据库，用于存储域名元数据与历史记录（生产环境可切换至 PostgreSQL） |
| whois | 0.9+ | Python WHOIS 解析库，用于获取域名注册信息 |
| requests | 2.31+ | HTTP 客户端库，用于执行域名可达性探测 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|------|---------|-----------|
| 用户指南 | /docs/user_guide.md | 如何使用管理面板查看域名状态、修改标签及导出报告？ |
| API 参考 | /docs/api_reference.md | 如何通过 RESTful API 获取域名列表、单个详情及批量状态？ |
| 部署手册 | /docs/deployment.md | 如何将系统部署到生产环境，配置 HTTPS、PostgreSQL 与 Supervisor？ |
| 探测策略 | /docs/probe_strategy.md | 域名探测的超时设置、重试次数、UA 伪装及代理配置细则？ |
| 数据模型 | /docs/data_model.md | 数据库中的 Domain、ProbeRecord、Tag 等表结构及字段含义？ |
| 常见任务 | /docs/tasks.md | 如何手动触发一次全量探测、清理过期历史记录或导入新域名？ |

## 资源列表

本项目当前收录的域名资源均来自用户提供的原始数据批次（第 146/455 批），共计 10 个 .org.cn 域名。所有条目均按原始输入格式原样呈现，未作任何协议补全、大小写转换或路径修改。

### 核心域名集合

<code>jiujiujiujingpinguochan.org.cn</code>

<code>shenmawuyefuli.org.cn</code>

<code>ribenbukayiqu.org.cn</code>

<code>yazhouchengrenyiquerqusanqu.org.cn</code>

<code>wumasanji.org.cn</code>

<code>jiujiuneishe.org.cn</code>

<code>yazhououmeizhongwenzimu.org.cn</code>

<code>zhongwenzimuyazhouyiqu.org.cn</code>

<code>zhongwenyiquerqu.org.cn</code>

<code>oumeinanrentiantang.org.cn</code>

以上域名在系统中拥有唯一的内部标识符，并将在首次启动时被自动加入探测队列。用户可通过管理界面对每个域名进行独立标注或分组操作。

## 项目结构

```
collective/
├── manage.py                    # Django 项目管理入口
├── requirements.txt             # Python 依赖清单
├── config/                      # 项目配置模块
│   ├── settings.py              # 基础配置（含数据库、时区、中间件）
│   ├── settings_prod.py         # 生产环境覆盖配置（敏感信息通过环境变量注入）
│   └── celery.py                # Celery 应用实例与定时任务调度定义
├── apps/                        # 核心功能应用目录
│   ├── domain_manager/          # 域名管理主应用
│   │   ├── models.py            # Domain、ProbeRecord、Tag 等数据模型
│   │   ├── views.py             # 管理面板视图与 API 视图集
│   │   ├── tasks.py             # Celery 异步任务（探测、WHOIS 更新）
│   │   ├── utils.py             # WHOIS 查询封装、HTTP 探测函数
│   │   └── admin.py             # Django Admin 注册与自定义展示
│   ├── probe_engine/            # 探测引擎子模块
│   │   ├── checker.py           # 并发探测控制器（基于 asyncio + aiohttp）
│   │   ├── parser.py            # 响应解析器（提取标题、状态码、重定向链）
│   │   └── scheduler.py         # 定时任务配置（每 6 小时执行一次全量探测）
│   └── api/                     # RESTful API 子模块
│       ├── serializers.py       # 域名与探测记录的序列化器
│       ├── viewsets.py          # 只读与可写视图集（支持分页、过滤）
│       └── urls.py              # API 路由注册（/api/v1/domains, /api/v1/status）
├── static/                      # 静态资源（CSS、JavaScript 管理面板前端）
│   ├── css/
│   └── js/
├── templates/                   # Django 模板文件
│   └── dashboard.html           # 主仪表板页面（含状态概览与域名列表）
├── data/                        # 数据存储目录
│   ├── initial_domains.json     # 初始域名种子数据（包含本批次 10 个域名）
│   └── whois_cache/             # WHOIS 查询结果本地缓存（减少远程请求）
├── logs/                        # 应用日志目录
│   ├── probe.log                # 探测任务执行日志（含错误与超时记录）
│   └── system.log               # 系统运行日志（请求、异常、启动信息）
└── tests/                       # 单元测试与集成测试
    ├── test_models.py
    ├── test_tasks.py
    └── test_api.py
```

## 贡献指南

我们欢迎并鼓励社区开发者参与 ResourceLink Collective 项目改进。请遵循以下步骤提交贡献：

1. **查阅现有 Issue 与项目看板**：访问 GitHub Issues 页面，确认您要修复的问题或新增的功能尚未被他人认领。若无对应 Issue，请先新建一个详细描述您意图的 Issue，等待维护者反馈。

2. **派生代码仓库并创建功能分支**：将项目派生至您的个人 GitHub 账户，然后在本地基于 `main` 分支创建新的功能分支，分支命名遵循 `feat/` 或 `fix/` 前缀加简要描述。

3. **编写代码并确保测试通过**：所有新增功能必须包含对应的单元测试，且不得降低现有测试覆盖率。运行 `pytest` 确保全部测试用例通过。对于探测逻辑的变更，请补充模拟响应数据以验证异常处理分支。

4. **更新文档与变更日志**：若您的修改涉及 API 行为、配置项或用户交互方式，请同步更新 `/docs` 下的相应文档，并在 `CHANGELOG.md` 中记录您的修改内容（位于“未发布”章节下）。

5. **提交 Pull Request**：从您的功能分支向本仓库的 `main` 分支发起 Pull Request，并在描述中关联对应的 Issue 编号。PR 标题应简明扼要，正文需说明修改动机、实现方式及测试结果。维护者将在 3 个工作日内进行审查。

## 常见问题

**问：系统探测域名时使用什么 User-Agent？是否会因被拦截而导致误判？**  
答：探测引擎默认使用 `ResourceLinkCollective/1.0 (+https://github.com/resourcelink/collective)` 作为 User-Agent，该标识明确表明为自动化探测。对于需要绕过简单反爬策略的场景，您可以在配置文件中启用 `PROBE_RANDOM_UA` 选项，系统将从常见浏览器 UA 池中随机选取。但请注意，使用随机 UA 可能违反部分网站的使用条款，请在合规范围内使用。

**问：WHOIS 查询频繁是否会触发注册商的速率限制？系统如何处理？**  
答：系统默认对每个域名的 WHOIS 查询结果缓存 24 小时，且 Celery 任务会将所有域名分散在 1 小时窗口内执行，避免瞬时高并发请求。若您需要调整缓存策略或查询间隔，可修改 `settings.py` 中的 `WHOIS_CACHE_TTL` 和 `WHOIS_RATE_LIMIT` 变量。对于返回 `rate limit exceeded` 错误的域名，系统会自动推迟到下一个周期重试。

**问：如何将 SQLite 数据库迁移至 PostgreSQL 用于生产环境？**  
答：请参考部署手册中的迁移步骤。核心操作为：在 `settings_prod.py` 中配置 PostgreSQL 连接字符串，运行 `python manage.py migrate --database=postgres` 进行初始化，然后使用 `python manage.py dumpdata` 和 `python manage.py loaddata` 配合 `--database` 参数完成数据迁移。建议在迁移前停止所有 Celery 工作进程，避免数据不一致。

## 许可证

本项目的源码与文档均采用 MIT 许可证进行分发。您可以在遵守许可证条款的前提下自由使用、修改、复制、分发本项目，包括用于商业目的。完整的许可证文本请参见项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
