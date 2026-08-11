# ResourceForge

ResourceForge 是一个面向技术内容聚合与外部资源导航的开源工具集，定位于为开发者、技术博主、研究分析人员以及站点运维工程师提供高效、可定制的技术资源外链管理与展示能力。该项目通过结构化的数据组织方式和轻量级的静态站点生成逻辑，帮助用户将大量分散的参考链接、文档入口与专题资源整合为清晰、易维护的知识导航体系，解决信息碎片化、链接遗忘、团队共享困难等实际问题。

ResourceForge 不依赖复杂的前端框架或数据库系统，其核心设计理念为“以代码管理资源，以版本控制驱动更新”，使技术团队能够像维护代码库一样维护外部知识索引。项目本身可作为独立站点运行，也可嵌入现有文档系统，适用于个人知识库构建、团队开发文档门户、专题技术研究资料汇总等多种场景。

## 功能概览

- **多源链接批量导入与去重**：支持从文本文件、CSV 或 JSON 结构中批量导入外部 URL，并基于域名与路径层级自动识别重复条目，减少人工整理成本。

- **分类与标签双维度组织**：允许用户为每条资源链接分配所属类别（如“协议规范”“编码工具”“社区论坛”）和自定义标签，实现灵活的多维筛选与分组展示。

- **ASCII 目录树自动生成**：根据资源分类和子分类层级，自动生成用于 README 或文档页面的 ASCII 风格目录树，便于在代码仓库中直接呈现结构。

- **Markdown 表格渲染引擎**：将链接列表、依赖说明、文档导航等结构化数据统一渲染为符合开源项目规范的 Markdown 表格，保证文档风格一致性。

- **静态 HTML 导出功能**：提供轻量级构建命令，可将所有资源数据与配置导出为纯静态 HTML 页面，无需动态服务即可部署至任意 HTTP 服务器或 CDN。

- **链接可用性巡检接口**：内置基于 HTTP 状态码的链接存活检查模块，支持定时或手动触发，并输出失效链接报告，帮助维护资源质量。

- **权限分级视图（可选）**：通过环境变量控制外部资源的可见性层级，支持公开访问、团队内部可见及仅维护者可见三种模式，适配不同共享需求。

## 应用场景

**技术团队内部文档门户统一入口**  
开发团队可将日常使用的 API 参考文档、设计规范、运维手册、代码生成工具等外部链接统一纳入 ResourceForge 管理，生成团队共享的导航页面，避免各成员自行收藏导致的版本不一致或链接失效问题。

**开源项目外链资源汇总页**  
开源项目维护者可以利用 ResourceForge 为项目生成独立的资源附录页面，集中陈列相关协议文本、第三方依赖主页、社区讨论区、镜像下载站等信息，提升项目文档的专业度与实用性。

**专题技术研究与学习路径组织**  
在进行新技术调研或系统性学习时，研究人员可将查阅到的论文链接、视频教程、示例仓库、在线 Sandbox 环境等按照学习阶段分类整理，形成可复用的研究资源包，便于后续回顾或分享。

**站点迁移或域名替换时的链接审计**  
当团队需要更换文档站点域名或进行架构升级时，ResourceForge 的链接巡检功能可快速扫描全部外链资源，输出可访问性报告，辅助决策哪些链接需要更新或废弃，降低迁移风险。

## 快速开始

以下操作步骤适用于 Linux / macOS / Windows WSL 环境，确保系统已安装 Git 和 Node.js（v16 及以上版本）。

```bash
# 1. 克隆项目仓库
git clone https://github.com/resourceforge/resourceforge-core.git
cd resourceforge-core

# 2. 安装项目依赖
npm install

# 3. 使用示例数据运行开发构建
npm run build -- --sample-data
npm run serve
```

执行完成后，访问控制台输出的本地服务地址（默认为 http://127.0.0.1:5500）即可查看生成的资源导航页面。如需使用自定义数据，请参考 `docs/custom-data.md` 中的配置文件格式说明。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | v16.20.0 或更高 | 运行时环境，用于执行构建脚本与依赖管理 |
| npm | v8.0.0 或更高 | 包管理器，用于安装项目依赖及运行脚本命令 |
| Git | v2.25.0 或更高 | 版本控制工具，用于克隆仓库及提交更新 |
| 文件系统读写权限 | 读/写 | 用于读取资源数据文件及输出构建产物 |
| 网络访问（可选） | 外网连通 | 链接巡检功能需要向外发送 HTTP 请求 |
| 现代浏览器（仅开发时） | 最新两个版本 | 用于预览生成的静态页面效果，生产环境无要求 |

## 文档导航

| 层面 | 目录 / 文档 | 回答的问题 |
|------|-------------|------------|
| 用户指南 | `docs/quick-start.md` | 如何快速配置第一条资源链接并生成页面？ |
| 配置参考 | `docs/config-schema.md` | 支持哪些数据字段？分类层级如何定义？ |
| 开发指南 | `docs/development.md` | 如何二次开发插件或修改渲染模板？ |
| API 接口 | `docs/api-http.md` | 是否提供 REST 接口供外部系统调用？ |

## 资源列表

### 主要外链资源

<code>guochanrihanzhongwenzimu.org.cn</code>

<code>henhendaxiangjiao.org.cn</code>

<code>oumeixingshou.org.cn</code>

<code>yirenguochanjingpin.org.cn</code>

<code>rihanzaixianbuka.org.cn</code>

<code>sihuyingyin.org.cn</code>

<code>rihantingting.org.cn</code>

<code>oumeiwuyefuli.org.cn</code>

<code>oumeiyixiangaobendao.org.cn</code>

<code>wuyuejingpin.org.cn</code>

## 项目结构

```
resourceforge-core/
├── src/                                # 核心源代码目录
│   ├── cli/                            # 命令行入口与参数解析模块
│   │   └── index.ts                    # 主 CLI 逻辑，处理 build/serve/check 命令
│   ├── core/                           # 核心数据模型与处理引擎
│   │   ├── LinkRegistry.ts             # 链接注册与去重管理类
│   │   ├── CategoryTree.ts             # 分类树构建与遍历算法
│   │   └── ConfigLoader.ts             # 加载与验证用户配置文件
│   ├── renderers/                      # 输出渲染器集合
│   │   ├── MarkdownRenderer.ts         # 生成 README 风格 Markdown 表格与目录树
│   │   ├── HTMLRenderer.ts             # 导出为完整静态 HTML 页面
│   │   └── TreeFormatter.ts            # ASCII 目录树格式化工具
│   ├── checkers/                       # 链接可用性巡检模块
│   │   ├── HttpStatusChecker.ts        # 并发 HTTP 请求状态检查
│   │   └── ReportGenerator.ts          # 生成失效链接 CSV / JSON 报告
│   └── types/                          # TypeScript 类型定义
│       └── resource.d.ts               # ResourceItem, Category, Config 等接口
├── data/                               # 默认示例数据与用户数据存放目录
│   ├── samples/                        # 示例资源链接与分类配置
│   └── user/                           # 用户自定义数据（不提交至版本库）
├── docs/                               # 项目文档
│   ├── quick-start.md                  # 快速入门指南
│   ├── config-schema.md                # 配置结构完整说明
│   ├── development.md                  # 开发环境搭建与测试流程
│   └── api-http.md                     # HTTP API 文档（如启用服务模式）
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 各模块单元测试用例
│   └── integration/                    # 端到端构建测试
├── .github/                            # GitHub 社区配置文件
│   ├── ISSUE_TEMPLATE/                 # 问题报告与功能请求模板
│   └── workflows/                      # CI 持续集成流水线（构建与测试）
├── package.json                        # npm 项目依赖与脚本声明
├── tsconfig.json                       # TypeScript 编译配置
├── .eslintrc.cjs                       # 代码风格检查规则
└── README.md                           # 项目总览文档（本文件）
```

## 贡献指南

1. 在 GitHub 仓库页面点击 “Fork” 按钮，将项目复制至个人账户下，随后克隆该副本至本地开发环境。

2. 创建新的功能分支，分支命名需符合 `feature/功能简述` 或 `fix/问题简述` 格式，确保与主分支保持同步。

3. 进行代码修改或文档更新时，请遵循项目内的 ESLint 代码规范，并为新增功能补充对应的单元测试用例，测试覆盖率不得低于 80%。

4. 提交变更前，运行 `npm run test` 和 `npm run lint` 确认所有检查通过，并更新 `docs/` 下相关文档以反映变更内容。

5. 发起 Pull Request 至主仓库的 `main` 分支，描述中需清晰说明改动目的、实现方式及影响范围，等待项目维护者审阅。

## 常见问题

**Q：ResourceForge 是否必须联网才能使用？**  
A：核心构建和渲染功能完全离线可用，仅链接巡检模块需要外网 HTTP 访问权限。若无需巡检，可在配置中禁用该功能，项目正常运行不受影响。

**Q：如何迁移已有的大量书签或浏览器收藏夹数据？**  
A：项目提供了 `tools/import-browser-bookmarks.js` 辅助脚本，支持解析 Chrome / Firefox 导出的 HTML 书签文件，自动转换为 ResourceForge 所需的 JSON 数据格式。具体用法参见 `docs/migration.md`。

**Q：生成的静态页面是否支持移动端适配？**  
A：默认的 HTML 渲染模板基于响应式 CSS 设计，在手机、平板和桌面设备上均能自适应显示。用户也可通过替换 `src/renderers/templates/` 下的模板文件完全自定义样式。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:28
