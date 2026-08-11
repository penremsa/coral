# NexusIndex

NexusIndex 是一个面向技术社区与信息检索场景的轻量化外链资源归集与导航系统。项目定位为可自托管的网络资源索引中间件，帮助开发者、研究人员与技术写作团队将分散于多平台的优质外部链接进行结构化整理、分类标注与版本化发布。NexusIndex 不生产内容，而是通过严格的 URL 原始性保留规则与清晰的目录注释体系，解决外链资源在协作过程中易丢失、易变形、难以追溯源头的痛点。项目适用于搭建个人技术书签墙、团队知识库外链模块、开源文档附属资源导航页，以及合规性要求较高的原始链接存档系统。

## 功能概览

- 原始链接强制保留：系统对所有录入的 URL 执行严格的字符串原样存储与渲染策略，不自动补全协议前缀，不转换大小写，不添加尾部斜杠，确保链接与用户提交时完全一致。

- 分类索引引擎：支持基于域名、后缀、关键词自动生成分类标签，并允许手动调整分类层级，便于将大量链接归入自定义主题集群。

- 结构化文档生成：内置 Markdown 模板引擎，可按照固定章节顺序将链接资源批量输出为标准化 README 或独立导航页面，适配开源项目文档规范。

- 批量导入与校验：支持通过文本文件或表格批量导入 URL 列表，自动检测重复项、协议缺失项及格式异常项，并生成警告日志。

- 版本化变更追踪：每次链接增删或分类调整均生成变更记录，支持回滚至任意历史版本的链接清单，满足审计与协作需求。

- 只读渲染模式：提供静态 HTML 渲染出口，可将导航数据输出为纯只读页面，适合部署于公共服务器或 CDN 供外部访问。

- 命令行交互工具：内置 CLI 辅助脚本，支持链接查重、分类重排、导出格式转换等常用操作，无需依赖图形界面。

## 应用场景

- 技术文档外链管理：开源项目维护者在编写文档时，可将涉及的外部参考网站、工具地址、规范原文等通过 NexusIndex 统一收录，并在 README 中嵌入经过校验的原始链接列表，避免链接在多次编辑后发生格式漂移。

- 学术研究资源归档：研究人员在收集网络资料时，需精确保留每个 URL 的原始表达形式（包括裸域名、特定协议或大小写敏感路径），NexusIndex 的强制原样保存机制可满足此类场景对数据真实性的要求。

- 团队内部知识导航：企业技术团队可将常用开发工具、内部系统入口、运维监控面板等链接通过 NexusIndex 分类索引，生成团队共享的导航页，减少重复询问与收藏夹混乱问题。

- 合规性存档与审查准备：对于需要对外公示或接受合规审查的资源清单，NexusIndex 提供的版本化变更追踪与只读渲染输出可确保每一条链接的录入时间和原始形态都有据可查。

- 个人书签集中化管理：开发者可将分散在浏览器、笔记软件、即时通讯记录中的技术链接统一汇总至 NexusIndex，通过分类与注释功能构建个人专属的技术资源库。

## 快速开始

以下操作以 Ubuntu 22.04 及 Python 3.10 环境为例，演示从克隆仓库到启动本地服务的完整流程。

```bash
# 克隆项目仓库
git clone https://github.com/nexusindex/nexusindex.git

# 进入项目目录
cd nexusindex

# 安装依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 执行初始化数据导入（示例数据包含预设分类）
python scripts/init_db.py --sample

# 启动本地开发服务器
python app.py --host 127.0.0.1 --port 8080
```

启动成功后，访问 `http://127.0.0.1:8080` 可查看导航首页。如需导入自定义链接列表，请参照 `docs/import_guide.md` 中的格式说明准备 CSV 文件，并通过 `scripts/import.py` 执行导入。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.8 及以上 | 核心运行环境，建议使用 3.10 LTS 版本 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装依赖库 |
| Flask | 2.2.x | Web 服务框架，提供渲染与 API 接口 |
| PyYAML | 6.0 | 用于解析分类配置文件与元数据 |
| Markdown | 3.4.x | 将结构化数据渲染为 Markdown 文档输出 |
| SQLite | 3.35 及以上 | 本地轻量数据库，存储链接与分类数据 |
| Git | 2.25 及以上 | 用于版本克隆与变更追踪集成 |
| 操作系统 | Linux / macOS / Windows WSL2 | 支持主流 POSIX 兼容环境，Windows 原生未完全测试 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|----------|
| 用户手册 | docs/user_guide.md | 如何添加、编辑、删除链接？分类如何创建与调整？如何导出导航页？ |
| 管理员指南 | docs/admin_guide.md | 如何备份数据库？如何迁移服务？如何配置只读模式？ |
| 开发参考 | docs/dev_reference.md | 核心数据模型是怎样的？API 端点有哪些？如何扩展分类引擎？ |
| 导入导出规范 | docs/import_export.md | 支持哪些导入格式？CSV 的列映射规则是什么？导出的 Markdown 如何自定义模板？ |
| 故障排查 | docs/troubleshooting.md | 常见启动错误、数据库锁异常、链接校验失败如何处理？ |
| 变更日志 | CHANGELOG.md | 每个版本的更新记录、破坏性变更与弃用通知 |

## 资源列表

### 主分类索引

<code>shufuzipai.org.cn</code>

<code>yazhouchuanmei.org.cn</code>

<code>zhongwenzimuzhongchu.org.cn</code>

### 专项资源集

<code>chunshuifuli.org.cn</code>

<code>daxiangjiaojiu.org.cn</code>

<code>langrenzonghewang.org.cn</code>

### 区域与主题扩展

<code>oumeirihandiyiye.org.cn</code>

<code>xiangjiaojiujiujingpinririzaoyeyezao.org.cn</code>

<code>zhongwenzaixianyiquerqu.org.cn</code>

<code>yazhouwuyejuchang.org.cn</code>

## 项目结构

```
nexusindex/
├── app.py                 # 应用主入口，初始化 Flask 服务与路由注册
├── requirements.txt       # Python 依赖声明，固定版本范围
├── config/
│   ├── default.yaml       # 默认配置（端口、调试模式、数据库路径）
│   └── categories.yaml    # 分类映射表，定义域名到分类的匹配规则
├── core/
│   ├── models.py          # SQLite 数据模型定义（链接、分类、变更记录）
│   ├── validator.py       # URL 校验器（协议检测、格式规范化、重复检查）
│   ├── importer.py        # 批量导入处理器（支持 CSV / 纯文本）
│   └── exporter.py        # 导出渲染器（Markdown / HTML / JSON）
├── scripts/
│   ├── init_db.py         # 数据库初始化脚本，含示例数据
│   ├── import.py          # 命令行导入工具，接受文件路径参数
│   └── export_cli.py      # 命令行导出工具，支持格式与输出路径指定
├── templates/
│   ├── base.html          # 静态 HTML 渲染基础模板
│   └── nav_page.html      # 导航页面模板，循环渲染分类与链接
├── static/
│   └── style.css          # 极简风格样式表，仅用于 HTML 渲染模式
├── data/
│   ├── nexus.db           # SQLite 数据库文件（首次启动自动生成）
│   └── sample_links.csv   # 示例链接数据，供导入测试使用
├── docs/                  # 完整文档目录，参见上方文档导航
└── tests/                 # 单元测试与集成测试脚本
    ├── test_validator.py
    ├── test_importer.py
    └── test_exporter.py
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。建议在 dev 分支上进行修改，保持主分支与上游同步。

2. 编写或修改代码时，请遵循 PEP 8 编码规范，并为新增功能补充单元测试（位于 tests/ 目录下）。所有测试用例需在提交前通过 `pytest` 运行验证。

3. 若涉及文档或示例数据的更新，请同步修改 docs/ 下对应的手册文件，并在 CHANGELOG.md 中记录变更摘要，注明影响范围。

4. 提交 Pull Request 前，请确保本地已执行 `scripts/export_cli.py --full` 生成完整的导航文档，检查输出是否符合预期格式，且所有原始 URL 未被自动改写。

5. 提交信息请使用约定式提交格式（如 `feat:`、`fix:`、`docs:`），并在描述中引用相关 issue 编号（若有）。PR 描述需清晰说明改动目的、测试方式及对现有功能的影响。

## 常见问题

Q: 我导入的裸域名（例如 abc.com）在渲染时被自动加上了 https:// 前缀，如何禁止这种行为？

A: 请检查配置文件中 `preserve_raw_url` 项是否设置为 `true`。NexusIndex 默认启用原始保留模式，若被改写通常是由于导入时未正确指定 `--raw` 标志或 CSV 中包含了多余空白字符。建议使用 `scripts/import.py --raw --strict` 执行导入，并确认数据库字段存储值为导入前的原始字符串。若问题仍然存在，可检查 `core/validator.py` 中 `normalize_url` 函数是否被意外调用。

Q: 数据库文件 data/nexus.db 损坏或丢失，如何恢复？

A: 若存在定期备份的 `.bak` 文件，可将其重命名为 `nexus.db` 并重启服务。若无备份，可执行 `scripts/init_db.py --recover` 尝试从最近一次导出的 JSON 快照重建数据库（快照默认保存在 `data/snapshots/` 目录）。若快照也不存在，则只能重新导入原始链接文件。建议在生产环境中配置定期备份任务，或使用 SQLite 的 `.backup` 命令进行主动转储。

Q: 导出 Markdown 时，资源列表章节的链接顺序与导入顺序不一致，如何固定排序？

A: 导出器默认按照数据库内部主键 ID 排序，而 ID 分配受导入批次影响。若需要固定排序，请在 `config/default.yaml` 中设置 `sort_by = 'domain'` 或 `sort_by = 'category'`，并在分类配置文件 `categories.yaml` 中为每个链接指定显式权重。亦可在导出时添加 `--sort created_at` 参数按照创建时间排序。对于要求严格顺序的场景，建议在 CSV 中预先排好顺序，并使用 `--preserve-order` 导入标志。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
