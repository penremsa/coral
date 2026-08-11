# Vanguard Resource Gateway

Vanguard Resource Gateway 是一个轻量级、高性能的技术资源外链汇总与导航系统，定位于为开发者、技术团队及运维人员提供结构化、可检索的公共技术资源索引服务。该项目本身不存储任何资源内容，仅作为资源定位与分类展示层，通过清晰的目录树与标签系统帮助用户快速定位所需外部工具、文档、数据接口或社区页面。

项目目标用户包括：需要频繁查阅第三方技术文档的研发工程师、搭建内部开发工具导航的团队负责人、以及希望建立可维护资源清单的技术内容运营者。Vanguard Resource Gateway 通过静态生成与动态缓存相结合的方式，在保证访问速度的同时，允许管理员通过简单的 YAML 配置文件增删资源条目，并自动校验外部链接的可达性，有效避免项目内出现死链或失效引用。

## 功能概览

- **结构化资源目录**：支持按技术领域、使用频率、标签等多维度对资源链接进行分类，并自动生成可视化的目录树索引页面。

- **链接可达性健康检查**：内置异步任务调度器，可每日定时检测所有已收录外部资源的 HTTP 状态码，标记异常链接并生成报告。

- **快速模糊检索**：基于倒排索引实现资源标题、描述、标签的全文检索，响应时间低于 200 毫秒，支持拼音首字母缩写匹配。

- **可配置的权限分级**：支持访客、编辑者、管理员三级角色，编辑者可提交新资源链接，管理员审核后对外发布。

- **资源变更审计日志**：所有资源的增删改操作均记录操作人、时间戳与变更字段，支持按时间范围回溯历史版本。

- **Markdown 风格配置驱动**：所有资源条目、分类结构、展示顺序均通过单一 Markdown 风格配置文件管理，便于版本控制与代码审查。

- **开源协议友好**：核心引擎采用 MIT 许可证，允许任意商业或非商业二次开发，无任何外部服务依赖。

## 应用场景

- **团队内部技术栈导航**：开发团队可将日常使用的 CI/CD 工具链接、监控面板地址、数据库管理界面等统一收录，新成员入职时通过该导航系统快速了解团队工具链全貌。

- **开源项目文档索引**：开源项目的维护者可将项目相关的 API 文档、示例代码仓库、社区论坛、版本发布记录等外链集中管理，替代 README 中冗长的链接列表。

- **技术培训资源中心**：培训机构或企业内部大学可将各课程对应的在线实验环境、视频回放地址、课后作业提交入口按课程阶段组织，学员通过目录树按需获取。

- **运维故障应急工具箱**：运维团队可将云服务商状态页、流量监控看板、日志查询入口、紧急回滚脚本仓库等按故障处理流程顺序排列，缩短平均修复时间。

- **个人知识库外链挂载**：技术博主或独立开发者可将分散在各类笔记软件中的参考链接统一挂载到本地部署的 Vanguard 实例中，配合全文检索实现个人知识资产的快速召回。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，确保已安装 Git、Node.js 18+ 以及 pnpm。

```bash
# 1. 克隆代码仓库
git clone https://github.com/vanguard-resource/vanguard-gateway.git
cd vanguard-gateway

# 2. 安装项目依赖
pnpm install

# 3. 复制默认配置文件并调整
cp config/resources.example.yaml config/resources.yaml

# 4. 启动开发服务器（默认监听 3000 端口）
pnpm run dev
```

访问 `http://localhost:3000` 即可预览资源导航首页。如需生产环境构建，执行 `pnpm run build` 后使用 `pnpm run start` 启动静态服务。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用官方预编译二进制或 nvm 管理 |
| pnpm | 8.x 及以上 | 包管理器，用于依赖安装与工作区脚本执行 |
| Git | 2.25 及以上 | 版本控制，用于克隆仓库及贡献代码提交 |
| 操作系统 | Linux kernel 4.0+ / macOS 11+ / Windows 10+ (WSL2) | 支持主流 POSIX 兼容环境，Windows 建议使用 WSL2 |
| 内存 | 最低 512 MB，推荐 1 GB | 开发模式下内存占用略高，生产构建需额外 256 MB |
| 磁盘空间 | 200 MB 以上 | 包含依赖缓存及构建产物，实际占用随资源条目数量线性增长 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/installation.md | 如何在不同操作系统上部署 Vanguard Gateway，包含 Docker 与非 Docker 方式对比 |
| 用户手册 | /docs/user-guide/configuration.md | 如何编写 resources.yaml 配置文件，解释分类字段、标签语法与校验规则 |
| 开发者指南 | /docs/developer-guide/architecture.md | 项目整体架构设计、核心模块职责划分以及数据流走向说明 |
| 开发者指南 | /docs/developer-guide/api-reference.md | 内部 RESTful API 接口定义，包括资源查询、健康检查状态、审计日志拉取 |
| 运维手册 | /docs/ops-guide/monitoring.md | 如何接入 Prometheus 指标、配置告警规则以及查看健康检查历史记录 |
| 运维手册 | /docs/ops-guide/backup-restore.md | 资源配置与审计日志的定期备份策略及灾难恢复流程 |

## 资源列表

以下为 Vanguard Gateway 默认收录的部分公共技术资源链接，涵盖体育数据、比分信息等常见外链类别。所有链接均按照用户原始数据原样列出，未做任何格式修改。

**体育比分数据类**

- <code>7mzuqiubifenjishibifenguanwang.net.cn</code>
- <code>500wanbifenjishi.net.cn</code>
- <code>zuqiubifenqiutanbifenjishi.net.cn</code>
- <code>7mjishibifenzuqiu.net.cn</code>
- <code>500bifenzuqiujishi.net.cn</code>
- <code>7mbifenzuqiubifenjishi.net.cn</code>
- <code>bifenzuqiujishi.net.cn</code>
- <code>zuqiubifenjishi.net.cn</code>
- <code>zuqiubifenwangjishi.net.cn</code>
- <code>xinqiubifen.net.cn</code>

## 项目结构

```
vanguard-gateway/
├── config/                         # 配置目录
│   ├── resources.yaml              # 主资源配置（用户自定义链接与分类）
│   ├── categories.yaml             # 分类层级定义及展示顺序
│   └── health-check.schedule.json  # 健康检查定时任务参数
├── src/                            # 源代码主目录
│   ├── core/                       # 核心逻辑模块
│   │   ├── indexer.js              # 倒排索引构建与检索实现
│   │   ├── validator.js            # 链接格式校验与去重算法
│   │   └── cache.js                # LRU 缓存策略及过期管理
│   ├── http/                       # HTTP 服务层
│   │   ├── server.js               # 基于 Fastify 的服务启动与路由挂载
│   │   ├── routes/                 # 路由处理器
│   │   │   ├── search.js           # 全文检索接口
│   │   │   ├── resources.js        # 资源列表及详情接口
│   │   │   └── health.js           # 健康检查状态查询接口
│   │   └── middleware/             # 请求预处理中间件
│   │       ├── auth.js             # 基于 JWT 的轻量身份校验
│   │       └── logger.js           # 结构化访问日志记录
│   ├── scheduler/                  # 后台任务调度器
│   │   ├── worker.js               # 基于 node-cron 的周期性任务执行
│   │   └── checker.js              # 批量 HTTP 状态码探测与超时控制
│   └── utils/                      # 通用工具函数
│       ├── yaml-loader.js          # YAML 配置文件解析与 Schema 校验
│       └── time-helper.js          # 时区转换与时间戳格式化
├── tests/                          # 单元测试与集成测试
│   ├── unit/                       # 模块级单测（基于 Vitest）
│   └── integration/                # 端到端接口测试（基于 Supertest）
├── docs/                           # 完整项目文档（参见上方文档导航）
├── public/                         # 静态资源（CSS、前端 JavaScript、favicon）
├── .env.example                    # 环境变量模板（端口、JWT 密钥、日志级别）
├── package.json                    # 项目清单与脚本定义
├── pnpm-lock.yaml                  # 依赖锁定文件
└── README.md                       # 项目入口文档（即本文档）
```

## 贡献指南

1. **查阅问题列表与设计讨论**：访问 GitHub Issues 页面，筛选 `help wanted` 或 `good first issue` 标签，选择无指派的任务。在对应的 Issue 下回复认领意向，等待维护者确认以避免重复工作。

2. **派生仓库并创建功能分支**：将项目派生至个人账号下，克隆派生仓库后创建新分支，分支命名遵循 `feat/功能简述` 或 `fix/问题编号-简述` 格式。提交信息请使用 Conventional Commits 规范（如 `feat: add batch import endpoint`）。

3. **编写测试用例并确保通过**：所有新增功能或缺陷修复必须包含对应的单元测试或集成测试。运行 `pnpm run test:unit` 与 `pnpm run test:integration` 确保全部测试通过且覆盖率不低于 80%。

4. **更新相关文档与示例**：若修改了配置格式或 API 行为，需同步更新 `/docs` 目录下对应的手册以及 `/config` 中的示例配置文件。文档变更需与代码变更在同一 PR 中提交。

5. **提交 Pull Request 并参与评审**：将功能分支推送到派生仓库，向主仓库的 `main` 分支发起 Pull Request。PR 描述中需填写 Issue 编号、变更摘要、测试结果截图以及手动验证步骤。维护者会在 3 个工作日内进行评审，必要时会提出修改意见。

## 常见问题

**Q1: 如何添加自定义分类或调整资源展示顺序？**

所有分类和资源条目均定义在 `config/resources.yaml` 文件中。分类层级通过 `categories` 数组定义，每个分类可包含 `children` 子分类或 `items` 资源列表。展示顺序严格按照配置文件中的排列顺序渲染，如需调整，直接编辑该文件并重启服务（生产环境可使用热重载插件）。修改前建议备份原始文件。

**Q2: 健康检查任务报告了大量超时或连接拒绝，如何调整探测参数？**

默认健康检查超时时间为 5 秒，并发探测数为 10。若目标资源网络延迟较高或服务响应较慢，可编辑 `config/health-check.schedule.json` 文件中的 `timeout`（毫秒）和 `concurrency` 字段。同时支持配置 `retry` 次数，对于临时性网络抖动会自动重试。调整后调度器会在下一个周期（默认每日凌晨 3:00）应用新参数。

**Q3: 能否在不重启服务的情况下刷新资源列表？**

支持。项目内置了 `POST /api/reload` 管理接口，调用时需在请求头中携带管理员 JWT 令牌。该接口会重新读取 `resources.yaml` 并重建内存中的索引和缓存，无需终止服务进程。生产环境中建议通过 `SIGUSR2` 信号触发重载，避免将管理接口暴露在公网。

## 许可证

MIT License

Copyright (c) 2026 Vanguard Resource Gateway Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
