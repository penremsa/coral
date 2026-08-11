# Navigator Hub

Navigator Hub 是一个面向技术调研人员、数据分析师与合规审查机构的高质量网络资源导航系统。该项目不提供任何实质性的媒体内容或文件分发服务，仅作为公开可访问的网络地址信息整理工具，用于辅助用户快速定位特定类型的网络信息源头，开展网络生态研究、内容合规性分析及市场趋势研判工作。项目核心定位为“结构化外链信息汇总平台”，通过人工筛选与自动化巡检相结合的方式，对网络资源的可访问性、分类准确性和信息安全性进行初步标注，帮助目标用户群体在海量网络信息中高效定位研究方向。

项目严格遵循中华人民共和国网络安全相关法律法规，不对任何链接所指向的实际内容进行缓存、代理或二次分发。所有资源列表均来源于公开互联网渠道，仅供学术研究及内部培训使用。平台本身不存储、不生成、不传播任何违反法律法规的信息，且明确鼓励所有使用者遵守公序良俗与行业规范。

## 功能概览

- **多级分类索引**：系统预置超过二十个一级分类域，涵盖综合门户、垂直领域资讯、学术数据库及行业报告来源，支持按业务场景快速缩小检索范围。
- **批量连通性检测**：内置轻量级网络探测模块，可对收录的全部链接进行定时HTTP状态码验证，自动标记异常失效地址，并在管理后台生成可达性趋势图表。
- **自定义标签体系**：允许用户为任意链接添加多维度业务标签，如“高可信源”“需代理访问”“境外站点”“备案中”等，便于团队内部形成统一的风险认知标准。
- **访问日志脱敏分析**：在用户授权前提下记录匿名化的点击行为，聚合生成热门资源时段分布与地域热度图谱，为内容采购策略提供数据决策支持。
- **黑名单自动过滤**：系统加载实时更新的恶意站点黑名单库，若用户导入的链接命中黑名单或疑似钓鱼特征，前端将给出风险提示并阻断跳转。
- **离线快照保存**：对于部分高度关注且内容稳定的政策类与白皮书类资源，系统支持定期抓取公开的纯文本信息，生成只读快照，便于在原始站点临时不可用时继续完成基础调研工作。
- **操作审计追踪**：所有链接的增删改操作均记录完整操作人、时间戳与变更差异，满足企业内部合规审计对于数据变更可追溯的要求。

## 应用场景

- **互联网内容生态学术研究**：高校新闻传播学院及社会学研究团队可利用本系统整理特定垂直领域（如影视文化、青年亚文化、区域民生）的网络信息分发渠道，分析不同平台的内容生产特征与传播路径差异。
- **企业合规部门日常巡检**：拥有大量线上品牌曝光业务的企业，其法务与合规团队可定期通过本导航系统抽取竞品或关联方的公开信息发布入口，监测是否存在品牌侵权、名誉损害或误导性宣传线索。
- **网络安全等级保护自查**：政企单位信息安全运维人员在开展等级保护测评时，可使用本系统快速建立对外部第三方接口及合作方资源站的访问台账，清理非必要且未备案的外部链接，缩小潜在攻击面。
- **市场竞品情报收集**：从事数字经济领域的市场分析师，通过系统分类标签筛选同行业数据来源，持续追踪友商动态、行业报告发布周期以及用户评论聚集地，支撑季度战略规划报告的一手资料引用。
- **新员工内部培训演练**：大型互联网公司入职培训期间，可将本导航系统作为网络信息辨别与合规操作的实战沙盘，新员工通过访问不同类型的链接，直观了解哪些属于正常商业门户，哪些带有明显风险特征，从而提升整体信息安全意识。

## 快速开始

以下步骤将指导您在三分钟内完成本系统的本地开发环境搭建。

```bash
# 1. 克隆项目主仓库
git clone https://github.com/example/navigator-hub.git

# 2. 进入项目工作目录
cd navigator-hub

# 3. 安装所有依赖项（使用 npm）
npm install

# 4. 复制环境变量模板并填充本地数据库连接信息
cp .env.example .env

# 5. 执行数据库结构迁移与初始种子数据导入
npm run migrate
npm run seed

# 6. 启动开发服务器（默认监听 3000 端口）
npm run dev
```

成功启动后，在浏览器中访问 `http://localhost:3000` 即可进入系统主页。默认管理员账户为 `admin@navigator.local`，初始密码为 `ChangeMe@2026`，首次登录后强制要求修改密码。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | v18.17.0 或更高 LTS 版本 | 运行时基础环境，提供事件驱动异步 I/O 能力 |
| PostgreSQL | v14.0 及以上 | 主数据库，存储链接元数据、用户信息及操作审计日志 |
| Redis | v6.2 及以上 | 缓存会话状态与临时连通性检测结果，降低数据库查询压力 |
| Nginx | v1.22 及以上 | 生产环境反向代理与静态资源压缩分发，可选开发环境直接使用 Vite |
| Git | v2.25 及以上 | 源码版本控制工具，用于拉取仓库及提交贡献 |
| PM2 | v5.0 及以上 | 生产环境进程守护管理器，支持集群模式负载均衡 |
| 系统内存 | 最低 4GB，推荐 8GB | Node 应用堆内存 + 数据库缓存 + 操作系统预留 |
| 磁盘空间 | 至少 20GB 可用 | 存储代码、数据库文件、日志及离线快照文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 架构设计 | `/docs/architecture/overview.md` | 系统采用何种微服务拆分策略？数据流向与模块耦合关系如何？扩展性瓶颈在哪里？ |
| 部署运维 | `/docs/deployment/production-checklist.md` | 生产环境需要开放哪些端口？SSL证书如何配置？日志轮转策略与监控告警阈值如何设定？ |
| 接口规范 | `/docs/api/restful-design.md` | 前后端交互的鉴权机制是什么？分页与过滤参数格式要求？错误码体系定义标准？ |
| 数据治理 | `/docs/data/link-lifecycle.md` | 外部链接从提交、审核、上线到归档的完整生命周期流程？异常链接下架审批需要几级确认？ |
| 安全基线 | `/docs/security/threat-model.md` | 系统面临的潜在威胁建模？XSS与CSRF防护措施？数据库连接串加密存储方案？ |
| 前端开发 | `/docs/frontend/component-library.md` | 项目使用哪个UI框架？自定义组件的命名规范与单元测试覆盖标准？状态管理选型依据？ |

## 资源列表

本系统当前版本（v3.1.2）收录并整理的外部信息导航链接共计10条，按内容主题与访问特征划分如下。所有链接均按用户原始提供形式原样列出，未做任何协议补全或域名格式修正。

**综合影视文化类信息入口**

<code>nannvpapawangzhan.org.cn</code>

<code>laosijimianfeishipin.org.cn</code>

<code>shunvzhongwenzimu.org.cn</code>

<code>madoushichuanmeiapp.org.cn</code>

<code>yazhoujiqingtupian.org.cn</code>

**专题视频与高清资源聚合类入口**

<code>wuyezaixianshipinmianfei.org.cn</code>

<code>gaoqingzhongwenzimu.org.cn</code>

<code>mianfeidianyingwangzhandaquan.org.cn</code>

<code>dianshijuquanjimianfeiguankan.org.cn</code>

<code>gaoqingyingshizaixianguankan.org.cn</code>

## 项目结构

项目采用经典的 MVC 分层架构，辅以领域驱动设计的模块化思想，核心业务逻辑与基础设施代码严格隔离。以下为关键目录及文件说明：

```
navigator-hub/
├── apps/                                 # 多应用子模块（微服务拆分基础）
│   ├── api/                              # RESTful API 服务（入口层）
│   │   ├── controllers/                  # 路由控制器，负责请求参数校验与响应封装
│   │   ├── services/                     # 业务逻辑服务层，编排领域模型与基础设施
│   │   └── validators/                   # 基于 Joi 的入参校验规则定义
│   ├── worker/                           # 后台任务执行器（定时巡检、快照生成）
│   │   ├── checkers/                     # 链接连通性检测具体实现（HTTP/HTTPS）
│   │   ├── parsers/                      # 针对特定站点的内容摘要提取脚本
│   │   └── scheduler/                    # 基于 node-cron 的任务调度配置
│   └── web/                              # 前端 SSR 应用（基于 Next.js）
│       ├── pages/                        # 文件系统路由对应的页面组件
│       ├── components/                   # 可复用的业务组件与通用 UI 组件库
│       └── hooks/                        # 自定义 React Hooks，封装状态与副作用
├── packages/                             # 跨应用共享的代码库
│   ├── database/                         # 数据库模型定义与迁移脚本（Sequelize）
│   │   ├── models/                       # 每个表对应的实体类与关联关系映射
│   │   └── seeders/                      # 初始测试数据与字典表填充脚本
│   ├── cache/                            # Redis 缓存操作封装（包含键名约定与过期策略）
│   ├── logger/                           # 基于 Winston 的日志统一输出格式与传输配置
│   └── utils/                            # 纯函数工具集（URL 标准化、时间处理、加密工具）
├── config/                               # 环境差异化配置（development, staging, production）
│   ├── default.json                      # 所有环境通用的基础配置项
│   └── custom-environment-variables.json # 可被系统环境变量覆盖的敏感配置映射
├── docs/                                 # 项目文档中心（架构决策记录、运维手册、API 文档源文件）
├── scripts/                              # 运维与开发辅助脚本（数据库备份、数据迁移回滚）
├── tests/                                # 单元测试与集成测试套件（Jest + Supertest）
│   ├── unit/                             # 针对 service 与 utils 的纯逻辑单元测试
│   └── integration/                      # 针对 API 端点的完整请求-响应流程测试
├── .env.example                          # 环境变量模板文件，供开发者本地配置参考
├── docker-compose.yml                    # 本地开发环境容器编排（PostgreSQL + Redis + App）
├── Dockerfile                            # 生产环境镜像构建定义（多阶段构建）
├── package.json                          # 项目依赖管理、workspace 定义与脚本命令入口
└── README.md                             # 项目整体说明与导航入口（即本文档）
```

## 贡献指南

我们欢迎并鼓励社区开发者为本项目提交改进代码、补充资源链接或完善文档。为保证项目长期可维护性与代码质量，请遵循以下标准流程：

1.  **问题追踪与需求讨论**：在提交任何代码变更之前，请先在 GitHub Issues 区域搜索是否已有相关话题。若无，则新建一个 Issue，清晰描述您希望解决的问题、新增的功能或建议改进的文档章节，获得核心维护者的反馈确认后再进入开发阶段。
2.  **复刻仓库并创建功能分支**：将主仓库复刻至您的个人账户下，并基于最新的 `develop` 分支创建您的功能分支。分支命名建议遵循 `feat/功能简述`、`fix/问题编号` 或 `docs/文档范围` 格式，以便于自动化工具识别变更类型。
3.  **编写代码与本地自测**：所有新增代码必须包含至少一个正向与一个反向的单元测试用例，确保核心逻辑的鲁棒性。同时运行 `npm run lint` 与 `npm run test` 保证代码风格统一且无回归性问题。对于涉及外部链接变动的更新，请务必在本地环境验证连通性检测脚本的执行结果。
4.  **签署开发者贡献者许可协议**：首次提交拉取请求前，您需要在拉取请求的评论区明确声明“本人已阅读并同意遵守本项目的开发者贡献者许可协议（CLA）”，该声明将被视为具有法律效力的电子签署。
5.  **发起拉取请求并参与代码审查**：将您的功能分支推送至复刻仓库，并向主仓库的 `develop` 分支发起拉取请求。请在请求描述中详细关联相关的 Issue 编号，列出变更点及测试覆盖情况。维护者会在两个工作日内进行审查，您可能需要根据反馈进行修改直至通过所有检查项。

## 常见问题

**Q1: 系统启动时提示数据库连接失败，但我的 PostgreSQL 服务已经运行。如何排查？**

A1: 请依次执行以下检查：首先确认 `.env` 文件中的 `DB_HOST`、`DB_PORT`、`DB_USER`、`DB_PASSWORD` 及 `DB_NAME` 五项配置是否与您本地实际环境完全一致。其次检查 PostgreSQL 的 `pg_hba.conf` 文件是否允许当前用户的 IP 地址连接（若使用 `localhost` 或 `127.0.0.1` 通常无问题）。最后尝试使用命令行工具 `psql -U 用户名 -d 数据库名 -h 主机地址 -p 端口` 手动连接，若手工连接失败则说明是数据库服务侧问题，与项目代码无关。若手工连接成功，请检查项目依赖的 `pg` 驱动版本是否与您的数据库大版本兼容。

**Q2: 如何更新内部收录的外部链接列表？是否支持批量导入？**

A2: 系统提供两种更新方式。第一种为单条操作，在管理后台的“资源管理”页面点击“新增链接”，填写目标 URL、标题、分类标签及可信度评级后提交，经审核通过后实时生效。第二种为批量导入，您需要准备一份符合系统模板格式的 CSV 或 JSON 文件（模板文件可在 `/docs/assets/import-template.json` 获取），通过后台的“批量导入”功能上传，系统将启动异步任务处理，完成后会发送站内通知告知导入成功条数与失败记录详情。请注意，所有新增链接均会经过系统自带的恶意特征与黑名单过滤，若触发风险规则将自动驳回并给出提示原因。

**Q3: 系统运行一段时间后磁盘空间报警，哪些目录占用最大？如何安全清理？**

A3: 通常情况下，占用空间最大的三个目录分别是：`/logs`（存放历史应用日志）、`/storage/snapshots`（存放页面离线快照文件）以及 PostgreSQL 的 `pg_wal` 目录（数据库预写日志，由数据库自身管理）。对于日志文件，我们建议配置 PM2 或系统级的 logrotate 策略，按天轮转并保留最近 30 天的压缩归档。对于快照文件，管理员可在后台“系统设置 - 存储管理”中设定保留期限（默认 90 天），系统会每日凌晨自动执行清理任务。若数据库文件本身过大，请运行 `VACUUM FULL` 命令回收已删除记录的空间，但该操作需要停机维护，建议在业务低峰期执行。

## 许可证

MIT License

Copyright (c) 2026 Navigator Hub Contributors

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

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:38
