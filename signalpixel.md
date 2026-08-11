# HyperLink Navigator

HyperLink Navigator 是一个面向技术社区的开源外链资源聚合与导航系统。该项目定位于为开发者、技术研究人员以及内容创作者提供结构化、高可读性的外部资源索引服务。它通过静态站点生成机制，将分散的领域相关链接进行主题归类、元数据标注与状态监控，解决技术文档中“链接失效”“上下文缺失”“检索效率低”等核心痛点。HyperLink Navigator 适用于个人知识库增强、团队技术文档补充以及开源项目附属资源站搭建等场景。

## 功能概览

- **多级分类索引**：支持按地域、主题、文件类型等维度建立链接分类树，便于用户快速定位资源分组。
- **链接状态健康检查**：内置异步 HTTP 探测器，定期对收录链接进行可达性检测，并标记异常状态。
- **全文元数据搜索**：基于链接标题、描述、标签以及域名信息进行关键词匹配，返回相关性排序结果。
- **批量导入与导出**：支持通过 JSON 或 CSV 格式批量新增资源条目，并支持将当前索引导出为标准书签文件。
- **访问统计看板**：记录各链接的点击频次与来源页面，提供简单热度分析视图。
- **自动生成资源快照**：对文本类外链内容生成摘要快照，用于链接临时不可访问时的降级展示。
- **自定义展示模板**：允许用户通过主题配置文件调整资源列表的布局样式与排序规则。
- **RSS 订阅输出**：按分类或标签生成 RSS 源，方便用户跟踪特定领域资源更新。

## 应用场景

- **开源项目文档站外参考**：当开源项目需要引用大量外部技术规范、标准文档或社区讨论帖时，HyperLink Navigator 可集中管理这些引用，并提供统一入口，避免散落在 README 或 Wiki 中难以维护。
- **技术培训与教学资源整理**：培训机构或高校教师可将课程所需的视频站点、在线工具、代码示例仓库等链接通过本系统组织成课程资源站，学生无需记忆多个域名即可一键访问。
- **领域研究资料归档**：研究员可围绕特定国家或地区的文化媒体资源建立专题导航，便于同行快速了解该领域可用的公开信息源，同时通过健康检查功能及时发现失效资源。
- **个人知识库外链增强**：个人笔记或博客作者可将经常引用的外部文章、工具站、数据平台等通过本系统建立索引，在写作时直接引用导航页链接，减少重复粘贴。

## 快速开始

以下操作指南适用于 Linux / macOS / Windows WSL 环境。

```bash
# 1. 克隆代码仓库
git clone https://github.com/example/hyperlink-navigator.git
cd hyperlink-navigator

# 2. 安装项目依赖（使用 pip 和 npm）
pip install -r requirements.txt
npm install --prefix frontend

# 3. 初始化示例数据并启动开发服务器
python scripts/init_db.py --sample-data
python app.py --host 127.0.0.1 --port 8080
```

启动成功后，打开浏览器访问 `http://127.0.0.1:8080` 即可查看默认资源导航页面。管理员后台默认路径为 `/admin`，初始账号密码请参阅 `docs/quick-start.md`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.12 | 后端核心运行环境，低于 3.9 将导致异步语法错误 |
| Node.js | 18.x 或 20.x LTS | 用于构建前端静态资源与执行主题编译脚本 |
| SQLite | 3.35.0 及以上 | 默认内置数据库，用于存储链接元数据与状态记录 |
| Redis | 6.2 及以上 | 可选，用于缓存健康检查结果与访问计数，非必需但推荐 |
| Nginx | 1.18 及以上 | 生产环境反向代理与静态资源服务建议版本 |
| Git | 2.25 及以上 | 用于版本管理与钩子脚本执行，开发环境必需 |
| make | 3.81 及以上 | 用于执行 Makefile 中定义的自动化任务（测试、打包等） |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | `docs/user-guide/` | 如何添加新链接、批量导入、查看统计以及自定义主题？ |
| 运维指南 | `docs/operations/` | 如何部署到生产服务器、配置 HTTPS、设置定时健康检查任务？ |
| API 参考 | `docs/api/` | 后端提供了哪些 RESTful 接口用于管理资源与查询状态？ |
| 开发文档 | `docs/development/` | 如何扩展新的分类规则、编写自定义检测插件或修改前端组件？ |

## 资源列表

### 地区文化媒体资源

<code>ribenrenqizhongwenzimu.org.cn</code>

<code>ribenyehuashipin.org.cn</code>

<code>oumeishunvwangzhan.org.cn</code>

<code>rihanjialeibi.org.cn</code>

<code>gaohuangzaixianguankan.org.cn</code>

### 辅助工具与素材资源

<code>shufuzhongwenzimu.org.cn</code>

<code>oumeilingleisetu.org.cn</code>

<code>daxiangjiaomianfei.org.cn</code>

### 综合导航与相关站

<code>laosijiwangzhi.org.cn</code>

<code>ouzhouyazhouzipai.org.cn</code>

## 项目结构

```
hyperlink-navigator/
├── app/                            # 后端主应用模块
│   ├── api/                        # RESTful API 路由层
│   │   ├── v1/                     # API 版本 v1 端点实现
│   │   └── middleware/             # 认证、日志、跨域中间件
│   ├── core/                       # 核心业务逻辑
│   │   ├── checker.py              # 链接健康检查异步任务
│   │   ├── indexer.py              # 元数据提取与索引更新
│   │   └── snapshot.py             # 文本快照生成工具
│   ├── models/                     # SQLAlchemy 数据表定义
│   │   ├── link.py                 # 资源链接实体模型
│   │   ├── category.py             # 分类树节点模型
│   │   └── stat.py                 # 点击与访问统计模型
│   └── utils/                      # 通用辅助函数集合
│       ├── http.py                 # 异步 HTTP 请求封装
│       └── parser.py               # 域名与 URL 解析工具
├── frontend/                       # 前端静态源码目录
│   ├── src/                        # Vue / React 组件源码（按框架实际调整）
│   ├── themes/                     # 可切换的主题样式文件
│   └── dist/                       # 构建输出目录（由 npm run build 生成）
├── scripts/                        # 运维与开发脚本
│   ├── init_db.py                  # 数据库初始化与种子数据加载
│   ├── export_bookmark.py          # 导出为 HTML 书签格式
│   └── health_check_cron.py        # 定时健康检查调度脚本
├── tests/                          # 单元测试与集成测试用例
│   ├── unit/                       # 独立模块测试
│   └── integration/                # API 与数据库联合测试
├── docs/                           # 完整文档源文件（参考上方文档导航）
├── requirements.txt                # Python 依赖清单
├── package.json                    # Node.js 前端依赖配置
├── Makefile                        # 常用任务自动化入口
└── README.md                       # 项目总览（当前文件）
```

## 贡献指南

1.  **问题追踪与功能提议**：请先查阅 GitHub Issues 中已有的讨论，若未发现重复议题，请使用提供的模板新建 Issue，清晰描述问题现象、复现步骤或预期功能行为。
2.  **分支开发流程**：从 `main` 分支切出新的功能分支，命名遵循 `feature/功能简述` 或 `fix/问题编号` 格式。所有开发工作在该分支上进行，并确保代码通过既有测试。
3.  **代码风格与测试**：Python 代码须通过 Black 格式化与 pylint 静态检查；JavaScript 代码须遵循 ESLint 配置。新增或修改功能必须附带对应的单元测试，且测试覆盖率不得低于原有水平。
4.  **提交规范与合并请求**：Commit 信息建议采用 Conventional Commits 风格。完成开发后，向 `main` 分支发起 Pull Request，并填写变更摘要与测试结果。至少需要一名维护者审核通过后方可合并。
5.  **文档同步更新**：任何影响用户使用方式或运维流程的变更，须同步更新 `docs/` 目录下的对应文档，并确保示例代码与实际保持一致。

## 常见问题

**Q：健康检查模块误报链接不可达，如何处理？**

A：检查网络环境是否允许对外发起 HTTP 请求。若目标站点有反爬机制或要求特定 User-Agent，可在 `app/core/checker.py` 中配置请求头。此外，可调整 `CHECK_TIMEOUT` 与 `CHECK_RETRY` 环境变量以放宽超时与重试阈值。手动验证链接可用后，可使用管理员接口强制更新其状态。

**Q：如何迁移数据库到 MySQL 或 PostgreSQL？**

A：项目默认使用 SQLite，但通过 SQLAlchemy 支持多数据库。您需要修改 `config.py` 中的 `SQLALCHEMY_DATABASE_URI` 为对应的连接字符串，然后运行 `scripts/init_db.py --migrate` 执行表结构迁移。注意，不同数据库的字段类型可能存在细微差异，请参照 `docs/operations/database-migration.md` 中的兼容性说明。

**Q：前端构建失败，提示内存不足或模块缺失？**

A：建议升级 Node.js 到 20.x LTS 版本，并增加 `NODE_OPTIONS=--max-old-space-size=4096` 环境变量。同时，删除 `node_modules` 和 `package-lock.json` 后重新执行 `npm install`。若仍存在问题，请检查操作系统是否开启了交换分区，或使用 CI 构建环境提供的标准镜像。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
