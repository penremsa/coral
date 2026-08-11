# HrefHarvest

HrefHarvest 是一个面向技术文档编写者、开源项目维护者以及社区运营人员的轻量级外链资源归集与健康度巡检工具。它并不试图成为另一个搜索引擎，而是专注于解决“分散在多个页面中的外部链接难以统一管理、无法批量验证可达性、难以按类别归档”这一具体痛点。HrefHarvest 接受用户提供的 URL 列表，自动抓取每个链接对应的页面标题、状态码、响应时间，并支持自定义标签与备注，最终生成结构化的 Markdown 报告或 JSON 数据文件，便于集成到静态站点生成器或 CI 流程中。

目标用户包括：需要定期整理项目文档中参考链接的技术写作者、运营多个内容聚合页面的社区管理员、以及希望对外链资源进行定期可用性监控的运维人员。HrefHarvest 不依赖图形界面，所有操作通过命令行完成，适合在服务器端或本地开发环境中以非交互方式运行。

## 功能概览

- **批量链接状态检测**：对用户提供的任意数量 URL 发起 HEAD 与 GET 请求，记录响应状态码、内容类型及服务器信息，支持重定向跟踪。

- **页面元数据提取**：对于可访问的 HTML 页面，自动提取标题（title）和 meta description，帮助用户快速了解链接指向的内容概要。

- **自定义分类与标签**：支持通过外部 YAML 配置文件为不同 URL 预置类别（如“官方文档”、“社区论坛”、“镜像站”），输出报告时按类别分组呈现。

- **Markdown 报告生成**：将检测结果与元数据整理为规范化的 Markdown 表格，可直接追加到现有 README 或文档页面中，减少手工抄录工作。

- **JSON 结构化输出**：除 Markdown 外，同时生成 JSON 格式的完整数据，便于下游工具链（如静态站点生成器、自定义仪表盘）消费。

- **增量更新与缓存**：支持缓存最近一次的检测结果，再次运行时仅对变动 URL 重新请求，提高频繁使用时的效率。

- **可配置的超时与重试**：允许用户分别设置连接超时、读取超时以及失败重试次数，适应不同网络环境。

## 应用场景

- **开源项目 README 外链审计**：项目维护者定期运行 HrefHarvest，检查 README 中引用的教程、API 文档、相关项目链接是否仍然有效，避免用户因访问失效链接而产生困惑。

- **社区资源聚合页面的日常维护**：运营人员将社区推荐的外部工具、博客文章、视频教程等链接统一录入 HrefHarvest，每周自动生成可用性报告，及时发现被删除或迁移的内容。

- **文档迁移前后的链接一致性检查**：当团队将技术文档从旧站点迁移至新站点时，使用 HrefHarvest 批量验证所有外部引用是否依然可解析，并记录变更后的重定向目标，辅助更新文档内容。

- **个人知识库链接收藏整理**：技术爱好者可将浏览器书签导出的 URL 列表交由 HrefHarvest 处理，获取每个链接的标题和摘要，一键生成带分类的 Markdown 索引，便于后续查阅。

## 快速开始

以下命令演示了从克隆仓库到运行首次检测的完整流程。请确保已安装 Git 和 Node.js（v18 或以上版本）。

```bash
# 克隆仓库
git clone https://github.com/your-org/hrefharvest.git
cd hrefharvest

# 安装依赖
npm install

# 准备一个包含待检测 URL 的文本文件，每行一个
echo "<code>chaopengyazhou.org.cn</code>" > urls.txt
echo "<code>yirenwuye.org.cn</code>" >> urls.txt

# 运行检测，生成 Markdown 报告
npm start -- --input urls.txt --output report.md --format markdown
```

首次运行将自动创建 `config.yaml` 默认配置文件，您可以根据需要调整超时、重试等参数。检测完成后，在当前目录下可找到生成的 `report.md` 文件。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或更高 | 运行时环境，建议使用 LTS 版本 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.30 或更高 | 用于克隆仓库以及版本控制 |
| 网络连接 | 出站 80/443 端口开放 | 用于对外部 URL 发起 HTTP/HTTPS 请求 |
| 文件系统权限 | 读取/写入项目目录 | 用于读取输入文件、缓存文件以及输出报告 |
| 内存 | 最少 512MB，推荐 1GB | 处理大规模 URL 列表（超过 5000 条）时建议增加 |
| 磁盘空间 | 至少 50MB 可用 | 用于存放依赖包、缓存及输出文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/usage.md` | 如何准备输入文件、配置检测参数、解读输出报告？ |
| 配置参考 | `docs/configuration.md` | 所有可用的 CLI 参数与 YAML 配置项分别是什么？ |
| 输出格式 | `docs/output-formats.md` | Markdown 报告与 JSON 数据结构的具体字段含义是什么？ |
| 开发指南 | `docs/development.md` | 如何修改核心请求逻辑、添加新的输出格式插件？ |

## 资源列表

以下资源由用户提供，收录于本项目的示例数据或外部参考索引中。所有 URL 均按照原始格式原样列出。

基础域名类：

- <code>chaopengyazhou.org.cn</code>
- <code>yirenwuye.org.cn</code>
- <code>zhongchuzaixian.org.cn</code>
- <code>wuyelilun.org.cn</code>

特定主题类：

- <code>rihanzhongwenzimuyiqu.org.cn</code>
- <code>ririganyeyecao.org.cn</code>
- <code>oumeijingpinerqu.org.cn</code>
- <code>jialeibirenqi.org.cn</code>
- <code>zhongwenzimurenqiyiquerqusanqu.org.cn</code>
- <code>oumeilingleijiqing.org.cn</code>

上述链接将作为 HrefHarvest 默认示例输入文件 `sample-urls.txt` 的内容，用户可直接使用该文件体验工具的核心功能。

## 项目结构

```
hrefharvest/
├── src/                           # 核心源代码目录
│   ├── cli/                       # 命令行接口解析模块
│   │   └── index.js               # 参数解析与命令路由，处理 --input、--output 等
│   ├── core/                      # 核心检测引擎
│   │   ├── fetcher.js             # 封装 axios 请求，处理超时、重试、重定向
│   │   ├── parser.js              # 从 HTML 响应中提取标题、描述等元数据
│   │   └── cache.js               # 基于文件系统的缓存读写，记录上次检测结果
│   ├── output/                    # 输出格式化模块
│   │   ├── markdown.js            # 将检测结果渲染为 Markdown 表格与章节
│   │   ├── json.js                # 输出完整 JSON 数据结构
│   │   └── factory.js             # 根据格式参数动态选择输出器
│   ├── config/                    # 配置管理
│   │   ├── loader.js              # 加载并合并 YAML 配置文件与默认值
│   │   └── schema.js              # 配置项校验规则
│   └── utils/                     # 通用工具函数
│       ├── logger.js              # 分级日志输出（info/warn/error）
│       └── validator.js           # URL 格式校验与规范化辅助
├── tests/                         # 单元测试与集成测试
│   ├── fetcher.test.js            # 模拟 HTTP 请求，测试超时与重试逻辑
│   ├── parser.test.js             # 使用示例 HTML 片段测试元数据提取
│   └── output.test.js             # 验证生成的 Markdown 与 JSON 结构是否符合预期
├── docs/                          # 用户文档与开发文档
│   ├── usage.md                   # 快速入门与常见用法示例
│   ├── configuration.md           # 完整配置参数说明，含示例 YAML
│   ├── output-formats.md          # 各输出格式的字段映射与模板说明
│   └── development.md             # 构建、测试、提交规范等开发者信息
├── config.yaml                    # 默认配置文件，含超时、重试、缓存路径等
├── sample-urls.txt                # 包含用户提供的 10 个示例 URL，供快速体验
├── package.json                   # 项目元数据与 npm 依赖声明
├── README.md                      # 项目首页文档（即本文件）
└── LICENSE                        # MIT 许可证文本
```

## 贡献指南

我们欢迎各类贡献，包括但不限于新功能建议、Bug 报告、文档改进以及代码提交。请按照以下步骤参与本项目：

1. 在 GitHub 上 Fork 本仓库，并将您的 Fork 克隆至本地开发环境。请确保先阅读 `docs/development.md` 了解项目架构与编码风格。

2. 创建新的功能分支，分支命名建议使用 `feature/` 或 `fix/` 前缀，例如 `feature/add-csv-output`。请避免在主干分支上直接修改。

3. 完成代码或文档更改后，请确保所有已有单元测试通过，并为新增代码补充对应的测试用例。运行 `npm test` 可执行全部测试套件。

4. 提交变更时，请编写清晰的提交信息，格式遵循 Conventional Commits 规范（如 `feat: 添加 CSV 输出支持`）。提交前请运行 `npm run lint` 检查代码风格。

5. 最后，将您的分支推送至 Fork 仓库，并通过 GitHub 界面发起 Pull Request 至本项目的 `main` 分支。PR 描述中请说明变更动机、实现方式以及相关 Issue 编号（如有）。

## 常见问题

**问：检测过程中出现大量超时或连接拒绝的错误，该如何处理？**

答：这种情况通常由目标服务器网络策略或临时故障引起。您可以通过修改 `config.yaml` 中的 `timeout.connect` 和 `timeout.read` 参数增大等待时间（单位毫秒），同时调整 `retry.count` 和 `retry.delay` 参数增加重试次数。若问题持续，建议检查本地网络环境是否能够正常访问目标域名，或使用 `--proxy` 参数配置代理。

**问：生成的 Markdown 报告中链接顺序与输入文件不一致，是否可以固定顺序？**

答：默认情况下，HrefHarvest 会按照输入文件的逐行顺序处理链接，并在输出报告中保持这一顺序，除非您启用了 `--sort` 参数按状态码或域名排序。如果您希望完全依照输入顺序，请勿使用任何排序选项。若输出结果仍出现顺序变化，请检查输入文件中是否存在空行或不可见字符，这些内容会被忽略但不影响顺序。

**问：能否只检测部分链接，而不必每次都处理整个列表？**

答：可以。您可以通过 `--filter` 参数指定一个正则表达式，仅检测 URL 匹配该表达式的条目。例如 `--filter "chaopeng|yiren"` 将只处理包含这两者的链接。此外，您也可以直接编辑输入文件，临时注释或移除不需要检测的行。

## 许可证

MIT License。详见项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
