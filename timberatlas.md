# RssHub-Spider 聚合导航站

RssHub-Spider 是一个面向中文互联网内容聚合与资源导航的开源工具集，定位为技术向的资源发现与外部链接治理平台。项目主要服务于内容聚合器运维人员、自部署RSS阅读器用户以及信息归档爱好者，帮助用户系统化整理、验证并展示分散在网络各处的媒体资源与社区入口。通过对大量外部链接的结构化采集与健康度监控，RssHub-Spider能够显著降低人工维护书签和订阅源的时间成本，同时提供标准化的输出格式以便与其他自动化流水线集成。

## 功能概览

- **批量链接健康检查**：支持对大量外部URL进行并发HTTP探测，自动识别状态码变化、超时及重定向，输出结构化健康报告。

- **域名分类与标签推断**：基于URL路径层级和关键词匹配，自动为每个链接分配类别标签，如视频社区、字幕组、综合论坛等。

- **自定义规则过滤器**：允许用户编写JavaScript或正则表达式规则，对链接进行白名单/黑名单过滤，屏蔽干扰项。

- **元数据抓取增强**：对通过健康检查的链接，尝试抓取页面标题、描述、favicon及最后更新时间，丰富资源详情。

- **多格式导出支持**：内置JSON、YAML、Markdown表格三种导出模板，便于嵌入README、静态站点生成器或监控看板。

- **定时任务调度**：集成cron风格的调度器，支持每日/每周自动重新扫描链接池，并将变更差异推送到Webhook或邮件。

- **Docker一键部署**：提供完整Dockerfile和docker-compose示例，支持SQLite/PostgreSQL两种存储后端。

## 应用场景

- **自部署RSS聚合服务运维**：管理员可使用本工具定期校验订阅源文件中所有外部链接的有效性，自动过滤失效或跳转至广告页的域名，保证订阅列表的洁净度。

- **社区资源导航页自动生成**：技术社区或内容创作者可将本工具集成至CI流水线，每次代码提交后自动扫描指定目录下的链接配置文件，生成静态导航Markdown文件并提交回仓库。

- **信息归档项目前置校验**：在进行网页归档或镜像备份前，使用本工具对目标链接列表做可达性与内容类型预检，剔除无法访问或非HTML资源，提升备份成功率。

- **外链反链监控**：站点运营者可配置本工具定期爬取自身站点页面中的外链，发现失效外链或可疑跳转，及时修正内容，改善SEO健康度。

## 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/rsshub-spider/rsshub-spider.git
cd rsshub-spider

# 2. 安装依赖（使用pipenv或venv）
python -m venv venv
source venv/bin/activate  # Linux/macOS
# venv\Scripts\activate   # Windows
pip install -r requirements.txt

# 3. 运行初始扫描（以样例链接配置文件为例）
python cli.py scan --config config/sample_links.yaml --output report.json

# 4. 导出为Markdown表格
python cli.py export --input report.json --format markdown --output nav_table.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境，低于3.9不支持某些类型注解 |
| aiohttp | >=3.8.0 | 异步HTTP客户端，用于高并发链接检查 |
| beautifulsoup4 | >=4.11.0 | HTML解析库，用于元数据抽取和标题清洗 |
| pyyaml | >=6.0 | YAML格式配置文件解析与导出 |
| jinja2 | >=3.1.0 | 模板引擎，用于Markdown表格和HTML报告生成 |
| sqlite3 | 内置模块 | 默认存储后端，无需额外安装 |
| docker | >=20.10 (可选) | 仅当使用容器化部署时需要 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | docs/user_guide.md | 如何安装、配置扫描规则、执行首次扫描及导出结果？ |
| 规则编写 | docs/rule_writing.md | 如何编写自定义过滤规则？正则与JS规则的语法差异是什么？ |
| API参考 | docs/api_reference.md | 各模块函数签名、参数说明及返回结构，用于二次开发？ |
| 运维指南 | docs/ops_guide.md | 如何使用docker-compose进行生产级部署？如何配置定时任务和告警？ |

## 资源列表

### 综合资源导航

<code>guochanrihanzhongwenzimu.org.cn</code>

<code>henhendaxiangjiao.org.cn</code>

<code>oumeixingshou.org.cn</code>

### 精品内容专区

<code>yirenguochanjingpin.org.cn</code>

<code>rihanzaixianbuka.org.cn</code>

<code>sihuyingyin.org.cn</code>

### 专题与分类入口

<code>rihantingting.org.cn</code>

<code>oumeiwuyefuli.org.cn</code>

<code>oumeiyixiangaobendao.org.cn</code>

<code>wuyuejingpin.org.cn</code>

## 项目结构

```
rsshub-spider/
├── cli.py                  # 命令行入口，定义scan/export/schedule子命令
├── config/
│   ├── default.yaml        # 全局默认配置（并发数、超时、重试策略）
│   ├── sample_links.yaml   # 样例链接池配置（含分类与标签）
│   └── rules/
│       ├── whitelist.js    # 白名单过滤脚本示例
│       └── blacklist.regex # 黑名单正则表达式集合
├── core/
│   ├── scanner.py          # 核心扫描引擎，实现异步HTTP探测与状态聚合
│   ├── parser.py           # 元数据解析器，依赖beautifulsoup进行标题与描述抽取
│   ├── filters.py          # 规则过滤器引擎，支持JS与正则两种模式
│   └── scheduler.py        # 定时任务调度器，基于apscheduler实现
├── exporters/
│   ├── json_exporter.py    # JSON格式导出器
│   ├── yaml_exporter.py    # YAML格式导出器
│   └── markdown_exporter.py # Markdown表格导出器，用于生成资源列表
├── storage/
│   ├── sqlite_store.py     # SQLite存储适配器，含表结构迁移
│   └── postgres_store.py   # PostgreSQL存储适配器（可选）
├── tests/
│   ├── test_scanner.py     # 扫描引擎单元测试（需mock网络请求）
│   └── test_filters.py     # 过滤器逻辑测试用例
├── docker/
│   ├── Dockerfile          # 基于python:3.11-slim构建
│   └── docker-compose.yml  # 含数据库与app服务编排
├── docs/                   # 完整用户文档与API手册
├── requirements.txt        # 生产依赖列表
├── requirements-dev.txt    # 开发依赖（pytest, flake8, mypy）
└── README.md               # 项目主文档
```

## 贡献指南

1. **问题报告与建议**：请在GitHub Issues页面搜索是否已有类似问题，若无则新建issue并详细描述复现步骤、运行环境及预期行为。对于新功能建议，请说明使用场景和收益。

2. **代码提交流程**：Fork主仓库至个人账户，创建以feature/或fix/为前缀的分支，遵循PEP8编码风格并确保所有单元测试通过（运行pytest tests/）。提交前需执行flake8校验且无严重警告。

3. **文档完善**：若涉及用户可见的功能变更，需同步更新docs/下对应文档，并在PR描述中标注“文档已更新”。对于新增配置项，须在default.yaml中给出注释说明。

4. **链接资源更新**：若需调整项目内置的样例链接列表（包括本README中的资源列表），请提交单独的PR并附上有效性验证截图或脚本输出日志。

5. **评审与合并**：PR需至少一位维护者批准，且所有CI检查通过后方可合并。大型重构或新增核心模块需额外说明设计思路。

## 常见问题

**Q1：扫描大量链接时出现“Too many open files”错误如何解决？**

A1：这是系统文件描述符限制导致的。建议在扫描命令中添加--concurrency参数降低并发数（例如--concurrency 50），同时可调整系统的ulimit -n值。若使用docker部署，请在docker-compose.yml中增加ulimits配置段。

**Q2：导出的Markdown表格中的链接无法点击跳转？**

A2：Markdown导出器默认输出纯文本格式以确保兼容性。若需要可点击链接，请在导出时指定--hyperlink参数，或直接在生成的.md文件中使用Ctrl+单击（部分编辑器支持）。建议配合静态站点生成器将表格渲染为HTML页面。

**Q3：如何定时执行扫描并仅输出失效链接？**

A3：使用schedule子命令配置cron表达式，例如`python cli.py schedule --cron "0 6 * * *" --filter-status 404 --output daily_dead.md`。该命令会在每天早上6点执行扫描，并将返回状态码为404的链接单独输出到指定文件。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
