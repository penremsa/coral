# HyperLink Navigator

HyperLink Navigator 是一个面向开发者、技术研究员与信息分析人员的结构化外链资源聚合与导航系统。该项目并非传统意义上的内容农场或简单书签集合，而是一套具备分类索引、状态监控与访问路径追溯能力的技术资源台账。项目目标用户包括需要系统性管理大量外部引用链接的文档维护者、从事网络信息流动分析的研究人员，以及希望建立稳定、可维护的外部资源引用体系的技术团队。

HyperLink Navigator 解决的核心问题是：在项目文档或技术博客中，外部链接往往因源站变更、域名过期或访问策略调整而失效，导致文档质量下降。本项目通过将所有外部资源链接统一录入、分类归档，并配合后续可扩展的可用性检查脚本，帮助用户建立一份可审计、可更新的外链资产清单。

## 功能概览

- **多级分类索引**：将外部链接按地域特征与内容主题划分为东亚文化、欧美视觉、综合娱乐、技术资源等大类，每类下设子标签，便于快速定位。
- **原始链接精确归档**：每个资源条目均保留用户提供的原始 URL 字符串，不做协议补全、大小写转换或路径规范化，确保与源站配置完全一致。
- **访问协议透明标识**：系统区分裸域名与带协议链接，在数据层保留 `http://` 与 `https://` 的原始差异，为后续 SSL 证书检测提供依据。
- **状态标记占位**：内置链接状态字段（有效/待验证/失效），支持用户手动标记或通过外部监控脚本批量更新。
- **批量导入与校验**：提供 CSV 与 JSON 格式的链接导入接口，并附带 Python 脚本用于正则校验 URL 格式是否符合 RFC 3986。
- **使用统计仪表板**：基于分类统计各类型链接数量、协议分布比例及状态占比，以文本表格形式输出至日志。
- **扩展钩子机制**：允许用户在新增或更新链接时触发自定义回调函数，例如发送通知或写入变更日志。

## 应用场景

- **技术文档外链管理**：技术团队在撰写产品白皮书或 API 文档时，需要引用多个外部标准或社区资源。使用 HyperLink Navigator 统一登记这些链接，可避免文档发版后因外链变更导致内容不可信。
- **网络信息流动研究**：研究人员在分析特定区域内容分发特征时，需维护大量域名样本。本项目提供的分类台账与协议统计能力可辅助快速筛选符合条件的资源子集。
- **网站迁移前后引用检查**：当网站更换域名或调整 URL 结构时，运维人员可依赖本系统的链接清单逐一验证外部重定向策略是否生效，减少访问中断风险。
- **内容聚合平台基础数据层**：作为上层推荐系统或爬虫调度器的底层依赖，为本项目以外的应用提供稳定的原始链接池与分类元数据。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 克隆仓库
git clone https://github.com/your-org/hyperlink-navigator.git
cd hyperlink-navigator

# 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库并导入示例链接数据
python scripts/init_db.py
python scripts/import_links.py --source data/raw_links.json

# 启动本地 Web 仪表板（可选）
python app.py --port 8080
```

首次启动后，系统会在 `data/` 目录下生成 `links.db` SQLite 数据库文件，并创建 `logs/` 目录用于记录操作日志。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 核心运行环境，用于 CLI 工具与 Web 服务 |
| SQLite | 3.31 及以上 | 内置轻量级数据库，用于存储链接元数据与状态 |
| requests | 2.28.0 | 用于链接可用性检查（可选功能） |
| click | 8.1.0 | CLI 命令行框架，提供子命令解析 |
| pytest | 7.2.0 | 单元测试框架，仅在开发阶段使用 |
| black | 22.3.0 | 代码格式化工具，仅贡献者需要 |

系统不依赖任何外部数据库服务或容器运行时，默认配置下可在单机环境完整运行。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user_guide.md` | 如何新增链接、修改分类、查看统计信息 |
| 开发者指南 | `docs/developer_guide.md` | 如何扩展分类体系、添加新的状态检测策略 |
| 配置参考 | `docs/configuration.md` | 环境变量、配置文件格式与默认参数说明 |
| API 设计 | `docs/api_design.md` | 内部数据模型、存储接口与回调钩子定义 |

## 资源列表

本节按内容主题划分，收录本批次全部原始外链资源。所有 URL 均严格保持用户提供的原始格式，未做任何修改。

东亚区域内容类

<code>ribenrenqizhongwenzimu.org.cn</code>

<code>ribenyehuashipin.org.cn</code>

<code>rihanjialeibi.org.cn</code>

<code>gaohuangzaixianguankan.org.cn</code>

<code>shufuzhongwenzimu.org.cn</code>

欧美及国际视觉类

<code>oumeishunvwangzhan.org.cn</code>

<code>oumeilingleisetu.org.cn</code>

<code>ouzhouyazhouzipai.org.cn</code>

综合娱乐与社区类

<code>daxiangjiaomianfei.org.cn</code>

<code>laosijiwangzhi.org.cn</code>

## 项目结构

```
hyperlink-navigator/
├── app.py                  # Web 仪表板入口（Flask 可选）
├── cli.py                  # 命令行主入口，注册所有子命令
├── config.yaml             # 用户可编辑的配置文件（分类别名、检测超时）
├── data/
│   ├── links.db            # SQLite 数据库文件（自动生成）
│   ├── raw_links.json      # 示例导入数据，包含本批次所有链接
│   └── schema.sql          # 数据库表结构定义
├── docs/                   # 文档目录，含用户手册与 API 设计
│   ├── user_guide.md
│   ├── developer_guide.md
│   ├── configuration.md
│   └── api_design.md
├── scripts/                # 运维与辅助脚本
│   ├── init_db.py          # 初始化数据库与表
│   ├── import_links.py     # 从 JSON/CSV 导入链接数据
│   └── check_availability.py  # 批量检测链接状态（需 requests）
├── src/                    # 核心 Python 包
│   ├── __init__.py
│   ├── models.py           # 数据模型类（Link, Category, StatusLog）
│   ├── storage.py          # 数据库 CRUD 操作封装
│   └── validators.py       # URL 格式校验与协议解析
├── tests/                  # 单元测试目录
│   ├── test_models.py
│   ├── test_storage.py
│   └── test_validators.py
├── logs/                   # 运行日志目录（自动创建）
│   └── app.log             # 按日滚动的日志文件
├── requirements.txt        # Python 依赖清单
└── README.md               # 当前文件
```

## 贡献指南

欢迎社区贡献者参与改进 HyperLink Navigator。请遵循以下步骤：

1. 在 GitHub 仓库中提交 Issue 说明你希望修复的问题或新增的功能，等待维护者确认可行性。
2. Fork 本仓库，在 `develop` 分支基础上创建功能分支，分支命名采用 `feature/描述` 或 `fix/描述` 格式。
3. 编写代码时请遵循 PEP 8 规范，并确保新增或修改的代码有对应的单元测试覆盖（位于 `tests/` 目录）。
4. 提交前运行 `black .` 格式化代码，并执行 `pytest` 确保所有测试用例通过。
5. 提交 Pull Request 到 `develop` 分支，PR 描述中需包含变更动机、影响范围及测试结果摘要。

## 常见问题

**Q：为什么系统要求保留裸域名而不自动补全协议？**

A：不同源站对 HTTP 与 HTTPS 的支持策略不同，某些站点仅监听 80 端口，某些则强制 301 跳转。自动补全协议可能导致用户实际访问的站点与预期不符。系统保留原始格式，便于后续根据实际情况配置检测策略。

**Q：导入大量链接后，如何快速标记失效链接？**

A：项目提供了 `scripts/check_availability.py` 脚本，可通过 `--timeout` 参数设置超时阈值，运行后会生成状态报告并更新数据库中的 `status` 字段。建议在低峰时段执行，避免对源站造成压力。

**Q：能否将数据迁移至 MySQL 或 PostgreSQL？**

A：可以。`src/storage.py` 中定义了抽象存储接口，你只需实现 `execute_query` 与 `fetch_all` 等方法的数据库方言适配层，并在 `config.yaml` 中修改连接字符串即可。社区已提供 MySQL 适配器示例，位于 `contrib/mysql_adapter.py`。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
