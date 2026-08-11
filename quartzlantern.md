# Yunzhi Resource Hub

Yunzhi Resource Hub is a lightweight, developer-oriented external resource aggregation and navigation system designed for technical teams, content researchers, and digital archivists who need to systematically catalog, validate, and present curated external links across multiple functional domains. Unlike general-purpose bookmark managers or social-style link collections, Yunzhi Hub focuses on structural clarity, availability monitoring, and batch lifecycle management — making it suitable for integration into internal dashboards, documentation portals, or knowledge-base pipelines.

The project targets maintainers who handle high-volume external reference collections (e.g., regulatory mirrors, regional content repositories, multilingual media indexes) and require a reproducible, scriptable framework to organize, annotate, and distribute these resources without vendor lock-in. Yunzhi Hub does not host or proxy any third-party content; it provides only metadata, classification schemas, and status-checking routines to help teams make informed decisions about external dependency usage.

## 功能概览

- **Bulk URL Import and Validation** – Accepts plain-text or CSV-based link lists, performs initial reachability and protocol compliance checks, and flags malformed or unreachable entries with detailed error logs.

- **Multi-Dimensional Categorization** – Supports custom tags, regional labels, content-type markers, and lifecycle states (active, deprecated, under-review) to enable flexible filtering and reporting.

- **Automated Availability Monitoring** – Scheduled health checks (HTTP HEAD/GET with configurable timeouts and retry policies) record response times, status codes, and SSL certificate expiry, with alert hooks for critical failures.

- **Static Site Generation Mode** – Renders the curated link set as a fully static, mobile-friendly HTML dashboard with search, sorting, and quick-copy functions, suitable for GitHub Pages or any static hosting.

- **Markdown-Based Maintenance Interface** – All resource entries are stored as human-editable Markdown files with YAML frontmatter, enabling version control, peer review, and offline editing without a database.

- **Export Adapters** – Outputs the active collection in JSON, CSV, and HTML table formats, with customizable field selectors for integration into external reporting or data visualization tools.

- **Audit Trail and Change Logging** – Tracks every addition, removal, or metadata update with timestamps and optional author attribution, simplifying compliance and rollback scenarios.

## 应用场景

- **Internal Technical Reference Portal** – Development teams can maintain a curated list of external SDK mirrors, API documentation sites, and package registry fallbacks, with automatic dead-link detection to reduce build pipeline failures caused by unreachable dependencies.

- **Content Curation for Regional Research** – Analysts studying regional digital content distribution can organize large sets of domain samples by geographic origin, content category, and accessibility patterns, using the monitoring module to gather baseline availability metrics over time.

- **Documentation Sidebar for Multi-Site Systems** – Projects that reference external resources across multiple subdomains or partner sites can embed Yunzhi Hub’s generated JSON feed into their existing documentation generators, ensuring that link lists remain consistent and up-to-date across all downstream pages.

- **Compliance and Vendor Review Workflows** – Legal or procurement teams can use the tagging and audit features to track external resources that require periodic re-approval, with automated expiry warnings for SSL certificates or domain registration renewals.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/yunzhi-io/yunzhi-resource-hub.git
cd yunzhi-resource-hub

# Install dependencies (Python 3.9+ required)
pip install -r requirements.txt

# Copy example configuration and adjust to your environment
cp config.example.yaml config.yaml

# Run the initial import pipeline with sample data
python hubctl.py import --source samples/links_197.csv --output data/

# Generate the static dashboard
python hubctl.py build --input data/ --output dist/

# Start the local preview server
python -m http.server 8000 --directory dist/
```

Open your browser at `http://localhost:8000` to view the generated dashboard.

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行时，用于 CLI 工具和监控调度器 |
| PyYAML | 6.0+ | 配置文件解析和 YAML frontmatter 处理 |
| requests | 2.28+ | HTTP 健康检查及资源可达性验证 |
| markdown | 3.4+ | 将维护者编写的 Markdown 条目转换为 HTML |
| jinja2 | 3.1+ | 静态站点模板渲染引擎 |
| pytest | 7.4+ | 单元测试和集成测试框架（仅开发环境） |
| click | 8.1+ | CLI 命令解析和交互式提示 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/getting-started.md` | 如何从零搭建实例？如何导入第一批链接？如何配置监控间隔？ |
| 维护手册 | `docs/maintenance.md` | 如何批量更新元数据？如何处理失效链接？如何回滚变更？ |
| 开发参考 | `docs/development.md` | 插件系统如何扩展？自定义导出格式的接口是什么？测试如何编写？ |
| 运维部署 | `docs/deployment.md` | 如何配置 systemd 定时任务？如何用 Docker 容器化运行？如何对接外部告警？ |

## 资源列表

本批次（第 197/455 批）包含以下 10 个外部资源链接，按域名后缀和内容特征分组。所有链接均以原始形式收录，未做任何协议补充或格式修改。

区域分类 - 亚洲综合索引

<code>yazhouyiersan.org.cn</code>

<code>yazhousetutoupai.org.cn</code>

主题分类 - 人物摄影与素材

<code>nannvwuyeshipin.org.cn</code>

<code>oumeishunvwang.org.cn</code>

专题分类 - 服饰与造型参考

<code>siwazhifudiyiye.org.cn</code>

<code>rihandaxiangjiao.org.cn</code>

内容分类 - 视频与影视档案

<code>yeyelushipin.org.cn</code>

<code>daxiangjiaoyirenjiujiu.org.cn</code>

综合分类 - 女性主题及家庭影视

<code>shunvshipinwangzhan.org.cn</code>

<code>sirenjiatingyingjuyuan.org.cn</code>

## 项目结构

```
yunzhi-resource-hub/
├── hubctl.py                 # 主 CLI 入口，整合导入、检查、构建、导出子命令
├── config.yaml               # 用户配置文件（监控频率、输出路径、通知渠道）
├── requirements.txt          # Python 依赖锁定列表
├── data/                     # 资源数据存储目录（每个条目对应一个 .md 文件）
│   ├── raw/                  # 原始导入数据缓存（CSV/JSON 备份）
│   ├── parsed/               # 解析后的标准化条目（YAML frontmatter + Markdown 正文）
│   ├── checks/               # 最近一次健康检查结果（JSON 格式）
│   └── archive/              # 已删除或废弃条目的历史快照
├── src/                      # 核心源码模块
│   ├── importer.py           # CSV/文本导入器，含格式探测和去重逻辑
│   ├── checker.py            # 异步 HTTP 检查器，支持超时重试和代理配置
│   ├── builder.py            # 静态站点生成器，基于 Jinja2 模板
│   ├── exporter.py           # JSON/CSV/HTML 导出适配器
│   ├── models.py             # ResourceEntry、CheckResult 等数据类定义
│   └── utils.py              # 日志、时间转换、URL 规范化等工具函数
├── templates/                # 静态站点 HTML 模板
│   ├── base.html             # 基础布局（响应式网格，含搜索框和筛选器）
│   ├── index.html            # 资源列表主视图
│   ├── detail.html           # 单个资源详情页（含历史检查曲线）
│   └── status.html           # 全局监控状态面板
├── static/                   # 前端静态资源（CSS/JS/字体）
│   ├── css/                  # 纯 CSS 框架（无外部依赖）
│   ├── js/                   # 交互逻辑（筛选、排序、一键复制）
│   └── assets/               # 图标和占位图形
├── tests/                    # 单元测试与集成测试
│   ├── test_importer.py
│   ├── test_checker.py
│   └── fixtures/             # 测试用样本数据
├── docs/                     # 用户文档和开发者指南
│   ├── getting-started.md
│   ├── maintenance.md
│   ├── development.md
│   └── deployment.md
└── scripts/                  # 辅助运维脚本（定时任务、数据迁移）
    ├── daily_check.sh        # 每日健康检查的 cron 包装脚本
    └── migrate_v2.sh         # 从旧版数据格式升级的迁移工具
```

## 贡献指南

1. **提交问题报告或功能请求** – 使用 GitHub Issues 模板，清晰描述预期行为、实际行为、复现步骤和运行环境（Python 版本、操作系统、配置文件关键项）。对于链接相关的缺陷，请附带具体的条目 ID 或原始 URL。

2. **分支开发流程** – 派生主仓库，在 `develop` 分支基础上创建功能分支（命名格式：`feature/描述` 或 `fix/描述`）。确保代码通过所有单元测试（`pytest tests/`）并遵守 PEP 8 风格约定。

3. **更新文档和示例** – 任何新增配置项、CLI 命令或导出格式变更，必须同步更新 `docs/` 下对应的手册页，并在 `examples/` 目录中提供新的用法示例（若有）。

4. **提交拉取请求** – PR 描述中须引用关联的 Issue 编号，附上变更摘要和测试覆盖率截图。合并前至少需要一位维护者 approve，且所有 CI 检查（包括 lint、类型检查、安全扫描）均为通过状态。

5. **维护者审核** – 对于涉及核心数据模型或监控调度器的变更，维护者将进行额外的性能影响评估，并可能在合并前要求补充集成测试或基准数据。

## 常见问题

**Q: 健康检查是否会对外部目标造成压力或被视为恶意行为？**  
A: 默认配置使用 HEAD 请求，超时设为 5 秒，并发数限制为 10，且每个目标每天最多检查两次。我们建议用户在正式部署前调整 `config.yaml` 中的 `checker.interval` 和 `checker.concurrency` 参数，以符合目标站点的 robots.txt 和访问策略。检查结果仅用于内部可用性判断，不涉及任何数据抓取或解析。

**Q: 如何迁移已有的大量链接集合（例如数百条记录）？**  
A: 使用 `hubctl.py import --bulk` 模式，指定 CSV 路径和列映射配置。系统支持增量导入，自动跳过完全重复的条目（基于 URL 归一化比较）。对于大型导入，建议先执行 `--dry-run` 预览变更数量，再移除该选项执行实际写入。

**Q: 生成的静态页面能否部署到非 GitHub Pages 的环境？**  
A: 可以。`build` 命令输出完全静态的 HTML/CSS/JS 文件，不依赖任何后端服务或 API 代理。您可以将 `dist/` 目录直接上传到任何静态托管服务（如 Netlify、Cloudflare Pages、阿里云 OSS + CDN），或通过 Nginx/Apache 本地托管。

## 许可证

MIT License

Copyright (c) 2026 Yunzhi IO Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
