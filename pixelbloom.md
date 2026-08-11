# VastLink Navigator

VastLink Navigator is a curated, high-availability technical resource aggregation and external link governance system. It is designed for developers, technical researchers, and content curation engineers who require a robust, category-based indexing mechanism for managing large volumes of unstructured external references. The project solves the problem of link rot, categorization drift, and manual bookmark overload by providing a lightweight, static-site-compatible metadata layer that validates, tags, and presents external URLs under a maintainable taxonomy. Target users include DevOps engineers building internal developer portals, technical writers maintaining documentation hubs, and open-source project maintainers who need to bundle reference materials alongside their primary codebases.

The system operates on a batch-oriented ingestion model. Each resource entry is treated as a first-class citizen with an immutable batch identifier, source timestamp, and category affinity. The current release corresponds to Batch 454/455, comprising ten distinct external references that have been processed through the pipeline. VastLink Navigator does not host, proxy, or modify the content of external resources; it acts solely as a structured navigation layer with validity checking and user-contextual annotation support. Out-of-the-box, the project provides a command-line interface for link validation, Markdown report generation, and static HTML export suitable for deployment to any web server or CDN endpoint.

## 功能概览

- **Batch-based Resource Ingestion** – Accepts plain-text URL lists and assigns them to batch identifiers with automatic timestamping and sequence numbering. Supports both single-entry and bulk-add operations.

- **Validity and Reachability Checking** – Performs asynchronous HEAD and GET requests against each external URL to verify server responsiveness and HTTP status code compliance. Timeout thresholds and retry policies are configurable per runtime environment.

- **Category Inference and Tagging** – Applies heuristic rules based on domain patterns, path segments, and keyword co-occurrence to suggest preliminary category labels. Users can override or supplement inferred tags via external mapping files.

- **Markdown and HTML Report Generation** – Produces structured documentation in Markdown format for version-controlled repositories, as well as standalone HTML pages with client-side filtering and search capabilities for end-user browsing.

- **Link Lifecycle Management** – Tracks each URL through states including "pending", "verified", "unreachable", and "archived". Supports scheduled re-validation jobs to detect and flag degraded resources.

- **Export and Integration Hooks** – Provides JSON and YAML output formats for integration with external systems such as content management platforms, documentation generators, and monitoring dashboards.

- **Batch History and Rollback** – Maintains a local SQLite journal of all ingestion operations. Supports rollback to previous batch states and differential comparison between batch versions.

## 应用场景

- **Technical Documentation External Reference Management** – Documentation teams maintaining large-scale developer guides can use VastLink Navigator to bundle all external references in a single, validated manifest. The system ensures that every hyperlink included in release notes, API guides, or tutorial series is reachable and correctly categorized before publication.

- **Open-Source Project Dependency Referencing** – Project maintainers who need to cite external tools, libraries, or informational resources alongside their source code can integrate VastLink Navigator into their CI pipeline. The generated Markdown report can be committed directly to the repository, serving as an always-up-to-date external resource appendix.

- **Internal Developer Portal Content Curation** – Platform engineering teams building internal developer portals can leverage the batch ingestion feature to periodically synchronize external learning materials, community forums, and third-party service endpoints. The HTML export can be embedded into portal dashboards as a curated "developer toolkit" section.

- **Academic and Research Reference Aggregation** – Researchers compiling technical paper references, data set sources, or tool repositories can use the batch ID system to version-link their reference collections alongside their publications. Each batch corresponds to a snapshot of external resources at the time of publication.

- **Compliance and Audit Trail Maintenance** – Organizations subject to external link auditing requirements can use the lifecycle tracking and historical journal features to demonstrate due diligence in monitoring third-party resource availability over time. The SQLite journal provides a verifiable audit trail.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/vastlink-navigator/vastlink-core.git
cd vastlink-core

# Install dependencies
pip install -r requirements.txt

# Run the ingestion pipeline with the sample URL list
python -m vastlink.ingest --batch 454 --source sample_urls.txt
python -m vastlink.validate --batch 454 --concurrency 10
python -m vastlink.export --batch 454 --format markdown --output docs/reference_batch_454.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行时。低于 3.9 版本不支持异步 HTTP 客户端特性 |
| aiohttp | 3.8.0 及以上 | 用于高并发异步 URL 验证。需配合 certifi 使用以处理 SSL 证书 |
| SQLite | 3.35.0 及以上 | 本地批处理日志存储。嵌入于 Python 标准库，无需额外安装 |
| PyYAML | 6.0 及以上 | 用于读写分类映射配置文件和自定义标签覆盖文件 |
| Markdown | 3.4.0 及以上 | 用于生成结构化参考报告。输出兼容 GitHub 和 GitLab 风格 |
| Jinja2 | 3.1.0 及以上 | 用于 HTML 报告模板渲染。支持自定义主题覆盖 |
| pytest | 7.0.0 及以上 | 仅开发测试需要。生产部署可不安装 |
| black | 22.0.0 及以上 | 仅代码格式化需要。贡献者可选安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide/batch-ingestion.md | 如何创建新批次、添加单个链接、批量导入外部列表文件 |
| 用户指南 | docs/user-guide/validation-tunning.md | 如何调整超时参数、重试策略、并发数以及自定义验证规则 |
| 运维手册 | docs/operations/scheduled-validation.md | 如何部署定时校验任务、配置邮件告警、以及处理失效链接 |
| 运维手册 | docs/operations/static-export.md | 如何导出 HTML 报告、配置 CDN 部署、以及定制搜索过滤行为 |
| 开发参考 | docs/development/api-reference.md | 核心类 IngestionPipeline 和 ValidatorEngine 的方法签名与扩展点 |
| 开发参考 | docs/development/category-plugins.md | 如何编写自定义分类插件以支持新的域名模式或关键词规则 |
| 常见任务 | docs/how-to/rollback-batch.md | 如何撤销最近一次批次导入，并恢复之前的状态快照 |
| 常见任务 | docs/how-to/compare-batches.md | 如何生成两个批次之间的差异报告，比较新增、删除和变更链接 |

## 资源列表

### 当前批次资源（第 454/455 批）

本批次包含十项外部参考链接，已通过初步格式校验并进入验证队列。列表按原始输入顺序排列，保留完整的域名或协议形式。

<code>renqisiwazhongwenzimu.org.cn</code>

<code>guochanshoujiav.org.cn</code>

<code>shoujiavzhongwenzimu.org.cn</code>

<code>51mianfeichengrenshipinzaixianguankan.org.cn</code>

<code>yongjiumianfeibushoufeidewangzhanapp.org.cn</code>

<code>shenmafuliye.org.cn</code>

<code>chengrenxingshengjiaodaquanmian.org.cn</code>

<code>xieedongtai.org.cn</code>

<code>jiujiushoujishipin.org.cn</code>

<code>tiantiancaoyeyecao.org.cn</code>

## 项目结构

```
vastlink-core/
├── src/
│   └── vastlink/
│       ├── __init__.py               # 包初始化，暴露核心 API
│       ├── cli.py                    # 命令行入口，解析子命令参数
│       ├── ingest.py                 # 批次导入引擎，处理 URL 列表解析与入库
│       ├── validate.py               # 异步验证器，执行并发 HTTP 检查
│       ├── export.py                 # 导出器，支持 Markdown / HTML / JSON 输出
│       ├── categories.py             # 分类推断引擎，基于域名模式和关键词
│       ├── journal.py                # SQLite 日志接口，管理批次历史与回滚
│       └── utils.py                  # 通用工具函数（日期处理、字符串清洗）
├── tests/
│   ├── test_ingest.py                # 导入流程单元测试
│   ├── test_validate.py              # 验证器模拟测试（含 mock 响应）
│   └── fixtures/
│       └── sample_urls.txt           # 示例输入文件，用于集成测试
├── docs/
│   ├── user-guide/                   # 面向最终用户的指南文档
│   ├── operations/                   # 面向运维人员的部署与调度文档
│   ├── development/                  # 面向贡献者的 API 与插件开发文档
│   └── how-to/                       # 按场景划分的快速任务说明
├── templates/
│   ├── report.md.j2                  # Markdown 报告模板（Jinja2）
│   └── report.html.j2                # HTML 报告模板（含搜索过滤功能）
├── config/
│   ├── default.yaml                  # 默认配置（超时、并发、重试策略）
│   └── categories.yaml               # 分类规则映射（域名模式到标签）
├── requirements.txt                  # 生产依赖列表
├── requirements-dev.txt              # 开发与测试额外依赖
├── setup.py                          # 安装脚本，支持 pip install -e .
├── README.md                         # 项目主文档（本文件）
└── LICENSE                           # MIT 许可证文本
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** – 从主仓库 fork 副本，然后基于 main 分支创建以你的功能或修复命名的分支，例如 `feature/custom-export-template`。确保分支名称具有描述性。

2.  **编写或更新测试用例** – 所有新功能或对现有行为的修改必须包含对应的测试用例，位于 `tests/` 目录下。使用 pytest 框架编写测试，确保覆盖正常路径和异常路径。运行 `pytest tests/` 验证所有测试通过。

3.  **更新文档字符串和内联注释** – 公共函数、类和方法必须包含符合 PEP 257 标准的文档字符串。复杂逻辑部分添加内联注释，说明算法意图和边界条件。确保新增或修改的配置项在 `config/default.yaml` 中有对应注释。

4.  **提交变更并签署开发者原创声明** – 提交信息应遵循常规提交格式（类型和作用域），例如 `feat(export): add CSV output format`。在 PR 描述中确认你已阅读并同意开发者原创声明（Developer Certificate of Origin），表明你有权提交该代码。

5.  **发起 Pull Request 并等待审核** – 推送分支到你的远程仓库，然后向主仓库的 main 分支发起 PR。PR 标题应简明，描述部分需列出变更点、测试结果和文档更新情况。至少一位核心维护者审核通过后即可合并。

## 常见问题

**问：验证器是否支持内部网络或需要特定认证的端点？**

答：支持。你可以在 `config/default.yaml` 中配置自定义请求头部，例如 `Authorization` 或 `X-API-Key`。此外，可以通过 `--allow-private` 标志强制验证私有 IP 地址段。默认情况下，验证器会跳过私有和保留地址段以保证安全性。对于需要客户端证书的端点，可以扩展 `validate.py` 中的 `SSLContext` 配置。

**问：如何处理批次中某个 URL 失效或永久重定向的情况？**

答：验证器会记录响应的状态码和最终重定向目标。对于 301/302 状态码，系统会追踪最多五跳重定向链，并在报告中标记最终可达地址。对于 404 或超时错误，该条目被标记为 "unreachable" 状态。管理员可以通过 `--update` 参数将失效条目从当前批次移除，或使用 `--redirect-follow` 选项自动更新为最终的永久地址。所有变更均记录在 SQLite 日志中以便追溯。

**问：能否将 VastLink Navigator 作为定时任务自动运行？**

答：可以。项目提供了 `vastlink scheduled` 子命令，专为 cron 或 systemd timer 设计。该命令会读取预先配置的批次源文件列表，执行完整的导入、验证和导出流程，并将生成的报告输出到指定目录。结合 `--notify` 选项，可以在验证失败率达到阈值时发送邮件通知。参考 `docs/operations/scheduled-validation.md` 获得 systemd 单元文件示例和调度策略建议。

## 许可证

This project is licensed under the terms of the MIT License. See the LICENSE file for the full license text. The MIT License grants permission to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject to the following conditions: the above copyright notice and this permission notice shall be included in all copies or substantial portions of the software. The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:38
