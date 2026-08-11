# NexusIndex

NexusIndex 是一个轻量级、可自托管的网络资源导航与分类汇总平台，面向技术社区运营者、个人知识管理者以及小型团队内部信息中枢建设需求。项目定位为“外链资源的结构化治理工具”，旨在解决大量分散网络链接难以组织、难以追溯、难以共享的问题。NexusIndex 不提供内容存储，不进行数据抓取，仅以确定性方式对用户输入的 URL 进行归类和展示，确保资源引用的透明性与可维护性。项目适用于需要高频维护外部参考链接的技术文档库、项目手册、内部知识库及社区资源推荐页。

## 功能概览

- **多级分类目录系统**：支持用户自定义一级及二级分类，每个资源条目可归属多个分类标签，便于多维度检索。
- **原始 URL 严格保真存储**：系统对用户提交的每一个链接进行原样保存，不自动补全协议、不修改域名大小写、不添加或移除尾部斜杠，确保地址的精确可复现性。
- **Markdown 原生渲染视图**：所有资源列表以 Markdown 表格和列表形式呈现，与 README、文档站点、GitHub 项目页无缝集成。
- **批次化资源管理**：内置批次导入功能，支持按批次编号（如第 281/455 批）对链接进行分组管理，便于追溯资源引入时间与来源。
- **快速模糊搜索**：基于标题、分类、标签和 URL 片段的轻量级全文检索，支持中英文混合查询。
- **静态站点生成模式**：提供构建命令，可将当前资源库一键导出为纯静态 HTML 文件，适合部署于 Nginx、GitHub Pages 或对象存储服务。
- **权限分级占位**：预留管理员与普通编辑者角色接口，支持后续接入 OAuth 或基础 HTTP 认证，适合团队协作维护。

## 应用场景

- **技术文档外链附录管理**：项目维护者在编写用户手册或 API 文档时，需引用大量外部规范、SDK 下载页、社区讨论帖。NexusIndex 可作为独立附录模块，保持文档正文简洁，同时确保所有外链可集中校验和更新。
- **社区优质资源周报**：开源社区运营人员可每周导入一批精选链接（如本批 10 个资源），通过分类标签整理为“推荐阅读”“视频教程”“官方公告”等分区，生成周报页面供社区成员订阅。
- **个人知识库外部参考索引**：研究员或工程师在构建个人知识笔记时，常需要记录参考文章链接。NexusIndex 提供轻量化索引层，避免笔记正文被长链接污染，同时支持按项目或主题快速筛选。
- **内部团队技术选型记录**：团队进行技术方案对比时，可将各候选方案的官网、性能测试报告、Issue 讨论帖等链接统一录入，附加备注字段记录评估结论，形成可追溯的选型档案。
- **多版本资源对照表**：当同一资源存在多个镜像站、旧版存档、不同语言入口时，可将其归入同一分组，通过 URL 原样展示区分各入口，方便用户按需选择。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，要求已安装 Git 和 Node.js（v18 及以上）。

```bash
# 1. 克隆项目仓库
git clone https://github.com/nexus-index/nexusindex.git
cd nexusindex

# 2. 安装依赖
npm install

# 3. 启动开发服务
npm run dev
```

执行成功后，访问控制台输出的本地地址（默认为 http://localhost:5173 ）即可进入资源管理界面。首次启动会自动生成示例数据，您可随后清空并导入自己的链接批次。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建与服务脚本 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 用于克隆仓库及版本控制 |
| 操作系统 | Linux / macOS / Windows（WSL2 推荐） | 开发与部署均可跨平台，Windows 原生 PowerShell 可能存在路径兼容问题，建议使用 WSL |
| 浏览器 | 支持 ES2022 的现代浏览器（Chrome 110+ / Firefox 110+ / Edge 110+） | 仅管理界面需要浏览器访问，静态输出产物无浏览器版本限制 |
| 可选：Nginx / Apache | 任意稳定版本 | 用于部署静态导出产物，非运行必需 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide.md | 如何添加、编辑、删除资源条目；如何创建分类与标签；如何导入批次数据；如何切换视图模式。 |
| 管理员指南 | /docs/admin-guide.md | 如何配置权限验证；如何调整分类层级上限；如何备份与恢复资源数据库（JSON 文件）；如何迁移数据到新实例。 |
| 静态导出部署 | /docs/deployment.md | 如何将当前资源库导出为纯静态 HTML；如何配置 basePath 以适配子目录部署；如何使用 GitHub Actions 自动化构建发布。 |
| API 参考 | /docs/api-reference.md | 提供内部数据读写接口的请求/响应格式说明，包括资源增删改查、批次管理、分类树查询等，便于二次开发或集成到其他前端。 |

## 资源列表

### 本批资源（第 281/455 批）

<code>henhenjiujiu.org.cn</code>

<code>wuyedaxiangjiao.org.cn</code>

<code>fengmanrenqi.org.cn</code>

<code>jiujiushaofu.org.cn</code>

<code>rihanguochanoumei.org.cn</code>

<code>daxiangyiren.org.cn</code>

<code>oumeiguochanjingpin.org.cn</code>

<code>yiquerqubuka.org.cn</code>

<code>ribenbukayiquerqu.org.cn</code>

<code>tingtingyiquerqu.org.cn</code>

## 项目结构

```
nexusindex/
├── src/                           # 源代码主目录
│   ├── core/                      # 核心数据模型与业务逻辑
│   │   ├── resource.model.js      # 资源条目实体定义（含 URL 保真规则）
│   │   ├── batch.service.js       # 批次导入、查询与分组逻辑
│   │   └── category.tree.js       # 分类树构建与层级维护
│   ├── routes/                    # HTTP 路由层（开发服务与 API）
│   │   ├── resource.routes.js     # 资源增删改查端点
│   │   └── export.routes.js       # 静态导出触发与下载端点
│   ├── render/                    # 渲染引擎相关
│   │   ├── markdown.builder.js    # 将资源数据转换为 Markdown 表格/列表
│   │   └── html.generator.js      # 基于模板生成静态 HTML 页面
│   └── utils/                     # 工具函数集合
│       ├── url.validator.js       # URL 格式校验（不修改原始输入）
│       └── batch.parser.js        # 批量文本解析器（支持按行或按逗号分隔）
├── data/                          # 数据存储目录（默认 JSON 文件）
│   ├── resources.json             # 所有资源条目的持久化存储
│   └── categories.json            # 分类与标签定义
├── static/                        # 静态资源输出目录（导出产物存放位置）
│   └── index.html                 # 导出的默认首页
├── docs/                          # 项目文档（用户手册、管理员指南等）
│   ├── user-guide.md
│   ├── admin-guide.md
│   ├── deployment.md
│   └── api-reference.md
├── tests/                         # 单元测试与集成测试脚本
│   ├── resource.model.test.js
│   └── url.validator.test.js
├── config/                        # 环境配置文件
│   ├── default.json               # 默认端口、数据路径、分类默认值
│   └── production.json            # 生产环境覆盖配置
├── .github/                       # GitHub 社区配置
│   └── workflows/                 # CI 工作流（自动构建与静态导出）
├── package.json                   # 项目依赖与脚本定义
├── README.md                      # 项目介绍与快速入口（即本文档）
└── LICENSE                        # MIT 许可证文件
```

## 贡献指南

1.  **查阅现有 Issue 与 Projects**：访问 GitHub 仓库的 Issues 和 Projects 看板，确认您要修复的问题或要新增的功能未被他人认领。如无对应议题，请先创建一个新 Issue 描述您的修改意图。
2.  **派生仓库并创建功能分支**：将主仓库派生到您个人的 GitHub 账户下，然后基于 `main` 分支创建新的功能分支，分支命名建议使用 `feature/功能简述` 或 `fix/问题简述`。
3.  **编写或修改代码，并补充单元测试**：针对新增功能或修复，请在 `tests/` 目录下补充对应的测试用例，确保所有现有测试通过（运行 `npm test`）。对于涉及 URL 处理的变更，必须覆盖边缘情况（如裸域名、带端口、带验证信息的链接）。
4.  **更新相关文档**：若您的变更影响用户操作方式或配置项，请同步更新 `/docs` 下对应的手册以及本 README 中的功能概览或安装要求部分。文档变更与代码变更需在同一个 Pull Request 中提交。
5.  **提交 Pull Request 并等待审核**：推送您的分支到派生仓库，然后向主仓库的 `main` 分支发起 Pull Request。请在 PR 描述中清晰关联对应的 Issue 编号，并简述测试结果。核心维护者将在 3 个工作日内进行审核或提出修改意见。

## 常见问题

**Q：我提交的 URL 中包含大写字母或混合大小写，系统会自动转小写吗？**

A：不会。NexusIndex 对原始 URL 执行严格的保真存储策略。系统不会对域名部分进行大小写转换，也不会对协议或路径部分做任何修改。搜索功能会忽略大小写进行匹配，但展示和导出时始终使用您最初输入的形式。这一设计确保了与大小写敏感的服务器或 CDN 地址的兼容性。

**Q：静态导出模式是否支持完全离线浏览？**

A：导出的静态 HTML 页面本身不依赖任何外部网络资源（如 CDN 脚本、字体库），所有样式和交互脚本均内联在单文件中。但页面中的资源链接（即您录入的 URL）仍然指向外部站点，点击后需要用户的设备具备访问这些站点的网络能力。NexusIndex 本身不缓存或代理外部内容。

**Q：如何将现有数据迁移到新部署的实例？**

A：您可以直接复制 `data/` 目录下的 `resources.json` 和 `categories.json` 文件到新实例的相同相对路径下，然后重启服务。两个 JSON 文件采用纯文本格式，兼容跨平台复制。若新实例使用不同数据存储后端（如 PostgreSQL），请参考 `/docs/admin-guide.md` 中的迁移脚本说明，使用内置的 `npm run migrate` 命令进行数据转换。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:28
