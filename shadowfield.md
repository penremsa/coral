# 115 Resource Aggregator

115 Resource Aggregator 是一个面向技术内容聚合与网络资源导航的开源工具集，定位于帮助开发者、运维人员与技术研究员高效整理、分类与访问高价值的外部链接资源。项目本身不生产内容，而是提供一套标准化的资源索引框架与本地化预览环境，用于快速部署个人或团队内部的导航门户。

目标用户包括需要频繁查阅特定领域外链资料的技术人员、希望建立团队共享资源库的工程主管，以及希望将大量分散链接以结构化方式呈现的内容运营者。项目通过提供可定制的分类模板、静态站点生成逻辑与轻量级检索接口，解决链接信息过载、检索效率低下与资源不可用难以追踪等问题。

## 功能概览

- **分类资源索引**：支持按照预设分类标签对海量外链进行自动分组，并提供多级目录视图，便于按主题快速定位。

- **链接可用性监测**：内置简易的 HTTP 状态检测模块，可定期对收录链接进行可达性检查，并在界面中标记异常状态。

- **本地全文检索**：基于标题、描述与标签字段实现关键词搜索，检索结果按相关度排序，响应时间低于 200 毫秒。

- **静态站点生成**：提供命令行工具将资源数据导出为纯静态 HTML 文件，可直接部署至任意 Web 服务器或 CDN。

- **数据导入与导出**：支持从 CSV、JSON 及通用书签 HTML 格式批量导入链接记录，同时支持导出为标准备份格式。

- **自定义分类模板**：允许用户通过 YAML 配置文件自定义分类层级、显示顺序与图标映射，无需修改核心代码。

- **访问统计看板**：记录每个链接的点击次数与最后访问时间，并提供简单的趋势图表，辅助判断资源热度。

## 应用场景

- **技术文档聚合门户**：技术团队可将日常使用的 API 文档、框架官网、规范标准等链接统一收录，并部署为内部首页，减少查找时间。

- **开源项目外链备份**：开源维护者可将项目依赖的第三方资源、参考文献与社区讨论链接集中托管，防止原链接失效后信息丢失。

- **运维故障排查手册**：运维人员可将常见报错码对应的解决方案链接、官方补丁公告与社区讨论帖分类整理，形成快速响应知识库。

- **教育培训资源索引**：培训机构或高校实验室可将课程涉及的在线工具、实验平台与参考资料组织为导航站，方便学生按章节访问。

- **个人兴趣收藏整理**：个人开发者可将长期积累的技术博客、播客频道与开源仓库链接进行结构化归档，并定期导出备份。

## 快速开始

以下命令适用于 Linux 与 macOS 环境，Windows 用户可使用 WSL2 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/example/115-resource-aggregator.git

# 进入项目目录
cd 115-resource-aggregator

# 安装依赖（使用 pip 安装 Python 依赖）
pip install -r requirements.txt

# 初始化资源数据库
python manage.py initdb

# 导入示例资源数据（包含预置分类与链接样例）
python manage.py import --source samples/links.json

# 启动本地开发服务器（默认端口 8080）
python manage.py runserver --port 8080
```

访问 `http://localhost:8080` 即可查看资源导航页面。如需生成静态站点，执行：

```bash
python manage.py build --output ./dist
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.8 及以上 | 核心运行环境，用于执行管理命令与后端服务 |
| pip | 20.0 及以上 | Python 包管理器，用于安装项目依赖 |
| SQLite | 3.31 及以上 | 内嵌数据库，用于存储链接元数据与分类信息 |
| Git | 2.25 及以上 | 用于克隆仓库及版本管理 |
| Node.js | 14.0 及以上 | 仅当启用前端构建优化时需要，可选依赖 |
| make | 3.81 及以上 | 用于执行自动化构建脚本（非 Windows 环境） |
| curl | 7.68 及以上 | 用于链接可用性检测模块（可选，如不使用检测可忽略） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/ | 如何导入链接、配置分类、执行搜索与生成静态站点 |
| 管理员指南 | /docs/admin-guide/ | 如何自定义模板、调整检测间隔、备份与恢复数据 |
| 开发文档 | /docs/developer-guide/ | 如何扩展分类解析器、添加新的导入格式或修改前端界面 |
| 部署参考 | /docs/deployment/ | 如何在 Nginx、Apache 或云函数环境下部署静态生成结果 |
| 常见问题 | /docs/faq/ | 收录链接失效如何处理、检索结果不全如何调整、数据库迁移注意事项 |

## 资源列表

### 分类索引类

<code>tingtingqingse.org.cn</code>

<code>jingpinguochanoumei.org.cn</code>

<code>oumeidiyiye.org.cn</code>

<code>chengrendaxiangjiao.org.cn</code>

### 移动端适配类

<code>rihanavshoujiban.org.cn</code>

<code>guochanavshoujiban.org.cn</code>

### 综合导航类

<code>yirendaohang.org.cn</code>

### 字幕与媒体类

<code>huangsezhongwenzimu.org.cn</code>

<code>jiujiuyirendaxiangjiao.org.cn</code>

<code>zaixianguankanzhongwenzimuw.org.cn</code>

## 项目结构

```
115-resource-aggregator/
├── manage.py                # 主命令行入口，集成所有管理操作
├── requirements.txt         # Python 依赖清单（Flask, requests, etc.）
├── config/
│   ├── default.yaml         # 默认分类模板与全局配置
│   └── custom.yaml          # 用户自定义配置（覆盖默认值）
├── core/
│   ├── __init__.py
│   ├── database.py          # SQLite 连接与 ORM 映射
│   ├── importer.py          # 支持 CSV/JSON/HTML 书签导入
│   ├── checker.py           # 链接可用性异步检测引擎
│   └── search.py            # 基于 SQLite FTS5 的全文检索实现
├── web/
│   ├── static/              # CSS、JS 与图片资源
│   ├── templates/           # Jinja2 模板文件
│   └── routes.py            # Flask 路由定义与视图逻辑
├── samples/
│   └── links.json           # 示例资源数据（含 50+ 预置链接）
├── tests/
│   ├── test_database.py
│   ├── test_importer.py
│   └── test_checker.py
├── scripts/
│   ├── build.sh             # 静态站点生成脚本
│   └── backup.sh            # 数据库定时备份脚本
└── docs/
    ├── user-guide/
    ├── admin-guide/
    ├── developer-guide/
    ├── deployment/
    └── faq/
```

## 贡献指南

1. **问题反馈与建议**：请在 GitHub Issues 中描述清晰的问题复现步骤或建议内容，并附上相关日志或截图。对于链接资源类建议，请提供分类依据与预期显示效果。

2. **功能开发流程**：Fork 仓库至个人账户，创建以 `feature/` 或 `fix/` 为前缀的分支，确保所有新代码包含单元测试且测试通过，最后提交 Pull Request 并关联对应 Issue。

3. **文档完善**：欢迎改进现有文档或翻译其他语言版本。修改 `docs/` 目录下的 Markdown 文件后，请确保本地 `mkdocs` 构建无警告，并保持术语一致性。

4. **分类模板扩展**：若需要新增默认分类模板，请在 `config/default.yaml` 中按照现有格式添加，并同步更新 `samples/links.json` 中的示例数据以保持一致性。

5. **代码规范**：Python 代码遵循 PEP 8 规范，使用 `black` 进行格式化，提交前运行 `make lint` 检查。JavaScript 代码遵循 ESLint 推荐配置。

## 常见问题

**Q：导入包含上千条链接的大型 CSV 文件时，页面响应缓慢或超时怎么办？**

A：建议将大文件分割为多个小于 500 条记录的文件分批导入。同时可在 `config/custom.yaml` 中调整批量提交大小（batch_size）参数，默认值为 100，可根据服务器内存情况适当降低至 50。也可使用命令行导入模式 `python manage.py import --batch-size 50 --file large.csv` 以避免 Web 超时限制。

**Q：链接可用性检测报告大量误判，将正常站点标记为不可达，如何调整检测策略？**

A：检测模块默认超时时间为 5 秒，重试次数为 2 次。若目标站点响应较慢，可在配置文件中将 `checker.timeout` 调整至 10 秒，并将 `checker.retries` 设置为 3。此外，部分站点可能拒绝 HEAD 请求，检测模块会自动回退至 GET 请求并限制响应体大小，确保不会因下载大文件而阻塞检测队列。

**Q：如何从旧版本迁移数据到新版本，并保留原有的分类与点击统计？**

A：项目提供 `manage.py export` 命令，可导出完整数据为 JSON 格式，包含所有链接字段、分类映射和统计计数。升级新版本后，执行 `manage.py import --merge` 即可合并数据，不会覆盖已有的统计信息。若数据库结构发生重大变更，迁移脚本会自动执行 ALTER 操作，建议在迁移前先执行 `manage.py backup` 生成 SQLite 文件备份。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
