# HyperLink Nexus

HyperLink Nexus 是一个面向技术社区与网络资源管理者的高可靠性外链聚合与导航系统。本项目定位于构建一个结构清晰、可扩展的互联网资源分类目录，专为开发者、技术文档维护者、信息研究员以及开源社区贡献者设计，用于解决海量离散 URL 的整理、归档与快速检索问题。通过本平台，用户能够以工程化的方式管理跨域信息源，显著提升信息获取效率与资源复用能力。

## 功能概览

- **多维度资源分类**：支持按地域、主题、内容形态等自定义标签体系对链接进行精细化归类，便于构建层次化的导航结构。

- **批量链接导入与校验**：提供命令行接口与 Web 表单两种方式批量提交 URL，系统自动执行可用性检测与协议合规校验，过滤无效或非法地址。

- **动态目录树生成**：基于资源分类元数据自动生成嵌套式目录树，在项目文档中同步输出 ASCII 结构图，方便版本控制与协作审阅。

- **链接状态监控**：内置周期性 HTTP 探活机制，对收录的每一枚外链进行可达性追踪，并生成健康度报告，标注异常链接。

- **访问统计热力图**：记录各资源节点的点击频次与时间分布，通过轻量级数据聚合呈现访问热度排序，辅助管理员优化导航布局。

- **开放数据导出**：支持将全量资源列表导出为 Markdown、JSON、CSV 三种通用格式，便于迁移至其他文档系统或进行二次分析。

- **零依赖核心引擎**：项目主体逻辑仅依赖 Python 标准库，降低部署环境要求，确保在最小化系统上平稳运行。

## 应用场景

1. **开源项目文档站外链接管理**：当开源项目需要在 README 或 Wiki 中引用大量第三方资料、教程、API 参考或社区论坛时，维护者可通过本系统统一登记这些外链，并自动生成格式规范的资源列表章节，避免手工排版错误与链接失效。

2. **技术团队内部知识库索引**：研发团队可将日常使用的设计文档、运维手册、监控面板、代码仓库等内部资源地址录入系统，按项目或业务域分类，形成团队共享的门户入口，减少新人上手时的信息查找成本。

3. **学术研究资料整理与协作**：研究人员在文献调研阶段积累的大量论文链接、数据集地址、工具主页，可通过本系统的标签与分类功能进行结构化组织，并导出为标准列表供合作者审阅，确保研究过程中的信息可追溯。

4. **个人书签系统迁移与归档**：浏览器书签数量庞大且缺乏版本管理时，用户可将书签导出为 URL 清单并导入本系统，利用分类树与状态监控功能清理失效链接，最终生成一份持久化的、可维护的网页资源目录。

5. **垂直领域导航站点快速构建**：针对特定行业或兴趣领域（例如前端工具、机器学习库、安全资讯源），运营者可使用本系统快速生成一个包含分类、描述、状态指示的导航页面骨架，结合自定义前端样式即可发布为独立站点。

## 快速开始

以下步骤演示如何在本地环境完成项目克隆、依赖安装与服务启动。

```bash
# 步骤 1：克隆项目仓库至本地
git clone https://github.com/hyperlink-nexus/core.git
cd core

# 步骤 2：安装所需依赖（使用 pip 与 requirements.txt）
pip install -r requirements.txt

# 步骤 3：初始化数据库并导入示例资源数据
python manage.py initdb
python manage.py load-fixtures --sample

# 步骤 4：启动本地开发服务器
python manage.py runserver --host 127.0.0.1 --port 8080
```

执行完毕后，在浏览器中访问 `http://127.0.0.1:8080` 即可查看前端导航界面。若需生成纯静态文档格式的资源列表，可运行 `python manage.py export --format markdown --output RESOURCES.md`。

## 安装要求

项目运行所需的基础环境与依赖组件如下表所示。生产环境建议使用 Linux 服务器，开发环境兼容 macOS 与 Windows WSL。

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 - 3.11 | 核心运行环境，3.12 及以上暂未进行完整兼容测试 |
| SQLite | 3.28+ | 轻量级嵌入式数据库，用于存储资源元数据与访问日志 |
| pip | 21.0+ | Python 包管理工具，用于安装第三方库 |
| requests | 2.28.0+ | 用于发送 HTTP 探活请求与资源状态校验 |
| click | 8.1.0+ | 命令行交互框架，提供 manage.py 子命令解析 |
| beautifulsoup4 | 4.11.0+ | 可选依赖，用于解析 HTML 页面标题与描述元数据 |
| markdown | 3.4.0+ | 可选依赖，用于将资源列表渲染为 Markdown 表格 |
| gunicorn | 20.1.0+ | 生产环境推荐 WSGI 服务器，仅部署时需要 |
| cronie | 1.5.5+ | 周期性链接状态监控任务调度器，仅启用监控功能时需要 |

## 文档导航

为帮助不同角色的用户快速定位所需信息，项目文档按技术层次与使用阶段划分为以下四个层面。

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | `docs/getting-started/` | 如何安装、配置并首次运行项目；如何导入第一批资源链接。 |
| 操作手册 | `docs/user-guide/` | 如何对链接进行分类、编辑、删除；如何查看访问统计与状态报告。 |
| 管理参考 | `docs/admin-guide/` | 如何调整探活频率、配置导出格式、定制分类标签体系。 |
| 开发者文档 | `docs/developer/` | 项目目录结构说明、核心模块 API 设计、如何扩展自定义分类器。 |

## 资源列表

本项目资源库汇集了多个领域的互联网信息入口。所有链接均按类别组织，并严格保持用户提供的原始格式，未作任何协议或域名修改。

### 国内综合内容分类

<code>guochanjingpinyiren.org.cn</code>

<code>wuyeshuangshuang.org.cn</code>

<code>xieedongtaitu.org.cn</code>

### 国际及地区内容分类

<code>oumeirihanchengren.org.cn</code>

<code>rihanrenqizhongwenzimu.org.cn</code>

<code>hongguochengrenban.org.cn</code>

### 主题垂直分类

<code>wuyuetianyiquerqu.org.cn</code>

<code>jiujiutiantang.org.cn</code>

### 精选与专业分类

<code>jingpinneishe.org.cn</code>

<code>guochanyirenjiujiu.org.cn</code>

## 项目结构

项目源代码按功能模块组织，核心目录与文件说明如下。注释标注了各路径的主要职责。

```
core/
├── manage.py                 # 统一命令行入口，集成初始化、导入、导出、监控等子命令
├── requirements.txt          # 生产环境核心依赖清单，不含可选解析库
├── config/
│   ├── settings.py           # 全局配置变量（数据库路径、探活超时、导出格式等）
│   └── logging.conf          # 日志分级与输出目标配置（文件/控制台）
├── app/
│   ├── __init__.py           # 应用工厂函数，创建 Flask 核心实例
│   ├── models.py             # SQLAlchemy 数据模型定义（Resource, Category, AccessLog）
│   ├── schemas.py            # 请求与响应数据结构序列化校验（Pydantic）
│   ├── routes/
│   │   ├── api.py            # RESTful 接口：资源增删改查、批量导入、状态查询
│   │   └── web.py            # 前端页面路由：首页导航、分类视图、统计面板
│   ├── services/
│   │   ├── validator.py      # URL 协议、域名合法性校验与去重逻辑
│   │   ├── probe.py          # 链接可达性探测（异步并发请求与超时控制）
│   │   └── exporter.py       # 资源列表导出为 Markdown / JSON / CSV 格式
│   └── static/               # 前端静态资源（CSS 样式、JavaScript 交互脚本）
├── tests/
│   ├── unit/                 # 单元测试用例（数据模型、校验器、导出器）
│   └── integration/          # 集成测试（API 完整流程、数据库迁移）
├── docs/                     # 项目文档源码，包含入门、用户、管理、开发四部分
└── fixtures/
    ├── sample_links.json     # 示例资源数据，用于快速演示与开发调试
    └── categories.yaml       # 预置分类标签体系，支持用户自定义扩展
```

## 贡献指南

我们欢迎社区开发者以多种形式参与本项目。请遵循以下步骤提交贡献。

1.  **问题反馈与建议**：在 GitHub Issues 中搜索是否已有类似话题，若无则新建 Issue，并详细描述使用场景、预期行为与当前表现，附带运行环境信息。

2.  **分支开发工作流**：将主仓库 fork 至个人账户，基于 `develop` 分支创建功能特性分支（命名格式为 `feature/简述` 或 `fix/简述`），所有代码修改请保持与现有编码规范一致（PEP 8）。

3.  **单元测试覆盖**：新增功能或修复缺陷时，需在 `tests/` 目录下补充对应的单元测试或集成测试用例，确保代码行覆盖率不低于 85%。运行 `pytest` 验证全部用例通过。

4.  **文档同步更新**：若修改涉及用户可见行为（例如新增配置项、修改命令行参数、调整输出格式），请同步更新 `docs/` 下对应的手册章节，并确保示例代码片段可执行。

5.  **发起拉取请求**：完成本地自测后，向主仓库的 `develop` 分支发起 Pull Request。在 PR 描述中关联相关 Issue 编号，列出主要改动点与测试结果摘要。PR 经至少一名维护者审核通过后合并。

## 常见问题

**问：项目是否必须依赖 Flask 框架？能否仅使用命令行模式运行？**

答：Flask 仅用于提供 Web 导航界面与可视化统计面板，非核心必须组件。若您仅需命令行管理资源列表，可直接使用 `manage.py` 的子命令（如 `import`、`export`、`probe`）完成全部操作，无需启动 Web 服务。此时可注释或移除 `requirements.txt` 中的 Flask 依赖。

**问：导入大批量 URL 时出现超时或连接重置错误，如何处理？**

答：系统默认的 HTTP 探活超时时间为 5 秒，并发线程数为 10。若导入链接数量超过 1000 条或目标服务器响应较慢，建议修改 `config/settings.py` 中的 `PROBE_TIMEOUT` 与 `PROBE_MAX_WORKERS` 参数。同时可分批执行导入，每次处理 200 条，以减少单次负载。

**问：资源分类标签支持多级嵌套吗？如何自定义？**

答：支持无限级父子嵌套。分类结构定义在 `fixtures/categories.yaml` 文件中，用户可直接编辑该文件添加、删除或重命名分类节点。编辑后执行 `python manage.py load-categories` 即可更新数据库。若需通过 API 动态管理，请参考 `docs/developer/api.md` 中的分类接口说明。

## 许可证

MIT License

Copyright (c) 2026 HyperLink Nexus Contributors

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
