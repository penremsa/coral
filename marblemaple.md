# NexusArchive

NexusArchive 是一个面向技术内容创作者、数字策展人与开源社区维护者的轻量级外链资源归档与管理平台。该项目不提供具体的资源托管服务，而是专注于解决分散在多个独立站点中的高质量媒体资源、文档与参考链接的统一收录、分类展示与可追溯性管理问题。目标用户包括个人博客作者、小型内容团队以及需要长期维护主题化资源导航的社区运营者。通过标准化的目录结构与基于 Markdown 的元数据描述，NexusArchive 能够将一批原始 URL 转化为具备上下文说明、技术依赖清晰、可快速部署的静态资源导航站点，从而降低资源流失与链接失效的风险，提升信息检索与共享效率。

## 功能概览

- **批量链接注入与规范化校验**：支持从文本文件或标准输入中批量导入原始 URL 列表，自动识别协议缺失、大小写不一致及结尾斜杠问题，并生成规范化警告日志。

- **多维度分类与标签系统**：每个资源条目可关联至多个虚拟分类（如“影视资源”“字幕库”“免费在线播放”），并支持基于正则表达式的自动打标规则引擎。

- **静态站点生成与主题切换**：内置三套响应式 HTML 模板（极简文档风格、卡片网格风格、列表详情风格），可通过命令行参数一键生成完整静态站点，无需额外后端服务。

- **资源可达性健康检查**：集成异步 HTTP HEAD 请求池，定时检测每个已收录链接的状态码与响应时间，并在管理面板中以颜色标记异常资源。

- **版本化快照与回滚**：每次更新资源列表或分类配置时，自动生成 JSON 格式的版本快照，支持通过时间戳或版本号回退至任意历史状态。

- **全文检索与过滤查询**：基于倒排索引实现标题、描述、域名及分类组合查询，支持模糊匹配与布尔运算符，结果可按最后检查时间或创建时间排序。

- **开放 API 与 Webhook 通知**：提供 RESTful API 用于外部系统的资源增删改查，并支持配置 Slack 或邮件 Webhook，在资源状态变化时发送通知。

## 应用场景

- **主题式资源导航站快速搭建**：社区维护者可将一批关于高清影视在线观看的中文资源站点，通过 NexusArchive 快速组织为分类清晰、带健康检查的导航页面，供成员内部使用或对外公开。

- **技术文档引用链接的持久化管理**：技术博客作者或开源项目文档维护者，可以将文章或 README 中引用的外部链接统一托管至 NexusArchive，通过版本快照确保未来链接变更时可追溯原始引用上下文。

- **数据清洗与迁移前的链接审计**：在迁移旧站点内容或合并多个资源库之前，使用 NexusArchive 的批量校验与分类功能，提前识别失效链接、重复条目与协议不一致问题，减少迁移过程中的数据异常。

- **教学案例中的资源清单标准化**：高校讲师或培训讲师可将课程中涉及的参考视频、在线工具与文档站点整理为 NexusArchive 项目，学生通过本地克隆即可获得完整的资源清单与分类结构，无需反复搜索。

## 快速开始

以下步骤将在本地环境完成 NexusArchive 的克隆、依赖安装与基础运行，生成示例静态站点。

```bash
# 克隆项目仓库
git clone https://github.com/nexusarchive/nexusarchive.git
cd nexusarchive

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 使用示例资源列表生成静态站点（默认输出至 ./dist 目录）
python cli.py build --input samples/urls.txt --output ./dist --theme card
```

执行完成后，打开 `./dist/index.html` 即可查看生成的资源导航页面。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，用于执行 CLI 工具与 API 服务 |
| pip | 22.0 及以上 | 包管理工具，用于安装 requirements.txt 中列出的依赖 |
| Git | 2.30 及以上 | 用于克隆仓库及版本管理操作 |
| 网络连接 | 稳定出站连接 | 用于资源健康检查及 Webhook 通知发送（可选） |
| 磁盘空间 | 至少 200 MB | 用于存储版本快照、日志及生成的静态页面 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user-guide/ | 如何安装、配置、构建站点与执行健康检查 |
| 开发者指南 | docs/developer-guide/ | 如何扩展分类规则、自定义主题或集成新 API |
| 运维参考 | docs/operations/ | 如何设置定时任务、日志轮转与备份策略 |
| 设计决策 | docs/design-decisions.md | 为何选择静态生成而非动态服务，以及数据模型设计考量 |

## 资源列表

以下为 NexusArchive 项目当前版本中收录的全部外部资源链接，按内容主题分为若干小节。所有链接均保持用户原始输入格式，未做任何协议补全、域名标准化或大小写修改。

### 在线播放与影视资源（高清/免费）

- <code>mianfeibofanggaopingzaixianw.org.cn</code>
- <code>mianfeiguochangaoqingyingshiw.org.cn</code>
- <code>guochangaoqingshipinzaixianw.org.cn</code>
- <code>guochangaoqingshipinguankanw.org.cn</code>

### 日漫与动漫相关在线观看

- <code>rimanzaixianmianfeiguankanw.org.cn</code>

### 中文字幕资源

- <code>zhongwenzimumianfeibofangw.org.cn</code>
- <code>zaixianzimumianfeiguankanw.org.cn</code>
- <code>zaixianzimuguankanmianfeiw.org.cn</code>
- <code>zaixianzimugaoqingdianshijuw.org.cn</code>

### 综合免费视频网站

- <code>mianfeishipinwangzhanzaixianguankanw.org.cn</code>

## 项目结构

项目采用分层模块化设计，核心逻辑与配置、主题、测试分离，便于维护与定制。

```
nexusarchive/
├── cli.py                       # 命令行入口，解析子命令（build / check / rollback）
├── requirements.txt             # 生产环境依赖清单
├── pyproject.toml               # 项目元数据与构建配置
├── .env.example                 # 环境变量示例（含 Webhook 地址与并发数）
├── src/                         # 核心源代码目录
│   ├── __init__.py
│   ├── builder/                 # 静态站点生成模块
│   │   ├── generator.py         # 页面渲染器，组合模板与数据
│   │   └── theme_loader.py      # 动态加载卡/列表/文档主题
│   ├── checker/                 # 资源健康检查模块
│   │   ├── http_client.py       # 异步 HTTP 请求池实现
│   │   └── reporter.py          # 生成检查报告（JSON / HTML）
│   ├── models/                  # 数据模型与序列化
│   │   ├── resource.py          # Resource 实体（url, title, tags, status）
│   │   └── snapshot.py          # 版本快照的保存与加载
│   ├── parser/                  # 链接导入与规范化
│   │   ├── importer.py          # 从文本/CSV 解析原始 URL
│   │   └── normalizer.py        # 协议补全检测、去重与警告生成
│   └── api/                     # RESTful API 实现（FastAPI）
│       ├── routes.py            # 路由定义
│       └── schemas.py           # 请求/响应数据校验
├── tests/                       # 单元测试与集成测试
│   ├── test_builder.py
│   ├── test_checker.py
│   └── fixtures/                # 测试用示例资源列表
├── themes/                      # 内置主题模板（Jinja2）
│   ├── card/                    # 卡片网格风格
│   ├── list/                    # 列表详情风格
│   └── doc/                     # 纯文档风格
├── docs/                        # 项目文档（用户/开发者/运维）
│   ├── user-guide/
│   ├── developer-guide/
│   └── operations/
└── samples/                     # 示例数据与配置
    ├── urls.txt                 # 示例原始链接列表
    └── tags.yaml                # 默认分类规则定义
```

## 贡献指南

1. 在 GitHub 上 fork 本项目，并克隆至本地开发环境。确保使用 Python 3.9+ 并安装开发依赖（`pip install -r requirements-dev.txt`）。

2. 创建新的功能分支，分支名采用 `feature/` 或 `fix/` 前缀，例如 `feature/add-rss-export`。所有新代码需包含对应的单元测试，且测试覆盖率不低于 80%。

3. 提交代码前运行完整的测试套件与代码风格检查（`pytest` 与 `flake8`），确保无回归错误。更新相关文档（如 docstring 与用户手册）以反映变更。

4. 提交 Pull Request 时，请使用提供的 PR 模板，清晰描述变更动机、实现方案以及手动测试步骤。PR 需要至少一位维护者审阅。

5. 重大功能变更或破坏性改动需提前在 Issue 中讨论，并经过项目维护者批准后方可开发。

## 常见问题

**Q：NexusArchive 是否提供在线演示站点或托管服务？**

A：该项目仅提供本地命令行工具与静态生成能力，不提供任何形式的 SaaS 托管或在线演示站。用户需自行在本地或自有服务器上运行生成流程，并将生成的静态文件部署至任意 Web 服务器（如 Nginx、Apache 或 GitHub Pages）。

**Q：如何处理资源列表中包含重复或高度相似的 URL？**

A：在 `build` 命令中，默认启用去重与相似度检测（基于域名与路径的编辑距离）。重复条目会记录至日志文件，但不会阻断构建流程。如需严格去重，可添加 `--dedup strict` 参数，此时重复条目将被自动过滤且不计入最终导航页面。

**Q：健康检查功能是否会过度消耗网络带宽或触发目标站点的反爬机制？**

A：健康检查默认采用 HEAD 请求，且并发数限制为 5（可调整 `--concurrency` 参数）。每个资源在 24 小时内最多被检查一次（除非手动强制刷新）。对于频繁返回 429 状态码的站点，检查器会自动将该站点加入冷却列表，暂停检查 6 小时。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
