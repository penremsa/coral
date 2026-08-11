# LinkPilot Resource Aggregator

LinkPilot 是一个面向技术内容创作者、本地化工程师和多媒体资源管理者的轻量级外链资源汇总与导航系统。该项目定位于解决分散在多平台的多媒体资源链接（尤其是中文字幕、影视素材、在线播放源等）难以统一归档、检索和分享的问题，通过结构化的 Markdown 数据存储与静态站点生成逻辑，帮助用户快速建立私有或团队共享的资源索引库。

目标用户包括独立影视翻译爱好者、字幕组运营人员、海外华人内容策展人以及需要批量管理在线视频播放链接的产品经理。LinkPilot 不提供任何实际媒体内容的托管或分发，仅作为 URL 元数据的组织工具，所有引用的外部资源均需用户自行核实其合法性与可用性。

## 功能概览

- **多级分类索引**：支持按语言类型（中文字幕、外文字幕）、媒体格式（MP4、MKV、WebM）、播放源性质（国产、海外、聚合站）等维度自定义标签体系，实现链接的精细化分组。

- **批量导入与去重**：通过 CSV 或 TSV 模板一次性导入大量 URL，系统自动检测重复条目并基于域名和路径相似度算法给出合并建议，减少人工整理开销。

- **可用性巡检**：内置定时调度任务，对已收录的在线播放链接进行 HTTP 状态码检查（200/403/404/超时），生成可用性报表并以邮件或 Webhook 方式通知维护人员。

- **快速检索与过滤**：基于内存索引的即时搜索响应，支持域名、页面标题、关键词描述、录入时间区间等多条件组合筛选，结果可按相关性或最后检查时间排序。

- **导出与分享**：将任意分类或搜索结果集导出为纯 Markdown 列表、JSON 结构化数据或 HTML 书签文件（bookmarks.html），便于嵌入团队 Wiki 或浏览器导入。

- **访问统计看板**：记录每个外链在系统内的点击次数、最后访问时间、引用来源页面，帮助管理员识别高频使用资源与僵尸链接。

- **权限分级**：支持只读访客、编辑者、管理员三种角色，编辑者可新增/修改/软删除链接，管理员可调整分类架构和巡检策略，适合多人协作维护。

- **变更历史追踪**：每次对链接元数据的增删改操作均记录操作人、时间戳和变更字段，支持回滚至任意历史版本，保障数据可审计性。

## 应用场景

**场景一：字幕组内部资源库管理**  
字幕组成员日常需要频繁引用多个在线中文字幕下载站和播放源，但各站点域名经常变更或失效。LinkPilot 允许组长统一录入常用源站 URL，成员可通过检索快速定位可用链接，巡检功能自动标记死链并提示更新，显著降低沟通成本。

**场景二：海外华人视频内容策展**  
面向海外华人的内容聚合博客需要定期发布“本周国产剧高清播放指南”类文章，编辑使用 LinkPilot 按剧集、地区、清晰度标签归类大量播放链接，生成 Markdown 表格后直接粘贴至 CMS，发布效率提升约 40%。

**场景三：技术文档中的外链引用管理**  
开源项目文档或技术博客中常包含数十个外部参考链接（如规范文档、API 参考、视频教程）。LinkPilot 可作为独立的外链备份层，当原始页面移动或删除时，能够快速提供候选替代链接或缓存快照提示，避免文档出现大面积失效引用。

**场景四：多媒体内容合规性审查辅助**  
法务或合规团队需要对产品内引用的所有在线视频源进行定期审查。LinkPilot 的导出功能可生成完整的 URL 清单（含域名、路径、录入人、录入时间），配合外部自动化脚本可对接云服务商的内容审核 API，实现合规性流水线的一部分。

## 快速开始

以下步骤适用于 Linux/macOS 系统，Windows 用户建议使用 WSL2 或 Git Bash 环境。

```bash
# 1. 克隆项目仓库
git clone https://github.com/linkpilot-io/linkpilot-core.git
cd linkpilot-core

# 2. 安装依赖（使用 Python 虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化本地数据库（SQLite）
python manage.py migrate

# 4. 导入示例资源数据（包含本批次全部 URL）
python manage.py import-batch --file data/batch_351_455.csv

# 5. 启动开发服务器
python manage.py runserver --port 8080
```

访问 `http://localhost:8080` 进入管理仪表板，默认管理员账号 `admin` / `linkpilot2026`（首次启动后强制修改）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 暂未通过完整测试 |
| SQLite | 3.35+ | 默认嵌入式数据库，适合小型部署（< 10 万条链接） |
| PostgreSQL | 15.x (可选) | 生产环境推荐，需额外配置 pg_config 和 libpq-dev |
| Redis | 7.x (可选) | 用于缓存搜索结果和分布式巡检任务锁，非必需但强烈建议 |
| Node.js | 18.x LTS | 仅用于前端资源构建（Tailwind CSS + Alpine.js），后端运行不依赖 |
| Nginx | 1.24+ (生产) | 反向代理与静态文件服务，开发环境可使用内置 WSGI 服务器 |
| 系统依赖 | build-essential / libssl-dev / libffi-dev | 编译 Python 某些加密库所需，Ubuntu/Debian 需预先安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `docs/user-guide/getting-started.md` | 如何注册账号、添加第一条链接、创建分类？ |
| 管理员手册 | `docs/admin/configuration.md` | 如何调整巡检频率、配置邮件通知、备份数据库？ |
| 开发参考 | `docs/developer/api-endpoints.md` | 所有 RESTful API 的请求/响应格式、鉴权方式是什么？ |
| 部署运维 | `docs/operations/deployment-options.md` | 支持 Docker Compose 还是 K8s？如何做蓝绿发布？ |
| 数据模型 | `docs/developer/data-schema.md` | 链接表、标签表、审计日志表的字段定义和关联关系？ |
| 巡检引擎 | `docs/developer/health-check-architecture.md` | 异步任务队列如何设计？超时和重试策略怎样？ |
| 贡献规范 | `CONTRIBUTING.md` | PR 标题格式、测试覆盖率要求、Commit 消息规范？ |

## 资源列表

### 中文字幕在线资源（高清/免费播放类）

- <code>zhongwenzaixianzimumianfeigaoqing.org.cn</code>
- <code>zaixianbofangzhongwenzimu.org.cn</code>
- <code>zhongwenzimuzaixianmianfei.org.cn</code>
- <code>yiquerzhongwenzimu.org.cn</code>
- <code>zhongwenzimuzhifusiwang.org.cn</code>
- <code>zhongwenzimushaofurenqi.org.cn</code>

### 国产视频在线播放源

- <code>yirenguochanzaixianshipin.org.cn</code>

### 高清/美女类视频播放站点

- <code>gaoqingshipinzaixianguankanw.org.cn</code>
- <code>meinvshipinzaixianguankan.org.cn</code>

### 综合聚合类播放平台

- <code>jiujiumitaozaixianbofang.org.cn</code>

## 项目结构

```
linkpilot-core/
├── backend/                          # 后端核心代码（Python Django）
│   ├── apps/
│   │   ├── links/                    # 链接资源管理模块（增删改查、标签、去重）
│   │   ├── health/                   # 可用性巡检引擎（异步检查 + 回调通知）
│   │   ├── audit/                    # 审计日志与变更历史（记录所有写操作）
│   │   └── accounts/                 # 用户认证、角色权限（基于 Django 权限系统）
│   ├── core/                         # 项目配置（settings, urls, wsgi）
│   │   ├── settings/                 # 分环境配置（base, dev, prod, test）
│   │   └── asgi.py                   # 异步支持入口（用于 WebSocket 统计推送）
│   └── manage.py                     # Django 管理脚本
├── frontend/                         # 管理面板 UI（Vite + Tailwind + Alpine）
│   ├── src/
│   │   ├── pages/                    # 仪表板、列表页、详情页、导入向导
│   │   ├── components/               # 复用组件（搜索框、标签选择器、状态徽章）
│   │   └── stores/                   # 前端状态管理（Pinia 风格，轻量响应式）
│   └── dist/                         # 构建产物（部署时静态文件）
├── data/                             # 示例数据与批处理导入目录
│   ├── batches/                      # 按批次存放 CSV 导入文件（含第 351/455 批）
│   └── fixtures/                     # 初始分类与标签种子数据
├── docs/                             # 完整文档（用户指南、管理员手册、API 参考）
│   ├── user-guide/                   # 面向普通用户的操作说明
│   ├── admin/                        # 面向运维人员的部署与调优手册
│   └── developer/                    # 面向贡献者的架构设计与接口文档
├── scripts/                          # 辅助脚本（数据库备份、迁移、批量 URL 规范化）
│   ├── health_check_worker.py        # 独立运行的巡检守护进程
│   └── url_normalizer.py             # URL 标准化工具（去重前置处理）
├── tests/                            # 单元测试与集成测试（pytest 框架）
│   ├── unit/                         # 模型层、工具函数单测
│   └── integration/                  # API 端到端测试、巡检任务模拟
├── docker-compose.yml                # 本地开发全栈编排（PostgreSQL + Redis + Nginx）
├── Dockerfile                        # 生产容器镜像构建定义（多阶段构建）
├── requirements.txt                  # Python 依赖清单（精确版本锁定）
├── .env.example                      # 环境变量模板（数据库连接、密钥、邮件 SMTP）
└── LICENSE                           # MIT 许可证
```

## 贡献指南

1. **查阅项目看板与议题**  
   访问 GitHub Issues 板块，筛选标签为 `good first issue` 或 `help wanted` 的任务。新功能或重大变更建议先创建讨论议题（Discussion）以征询维护者意见，避免无效 PR。

2. **Fork 仓库并创建特性分支**  
   从主仓库的 `main` 分支派生个人 Fork，本地新建分支命名遵循 `feature/描述` 或 `fix/描述` 格式（例如 `feature/support-https-probe`）。禁止直接向 main 分支推送。

3. **编写测试与执行静态检查**  
   所有新增后端 API 或工具函数必须附带至少 3 个正向/异常单元测试，前端组件变更需通过 ESLint 和 Prettier 检查。运行 `make test` 和 `make lint` 确保通过全部检查项。

4. **更新相关文档**  
   若变更涉及用户可见功能（如新增配置项、修改 API 响应字段），同步更新 `docs/` 下对应的 Markdown 文件。文档缺失或过时将被要求补充后再合并。

5. **提交 PR 并填写变更清单**  
   PR 描述中需包含变更动机、测试结果截图（或日志）、破坏性变更说明。至少需要一名核心维护者（core maintainer）的 Approve 方可合并。合并方式采用 Squash and Merge，以保持历史整洁。

## 常见问题

**问：LinkPilot 是否存储或缓存外部链接的实际媒体内容（视频、字幕文件）？**  
答：LinkPilot 仅存储 URL 字符串及其元数据（标题、标签、录入时间、检查状态）。系统不下载、不转存、不代理任何第三方站点的音视频或文本文件。所有收录的链接均以超链接形式展示，用户点击后直接跳转至原始站点，完全由外部服务提供实际内容。

**问：导入的 URL 数量达到数千或数万级别时，巡检性能如何？**  
答：默认巡检采用基于 Celery 的分布式任务队列（支持 Redis/RabbitMQ），单工作进程并发数可调。对于 5 万条链接，首次全量巡检（超时 10 秒、重试 2 次）在 8 核 16GB 内存服务器上约需 90 分钟完成。建议将巡检分散至低峰时段执行，并可结合域名分组策略降低目标站点的请求压力。

**问：能否将 LinkPilot 部署在内网环境，完全不访问公网？**  
答：可以。LinkPilot 本身不需要任何外网调用来执行核心功能（CRUD、检索、导出）。但可用性巡检功能依赖对外部链接发起 HTTP 请求，若部署于完全隔离内网，该功能将无法正常工作，此时可关闭巡检调度或将其配置为仅检查内网资源。所有依赖包均可通过离线 PyPI 镜像或 vendor 目录预先提供。

## 许可证

MIT License

Copyright (c) 2026 LinkPilot Contributors

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
