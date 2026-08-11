# RimeLink

RimeLink 是一个面向中文技术社区的开源外链资源聚合与管理项目。它并非一个传统的爬虫或采集系统，而是一个以人工精选与社区共建为核心的高质量技术导航与信息溯源平台。项目定位于帮助开发者、研究员及技术决策者快速定位特定领域（如全栈开发、云计算、开源硬件、AI 推理等）的权威一手资源，有效规避信息过载与低质内容干扰，将分散于网络各角落的优质外链进行结构化整理与语义化呈现。

RimeLink 本质上解决的是“资源确定性”问题。在技术迭代加速的今天，开发者经常面临以下困境：收藏夹无序、官方文档入口难以寻找、技术栈依赖链复杂、合规资源引用困难。RimeLink 通过严格的资源准入评审与版本化外链管理机制，为每个收录条目提供上下文描述、快照状态检测与关联场景标签，使之成为团队内部知识库的有效延伸，以及个人开发者构建第二大脑的基础数据管道。

## 功能概览

- **多级分类与标签体系**：每个资源条目支持自定义标签与层级目录归属，允许用户按技术栈、使用频率、合规状态进行多维度筛选，便于构建符合自身认知习惯的资源地图。

- **外链存活与状态监控**：系统定期对收录的域名与路径发起可用性探测，自动标记失效链接、内容变更警告及证书过期风险，确保资源列表的实时有效性。

- **一键快速导入与导出**：支持批量导入现有收藏夹文件（HTML 书签格式或 JSON 结构化数据），并可导出为标准 Markdown 列表、CSV 报告或 JSON API 格式，便于与其他工具链集成。

- **社区共建与审核流**：注册用户可提交新资源或更新已有资源描述，所有变更经过至少两名核心维护者的审核与讨论后方可合并，保证条目质量与描述准确性。

- **版本化变更日志**：每次对资源列表的增删改操作均生成变更记录，支持按时间、操作人、标签范围进行回溯，方便团队审计与责任追踪。

- **个性化视图与工作区**：用户可根据当前项目需求创建独立工作区，将特定资源加入工作区看板，并可添加个人备注、到期提醒与关联任务链接，提升资源复用效率。

- **RESTful API 与 Webhook 通知**：提供完整的只读与写入 API，支持第三方工具（如 CI/CD 流水线、监控机器人、内部 Wiki）订阅资源变更事件，实现自动化同步与通知。

## 应用场景

- **新项目技术选型调研**：当团队启动一个新微服务项目时，架构师可通过 RimeLink 快速检索“服务网格”、“可观测性”、“配置中心”等标签下的官方项目地址、基准测试报告与社区最佳实践案例，大幅缩短调研周期。

- **内部知识库资源锚点管理**：企业技术文档中往往需要引用大量外部标准、规范与依赖库。使用 RimeLink 作为统一资源锚点库，可确保文档内的超链接长期有效，避免因外部页面移动或下线导致文档失效。

- **开源社区贡献者入门引导**：开源项目维护者可将 RimeLink 作为新手引导页的资源后盾，集中列出代码仓库、贡献指南、编码风格规范、CI 状态看板及社区交流渠道，降低新贡献者的参与门槛。

- **合规审计与依赖溯源**：安全合规团队需要对项目所引用的所有第三方库、在线服务及数据源进行登记与版本追踪。RimeLink 的外链版本化与快照描述功能可提供可靠的引用记录，满足内部审计与外部合规检查要求。

## 快速开始

以下步骤帮助您在本地环境快速启动 RimeLink 实例，并导入示例资源数据。

```bash
# 1. 克隆项目代码仓库
git clone https://github.com/rimelink/core.git rimelink-core
cd rimelink-core

# 2. 安装项目依赖（使用 pnpm，也支持 npm 或 yarn）
pnpm install

# 3. 配置环境变量，复制示例配置并修改数据库连接信息
cp .env.example .env

# 4. 执行数据库迁移与初始数据填充
pnpm run migrate
pnpm run seed

# 5. 启动开发服务器（默认监听端口 3000）
pnpm run dev
```

访问 `http://localhost:3000` 即可进入本地实例的仪表盘，开始浏览、搜索和管理资源条目。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 项目运行时环境，推荐使用最新的 LTS 版本以获取长期安全更新 |
| PostgreSQL | 14.x 或更高 | 主数据存储库，用于存储资源条目、用户信息、变更日志及工作区数据 |
| Redis | 7.x 或更高 | 缓存与会话存储层，用于提升高频查询性能及 Webhook 任务队列管理 |
| pnpm | 8.x 或更高 | 包管理与任务编排工具，确保依赖安装的一致性与快速性 |
| Docker / Docker Compose | 20.x 或更高 | 可选依赖，用于快速启动本地开发所需的 Postgres 与 Redis 容器环境 |
| Git | 2.30 或更高 | 用于版本控制及贡献流程中的分支管理与提交签名验证 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | `/docs/user-guide/` | 如何注册账号、创建工作区、添加资源、使用标签筛选以及配置个人通知偏好 |
| 管理员手册 | `/docs/admin-handbook/` | 如何审核提交、配置站点元数据、管理用户权限以及调整系统监控阈值 |
| 贡献者指引 | `/docs/contributing/` | 如何提交新资源、更新现有描述、编写单元测试及遵循代码提交规范 |
| API 参考 | `/docs/api-reference/` | 所有对外 RESTful 接口的请求/响应结构、鉴权方式、分页参数与错误码定义 |
| 部署运维 | `/docs/deployment/` | 生产环境容器化部署方案、反向代理配置、SSL 证书自动续期及备份恢复策略 |
| 设计文档 | `/docs/design/` | 系统整体架构图、数据模型 ER 图、缓存更新策略及扩展性设计考量 |

## 资源列表

以下为 RimeLink 项目初始收录的部分精选外链资源，按类别分组展示。所有链接均保持原始格式原样输出，未做任何协议或域名修改。

### 中文高清视频资源类

- <code>guochangaoqingshipinzaixian.org.cn</code>
- <code>guochangaoqingshipinguankan.org.cn</code>
- <code>rimanzaixianmianfeiguankan.org.cn</code>

### 中文字幕与在线播放类

- <code>zhongwenzimumianfeibofang.org.cn</code>
- <code>zaixianzimumianfeiguankan.org.cn</code>
- <code>zaixianzimuguankanmianfei.org.cn</code>
- <code>zaixianzimugaoqingdianshiju.org.cn</code>

### 综合免费视频网站类

- <code>mianfeishipinwangzhanzaixianguankan.org.cn</code>

### 特定语言及地区视频类

- <code>rihanzaixianmianfeishipinw.org.cn</code>
- <code>oumeizaixianmianfeishipinw.org.cn</code>

## 项目结构

```
rimelink-core/
├── apps/                                   # 应用程序层
│   ├── web/                                # 主 Web 应用（Next.js 仪表盘与公共页面）
│   │   ├── src/                            # 页面组件、布局与路由处理
│   │   └── public/                         # 静态资源（favicon、站点图标、字体文件）
│   └── api/                                # 独立的 RESTful API 服务（Fastify 实现）
│       ├── routes/                         # 按领域划分的路由定义（resources, users, workspaces）
│       └── middleware/                     # 鉴权、日志、限流及错误处理中间件
├── packages/                               # 共享包与核心库
│   ├── core/                               # 领域模型、业务逻辑与数据访问抽象层
│   │   ├── entities/                       # TypeORM 实体定义（Resource, Tag, ChangeLog, User）
│   │   └── services/                       # 资源监控服务、审核流引擎、搜索索引服务
│   ├── utils/                              # 通用工具函数（URL 规范化、时间处理、加密哈希）
│   └── types/                              # 全局 TypeScript 类型声明与 Zod 校验模式
├── scripts/                                # 运维与开发辅助脚本
│   ├── seed/                               # 种子数据生成器（用于填充开发数据库）
│   └── health/                             # 外链存活探测与状态上报脚本
├── tests/                                  # 测试套件
│   ├── unit/                               # 单元测试（Jest + 模拟依赖）
│   └── e2e/                                # 端到端测试（Playwright 覆盖关键用户路径）
├── configs/                                # 配置文件集中管理
│   ├── eslint/                             # ESLint 规则集与插件配置
│   └── prettier/                           # 代码格式化统一规则
├── docker-compose.yml                      # 本地开发服务编排（Postgres + Redis + MinIO）
├── Dockerfile                              # 生产环境多阶段构建镜像定义
├── .env.example                            # 环境变量模板（含数据库连接、JWT 密钥、邮件服务）
├── package.json                            # 根项目依赖定义与工作空间配置
└── README.md                               # 项目总览与入口文档（即本文档）
```

## 贡献指南

我们欢迎并鼓励社区成员以多种形式参与贡献，包括但不限于提交新资源、修复文档错误、提出功能建议或完善测试用例。请遵循以下步骤开始您的贡献旅程：

1. **查阅贡献者行为准则**：在提交任何贡献前，请阅读并同意《贡献者公约》中关于尊重、包容与专业协作的约定。所有参与者均需遵守此准则以维护社区健康。

2. **认领或提交 Issue**：访问 GitHub Issues 页面，查看当前待解决的问题列表。如果您发现了新的问题或希望增加新资源条目，请先创建一个 Issue 详细描述您的建议，并与维护者讨论可行性。

3. **创建功能分支**：从主分支 `main` 切出新的分支，命名格式为 `feature/资源名称-简述` 或 `fix/问题编号-简述`。请确保分支名称清晰反映变更内容。

4. **编写变更并自测**：在本地完成代码或文档修改后，请运行完整的测试套件（`pnpm run test`）以确保未引入回归错误。若涉及新资源添加，请附带资源有效性验证说明。

5. **提交拉取请求**：推送您的分支到远程仓库，并创建 Pull Request。在 PR 描述中请清晰列出变更点、关联 Issue 编号以及测试覆盖情况。至少两名核心维护者将审阅您的提交，并在必要时请求修改。合并后您的贡献将出现在贡献者名单中。

## 常见问题

**问：RimeLink 是否会主动抓取或缓存收录链接的内容？**

答：不会。RimeLink 仅存储外链的元数据（标题、描述、标签、分类及状态），不存储或代理任何目标页面内容。系统进行的存活探测仅发送 HTTP HEAD 请求以验证可访问性，不解析或下载正文数据。所有内容版权归属原始站点，本项目不承担任何内容审查或分发责任。

**问：如何确保收录资源的合规性与安全性？**

答：每个资源条目在首次收录及每次更新时均需经过人工审核，审核者将依据项目内容政策（禁止包含恶意软件、钓鱼页面、侵权内容或明显违反中国法律法规的站点）进行评判。此外，系统会定期对收录域名进行安全信誉库比对，发现风险条目将自动标记并通知管理员复核。用户也可通过举报功能反馈疑似问题资源。

**问：能否将 RimeLink 部署到内网环境或离线环境？**

答：支持。项目所有依赖包均可通过私有 npm 镜像或本地缓存方式在内网安装。数据库与缓存组件均可使用内网自建实例。离线环境下，外链存活监控与 Webhook 通知功能将受限于网络可达性，但核心的资源管理与检索功能可正常运行。建议在内网部署时关闭公网探测任务，或替换为内网专有探测端点。

## 许可证

MIT License

Copyright (c) 2026 RimeLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
