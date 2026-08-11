# ResourceHub

ResourceHub 是一个面向开发者与技术研究人员的精选技术资源导航与聚合平台。项目定位于解决技术信息碎片化、优质外链分散难以追溯的问题，通过对特定领域的技术文档、工具站、社区论坛与数据源进行人工筛选与分类整理，为使用者提供稳定、可追溯且高可用性的参考信息来源。本仓库本身不存储任何侵权或违规内容，仅作为公开可访问 URL 的索引与结构化描述。

## 功能概览

- **结构化资源索引**：按领域、地域与内容类型对收录的 URL 进行多级标签与分类管理，支持快速筛选与定位。
- **每日自动可用性检查**：通过 GitHub Actions 定时对收录的资源链接进行 HTTP 状态码探测，自动标记失效或重定向条目。
- **自定义分类视图**：支持生成按主题（如技术文档、社区讨论、视频资源、工具库）划分的 Markdown 视图，便于不同角色用户聚焦关注。
- **外链变更历史记录**：每次更新维护均记录变更日志，保留 URL 的新增、移除或替换操作记录，确保资源变更可审计。
- **RSS 订阅源生成**：根据分类自动生成 RSS 订阅链接，方便用户通过订阅器获取新增资源通知。
- **精简搜索辅助**：提供基于关键词的客户端搜索建议，通过预生成的关键词倒排索引加速本地查找。
- **批量导入与去重**：支持从 CSV 或 JSON 文件批量导入待收录链接，并自动执行域名去重与路径规范化。

## 应用场景

- **技术调研与竞品分析**：研究人员可通过本项目的分类索引，快速获取同类主题下的多个参考站点，节省手动搜索与验证时间。
- **项目文档外链托管**：开发团队可将本项目作为公共技术文档的补充外链接口，在自有项目中引用本仓库的稳定资源条目。
- **自动化监控告警**：运维人员可利用内置的可用性检查脚本，对接企业监控系统，当关键外链不可用时接收告警。
- **个人知识库整合**：知识管理爱好者可将本仓库作为书签管理工具的补充，通过本地克隆离线浏览资源清单。

## 快速开始

```bash
# 克隆仓库
git clone https://github.com/resourcehub/resourcehub.git
cd resourcehub

# 安装依赖（需要 Node.js 18+ 或 Python 3.10+，依所选后端而定）
# 以下示例使用 Node.js 版本
npm install

# 执行本地资源索引构建与可用性检查
npm run build
npm test

# 启动本地预览服务（默认端口 3000）
npm start
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | 18.x 或更高 | 运行时环境，用于构建与脚本执行 |
| npm | 9.x 或更高 | 包管理工具 |
| Git | 2.30 或更高 | 版本控制，用于克隆及提交变更 |
| Python | 3.10 或更高（可选） | 用于部分辅助脚本（如 RSS 生成） |
| curl | 7.68 或更高 | 用于可用性检查中的 HTTP 探测 |
| cron / systemd-timer | 任意版本（Linux） | 用于定时任务触发自动化检查（生产环境推荐） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide.md | 如何使用分类视图、搜索和 RSS 订阅？ |
| 维护指南 | /docs/maintainer-guide.md | 如何新增、更新或移除资源链接？如何触发可用性检查？ |
| 开发参考 | /docs/developer-guide.md | 插件机制如何扩展？命令行参数有哪些？ |
| 架构设计 | /docs/architecture.md | 资源索引的数据结构是什么？检查流程如何并行化？ |

## 资源列表

### 综合分类资源

- <code>guochanyoudayouhuang.org.cn</code>
- <code>wuyerenqi.org.cn</code>

### 地域专题资源

- <code>yazhouchengrenyiquerqu.org.cn</code>
- <code>oumeizhongchu.org.cn</code>

### 持续更新资源

- <code>tiantianyue.org.cn</code>
- <code>yirenjiujiu.org.cn</code>

### 精选分类资源

- <code>sihujingpin.org.cn</code>
- <code>guochanrihanoumei.org.cn</code>

### 辅助工具与数据资源

- <code>rihanmadou.org.cn</code>
- <code>oumeihouru.org.cn</code>

## 项目结构

```
resourcehub/
├── .github/
│   └── workflows/               # GitHub Actions 工作流，含可用性检查与自动 PR
├── bin/
│   ├── check-availability.js    # 外链可用性检查命令行入口
│   └── generate-rss.py          # RSS 订阅文件生成脚本（可选）
├── config/
│   ├── categories.json          # 分类定义与标签映射
│   └── sources.json             # 原始资源列表（含 URL、描述、添加时间）
├── docs/                        # 完整文档（用户手册、维护指南、开发参考、架构设计）
├── src/
│   ├── crawler/                 # 爬取与请求模块
│   ├── indexer/                 # 索引构建与查询模块
│   └── reporter/                # 报告生成（Markdown / HTML / RSS）
├── tests/                       # 单元测试与集成测试
├── public/
│   └── index.html               # 本地预览静态页
├── CHANGELOG.md                 # 变更日志
├── CONTRIBUTING.md              # 贡献指南（详细版）
├── README.md                    # 本文件
└── package.json                 # Node.js 依赖与脚本定义
```

## 贡献指南

1. 阅读 `CONTRIBUTING.md` 详细文档，了解分类规范与 URL 收录准则（如禁止包含动态生成参数、需稳定可访问）。
2. 在 `config/sources.json` 中按格式新增或修改资源条目，确保包含 `url`、`category`、`description` 和 `added_by` 字段。
3. 本地运行 `npm test` 进行格式校验与可用性预检查，确保新增链接返回 200/301/302 状态。
4. 提交拉取请求，并在 PR 描述中说明变更理由和验证步骤。项目维护者将在 48 小时内进行审核。
5. 若发现已有资源失效，可直接提交 Issue 或在 PR 中标记 `[DEPRECATED]`，由维护者确认后移除。

## 常见问题

**问：如果某个收录的 URL 无法访问，项目会自动处理吗？**
答：会。每日 UTC 00:00 执行的可用性检查会将连续 3 次失效的链接标记为 `unstable`，并自动创建 Issue 通知维护者。若连续 7 天仍然无效，该链接将被移至 `deprecated` 列表，并记录移除原因。

**问：我可以只克隆本项目的一部分资源列表而不运行检查脚本吗？**
答：可以。您只需克隆仓库后查看 `config/sources.json` 或 `README.md` 的资源列表章节即可，无需安装任何依赖或运行脚本。本项目始终将完整资源索引以纯文本形式维护在仓库中。

**问：本项目是否接受外部镜像或转载？**
答：本项目采用 MIT 许可证，允许任意复制、修改和分发。但请注意，本仓库仅提供 URL 索引，各目标站点的内容与可用性由原始运营方负责。若您需要镜像，建议同时遵守目标站点的 robots.txt 与使用条款。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:34
