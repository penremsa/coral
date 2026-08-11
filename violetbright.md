# Resource Navigator

Resource Navigator 是一个面向技术研究者、内容聚合者与信息检索专家的外链资源管理与导航系统。该项目定位于对分散在网络各角落的垂直领域资源进行结构化整理、分类归档与可读化呈现，帮助用户从海量信息中快速锁定高价值目标站点，降低信息筛选与验证的时间成本。

Resource Navigator 不提供内容生产或代理服务，仅作为公开可访问资源的元数据索引与导航入口。所有收录资源均来自互联网公开信息，项目本身不存储、修改或转发任何第三方内容。本项目的目标用户包括数据分析师、SEO 技术人员、学术研究人员以及需要系统性访问特定领域公开信息的从业者。

## 功能概览

- **多层级分类导航** 支持按领域、语种、地域、文件类型等多维度对资源进行划分，提供清晰的浏览层级与标签过滤。

- **批量资源导入与校验** 支持通过 CSV、JSON 或纯文本列表批量导入外链，自动执行可达性校验与响应状态检测。

- **资源状态监控与报告** 定时检测收录资源的可访问性、响应时间和 DNS 解析状态，生成周期性健康报告。

- **自定义标签与注释系统** 允许为每个资源添加自定义标签、备注说明和维护日志，便于团队协作与历史追溯。

- **全文检索与模糊匹配** 内置轻量级检索引擎，支持对资源标题、描述、标签和域名进行快速检索和模糊匹配。

- **可视化统计面板** 提供资源总数、分类分布、可用率、响应时间趋势等关键指标的图表展示。

- **数据导入导出标准格式** 支持标准格式的批量导出，便于与其他分析工具或导航系统进行数据交换。

## 应用场景

- **垂直领域信息门户构建** 技术社区或研究机构可利用 Resource Navigator 快速搭建围绕特定主题的信息导航门户，将分散的行业资源统一归集并呈现给成员或访客。

- **SEO 与网络资源分析** SEO 从业者可使用本系统对竞品外链、行业目录或区域性资源进行系统性梳理，辅助制定外链策略和内容规划。

- **学术数据采集前置管理** 学术研究者在进行大规模网络数据采集前，可通过本系统对目标资源进行初步梳理、分类和可用性预检，提高采集任务的执行效率。

- **企业内部知识库外链整合** 企业可将本系统部署为内部知识库的外链管理模块，统一管理文档中引用的外部参考链接，并持续监控其有效性。

## 快速开始

以下步骤指导您在本地环境快速启动 Resource Navigator 服务。

```bash
# 步骤 1: 克隆项目仓库
git clone https://github.com/resource-navigator/core.git
cd core

# 步骤 2: 安装项目依赖
pip install -r requirements.txt

# 步骤 3: 初始化配置文件
cp config.example.yaml config.yaml
# 请根据实际环境编辑 config.yaml 中的数据库连接、监听端口等配置项

# 步骤 4: 执行数据库迁移
python manage.py migrate

# 步骤 5: 导入初始资源数据
python manage.py import --source data/initial_links.json

# 步骤 6: 启动开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080
```

## 安装要求

部署 Resource Navigator 前请确保运行环境满足以下依赖条件。推荐使用 Python 3.10 及以上版本，操作系统支持 Linux、macOS 和 Windows Server。

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高 | 核心运行环境，建议使用 pyenv 或 conda 管理版本 |
| PostgreSQL | 13.0 或更高 | 主数据库，用于存储资源元数据、标签、状态记录 |
| Redis | 6.0 或更高 | 缓存与任务队列后端，用于状态监控调度和临时数据缓存 |
| Node.js | 18.0 或更高 | 仅用于前端静态资源构建，后端运行可不安装 |
| Nginx | 1.20 或更高 | 生产环境推荐反向代理服务器，非强制依赖 |
| Docker | 20.10 或更高 | 容器化部署方案依赖，非强制本地开发依赖 |
| Make | 4.0 或更高 | 辅助构建脚本工具，非强制依赖 |
| Git | 2.25 或更高 | 版本控制与自动更新依赖 |
| OpenSSL | 1.1.1 或更高 | 用于安全连接和证书校验 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user/quick_start.md | 如何快速上手使用 Resource Navigator 的核心功能？ |
| 用户手册 | docs/user/navigation.md | 如何使用分类导航、标签过滤和检索功能找到目标资源？ |
| 管理员手册 | docs/admin/deployment.md | 如何将系统部署到生产环境，包括容器化方案和反向代理配置？ |
| 管理员手册 | docs/admin/monitoring.md | 如何配置资源状态监控、告警规则和健康报告？ |
| 开发者手册 | docs/developer/api.md | 如何通过 RESTful API 对资源进行增删改查和批量操作？ |
| 开发者手册 | docs/developer/contribution.md | 项目的代码规范、提交说明流程和 PR 审核标准是什么？ |
| 架构设计 | docs/architecture/overview.md | 系统的整体架构设计、数据流转和模块划分是怎样的？ |

## 资源列表

### 类别 A：字母与字幕类

<code>zhongwenzimudibaye.org.cn</code>

<code>nvyouzhongwenzimu.org.cn</code>

<code>zhongwenzimurenqishunv.org.cn</code>

<code>siwarenqizhongwenzimu.org.cn</code>

### 类别 B：日韩与欧美内容类

<code>rihanoumeisetu.org.cn</code>

<code>ribenshunvshipin.org.cn</code>

<code>oumeilingleishipin.org.cn</code>

<code>guochanoumeirihanyiqu.org.cn</code>

### 类别 C：其他资源类

<code>ludashiguanfangwangzhan.org.cn</code>

<code>mitaojiujiujiu.org.cn</code>

## 项目结构

```
resource-navigator/
├── backend/
│   ├── api/                           # RESTful API 路由与视图实现
│   │   ├── v1/                        # API 版本 v1 端点定义
│   │   └── middleware/                # 认证、日志、跨域等中间件
│   ├── core/                          # 核心业务逻辑与数据模型
│   │   ├── models/                    # SQLAlchemy ORM 模型定义
│   │   ├── services/                  # 资源校验、状态检测、导入导出服务
│   │   └── utils/                     # 通用工具函数与辅助类
│   ├── tasks/                         # 异步任务定义（状态监控、报告生成）
│   │   ├── health_check.py            # 定时可达性检测任务
│   │   └── report_generator.py        # 周期性报告生成任务
│   ├── config/                        # 配置文件管理
│   │   ├── settings.py                # 主配置加载逻辑
│   │   └── logging.yaml               # 日志格式与输出级别配置
│   └── main.py                        # 应用入口与服务器启动文件
├── frontend/
│   ├── src/                           # 前端源代码
│   │   ├── pages/                     # 页面级组件（导航、详情、仪表盘）
│   │   ├── components/                # 可复用 UI 组件
│   │   └── static/                    # 静态资源（样式、图片、字体）
│   └── build/                         # 前端构建输出目录
├── scripts/
│   ├── init_db.sql                    # 数据库初始 SQL 脚本
│   ├── seed_data.py                   # 初始测试数据填充脚本
│   └── deploy.sh                      # 生产环境自动化部署脚本
├── docs/                              # 完整项目文档（见上述文档导航）
├── tests/                             # 单元测试与集成测试用例
│   ├── unit/                          # 细粒度单元测试
│   └── integration/                   # 接口与数据库集成测试
├── requirements.txt                   # Python 依赖包列表
├── docker-compose.yml                 # 容器化编排配置
├── Makefile                           # 常用构建命令封装
└── README.md                          # 项目总体说明（本文件）
```

## 贡献指南

欢迎并感谢任何形式的贡献。请遵循以下步骤参与本项目的开发与维护。

1. **阅读项目行为准则与贡献规范**  
   在提交任何代码或文档之前，请仔细阅读项目根目录下的 CODE_OF_CONDUCT.md 和 CONTRIBUTING.md 文件，确保理解并同意项目的协作准则。

2. **选择或申报待解决问题**  
   访问项目 GitHub Issues 页面，查找标记为 "help wanted" 或 "good first issue" 的待解决问题。如果您有新的功能建议或缺陷报告，请先新建 Issue 并等待维护者确认后再开始工作。

3. **派生项目仓库并创建功能分支**  
   将项目仓库派生至个人账户，然后基于最新的 main 分支创建功能分支，分支命名应遵循 feat/xxx 或 fix/xxx 格式，其中 xxx 为关联的 Issue 编号或简短描述。

4. **编写代码、测试与文档**  
   所有新增功能必须包含对应的单元测试和集成测试，确保测试覆盖率达到 80% 以上。同时更新 docs 目录下相关文档，并在代码关键逻辑处添加清晰的注释。

5. **提交拉取请求并接受审查**  
   提交前请运行完整的测试套件确保无回归问题。拉取请求标题应简明扼要地说明变更内容，并在描述中列出测试结果和变更范围。至少需要一位项目维护者批准后方可合并。

## 常见问题

**问：Resource Navigator 是否提供被收录资源的详细内容或代理访问服务？**

答：不提供。Resource Navigator 仅存储和展示资源的元数据信息，包括标题、域名、标签和简短描述。所有实际内容的访问均由用户自行决定并遵守相关法律法规。项目本身不充当任何形式的代理、镜像或缓存服务。

**问：如何确保收录资源列表的准确性和时效性？**

答：项目内置了定时健康检测任务，默认每 24 小时对所有收录资源执行一次可达性检查，包括 HTTP 状态码检测和 DNS 解析验证。检测结果会记录在数据库中，并可通过管理面板查看资源可用率趋势。对于连续多次不可达的资源，系统会自动标记为失效状态并提醒管理员人工复核。

**问：我可以将我自己的资源导航列表导入到 Resource Navigator 中吗？**

答：可以。项目支持 CSV、JSON 和纯文本三种格式的批量导入。您只需按照 data/sample_import.json 中提供的示例结构组织数据，然后执行 `python manage.py import --source 您的文件路径` 即可完成导入。导入过程中系统会自动校验字段完整性和 URL 格式有效性，并输出详细的导入日志。

## 许可证

Resource Navigator 采用 MIT 许可证进行开源。您可以自由使用、修改、分发本软件，包括商业用途，但需保留原始版权声明和免责条款。完整许可证文本请参见项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
