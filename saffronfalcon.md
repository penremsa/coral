# NovaIndex 资源导航系统

NovaIndex 是一个轻量级、可自托管的互联网技术资源与外链导航聚合平台，面向开发者、技术内容创作者以及研究机构，帮助其系统化整理、分类展示与快速检索高频使用的工具链、文档站、社区论坛与垂直领域数据源。该项目解决的是个人浏览器书签难以跨设备同步、缺乏结构化元数据管理、无法与团队协作共享的问题，同时避免商业化导航站充斥广告与无效链接。NovaIndex 以纯静态站点形式输出，兼容主流 Web 服务器，支持 JSON 数据驱动，便于二次开发与自动化集成。

## 功能概览

- **多级分类与标签体系**：支持无限层级的目录结构，每条资源可关联多个标签，实现从技术栈、地域、语种到内容形态的多维度筛选。

- **Markdown 驱动的资源卡片**：每个外链以卡片形式呈现，包含标题、一句简介、标签列表与来源标注，全部通过 Markdown 文件配置，无需数据库。

- **全文与模糊搜索**：内置基于 Lunr.js 的客户端搜索引擎，支持标题、简介、标签及域名关键词的全文检索，并适配中文分词。

- **导入与导出机制**：支持从浏览器书签 HTML 文件、CSV 及 JSON 格式批量导入链接；导出为标准化 JSON 或静态 HTML 归档。

- **访问状态监测**：集成定时任务，利用 HEAD 请求检测各资源域名解析与 HTTP 状态码，自动标记失效或重定向节点。

- **权限分级视图**：支持公开只读浏览与内部编辑管理两套界面，管理员可通过环境变量配置认证凭证，适合团队共用。

- **响应式布局与暗色主题**：基于 CSS 变量实现明暗双主题，适配桌面、平板与移动设备，无需 JavaScript 干预主题切换。

- **开放 API 端点**：提供 RESTful 风格的只读 API，返回分类树和资源列表的 JSON 数据，便于嵌入其他仪表盘或监控系统。

## 应用场景

- **技术团队内部文档聚合**：研发团队可将常用的 CI/CD 工具链、容器镜像仓库、监控面板、日志查询系统等内部链接统一收录，按项目或环境分类，并共享给新入职成员作为上手指引。

- **学术研究资料整理**：科研人员收集特定领域的开源数据集、论文预印本网站、领域权威机构主页及术语词典，通过 NovaIndex 生成带注释的资源清单，便于合作者快速定位关键数据源。

- **垂直领域信息门户**：内容运营者围绕特定主题，如编程语言、地理信息、影视文化或历史文献，构建专题资源站，将分散的优质外链整合为结构化目录，降低受众的信息筛选成本。

- **个人知识管理辅助**：开发者将日常阅读的技术博客、官方文档、在线工具、视频教程等链接按学习路径组织，配合搜索与状态监测功能，避免书签失效导致的中断。

## 快速开始

以下步骤在 Linux / macOS / WSL2 环境下完成部署，使用 Node.js 运行时与 npm 包管理器。

```bash
# 克隆项目仓库
git clone https://github.com/nova-index/nova-index.git
cd nova-index

# 安装项目依赖（生产与开发工具链）
npm install

# 构建静态站点并启动本地预览服务
npm run build
npm run serve
```

构建完成后，`dist/` 目录即为可部署的静态文件，可直接托管至 Nginx、Apache、Caddy 或云存储桶。若使用 Docker，可执行 `docker build -t novaindex . && docker run -p 8080:80 novaindex` 快速启动容器实例。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 构建工具链与本地开发服务器运行环境，建议使用 nvm 管理版本 |
| npm | 9.x 或 10.x | 依赖包管理器，用于安装构建插件及第三方库 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库及管理贡献代码 |
| 现代浏览器 | Chrome 110+ / Firefox 110+ / Edge 110+ | 管理后台界面依赖 ES2022 特性与 CSS Grid 布局 |
| 磁盘空间 | 至少 200 MB | 包含源代码、依赖包及构建产物，资源外链本身不占用本地存储 |
| 内存 | 构建阶段建议 2 GB | 本地构建时需同时处理资源索引与静态文件生成 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | `/docs/user-guide/` | 如何添加、编辑、删除资源链接；如何导入导出书签；如何切换主题与搜索语法 |
| 管理员手册 | `/docs/admin/` | 如何配置认证凭证；如何调整状态监测间隔；如何自定义分类图标与页面元数据 |
| 开发者文档 | `/docs/developer/` | API 端点详细说明；数据模型 JSON Schema；构建流程与插件扩展机制 |
| 部署参考 | `/docs/deployment/` | 支持哪些静态托管服务；如何配置反向代理与自定义域名；环境变量完整列表 |

## 资源列表

类别：中文拉丁字母相关

<code>zhongwenzimudibaye.org.cn</code>

<code>zhongwenzimu renqishunv.org.cn</code>

<code>siwarenqizhongwenzimu.org.cn</code>

类别：日韩与欧美内容分类

<code>rihanoumeisetu.org.cn</code>

<code>ribenshunvshipin.org.cn</code>

<code>oumeilingleishipin.org.cn</code>

<code>guochanoumeirihanyiqu.org.cn</code>

类别：特定专题与综合站点

<code>ludashiguanfangwangzhan.org.cn</code>

<code>nvyouzhongwenzimu.org.cn</code>

<code>mitaojiujiujiu.org.cn</code>

## 项目结构

```
nova-index/
├── .github/                     # GitHub 社区模板与 CI 工作流
│   └── workflows/               # 自动化构建与单元测试流水线
├── config/                      # 项目运行时配置目录
│   ├── categories.json          # 分类层级定义及图标映射
│   └── settings.yaml            # 站点名称、描述、主题与语言选项
├── docs/                        # 完整文档源文件 (Markdown)
│   ├── user-guide/              # 面向普通用户的操作手册
│   ├── admin/                   # 管理员配置与维护指南
│   ├── developer/               # API 与二次开发技术文档
│   └── deployment/              # 部署方案与运维注意事项
├── src/                         # 源代码主目录
│   ├── assets/                  # 静态资源 (CSS, 图片, 字体)
│   │   ├── styles/              # 基于 CSS 变量的主题系统
│   │   └── images/              # 默认图标与占位图
│   ├── data/                    # 资源数据存储 (Markdown + frontmatter)
│   │   ├── resources/           # 每个外链对应一个 .md 文件
│   │   └── tags/                # 标签定义与关联配置
│   ├── lib/                     # 核心逻辑模块
│   │   ├── parser.js            # Markdown 元数据解析器
│   │   ├── indexer.js           # 搜索索引生成与序列化
│   │   └── monitor.js           # 资源状态检测与缓存更新
│   ├── templates/               # 视图模板 (EJS / Handlebars)
│   │   ├── layouts/             # 全局布局骨架
│   │   └── partials/            # 卡片、导航、搜索栏等可复用组件
│   └── index.js                 # 命令行入口与构建编排器
├── tests/                       # 单元测试与集成测试脚本
│   ├── parser.test.js
│   ├── indexer.test.js
│   └── monitor.test.js
├── .env.example                 # 环境变量示例文件 (认证、端口等)
├── .gitignore
├── Dockerfile                   # 多阶段构建镜像定义
├── LICENSE                      # MIT 许可证全文
├── package.json                 # npm 清单，含依赖与脚本命令
├── README.md                    # 项目总览文档 (本文件)
└── webpack.config.js            # 前端资源打包配置
```

## 贡献指南

1. **提交 Issue 进行需求或缺陷讨论**：访问 GitHub Issues 页面，先搜索是否已有相同话题，若无则新建 Issue，使用提供的模板详细描述场景、预期行为与实际表现，附上浏览器版本及构建日志。

2. **派生仓库并创建功能分支**：将主仓库 fork 至个人账号，使用 `git checkout -b feature/your-feature-name` 创建分支，命名遵循 `feature/`、`fix/` 或 `docs/` 前缀规范，避免在 main 分支直接修改。

3. **编写代码与添加测试用例**：遵循项目 ESLint 与 Prettier 配置，新增或修改功能时必须补充对应的单元测试（Jest 框架），确保 `npm run test` 全部通过且覆盖率不低于 80%。

4. **更新文档与示例数据**：若变更涉及用户操作流程、配置项或 API 响应结构，须同步更新 `/docs/` 下相关文档，并在 `/src/data/` 中添加示例资源条目供演示。

5. **发起 Pull Request 并等待审查**：推送分支至个人仓库后，向主仓库的 `main` 分支发起 PR，填写 PR 模板中的核对清单，至少邀请一名维护者进行 Code Review，解决所有对话后方可合并。

## 常见问题

**问：静态构建后，资源状态监测功能是否仍然生效？**

答：状态监测由独立的 Node.js 后台任务执行，默认在构建阶段生成一份快照，并在部署后通过定时触发的云函数或 CI 流水线更新。若采用纯静态托管，可借助 GitHub Actions 每周运行一次监测并自动提交新的状态数据，重新构建站点。本地预览时，监测任务会以开发模式模拟运行，不会实际发送大量 HEAD 请求。

**问：如何迁移已有的浏览器书签或第三方导航站数据？**

答：NovaIndex 的导入模块支持 Netscape 书签 HTML 格式（所有主流浏览器通用导出格式），以及 JSON 数组格式。执行 `npm run import -- --source=bookmarks.html --format=html` 即可自动解析并生成对应的 Markdown 资源文件。对于第三方导航站，若其提供公开 API 或可抓取的列表页，可参考开发者文档中的适配器示例编写自定义转换脚本。

**问：资源链接显示失效后，系统能否自动替换或通知？**

答：监测模块仅记录状态变更并生成报告，不会自动修改资源内容，避免误操作导致错误替换。管理员可在管理后台查看「异常资源」清单，并手动编辑更新 URL 或删除无效条目。同时，系统支持配置 Webhook 通知（如发送至企业微信、Slack 或邮件），在首次检测到失效时推送告警，便于及时处理。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
