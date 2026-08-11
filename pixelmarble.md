# OpenBet Resource Hub

OpenBet Resource Hub 是一个面向体育数据分析与竞彩技术研究领域的开源资源聚合平台。项目定位为技术型外链导航与元数据索引系统，主要服务于从事体育赛事建模、赔率趋势分析、竞彩策略研究的开发者与量化分析师。本项目不提供任何投注建议或结果预测，仅作为公开网络资源的结构化索引工具，帮助研究者快速定位相关数据源与信息渠道。

平台通过人工筛选与自动化健康检查相结合的方式，对体育数据领域的垂直站点进行归类、标签化与可用性监测，解决研究者在数据采集、历史对照、赔率波动分析等环节中信息分散、链接失效、来源不明的痛点。项目本身不存储任何赛事数据或用户信息，所有外部链接均以原始形式呈现，用户点击后即跳转至第三方站点。

## 功能概览

- **资源分类索引**：按站点功能属性划分为预测分析、数据前瞻、情报汇总等核心类别，支持按标签快速筛选。

- **链接健康监控**：每日定时检测收录链接的可访问性与响应状态码，异常链接自动标记并移入待审核队列。

- **元数据提取**：对目标站点进行结构化信息提取，包括站点标题、关键词、描述、服务器地理位置及最后更新日期。

- **历史快照对比**：记录收录站点首页内容变更的哈希值变化，辅助研究者判断信息来源的稳定性与内容迭代频率。

- **自定义收藏夹**：用户可基于项目提供的资源列表创建个人收藏子集，并通过 JSON 格式导出供其他工具导入。

- **RSS 更新订阅**：针对收录站点的内容更新频率生成聚合 RSS 源，支持通过本地搭建的订阅服务实时获取新增信息。

- **访问统计看板**：提供收录站点的点击热度、时段分布、用户地域分布等匿名化统计图表，帮助管理员优化资源排序。

## 应用场景

- **赛事数据建模**：量化分析师可通过平台获取多个来源的赛前分析、历史对阵记录与赔率变化趋势，用于构建胜率预测模型或蒙特卡洛模拟器。

- **竞彩策略回测**：策略研究者可利用平台汇总的多个预测站点输出作为市场情绪指标之一，结合历史赛事结果进行策略胜率的回溯测试与归因分析。

- **舆情信息聚合**：媒体监测人员可通过平台快速浏览多个分析站点的头版头条与热点标签，把握赛前舆论焦点与市场关注度分布。

- **爬虫种子源管理**：数据采集工程师可将本平台作为爬虫入口层的种子列表，定期同步更新，避免因单一数据源失效导致采集管道中断。

- **学术研究参考**：体育经济学或博弈论领域的学者可将平台资源作为参考文献来源，用于标注数据采集渠道或行业实践案例。

## 快速开始

以下步骤适用于在本地环境部署 OpenBet Resource Hub 的索引管理面板，用于自主维护私有资源列表。

```bash
# 1. 克隆项目仓库至本地
git clone https://github.com/openbet-resource-hub/openbet-hub.git

# 2. 进入项目根目录
cd openbet-hub

# 3. 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 4. 初始化 SQLite 本地数据库与默认配置
python manage.py init_db
python manage.py load_default_resources

# 5. 启动本地开发服务器，默认监听 127.0.0.1:8080
python manage.py runserver
```

启动后，在浏览器访问 `http://127.0.0.1:8080` 即可查看资源列表与各功能面板。首次运行将自动创建 `data/resources.db` 数据库文件并导入项目内置的初始资源索引。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 至 3.11 | 核心运行环境，3.12 及以上版本暂不支持部分依赖库 |
| SQLite | 3.31 及以上 | 内置轻量级数据库，用于存储资源列表与用户配置 |
| requests | 2.28.0 及以上 | 用于链接健康检查与元数据抓取 |
| beautifulsoup4 | 4.11.0 及以上 | 用于解析目标站点的 HTML 结构与元数据提取 |
| lxml | 4.9.0 及以上 | 作为 beautifulsoup4 的解析器后端，提供更高性能的 DOM 遍历 |
| flask | 2.2.0 及以上 | 提供 Web 管理面板的后端服务框架 |
| flask-cors | 3.0.0 及以上 | 处理跨域请求，便于前端独立部署与 API 调用 |
| apscheduler | 3.10.0 及以上 | 定时调度链接健康检查与快照更新任务 |
| markdown | 3.4.0 及以上 | 用于动态生成资源说明文档与帮助页面 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 管理员指南 | `docs/admin/` | 如何配置定时检查间隔、添加私有资源分类、调整快照保留策略 |
| 开发者文档 | `docs/developer/` | 如何扩展元数据提取器、自定义健康检查规则、新增输出格式 |
| API 参考 | `docs/api/` | 资源列表的 RESTful 接口定义、请求参数、返回字段与错误码 |
| 用户手册 | `docs/user/` | 如何使用收藏夹、导出功能、RSS 订阅以及看板解读 |

各文档均提供 Markdown 源文件与编译后的 HTML 版本，位于 `docs/_build/` 目录下。推荐开发者从 `docs/developer/architecture.md` 开始阅读以了解整体模块划分。

## 资源列表

### 赛事预测与推荐分析类

- <code>zuqiubifentuijian.net.cn</code>
- <code>jinrizuqiutuijian.net.cn</code>
- <code>zuqiuyuce.net.cn</code>
- <code>zuqiuaiyuce.net.cn</code>

### 赛事问答与综合推荐类

- <code>zuqiuwendantuijian.org.cn</code>

### 赛前前瞻与走势分析类

- <code>zuqiusaiqiantuijian.org.cn</code>
- <code>zuqiubisaiqianzhan.org.cn</code>

### 数据情报与信息汇总类

- <code>zuqiuyucezixun.org.cn</code>
- <code>zuqiuyuceqingbao.org.cn</code>

### 赛事数据分析类

- <code>zuqiufenxizixun.org.cn</code>

## 项目结构

```text
openbet-hub/
├── app/                            # 核心应用模块
│   ├── api/                        # RESTful API 路由与控制器
│   │   ├── resources.py            # 资源增删改查接口
│   │   └── health.py               # 健康检查结果查询接口
│   ├── models/                     # 数据模型与 ORM 映射
│   │   ├── resource.py             # 资源条目模型，含 url、category、status 字段
│   │   └── snapshot.py             # 快照记录模型，存储内容哈希与更新时间
│   ├── services/                   # 业务逻辑服务层
│   │   ├── checker.py              # 链接可用性检查与响应时间测量
│   │   ├── scraper.py              # 元数据提取与页面摘要生成
│   │   └── scheduler.py            # 定时任务注册与调度管理
│   └── utils/                      # 通用工具函数库
│       ├── validators.py           # URL 格式校验与域名规范化
│       └── exporters.py            # JSON / CSV 格式导出工具
├── config/                         # 环境配置与常量定义
│   ├── development.py              # 开发环境配置（调试模式开启）
│   ├── production.py               # 生产环境配置（关闭调试、启用日志滚动）
│   └── default.py                  # 默认配置项，含检查间隔、超时阈值
├── data/                           # 本地数据存储目录
│   ├── resources.db                # SQLite 主数据库文件
│   └── snapshots/                  # 快照内容缓存目录，按资源 ID 分片存储
├── docs/                           # 完整文档目录
│   ├── admin/                      # 管理员操作指南
│   ├── developer/                  # 开发者扩展文档
│   └── user/                       # 终端用户使用手册
├── tests/                          # 单元测试与集成测试套件
│   ├── test_checker.py             # 健康检查模块测试用例
│   └── test_scraper.py             # 元数据提取模块测试用例
├── requirements.txt                # Python 依赖列表，固定版本号
├── manage.py                       # 命令行管理入口，集成 init_db、runserver 等命令
└── README.md                       # 项目首页说明文档
```

## 贡献指南

欢迎各类形式的贡献，包括但不限于新增资源链接、改进元数据提取规则、优化健康检查逻辑以及完善文档。请遵循以下步骤：

1. 在 GitHub 上 Fork 本仓库至个人账号，并克隆至本地开发环境。建议在 `develop` 分支基础上新建特性分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式。

2. 新增或修改资源列表时，请编辑 `data/default_resources.json` 文件，按照既有的 JSON Schema 格式添加条目，确保每个条目包含 `url`、`category`、`tags` 和 `description` 字段。提交前运行 `python manage.py validate_resources` 进行格式校验。

3. 若涉及代码逻辑修改，请同步更新对应的单元测试文件，确保测试覆盖率达到百分之八十以上。运行 `pytest tests/` 执行全部测试用例，确保无回归错误。

4. 编写或修改文档时，请遵循 `docs/` 目录下的 Markdown 样式规范，使用二级标题作为章节分隔，代码块需标注语言类型。新增文档需在 `docs/README.md` 的目录树中添加引用。

5. 提交 Pull Request 至本仓库的 `main` 分支，并在描述中清晰说明改动目的、影响范围以及测试情况。项目维护者将在三个工作日内进行 Review，必要时会邀请贡献者参与进一步讨论。

## 常见问题

**问题一：部分收录链接返回 403 或 521 状态码，是否意味着该资源已失效？**

并非绝对。部分站点可能配置了反爬策略或防火墙规则，会拒绝非浏览器的请求头。本项目的健康检查模块默认使用 Python requests 库的模拟浏览器 User-Agent 发起访问，但某些站点仍需特定的 Cookie 或 Referer 头才能正常响应。建议管理员在 `config/default.py` 中调整 `CHECK_HEADERS` 配置项，添加自定义请求头后重新触发检查。若连续三次检查均失败，系统会自动将该链接标记为“异常”并发送通知。

**问题二：如何将本平台部署为长期运行的后台服务，而非仅限本地开发？**

项目提供了 systemd 单元文件模板，位于 `deploy/openbet-hub.service`。将该文件复制到 `/etc/systemd/system/` 目录下，修改 `User` 和 `WorkingDirectory` 字段为实际运行用户与项目路径，然后执行 `systemctl enable openbet-hub` 与 `systemctl start openbet-hub` 即可。日志默认输出至 `/var/log/openbet-hub/`，可通过 `journalctl -u openbet-hub -f` 实时查看。生产环境下建议配合 Nginx 反向代理，将静态资源与 API 请求分离。

**问题三：系统每天何时执行链接健康检查？能否手动触发？**

默认调度策略为每日凌晨 2:00 执行全量检查，同时针对标记为“异常”的链接额外在 14:00 执行一次增量检查。若需立即检查，可通过命令行执行 `python manage.py run_health_check --force` 忽略时间窗口强制运行，或调用 API 接口 `POST /api/v1/health/run` 传入 `{"force": true}` 触发。执行结果会写入数据库的 `health_logs` 表中，并可通过管理面板的“检查记录”页面查看详细响应时间与状态信息。

## 许可证

MIT License

Copyright (c) 2026 OpenBet Resource Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
