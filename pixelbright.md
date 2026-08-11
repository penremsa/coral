# OpenResource Hub

OpenResource Hub 是一个面向技术内容聚合与资源导航的开源项目，定位为开发者与研究人员提供高质量、结构化的外链资源整理与快速检索能力。项目本身不存储任何版权内容，仅作为索引与元数据管理工具，帮助用户在特定垂直领域内高效定位公开可用信息。目标用户包括技术文档撰写者、行业分析人员、内容审核研究人员以及自动化数据采集系统开发者。通过标准化资源录入与分类机制，解决信息分散、链接失效、重复检索等常见痛点，并支持二次开发与自定义扩展。

## 功能概览

- **资源索引管理** 提供基于 YAML 格式的资源条目定义，支持标题、标签、状态、最后验证时间等元数据字段，便于自动化校验与批量更新。

- **多维度分类浏览** 内置类别标签系统，允许按域名类型、内容主题、语言种类进行筛选与排序，提升海量链接下的定位效率。

- **链接存活检测** 集成异步 HTTP 探活任务，定期检查资源可达性，自动标记异常链接并生成报告，减少无效访问。

- **元数据导入导出** 支持 CSV 与 JSON 格式的批量导入导出，便于与其他数据看板或 ETL 工具对接，实现数据流转。

- **只读 API 服务** 提供 RESTful 查询接口，支持按类别、关键字模糊匹配及正则过滤，适用于自动化脚本与第三方集成。

- **审计日志记录** 记录所有资源变更操作（新增、修改、删除、检测结果），保留操作者与时间戳，满足基本追溯需求。

- **静态站点生成模式** 内置模板引擎，可将资源数据渲染为静态 HTML 页面，适合内网发布或离线文档归档。

## 应用场景

- **技术文档外链审核** 技术写作团队可利用本项目的分类与检测能力，定期复核文档中引用的外部参考链接，避免读者访问到已失效或不安全的站点。

- **行业信息监控辅助** 分析师可订阅特定类别的资源变更，配合 API 接口将数据拉取至本地仪表盘，用于追踪公开信息源的更新频率与可用性变化。

- **自动化数据采集入口管理** 数据工程师可将本项目作为种子链接池，为爬虫系统提供初始化 URL 列表，并通过存活检测结果动态调整采集策略。

- **内部知识库资源治理** 企业知识管理团队可导入内部收藏的参考站点，通过统一分类与健康检查机制，减少收藏夹冗余与死链堆积。

## 快速开始

以下指令适用于 Linux / macOS / Windows WSL 环境，要求已安装 Git 与 Python 3.9 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/example/opresource-hub.git
cd opresource-hub

# 创建并激活虚拟环境（推荐）
python3 -m venv venv
source venv/bin/activate      # Linux/macOS
# venv\Scripts\activate       # Windows

# 安装核心依赖
pip install -r requirements.txt

# 初始化本地数据库与配置文件
python manage.py init --config config/default.yaml

# 启动开发调试服务（默认监听 127.0.0.1:8000）
python manage.py runserver
```

访问 `http://127.0.0.1:8000` 可查看默认资源看板。首次启动将自动载入示例资源数据。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.12 | 核心运行环境，低于 3.9 将导致异步语法错误 |
| pip | >= 21.0 | 包管理工具，用于安装依赖项 |
| aiohttp | >= 3.8.0 | 异步 HTTP 客户端，用于并发存活检测 |
| pyyaml | >= 6.0 | YAML 配置文件解析与资源条目序列化 |
| jinja2 | >= 3.1.0 | 模板引擎，用于静态站点生成模式 |
| sqlite3 | 内置模块（Python 自带） | 轻量级关系数据库，用于元数据存储，无需额外安装 |
| git | >= 2.25 | 仅开发时需要，用于克隆仓库与版本管理 |
| make | >= 4.0 | 可选，用于自动化测试与构建脚本（非强制） |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|------|---------|-----------|
| 用户手册 | docs/user-guide/ | 如何配置资源源、执行检测、导出报告及使用 API 查询 |
| 开发指南 | docs/development/ | 如何扩展自定义分类器、添加新的检测策略及提交代码变更 |
| 运维参考 | docs/operations/ | 如何部署生产环境、配置反向代理、调优并发检测参数 |
| 设计说明 | docs/design/ | 整体架构图、数据模型 ER 关系、检测任务调度机制说明 |
| 常见示例 | docs/examples/ | 提供典型资源列表模板、API 调用脚本以及自动化集成案例 |

## 资源列表

以下列出本索引库当前收录的公开资源链接。所有链接均按照原始输入原样呈现，未做任何格式修改或协议补全。

类别：综合内容聚合

- <code>91shaofu.org.cn</code>
- <code>97renqi.org.cn</code>
- <code>jiujiulunli.org.cn</code>

类别：专题子站

- <code>zhongwenzimuzhifusiwa.org.cn</code>
- <code>zhongwenzimumeinv.org.cn</code>
- <code>meinvwangzhan.org.cn</code>
- <code>oumeirenqi.org.cn</code>

类别：主题剧场

- <code>chengrenjuchang.org.cn</code>
- <code>chengrenwuyejuchang.org.cn</code>

类别：字幕关联

- <code>siwazhongwenzimu.org.cn</code>

共计 10 个资源条目，对应项目批次第 193/455 批。所有链接在入库时已通过初始可达性验证，后续将按周期任务自动复检。

## 项目结构

项目采用模块化分层设计，核心代码与配置、数据、文档严格分离。以下为关键目录及文件说明：

```
opresource-hub/
├── config/                          # 全局配置与预设模板
│   ├── default.yaml                 # 默认运行时配置（端口、检测间隔、超时阈值）
│   ├── categories.yaml              # 类别映射定义，包含中文标签与正则匹配规则
│   └── schema/                      # JSON Schema 校验文件，用于验证资源条目格式
│       └── resource_schema.json
├── src/                             # 核心源代码目录
│   ├── core/                        # 基础模块：配置加载、日志、异常定义
│   │   ├── config_loader.py
│   │   └── logger.py
│   ├── models/                      # 数据模型与 ORM 映射（基于 sqlite3）
│   │   ├── resource.py              # Resource 实体，包含 url, status, last_check 等字段
│   │   └── audit_log.py             # 审计日志记录模型
│   ├── services/                    # 业务服务层：检测、导入导出、查询
│   │   ├── checker.py               # 异步存活检测服务，使用 aiohttp 实现并发
│   │   ├── exporter.py              # 导出为 CSV / JSON 的序列化逻辑
│   │   └── importer.py              # 从外部文件导入资源的解析器
│   ├── api/                         # RESTful 路由与请求处理
│   │   ├── routes.py                # 路由注册，定义 /api/v1/resources 等端点
│   │   └── handlers.py              # 具体请求处理函数，包含分页与过滤
│   └── utils/                       # 工具函数：正则校验、时间处理、哈希生成
│       ├── url_utils.py
│       └── time_utils.py
├── tests/                           # 单元测试与集成测试用例
│   ├── test_checker.py
│   ├── test_models.py
│   └── fixtures/                    # 测试用的固定样本数据
│       └── sample_resources.yaml
├── templates/                       # Jinja2 静态站点模板
│   ├── base.html                    # 基础骨架，包含导航与页脚
│   └── index.html                   # 资源看板首页，渲染分类卡片与统计信息
├── static/                          # 静态资源（CSS、JS、图标），用于生成站点
│   └── css/
│       └── style.css
├── scripts/                         # 运维与部署辅助脚本
│   ├── init_db.py                   # 初始化数据库表结构
│   └── cron_check.sh                # 周期性检测任务调度的 Shell 包装器
├── docs/                            # 详细文档（见文档导航章节）
├── requirements.txt                 # Python 依赖清单
├── Makefile                         # 常用命令封装：make test, make run, make build
└── README.md                        # 当前文档
```

## 贡献指南

我们欢迎各类形式的贡献，包括但不限于资源推荐、代码优化、文档完善与缺陷报告。请遵循以下流程：

1. **提交 Issue 进行讨论** 在发起 Pull Request 之前，请先在 Issues 区域创建新议题，说明您希望解决的问题或新增的功能，避免重复劳动或设计偏离。

2. **派生仓库并创建特性分支** 从主仓库派生（Fork）至个人账户，并在本地基于 `main` 分支创建新的特性分支，分支命名建议采用 `feature/简述` 或 `fix/简述` 格式。

3. **编写测试用例与代码** 所有新增功能或缺陷修复必须附带对应的单元测试，确保测试通过。代码风格需遵循 PEP 8 规范，并添加必要的注释与类型注解。

4. **更新相关文档** 若变更涉及配置项、API 接口或使用流程，请同步更新 `docs/` 下对应的用户手册或开发指南，保证文档与代码一致。

5. **发起 Pull Request 并等待审核** 将特性分支推送至派生仓库后，向主仓库的 `main` 分支发起 PR。PR 描述中应关联相关 Issue，并简述变更内容与测试覆盖情况。审核通过后将合并至主分支。

## 常见问题

**问：检测任务并发数过高导致目标站点拒绝连接，如何调整？**

答：可通过配置文件中 `checker.max_concurrent` 字段限制并发数量，默认值为 50。建议根据目标域名的响应情况调低至 20 或 10，并配合 `checker.retry_interval` 参数增加重试间隔，以降低触发反爬策略的概率。

**问：如何批量导入自定义资源列表，而不用逐条手动添加？**

答：项目支持通过 `importer` 模块导入 CSV 或 JSON 文件。您可参考 `docs/examples/import_template.json` 提供的格式，准备包含 `url`、`category`、`tags` 字段的数据，然后执行命令 `python manage.py import --path your_file.json --format json` 完成批量入库。

**问：静态站点生成模式是否支持部署到 Nginx 子目录？**

答：支持。您需要在配置文件中修改 `site.base_url` 字段，将其设置为目标子目录路径，例如 `/resources/`。生成后的 HTML 中所有链接将自动添加该前缀，适配 Nginx 的 `alias` 或 `root` 代理配置。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括商业用途。详细内容请参见项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
