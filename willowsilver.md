# NexusIndex

NexusIndex 是一个面向技术内容聚合与资源导航的开源元目录项目。项目定位为结构化的外链索引系统，旨在解决技术文档、社区教程、官方工具站与视频资源站点分散、难以统一检索与引用的问题。目标用户包括技术文档编写者、社区维护者、知识库管理员以及需要频繁引用外部技术视频或教程站点的开发者。

NexusIndex 不提供具体的内容存储或视频播放服务，而是以可维护、可版本化的 Markdown 索引结构，将高质量的外部资源链接组织为带注释的目录树，并提供标准的快速启动与部署方案。项目本身可作为静态站点生成器的数据源，也可嵌入现有文档系统作为外部资源引用模块。

## 功能概览

- **结构化链接索引**：按技术领域、资源类型、语言类别等多维度对链接进行标记与分组，支持 JSON 与 YAML 格式的元数据导出。
- **自动校验与死链检测**：集成定时检查任务，对收录的 URL 进行可用性探测，自动标记失效链接并生成报告。
- **标签与全文检索支持**：内置基于 Lunr.js 的离线检索方案，可按关键词、分类标签、域名后缀快速定位资源。
- **多格式数据导出**：支持将索引数据导出为 JSON、CSV、OPML 及 HTML 摘要页，便于导入其他知识管理工具。
- **版本化更新记录**：每次链接增删或元数据修改均通过 Pull Request 方式合并，保留完整的变更历史与审核痕迹。
- **响应式预览模板**：提供可选的静态 HTML 预览页面，采用移动优先的响应式设计，方便在移动端浏览索引目录。
- **RESTful API 查询接口**：基于 Flask 或 FastAPI 的轻量查询服务，支持按域名、分类、更新时间排序返回 JSON 结果。
- **自定义元数据扩展**：允许用户为每个链接添加自定义字段（如 难度等级、是否需要科学上网、所属专题编号），满足个性化组织需求。

## 应用场景

- **技术文档站外链管理**：当技术文档中需要引用大量外部视频教程或官方工具站时，可使用 NexusIndex 维护统一的引用清单，避免在文档正文中散落冗长 URL，同时便于统一更新失效链接。
- **社区知识库资源聚合**：开源社区或技术论坛可将 NexusIndex 作为社区维基的补充模块，用于整理成员推荐的优质视频站点或在线工具，新成员可通过索引快速了解社区常用资源分布。
- **离线文档打包资源映射**：在生成离线文档包（如 Dash、Zeal 或 DevDocs 格式）时，可借助 NexusIndex 导出的 JSON 映射表，将外部视频资源链接作为扩展参考条目嵌入离线文档的侧边栏。
- **自动化监控与告警**：运维或文档质量团队可部署 NexusIndex 的定时校验任务，当收录的视频站点或工具站出现访问异常时，自动发送告警通知，便于及时移除或替换问题链接。

## 快速开始

以下命令将在本地克隆项目、安装依赖并启动开发预览服务。

```bash
git clone https://github.com/nexusindex/nexusindex.git
cd nexusindex
pip install -r requirements.txt
python scripts/build_index.py --input data/sources.yaml --output dist/index.json
python serve.py --port 8080 --open
```

执行完成后，访问本地 8080 端口即可查看索引预览页面。如需生成静态 HTML 站点，可运行 `python scripts/generate_static.py` 并将 `dist/` 目录部署至任意静态托管服务。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心索引构建与 API 服务均基于 Python 运行 |
| Pip | 22.0 及以上 | 用于安装 requirements.txt 中列出的所有依赖包 |
| Git | 2.25 及以上 | 用于克隆仓库及管理贡献者提交的链接变更 |
| Node.js | 16.x 或 18.x | 仅当启用前端检索界面或预览模板编译时需要 |
| YAML 解析库 | PyYAML 6.0 | 用于解析 `data/sources.yaml` 中的链接元数据配置 |
| HTTP 请求库 | Requests 2.28 | 用于执行死链检测任务中的 HTTP 探活 |
| 静态服务 | 内置或 nginx | 用于托管生成的 HTML 预览页面，无特定版本要求 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `docs/user-guide/` | 如何添加新链接、如何修改已有索引元数据、如何生成预览站点 |
| 运维指南 | `docs/ops/` | 如何配置定时校验任务、如何调整死链阈值、如何迁移索引数据库 |
| 开发参考 | `docs/dev/` | API 接口的请求与响应格式、索引构建流程的类图与扩展点说明 |
| 设计文档 | `docs/design/` | 元数据 Schema 设计决策、标签体系演化策略、性能优化记录 |

## 资源列表

### 高清热门影视类

- <code>gaoqingzhongwenzimudianshiju.org.cn</code>
- <code>zaixiangaoqingzhongwenzimu.org.cn</code>
- <code>zaixianguankanrihandianshiju.org.cn</code>
- <code>zhongwenzimuyingshigaoqing.org.cn</code>
- <code>gaoqingyingshimianfeiguankan.org.cn</code>

### 免费播放与短视频类

- <code>mianfeiguankangaoqingdianyingwz.org.cn</code>
- <code>zaixianshipinbofangpingtai.org.cn</code>
- <code>zaixianguankanmianfeiduanju.org.cn</code>

### 综合高清在线类

- <code>mianfeibofanggaopingzaixian.org.cn</code>
- <code>mianfeiguochangaoqingyingshi.org.cn</code>

## 项目结构

```
nexusindex/
├── data/                        # 核心索引数据目录
│   ├── sources.yaml             # 主索引文件，记录全部链接及元数据
│   └── categories/              # 按分类拆分的子索引文件
│       ├── video.yaml           # 视频类资源子集
│       └── tool.yaml            # 工具类资源子集
├── scripts/                     # 构建与维护脚本
│   ├── build_index.py           # 从 YAML 生成 JSON/HTML 的主构建脚本
│   ├── check_dead_links.py      # 死链检测与报告生成脚本
│   └── export_opml.py           # 导出 OPML 格式供 RSS 阅读器导入
├── api/                         # RESTful API 服务源码
│   ├── app.py                   # Flask 应用入口与路由定义
│   └── search.py                # 基于内存索引的检索实现
├── static/                      # 预览站点静态资源
│   ├── templates/               # Jinja2 模板文件
│   └── assets/                  # CSS、JavaScript 及字体文件
├── tests/                       # 单元测试与集成测试用例
│   ├── test_builder.py          # 索引构建逻辑的测试
│   └── test_api.py              # API 接口返回数据结构的测试
├── docs/                        # 完整文档源码，包含用户手册与运维指南
├── requirements.txt             # Python 依赖清单
├── serve.py                     # 本地开发预览服务启动脚本
└── README.md                    # 项目入口说明文档（本文件）
```

## 贡献指南

1. **Fork 项目并创建特性分支**：从主仓库 Fork 到个人账户，然后基于 `main` 分支创建 `feature/your-change` 分支，避免直接在主分支上操作。
2. **修改索引文件并本地验证**：编辑 `data/sources.yaml` 中的链接条目，务必补全 `title`、`category`、`description` 字段，随后运行 `python scripts/build_index.py --validate` 执行格式与重复性检查。
3. **运行测试套件**：执行 `pytest tests/` 确保现有 API 与构建逻辑未被破坏，新增字段需同步补充对应的测试用例。
4. **提交 Pull Request 并填写变更模板**：提交时请使用仓库提供的 PR 模板，清晰说明新增链接的用途、来源以及为何需要收录，以便维护者快速审核。
5. **等待 CI 通过与维护者审核**：所有 PR 必须通过 GitHub Actions 中的构建校验与死链预检，维护者将在 3 个工作日内反馈合并意见。

## 常见问题

**Q：NexusIndex 是否存储或代理任何视频文件？**  
A：不存储。NexusIndex 只收录 URL 字符串及其元数据描述，不缓存、不转发、不镜像任何外部站点的媒体内容。所有链接指向的资源均属于原始第三方站点，用户访问时需遵守对应站点的使用条款。

**Q：如何报告收录链接失效或内容异常？**  
A：请在本项目的 Issues 页面提交新 Issue，选择「Broken Link」标签，并附上该链接在 `sources.yaml` 中的完整条目路径。项目维护者会通过死链检测脚本确认后予以移除或替换。同时也欢迎直接提交 Pull Request 修正。

**Q：可以仅导出 JSON 而不部署 API 服务吗？**  
A：可以。运行 `python scripts/build_index.py --output index.json` 即可在当前目录生成纯 JSON 索引文件，该文件包含全部链接及元数据，可直接用于静态站点生成器或本地脚本处理，无需启动任何网络服务。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
