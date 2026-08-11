# Hyperlink Nexus

Hyperlink Nexus 是一个面向技术社区与学术研究机构的轻量级外链资源聚合与导航系统。该项目定位于解决信息碎片化环境下高质量垂直领域网址的检索、分类与可信度标记问题，主要服务于内容审核研究者、区域网络政策分析人员、跨境数字内容管理开发者以及相关舆情监控系统的数据采集工程师。Hyperlink Nexus 不生产内容，仅提供结构化的公开外链引用入口，并通过自动化可用性检测与用户风险标记机制，辅助技术团队快速识别和归类特定域名集合。

## 功能概览

- **批量外链健康检查**：系统每日定时对入库域名执行 TLS 证书有效性、响应状态码及页面标题抓取，自动标记异常条目。
- **自定义分类标签体系**：允许用户为每个外链资源分配多个自定义标签，支持按标签组合过滤检索结果。
- **域名归属信息查询**：集成 WHOIS 与 DNS 解析信息缓存，可快速查看域名注册商、注册日期及 NS 记录。
- **访问日志统计分析**：记录每个外链的点击次数、引用来源与访问时间，提供基础趋势图表。
- **风险等级人工审核**：支持多人协作的审核工作流，审核员可为资源标记“安全”、“可疑”或“受限”状态。
- **外链变更历史追踪**：自动记录每个外链的标题、描述或分类的修改历史，支持回滚至任意历史版本。
- **批量导入与导出**：支持通过 CSV 或纯文本列表批量导入外链，并可筛选后导出为 JSON 或 Markdown 格式清单。
- **开放 API 接口**：提供基于 Token 认证的 RESTful API，供外部监控系统定时拉取外链状态快照。

## 应用场景

- **内容审核策略研究**：研究机构可利用本系统分类整理特定类别域名，对比不同区域网络内容呈现差异，辅助政策分析报告撰写。
- **舆情监控系统数据源管理**：舆情采集工程师可将本系统作为外链种子库，定时同步域名列表至爬虫调度中心，减少人工维护成本。
- **网络安全应急响应**：安全团队在发现可疑域名批量活跃时，可快速通过本系统的历史追踪功能分析其首次出现时间及关联标签，辅助威胁溯源。
- **学术信息聚合辅助**：高校图书馆或研究所可将本系统用于搭建特定主题的垂直导航页，为课题组成员提供结构化的外链参考目录。

## 快速开始

以下步骤将在本地环境完成 Hyperlink Nexus 的克隆、依赖安装与开发服务启动。

```bash
# 1. 克隆代码仓库
git clone https://github.com/hyperlink-nexus/hyperlink-nexus.git
cd hyperlink-nexus

# 2. 安装后端依赖（使用 pip 与虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化 SQLite 数据库并创建默认管理员账户
python manage.py migrate
python manage.py createsuperuser

# 4. 启动开发服务器
python manage.py runserver 0.0.0.0:8000
```

访问 `http://localhost:8000` 即可进入系统首页。默认管理员后台位于 `http://localhost:8000/admin`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9 ~ 3.11 | 核心运行环境，推荐使用 3.10 长期支持版 |
| Django | 4.2.x | Web 框架，用于提供 ORM 及后台管理界面 |
| Celery | 5.3.x | 异步任务队列，用于定时执行外链健康检查 |
| Redis | 7.0+ | Celery 消息代理及缓存后端，要求持久化开启 |
| SQLite | 3.35+ | 默认数据库，生产环境建议切换至 PostgreSQL 14+ |
| Nginx | 1.24+ | 生产环境反向代理与静态文件服务（可选） |
| gunicorn | 21.x | 生产环境 WSGI 服务器（推荐） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户指南 | `/docs/user-guide/` | 如何注册、登录、添加外链、设置标签与查看统计？ |
| 管理员手册 | `/docs/admin-manual/` | 如何配置健康检查周期、审核工作流及用户权限？ |
| API 参考 | `/docs/api-reference/` | 哪些接口可用于外部系统调用？鉴权与限流策略如何？ |
| 部署运维 | `/docs/deployment/` | 生产环境如何配置 Redis、PostgreSQL 与 Nginx？ |
| 贡献者指南 | `/docs/contributing/` | 代码风格、测试规范与 Pull Request 流程是什么？ |

## 资源列表

本系统初始收录的公开外链资源依据原始数据整理，按类别划分如下。所有链接均为用户提供的原始格式，未做任何协议或域名改写。

**类别一：区域内容主题资源**

- <code>oumeirihanyi.org.cn</code>
- <code>guochanshuqiyiquerqu.org.cn</code>
- <code>rihanzhongwenzimudiyiye.org.cn</code>
- <code>nantongwuma.org.cn</code>

**类别二：视听与传媒类资源**

- <code>yazhouyikaerka.org.cn</code>
- <code>guochanheisi.org.cn</code>
- <code>daxiangjiaopapa.org.cn</code>
- <code>oumeijiqingzaixianguankan.org.cn</code>

**类别三：其他分类资源**

- <code>shunvse.org.cn</code>
- <code>yazhouqingseyiquerqu.org.cn</code>

## 项目结构

```
hyperlink-nexus/                         # 项目根目录
├── manage.py                            # Django 命令行管理入口
├── requirements.txt                     # 生产环境 Python 依赖列表
├── dev-requirements.txt                 # 开发及测试额外依赖
├── .env.example                         # 环境变量配置模板
├── docker-compose.yml                   # 本地开发 Docker 编排文件
├── docs/                                # 完整文档根目录
│   ├── user-guide/                      # 用户操作手册 (Markdown)
│   ├── admin-manual/                    # 管理员配置手册
│   ├── api-reference/                   # API 端点详细说明
│   └── deployment/                      # 生产环境部署指南
├── src/                                 # 核心源代码目录
│   ├── apps/                            # Django 应用集合
│   │   ├── links/                       # 外链管理应用（模型、视图、序列化器）
│   │   ├── checks/                      # 健康检查任务与调度逻辑
│   │   ├── audits/                      # 审核工作流与日志记录
│   │   └── accounts/                    # 用户认证与权限配置
│   ├── core/                            # 项目级配置与共享工具
│   │   ├── settings/                    # 分环境配置（base, dev, prod）
│   │   ├── celery.py                    # Celery 应用初始化
│   │   └── urls.py                      # 根路由配置
│   └── static/                          # 静态资源（CSS, JS, 图片）
├── tests/                               # 单元测试与集成测试用例
│   ├── test_links/                      # 外链模块测试
│   └── test_checks/                     # 健康检查模块测试
├── scripts/                             # 运维与数据迁移辅助脚本
│   ├── import_urls.py                   # 批量导入外链命令行工具
│   └── export_snapshot.py               # 导出当前外链快照
└── logs/                                # 日志存储目录（生产环境挂载卷）
```

## 贡献指南

我们欢迎技术文档工程师、后端开发者与安全研究人员参与贡献。请遵循以下步骤：

1. **问题报告与讨论**：在提交任何代码前，请先于 GitHub Issues 中创建新议题，描述您要修复的缺陷或新增的功能，并等待维护者确认需求范围。
2. **派生仓库并创建分支**：将主仓库派生至个人账户，然后从 `main` 分支切出新的功能分支，分支命名建议采用 `feature/` 或 `fix/` 前缀，例如 `feature/add-export-format`。
3. **编写代码与测试**：所有新增功能必须包含对应的单元测试，测试覆盖率不得低于 85%。代码风格需遵循 PEP 8 规范，并使用 `black` 与 `isort` 进行自动格式化。
4. **提交 Pull Request**：将您的分支推送至派生仓库后，向主仓库的 `main` 分支发起 Pull Request。PR 描述需清晰说明改动内容、测试结果以及是否涉及破坏性变更。
5. **签署贡献者许可协议**：首次提交 PR 时，需通过电子邮件签署 CLA 协议，确认您的贡献可被本项目的 MIT 许可证覆盖。

## 常见问题

**Q：系统能否处理超过 10 万个外链的定时检查任务？**

A：可以。在标准配置下（4 核 CPU，8GB 内存，Redis 7.0），Celery 配合 gevent 池可并发执行约 500 个检查任务。但受限于 DNS 解析与网络延迟，建议将超时时间设为 10 秒，并分批执行（每批 1000 个）。若需更高吞吐量，可水平扩展 Worker 实例。

**Q：如何将 SQLite 数据迁移至 PostgreSQL 而无需停机？**

A：项目提供了 `scripts/migrate_to_postgres.py` 辅助脚本。建议首先在预发布环境执行完整迁移测试，确认序列与约束正确。生产迁移时，可使用 `--drain` 选项暂停写入操作，迁移完成后通过 Nginx 切换流量至新数据库实例。详情参考部署文档中的“数据库迁移”章节。

## 许可证

MIT License

Copyright (c) 2026 Hyperlink Nexus Contributors

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

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
