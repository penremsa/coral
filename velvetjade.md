# RSLinks Resource Aggregator

RSLinks Resource Aggregator is a lightweight, developer-oriented metadata catalog and external link management system. It provides structured storage, tag-based retrieval, and health monitoring for a curated collection of web resources. The project is designed for individual developers, small teams, and research analysts who need to maintain a clean, version-controlled reference index of frequently used online assets without relying on third-party bookmarking services.

The system solves the problem of link fragmentation and link rot by combining a static-site-friendly data schema with automated availability checking. Users can organize resources by domain category, assign custom attributes, and export the entire index as JSON or Markdown for integration into documentation pipelines. RSLinks is not a search engine, a crawler, or a dynamic web application; it is a structured data toolkit that treats links as first-class entities with versioned metadata.

## 功能概览

- **Hierarchical Category Tagging** – Assign one or multiple category labels to each resource, enabling faceted filtering across domains such as media, reference, and utility.
- **Automated Link Health Probe** – Schedule periodic HEAD requests against each stored URL to detect HTTP status anomalies and flag broken or redirected endpoints.
- **Markdown-to-JSON Compiler** – Convert the curated link list from human-editable Markdown tables into machine-readable JSON schemas for API consumption.
- **Custom Attribute Attachment** – Attach free-form key-value pairs to any resource, supporting use cases like access notes, region hints, or archival timestamps.
- **Export Pipeline** – Generate static HTML summary pages or plain-text reports from the indexed dataset without running a persistent database.
- **CLI Interactive Query** – Filter and display resources via terminal commands using regex patterns, status filters, or last-checked time ranges.
- **Git-Friendly Storage** – Store all metadata in plain text files, making every change traceable via commit history and branchable for experimental curation.

## 应用场景

- **Personal Bookmark Vault** – A developer maintains a private collection of reference sites for coding, design, and research. RSLinks provides a unified import/export flow to synchronize this vault across multiple workstations without cloud vendor lock-in.
- **Team Documentation Hub** – A technical writing team curates an approved list of external reference URLs for their product manuals. RSLinks generates a machine-readable allowlist that can be fed into automated link checkers during the documentation build process.
- **Data Journalism Resource Index** – A small investigative research group aggregates public data portals, archival databases, and media watchdogs. They use RSLinks to tag each resource by jurisdiction, topic, and update frequency, enabling rapid filtering during deadline-driven projects.
- **Educational Course Material** – An instructor compiles a semester-long reading list with supplementary video and interactive content. RSLinks produces a clean Markdown syllabus that renders seamlessly on static course sites, while the JSON export feeds a custom student dashboard.

## 快速开始

```bash
# 1. Clone the repository
git clone https://github.com/rslinks/rslinks-aggregator.git
cd rslinks-aggregator

# 2. Install dependencies (Python 3.9+ required)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. Initialize the default dataset and run health check
python cli.py init --source ./data/sample_links.md
python cli.py check --timeout 5 --parallel 4

# 4. Generate static summary report
python cli.py export --format html --output ./public/index.html

# 5. View interactive filters
python cli.py query --tag media --status active
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行时，用于 CLI 工具和调度器 |
| Pip | 21.0 及以上 | 包管理，用于安装依赖库 |
| Requests | 2.28.0 及以上 | HTTP 客户端，执行链接健康探测 |
| PyYAML | 6.0 及以上 | 可选配置文件的解析支持 |
| Markdown | 3.4.0 及以上 | 用于将资源表格转换为内部数据结构 |
| Pydantic | 2.0 及以上 | 数据模型校验和序列化 |
| Click | 8.1.0 及以上 | CLI 命令框架，提供交互式终端界面 |
| Git | 2.30 及以上 | 版本控制，用于追踪索引变更历史 |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|---|---|---|
| 用户手册 | ./docs/user_guide.md | 如何添加、删除、修改资源条目？如何运行健康检查？ |
| 数据格式参考 | ./docs/data_schema.md | 内部 JSON 结构长什么样？自定义属性的约束规则是什么？ |
| 命令行参考 | ./docs/cli_commands.md | 每个 CLI 子命令支持哪些参数和选项？ |
| 贡献者指南 | ./CONTRIBUTING.md | 如何提交新的资源类别定义？如何更新依赖版本？ |
| 运维说明 | ./docs/operations.md | 如何配置定时检查任务？如何迁移数据集到新环境？ |
| 设计决策记录 | ./docs/adr/ | 为什么选择静态存储而非数据库？为什么采用 Markdown 作为主输入格式？ |

## 资源列表

### 按字母排序的全部收录链接

- <code>ribenrenqizhongwenzimu.org.cn</code>
- <code>ribenyehuashipin.org.cn</code>
- <code>oumeishunvwangzhan.org.cn</code>
- <code>rihanjialeibi.org.cn</code>
- <code>gaohuangzaixianguankan.org.cn</code>
- <code>shufuzhongwenzimu.org.cn</code>
- <code>oumeilingleisetu.org.cn</code>
- <code>daxiangjiaomianfei.org.cn</code>
- <code>laosijiwangzhi.org.cn</code>
- <code>ouzhouyazhouzipai.org.cn</code>

### 类别参考分组

娱乐与多媒体类:
- <code>ribenrenqizhongwenzimu.org.cn</code>
- <code>ribenyehuashipin.org.cn</code>
- <code>rihanjialeibi.org.cn</code>
- <code>gaohuangzaixianguankan.org.cn</code>
- <code>oumeilingleisetu.org.cn</code>

文化及语言类:
- <code>shufuzhongwenzimu.org.cn</code>
- <code>oumeishunvwangzhan.org.cn</code>

综合门户与分类信息:
- <code>daxiangjiaomianfei.org.cn</code>
- <code>laosijiwangzhi.org.cn</code>
- <code>ouzhouyazhouzipai.org.cn</code>

## 项目结构

```
rslinks-aggregator/
├── cli.py                     # 主命令行入口，注册所有子命令
├── requirements.txt           # 生产环境依赖锁定列表
├── dev-requirements.txt       # 测试和代码风格检查工具
├── README.md                  # 项目首页文档（本文件）
├── CONTRIBUTING.md            # 贡献流程和代码规范说明
├── LICENSE                    # MIT 许可证全文
├── .gitignore                 # 忽略临时文件、缓存和本地配置
├── .pre-commit-config.yaml    # 提交前自动化检查钩子配置
├── data/
│   ├── sample_links.md        # 示例资源数据集（Markdown 表格）
│   ├── schema_v2.json         # 当前数据结构的 JSON Schema 定义
│   └── curated/               # 用户正式索引存放目录
│       ├── default.json       # 主数据集（编译后 JSON 格式）
│       └── history/           # 按日期归档的历史快照
├── src/
│   ├── core/                  # 核心数据模型和验证逻辑
│   │   ├── models.py          # Pydantic 实体定义（Resource, Tag, ProbeResult）
│   │   └── exceptions.py      # 自定义异常类层次结构
│   ├── parsers/               # 不同输入格式的转换器
│   │   ├── markdown_parser.py # 解析 Markdown 表格为内部数据
│   │   └── yaml_loader.py     # 加载可选 YAML 配置文件
│   ├── probes/                # 链接健康检查模块
│   │   ├── http_probe.py      # 基于 Requests 的并发探测
│   │   └── reporter.py        # 生成探测结果摘要
│   ├── exporters/             # 输出格式化工具
│   │   ├── html_exporter.py   # 生成静态 HTML 资源列表
│   │   ├── json_exporter.py   # 输出标准 JSON 数据集
│   │   └── markdown_exporter.py # 反向导出 Markdown 表格
│   └── cli/                   # 各子命令具体实现
│       ├── init.py
│       ├── check.py
│       ├── query.py
│       └── export.py
├── tests/                     # 单元测试和集成测试
│   ├── conftest.py            # pytest 共享夹具
│   ├── test_models.py         # 数据模型校验用例
│   └── test_probe.py          # 模拟网络请求测试套件
├── docs/                      # 详细用户手册和架构文档
│   ├── user_guide.md
│   ├── data_schema.md
│   ├── cli_commands.md
│   ├── operations.md
│   └── adr/                   # 架构决策记录
│       └── 001-static-storage.md
└── public/                    # 导出的静态站点默认输出目录
    └── index.html             # 示例生成的资源看板
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库，并克隆到本地。创建新分支时使用 `feature/` 或 `fix/` 前缀，例如 `feature/add-category-filter`，确保分支名称描述变更意图。
2. 编辑 `data/sample_links.md` 或 `data/curated/default.json` 来增加或修改资源条目。若修改 JSON 文件，需运行 `python cli.py validate` 验证数据符合 schema 约束。若修改 Markdown，需同步检查表格格式是否为标准三列（资源名称、URL、标签）且不包含空行。
3. 针对新增功能或修复问题，在 `tests/` 下补充对应的测试用例，使用 pytest 执行全部测试：`pytest -v`。确保所有测试通过且代码覆盖率达到 90% 以上。
4. 提交前执行 `pre-commit run --all-files` 进行代码风格检查（Black、Flake8、isort）。若存在警告，请修正后再提交。提交信息采用常规提交规范（Conventional Commits），例如 `feat: add interactive tag filter to query command`。
5. 推送分支到远程仓库，并提交 Pull Request 到 `main` 分支。PR 描述中请简要列出变更内容、测试结果以及是否影响现有数据结构。项目维护者将在两个工作日内进行审查和合并。

## 常见问题

**问：为什么所有链接必须以 <code></code> 标签形式写在 README 中，而不使用 Markdown 的超链接语法？**

答：本项目将 README 中的资源列表视为一种“机器可读的快照”。使用 <code> 标签包裹纯 URL 可以避免 Markdown 渲染器自动添加 rel 属性或改变链接文本，同时也便于外部脚本通过正则表达式直接提取裸 URL 列表，而不需要解析 HTML 的 href 属性。这一约定保证了文档本身可以作为数据源的单一事实来源。

**问：链接健康检查报错“连接超时”是否意味着该资源已永久失效？**

答：不一定。超时可能由网络环境、临时服务器负载或防火墙策略导致。RSLinks 的探测模块默认重试一次，并记录响应时间。建议用户在非高峰时段重新运行 `python cli.py check --timeout 10`，同时可以配合 `--exclude` 参数跳过特定域名的检查。如果连续三次检查均失败，则将该资源标记为“疑似失效”并输出到警告日志中，但不自动删除条目，以保留人工确认的窗口。

**问：如何将现有的浏览器书签批量导入 RSLinks？**

答：目前 RSLinks 不提供直接针对浏览器书签格式（如 Netscape HTML 或 JSON）的导入器。但是，用户可以将书签导出为 CSV 或 HTML 列表，然后使用 `src/parsers/` 目录下的辅助脚本将每行转换为符合 Markdown 表格格式的记录。社区贡献者正在开发一个独立的转换工具 `import_bookmarks.py`，预计在下个版本中合并。在此之前，推荐用户使用文本编辑器的多行查找替换功能来快速整理格式。

## 许可证

MIT License

Copyright (c) 2026 RSLinks Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:32
