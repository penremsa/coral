# NexusIndex

NexusIndex 是一个面向技术内容创作者、资源聚合站点运营者以及信息检索研究人员的轻量级外链资源导航框架。该项目定位于提供结构化、可维护、高可读性的外链资源清单管理方案，解决传统收藏夹或零散文档在组织大批量 URL 时缺乏版本控制、分类模糊、协作困难等核心痛点。NexusIndex 本身不存储任何第三方内容，也不提供代理或镜像服务，而是通过约定优于配置的 Markdown 工程化方案，帮助用户高效构建并发布自己的垂直领域资源门户。

目标用户包括开源文档维护者、技术社区运营人员、学术文献整理者以及任何需要定期维护大量外链资源列表的个人或团队。NexusIndex 将资源清单本身视为一等软件资产，借助 Git 工作流实现变更追踪、审核合并与自动化部署，从而将静态链接列表提升至可演进的工程制品层级。

## 功能概览

- **零依赖静态生成**：项目完全基于纯 Markdown 与 Shell 脚本构建，无需安装任何重型构建工具或前端框架，开箱即用。
- **分类多级目录体系**：支持按主题、地域、语种、文件类型等多维度创建无限层级的子目录，便于组织成千上万条外链资源。
- **自动链接健康检查**：内置定时检查脚本，可批量验证资源列表中各 URL 的可达性，并生成失效链接报告，便于及时清理或更新。
- **模板化条目注入**：提供标准化资源条目标记语法，支持批量导入、排序以及自定义元数据扩展（如添加备注、标签、维护人信息）。
- **变更历史可视化**：与 Git 提交日志深度集成，可通过标准 `git log` 命令追溯任意资源条目的添加、修改或删除时间点与作者信息。
- **多格式导出支持**：除 Markdown 视图外，提供脚本将资源列表转换为 JSON、CSV 或简单的 HTML 表格，便于嵌入其他系统或进行数据分析。
- **权限分级占位**：预留基于文件路径的权限声明占位机制，允许大型团队通过约定目录所有者来实现责任划分，避免资源冲突。

## 应用场景

- **技术文档站外链附录**：适用于开源项目文档中需要集中罗列参考链接、依赖官网、教程地址等外部资源的场景。维护者可将所有外链整理至 NexusIndex 管理的单一清单文件中，并在文档中通过固定锚点引用，确保链接变更时只需更新一处。
- **垂直领域资源周刊**：内容编辑或社区运营人员可利用 NexusIndex 按日期或主题创建每周资源汇总目录，配合 CI 流水线在每次推送后自动发布至静态页面托管服务，形成长期稳定的周报归档体系。
- **学术研究参考文献索引**：研究人员可将论文预印本、数据集地址、工具仓库、相关项目主页等数百条链接以结构化方式录入 NexusIndex，借助分类子目录按研究子课题分组，并利用链接健康检查定期验证预印本版本更新情况。
- **企业内部技术图谱登记**：企业架构团队可使用 NexusIndex 登记内部系统控制台地址、监控面板、日志接口、文档站点等关键内部资源，通过 Git 仓库权限控制访问范围，并结合变更历史审计资源信息的修改记录。

## 快速开始

以下命令演示如何在本地环境获取 NexusIndex 框架、安装辅助脚本并运行基础资源列表生成流程。

```bash
# 克隆项目框架
git clone https://github.com/nexusindex/nexusindex-starter.git nexusindex-workspace
cd nexusindex-workspace

# 安装本地脚本工具（将 bin/ 目录加入 PATH）
chmod +x bin/nexus
export PATH=$PWD/bin:$PATH

# 初始化资源索引并生成主清单
nexus init
nexus build --output ./docs/index.md
```

执行上述命令后，项目将在 `docs/` 目录下生成一份包含默认分类占位及示例条目的 Markdown 主清单文件。用户可直接编辑 `resources/` 目录下的各分类子文件，随后再次运行 `nexus build` 以合并生成最终完整清单。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.25 及以上 | 用于克隆仓库、提交变更以及查看历史记录 |
| Bash | 4.0 及以上 | 运行核心脚本 `nexus` 及各类辅助工具 |
| GNU Coreutils | 8.30 及以上 | 提供 `sort`、`uniq`、`date` 等基础命令支持 |
| curl | 7.68 及以上 | 用于链接健康检查脚本中的 HTTP 探测 |
| awk | 最新稳定版 | 用于解析和格式化资源条目元数据 |
| sed | 最新稳定版 | 用于流式编辑资源列表模板文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门 | `docs/quick-start.md` | 如何在 5 分钟内建立第一个资源清单，如何添加首条外链 |
| 操作 | `docs/category-management.md` | 如何新增、重命名或删除分类子目录，如何调整分类层级 |
| 进阶 | `docs/health-check.md` | 如何配置定时链接探测，如何阅读失效报告并批量替换旧域名 |
| 参考 | `docs/export-formats.md` | 支持哪些导出格式，如何定制 CSV 列顺序或 JSON 结构体字段 |
| 治理 | `docs/maintainer-handbook.md` | 多维护人场景下如何避免编辑冲突，如何定义目录所有权规则 |

## 资源列表

本项目中所有资源条目均来自用户原始输入，按类别整理如下。

通用影视资源类

- <code>gaoqingzhongwenzimudianshiju.org.cn</code>
- <code>zaixiangaoqingzhongwenzimu.org.cn</code>
- <code>zaixianguankanrihandianshiju.org.cn</code>
- <code>zhongwenzimuyingshigaoqing.org.cn</code>
- <code>gaoqingyingshimianfeiguankan.org.cn</code>
- <code>mianfeiguankangaoqingdianyingwz.org.cn</code>
- <code>zaixianshipinbofangpingtai.org.cn</code>
- <code>zaixianguankanmianfeiduanju.org.cn</code>
- <code>mianfeibofanggaopingzaixian.org.cn</code>
- <code>mianfeiguochangaoqingyingshi.org.cn</code>

## 项目结构

```text
nexusindex-workspace/
├── bin/                              # 可执行脚本目录
│   └── nexus                         # 主入口脚本，解析子命令 init/build/check
├── config/                           # 全局配置目录
│   ├── categories.toml               # 定义分类别名、排序权重与默认元数据模板
│   └── ignorelist.txt                # 健康检查时跳过的主机名或路径正则列表
├── resources/                        # 用户资源条目源文件目录
│   ├── video/                        # 影视类资源子目录（对应域名组）
│   │   ├── chinese-sub.md           # 中文字幕影视站点列表
│   │   ├── korean-jp.md             # 日韩剧集相关站点列表
│   │   └── free-hd.md               # 免费高清影视站点列表
│   ├── devtools/                    # 开发者工具类资源占位目录
│   │   └── ci-cd.md                 # CI/CD 相关链接占位文件
│   └── academic/                    # 学术文献类资源占位目录
│       └── preprints.md             # 预印本仓库链接占位文件
├── docs/                             # 构建输出的静态文档目录
│   ├── index.md                     # 主资源清单（由 nexus build 生成）
│   └── health-report-latest.txt     # 最近一次链接健康检查报告
├── templates/                        # Markdown 条目模板目录
│   ├── default.tmpl                 # 默认资源条目标记语法模板
│   └── csv-export.tmpl              # CSV 导出时的行格式模板
├── tests/                            # 单元测试与集成测试脚本目录
│   ├── test_parser.sh               # 测试资源条目解析器的正确性
│   └── test_health.sh               # 模拟健康检查场景的测试套件
└── README.md                         # 项目总体说明文件（当前文档）
```

## 贡献指南

1. **派生并克隆**：首先在 GitHub 上派生本仓库至个人账户，随后将派生仓库克隆至本地开发环境。请确保使用 SSH 协议克隆，以便后续推送变更。
2. **创建特性分支**：基于 `main` 分支创建一个新的特性分支，分支命名建议遵循 `feat/` 或 `fix/` 前缀，例如 `feat/add-japanese-drama-category`，以清晰表明变更意图。
3. **编辑资源文件**：根据变更目标，在 `resources/` 相应子目录下编辑或新增 `.md` 文件。所有资源条目必须遵循模板语法，包括 URL、标题、可选标签及备注字段。提交前请运行 `nexus build` 确保主清单能够正常生成。
4. **本地验证**：执行 `nexus check --local` 运行轻量级链接可达性测试，修复所有标记为失效或超时的条目。同时运行 `tests/` 目录下的核心测试脚本，确保未破坏既有解析逻辑。
5. **提交并推送**：编写符合 Conventional Commits 规范的提交信息，明确说明新增、修改或删除的资源条目数量及分类。推送分支至派生仓库后，通过 GitHub 界面发起 Pull Request 至主仓库的 `main` 分支，等待项目维护者审核合并。

## 常见问题

**问：如果某个外部资源域名已失效，我该如何处理？**

答：NexusIndex 提供的健康检查脚本会生成包含失效 URL 列表的报告。维护者应首先尝试搜索该站点是否已迁移至新域名，若确认完全停止服务，则需从资源文件中移除该条目，并在提交信息中注明关闭原因。若该站点为临时宕机，可在 `config/ignorelist.txt` 中临时添加该域名以跳过警告，并在后续检查中恢复。

**问：能否在资源列表中添加非 HTTP 协议链接，例如 FTP 或 SSH 地址？**

答：可以。NexusIndex 的解析器对 URL 协议部分不做强校验，仅要求条目符合基本的 URI 格式。但需注意，内置的链接健康检查模块仅支持 HTTP/HTTPS 探测，对于 FTP、SSH 或 `mailto:` 等协议，检查过程会自动跳过并记录为“未检测”，不会影响构建流程。

**问：如何将现有的大量收藏夹数据快速导入 NexusIndex？**

答：项目提供 `tools/import-bookmark.sh` 辅助脚本，支持解析常见浏览器导出的 HTML 书签文件（需为 Netscape 格式）。导入后脚本会根据书签文件夹名称自动分配至 `resources/` 下对应的分类子目录，并保留原始书签标题作为条目说明。对于 CSV 或 JSON 格式的收藏夹数据，建议先转换为标准书签格式再执行导入，或自行编写简单转换脚本。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
