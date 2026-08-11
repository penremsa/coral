# CloudLink 技术资源导航平台

CloudLink 是一个面向开发者和技术团队的高质量外链资源聚合与导航系统，专注于收录和分类整理互联网上分散的技术文档、数据服务、工具平台与社区资源。项目定位为技术基础设施的外围辅助层，帮助用户从海量信息中快速定位可用、稳定、低延迟的第三方服务与数据接口，减少重复查找成本，提升研发与运维效率。目标用户包括独立开发者、中小型技术团队、运维工程师以及数据采集与分析从业者。

项目本身不生产数据，也不存储任何第三方内容，仅提供结构化外链索引与基础可用性检测。核心设计理念是轻量、只读、可扩展，支持通过 JSON 配置文件新增或禁用资源条目，适合作为团队内部导航页的基础框架或云函数版静态站的数据源。

## 功能概览

- **按领域分类的资源索引**：系统内置 10 个以上技术子分类（如数据服务、监控告警、文档站、社区论坛、开源镜像、API 网关等），每个分类下聚合 5 至 20 条高质量外链，并记录每条链接的响应状态与更新时间。
- **一键可达的快速导航**：首页提供热门资源快捷入口，支持键盘快捷键（如 Ctrl+Shift+F 聚焦搜索框）和鼠标侧键后退，减少页面跳转时的操作成本。
- **可配置的健康检查轮询**：后台定时任务（默认每 6 小时）对收录的所有外链发起 HEAD 请求，自动标记不可用或响应过慢的链接，并在前端用状态色块提示用户。
- **全文检索与标签过滤**：支持按资源名称、域名、标签（如 "低延迟"、"国内加速"、"免费额度"）进行多维度筛选，检索结果按匹配度与历史点击率排序。
- **自定义资源分组**：用户可在本地配置文件中新增分组或调整现有分组顺序，无需修改核心代码即可完成个性化定制，适合团队内部分享。
- **访问统计与热点排行**：基于内存计数统计各资源的点击次数，按日、周、月三个时间窗口生成热点 Top 10 榜单，帮助团队识别常用服务。
- **响应式布局与移动端适配**：前端采用 Flexbox + Grid 布局，在手机、平板、桌面设备上均保持可读性与可操作性，导航栏自动折叠。
- **OpenAPI 规范的外链数据接口**：提供 `/api/v1/links` 和 `/api/v1/status` 两个只读 JSON 接口，方便其他系统或监控脚本批量拉取资源列表与健康状态。

## 应用场景

- **新成员入职环境搭建**：团队新加入的开发人员可通过 CloudLink 快速找到内部文档站、代码仓库镜像、依赖包代理仓库和日志查询平台，无需反复向老员工询问地址，将环境准备时间从平均 2 小时压缩至 20 分钟以内。
- **数据采集与爬虫任务辅助**：数据工程师在进行公开数据抓取时，需要频繁查询比分、赛果、实时统计等外部数据源。CloudLink 预先收录了多个相关数据接口域名，并提供可用性标记，帮助工程师优先选择当前稳定的服务端点，减少采集任务中的连接超时失败。
- **运维故障排查快速通道**：当线上服务出现异常时，运维人员需要同时查看监控面板、日志系统、告警历史、云服务商状态页等多个外部系统。CloudLink 将这些关键入口集中在同一页面，配合状态指示灯，可快速判断是本地网络问题还是第三方服务故障。
- **技术培训与分享会资料站**：技术团队内部举办培训或分享活动时，讲师可将参考文档、在线工具、API 测试平台等外链统一收录至一个临时分组，参会者通过一个 URL 即可获得全部资料列表，避免口头传递或零散聊天记录导致的遗漏。

## 快速开始

以下命令适用于 Linux / macOS / Windows（WSL 或 Git Bash）环境，要求已安装 Git 和 Node.js 18+。

```bash
# 克隆项目仓库
git clone https://github.com/cloudlink-io/cloudlink-navigator.git

# 进入项目目录
cd cloudlink-navigator

# 安装依赖（使用 npm 或 yarn）
npm install

# 启动开发服务（默认监听 3000 端口）
npm run dev
```

启动成功后，在浏览器中访问 `http://localhost:3000` 即可看到本地导航首页。如需构建生产版本并静态部署，执行 `npm run build` 后，将 `dist` 目录内容上传至任意静态托管服务（如 Nginx、CDN、对象存储）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 8.x 或 9.x | 包管理器，用于安装依赖及运行脚本命令 |
| Git | 2.25 及以上 | 版本控制工具，用于克隆仓库和管理补丁 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 前端运行时支持 ES2020 和 CSS Grid 特性 |
| 磁盘空间 | 至少 50 MB | 包含源代码、node_modules 及构建产物（按需） |
| 网络访问 | 外网可访问性 | 用于首次安装时下载 npm 包及健康检查轮询外部域名 |
| 操作系统 | Linux / macOS / Windows 10+ | 跨平台支持，Windows 下建议使用 WSL 或 PowerShell 7 |

## 文档导航

| 层面 | 目录 / 文档 | 回答的问题 |
|------|------------|-----------|
| 用户手册 | `docs/user-guide/quick-start.md` | 如何使用首页搜索、如何添加个人书签、如何切换分类视图 |
| 配置参考 | `docs/config/schema.md` | 外链配置文件的字段含义、数据类型、可选参数及示例 |
| 运维指南 | `docs/ops/health-check.md` | 健康检查轮询机制、超时阈值调整方法、告警通知集成方式 |
| 开发者文档 | `docs/developer/api-design.md` | 内部 API 设计思路、数据流转路径、单元测试编写规范 |
| 部署手册 | `docs/deployment/static-hosting.md` | 支持 Vercel / Netlify / 阿里云 OSS / 自建 Nginx 的详细部署步骤 |
| 常见问题 | `docs/faq/troubleshooting.md` | 依赖安装失败、跨域请求被拦截、页面加载空白等常见错误处理 |

## 资源列表

### 数据服务类（赛事比分与实时统计）

- <code>500jingcaizuqiusaichengjieguo.org.cn</code>
- <code>500zucaiwanzhengjishibifen.org.cn</code>
- <code>500zucaibifen.org.cn</code>
- <code>500zucaiwanzhengbifen.org.cn</code>
- <code>bifenzaixian.net.cn</code>
- <code>zuqiujishibifenjingcai.net.cn</code>
- <code>zuqiujishibifenwanzhengban.net.cn</code>
- <code>zuqiujishibifenjingcai.org.cn</code>
- <code>zuqiubifenjishibifen.org.cn</code>
- <code>zuqiujishibifenshoujiban.org.cn</code>

## 项目结构

```
cloudlink-navigator/
├── src/                           # 前端源码主目录
│   ├── assets/                    # 静态资源（图标、字体、默认占位图）
│   ├── components/                # Vue / React 风格的可复用 UI 组件
│   │   ├── LinkCard.vue          # 单个资源卡片，展示名称、描述、标签与状态灯
│   │   ├── SearchBar.vue         # 带自动补全建议的搜索输入框
│   │   └── StatusBadge.vue       # 显示链接可用/慢速/不可用三种状态
│   ├── layouts/                   # 整体布局模板（含头部导航、侧边栏、底部）
│   ├── pages/                     # 路由对应的页面视图（首页、分类页、关于页）
│   ├── store/                     # 状态管理（Pinia / Redux），存储链接列表与过滤条件
│   ├── utils/                     # 工具函数：域名解析、时间格式化、防抖节流
│   └── config/                    # 默认外链分组与标签的 JSON 配置（可被用户覆盖）
├── server/                        # 轻量后端服务（Express / Fastify）
│   ├── routes/                    # API 路由定义（/api/v1/links, /api/v1/status）
│   ├── services/                  # 健康检查调度器、缓存更新服务
│   └── worker/                    # 定时任务脚本（cron 式轮询）
├── docs/                          # 完整文档目录（覆盖用户、运维、开发三方面）
│   ├── user-guide/                # 面向普通使用者的操作指南
│   ├── ops/                       # 面向运维人员的部署与监控文档
│   └── developer/                 # 面向贡献者的架构说明与 PR 规范
├── tests/                         # 单元测试与集成测试（Jest / Vitest）
│   ├── unit/                      # 组件与工具函数的独立测试
│   └── e2e/                       # 端到端场景测试（Playwright）
├── scripts/                       # 构建辅助脚本（版本号更新、配置文件校验）
├── .github/                       # GitHub 社区模板（Issue 模板、PR 模板）
│   └── workflows/                 # CI 流水线（自动化测试 + 构建预览）
├── package.json                   # 项目依赖与脚本命令定义
├── vite.config.js                 # 构建工具配置（别名、代理、压缩）
└── README.md                      # 项目入口文档（即本文档）
```

## 贡献指南

1. 在 GitHub 仓库页面点击 `Fork` 按钮，将项目复制到个人账号下，然后使用 `git clone` 拉取到本地，并关联上游仓库以便后续同步更新。
2. 创建新的功能分支，分支名称应遵循 `feature/简短描述` 或 `fix/问题编号` 格式，例如 `feature/add-cache-layer`，避免直接在 `main` 分支上修改。
3. 在本地完成代码或文档修改后，运行 `npm run test` 确保所有现有测试通过，若新增功能需补充对应的单元测试或文档说明。
4. 提交变更时使用常规提交信息格式（`<type>: <subject>`），例如 `feat: 增加分组拖拽排序功能` 或 `docs: 更新部署手册中的环境变量列表`。
5. 推送分支到个人远程仓库，然后通过 GitHub 页面发起 Pull Request，描述中需说明变更目的、影响范围以及测试情况，等待项目维护者审核。

## 常见问题

**问：健康检查显示某个链接不可用，但我手动访问却是正常的，是什么原因？**

答：健康检查默认使用 HEAD 请求，且超时时间设置为 3 秒。部分服务端可能不支持 HEAD 方法，或对非浏览器 UA 有访问限制，导致误判为不可用。您可以在 `server/config/check.js` 中调整 `timeout` 参数，或将该链接的 `checkMethod` 配置项改为 `GET`。同时，健康检查不会跟随重定向（默认 `redirect: 'manual'`），若服务端返回 3xx 状态码也会被标记为异常，您可以根据实际情况启用 `followRedirect` 选项。

**问：如何在本地添加自己常用的内部资源，而不影响团队公共配置？**

答：项目支持用户级覆盖配置。您在 `src/config/user-links.json` 文件中添加自定义分组与链接列表，该文件默认被 `.gitignore` 忽略，不会提交到版本库。系统启动时会自动合并默认配置与用户配置，用户配置中的条目优先级更高，相同 id 的条目会覆盖默认值。如果您的团队使用私有部署，建议将团队公共配置放在 `src/config/team-links.json` 并通过环境变量 `CLOUDLINK_ENV=team` 激活。

**问：部署到生产环境后，页面刷新出现 404 错误，如何解决？**

答：这是因为项目使用 History 模式的前端路由，而您的静态服务器未正确配置回退规则。若使用 Nginx，请在配置文件中添加 `try_files $uri $uri/ /index.html;`；若使用 Vercel 或 Netlify，平台通常会自动处理，但需确保根目录存在 `_redirects` 或 `vercel.json` 文件并包含相应重写规则。具体配置示例可参考项目 `docs/deployment/static-hosting.md` 中的对应章节。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:24
