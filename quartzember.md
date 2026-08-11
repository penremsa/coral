# Terminus Navigator

Terminus Navigator 是一个面向技术研究者与内容聚合者的外链资源导航与元数据检索系统。该项目定位于解决海量分散域名资源的结构化管理与快速访问问题，尤其适用于需要频繁查阅特定领域在线资源的技术人员、内容策展人或数据标注团队。通过本项目提供的结构化索引与本地检索界面，用户可以在无需依赖外部搜索引擎的情况下，直接从本地环境定位并访问预先整理的高价值外部链接，极大缩短信息查找路径。

本项目并非一个在线导航站点，而是一个基于静态 Markdown 与本地脚本的轻量级资源管理工具。其核心价值在于将无序的 URL 集合转化为带有分类标签、场景说明与依赖约束的可维护知识库。项目附带自动化链接可用性检查脚本与元数据提取工具，帮助用户持续监控资源状态，确保收藏链接长期有效且可追溯。

## 功能概览

- **多层级资源分类体系**：支持按地域、语言、内容类型与主题对链接进行多维度标签化分类，便于快速筛选与批量操作。
- **本地化检索与过滤界面**：基于命令行工具提供关键词搜索与正则过滤功能，无需数据库即可实现毫秒级响应。
- **链接健康状态监测**：内置异步 HTTP 探测模块，定期检查每个 URL 的可达性与响应状态码，并生成健康报告。
- **元数据自动补全**：支持从目标页面解析标题、描述与关键词，自动填充资源清单中的缺失字段。
- **批量导入与导出机制**：支持 CSV 与 JSON 格式的链接批量导入，并可导出为标准 Markdown 报告或结构化 YAML 配置。
- **变更历史记录**：所有增删改操作均记录至本地变更日志，便于多人协作时追踪资源变动。
- **自定义标签与备注**：每条资源可附带自定义标签与多行备注，支持富文本格式存储于元数据文件中。

## 应用场景

- **技术文档聚合与维护**：技术团队可使用 Terminus Navigator 集中管理分散在多个外部站点上的 API 文档、规范草案与社区讨论帖，通过标签快速定位特定技术栈的相关资源，并在团队成员间同步链接变更状态。
- **数据标注源站管理**：数据标注团队可利用本工具维护一批固定的数据采集源站列表，通过健康监测功能定期确认各源站可用性，当某源站响应异常时，系统将自动标记并通知负责人，避免标注任务中断。
- **个人知识库外链整理**：独立研究员或技术博主可将长期积累的参考链接导入本系统，按照项目或主题分类，配合检索功能快速回溯早期参考过的资料，同时利用备注字段记录阅读心得与引用要点。
- **内容合规审查辅助**：内容审核团队可将待审查的域名列表纳入本系统，通过批量导出功能生成审查报告，并结合自定义标签区分已审、待审与异常状态，提升流程透明度。

## 快速开始

以下步骤将引导您在本地环境完成 Terminus Navigator 的克隆、依赖安装与首次运行。

```bash
# 克隆仓库至本地
git clone https://github.com/terminus-navigator/terminus-navigator.git
cd terminus-navigator

# 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 运行资源索引构建脚本
python build_index.py --input data/urls.yaml --output dist/index.json

# 启动本地命令行检索工具
python cli.py search --tag "video"
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心脚本运行环境，用于执行索引构建、健康检查与检索逻辑 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装 requirements.txt 中列出的第三方库 |
| Git | 2.25 及以上 | 版本控制工具，用于克隆仓库及后续更新同步 |
| aiohttp | 3.8.4 及以上 | 异步 HTTP 客户端库，用于并发链接健康检测 |
| pyyaml | 6.0 及以上 | YAML 格式解析库，用于读取资源分类配置文件 |
| pandas | 1.5.0 及以上 | 可选依赖，用于 CSV 格式批量导入导出时的数据处理 |
| tabulate | 0.9.0 及以上 | 可选依赖，用于命令行下以表格形式展示检索结果 |
| pytest | 7.2.0 及以上 | 开发依赖，用于运行单元测试与集成测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide/quick-start.md | 如何快速上手使用检索、添加与导出功能 |
| 配置参考 | docs/config/schema.md | 资源分类 YAML 文件的完整字段定义与示例 |
| 开发文档 | docs/developer/api-design.md | 核心模块的接口设计、事件钩子与扩展点说明 |
| 运维手册 | docs/ops/health-check.md | 如何部署健康监测定时任务与解读报告指标 |
| 结构说明 | docs/architecture/data-flow.md | 数据从输入到检索展示的完整流转路径与缓存策略 |
| 贡献指引 | CONTRIBUTING.md | 外部贡献者如何参与分支管理、提交代码与审阅流程 |

## 资源列表

本列表收录 Terminus Navigator 默认资源索引中包含的全部外部链接。所有链接均按内容类别分组，并严格保持用户提供的原始格式。

视频资源类

<code>guochangaoqingshipinzaixian.org.cn</code>
<code>guochangaoqingshipinguankan.org.cn</code>
<code>rimanzaixianmianfeiguankan.org.cn</code>
<code>zhongwenzimumianfeibofang.org.cn</code>
<code>zaixianzimumianfeiguankan.org.cn</code>
<code>zaixianzimuguankanmianfei.org.cn</code>
<code>zaixianzimugaoqingdianshiju.org.cn</code>
<code>mianfeishipinwangzhanzaixianguankan.org.cn</code>
<code>rihanzaixianmianfeishipinw.org.cn</code>
<code>oumeizaixianmianfeishipinw.org.cn</code>

## 项目结构

```
terminus-navigator/
├── cli.py                      # 命令行入口，包含 search / add / check 子命令
├── build_index.py              # 索引构建脚本，将 YAML 编译为 JSON 检索文件
├── requirements.txt            # 核心与可选依赖列表
├── config/
│   ├── settings.yaml           # 全局配置（超时、重试、缓存路径等）
│   ├── categories.yaml         # 分类层级定义与颜色映射
│   └── schema/                 # YAML 格式校验 JSON Schema 文件
├── data/
│   ├── urls.yaml               # 主资源索引文件，包含所有链接及元数据
│   ├── urls.archive.yaml       # 历史版本备份，每次变更自动生成
│   └── tags.yaml               # 标签库及同义词映射
├── src/
│   ├── fetcher/                # 异步 HTTP 探测模块
│   │   ├── client.py           # aiohttp 会话封装与重试逻辑
│   │   └── parser.py           # 元数据解析（标题/描述抽取）
│   ├── indexer/                # 索引构建与查询模块
│   │   ├── builder.py          # 从 YAML 构建倒排索引
│   │   └── query.py            # 布尔查询与正则过滤实现
│   ├── exporter/               # 导出模块（Markdown / JSON / CSV）
│   │   ├── md_renderer.py      # 将结果渲染为 Markdown 表格
│   │   └── csv_writer.py       # 批量写入 CSV 格式
│   └── utils/                  # 通用工具函数
│       ├── logger.py           # 日志配置与轮转
│       └── validator.py        # URL 规范化与格式校验
├── tests/
│   ├── unit/                   # 单元测试（pytest 用例）
│   └── fixtures/               # 测试用样本 YAML 与预期 JSON
├── dist/                       # 构建输出目录（索引文件存放处）
│   └── index.json              # 最终可加载检索文件
├── logs/                       # 运行日志存储目录（按天轮转）
│   └── navigator.log           # 当前活跃日志
└── docs/                       # 完整文档目录（参见文档导航章节）
```

## 贡献指南

1. 复刻本仓库至个人账号，并在本地新建功能分支（命名建议：feature/功能简述 或 fix/问题编号），确保分支基于最新的 main 分支。
2. 在 data/urls.yaml 中按现有格式添加或修改资源条目，同时更新对应的分类标签与备注字段。若涉及架构或脚本变更，需同步更新 docs/ 下对应技术文档。
3. 在 tests/unit/ 目录下为新增功能或修复补丁编写对应的单元测试用例，确保全部已有测试通过后方可提交。
4. 提交变更时请遵循语义化提交规范（如 feat: 增加批量导入CSV支持），并附上清晰的变更说明。推送至个人复刻仓库后，发起 Pull Request 至主仓库的 main 分支。
5. 项目维护者将在 3 个工作日内进行 Code Review，如有修改意见将通过 PR 评论反馈。合并后您的变更将自动纳入下一版本发布计划。

## 常见问题

**Q：索引构建失败，提示 YAML 解析错误，如何定位问题？**

A：请检查 data/urls.yaml 文件是否存在缩进不一致或冒号后缺少空格的问题。推荐使用支持 YAML 语法高亮的编辑器（如 VS Code 搭配 YAML 插件）进行编辑。也可运行 `python -c "import yaml; yaml.safe_load(open('data/urls.yaml'))"` 快速验证语法正确性。若仍无法解决，请查看 logs/navigator.log 获取详细堆栈信息。

**Q：健康检测脚本显示大量超时，但浏览器可以正常访问这些链接，为什么？**

A：这通常是由于目标服务器对非浏览器 User-Agent 头部做了限制或限流。您可以在 config/settings.yaml 中调整 fetcher.user_agent 字段为常用浏览器 UA 字符串，并适当增大 fetcher.timeout 与 fetcher.delay 参数以降低并发频率。另外，请确认本机网络环境允许访问这些域名，部分网络策略可能拦截脚本发起的批量请求。

**Q：如何将个人收藏的链接批量导入系统？**

A：您可以使用 `python cli.py import --format csv --path bookmarks.csv` 命令，CSV 文件需包含 url, title, tags, note 四列（标题与备注可为空）。导入前请使用 `python cli.py validate --file bookmarks.csv` 进行格式预检。导入成功后，系统会自动合并至 data/urls.yaml 并触发索引重建。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
