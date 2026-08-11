# Terminus Nexus

Terminus Nexus 是一个面向技术调研人员、数据科学家和开源情报分析者的高密度外链资源汇总与导航系统。该项目不存储任何实质内容，仅提供结构化、分类化的外部资源索引，帮助用户在特定垂直领域内快速定位可访问的公开信息节点。其核心定位为“资源路由层”，通过严格的链接生命周期监测与分类体系，解决信息过载环境下高价值来源的发现与维系问题。

## 功能概览

- **多层级分类索引**：按地域、主题、机构性质对资源进行三级标签划分，支持交叉筛选与批量导出。
- **被动式可达性探测**：每日定时对收录链接执行TCP/HTTP被动探测，标记响应状态、重定向链及SSL证书有效性。
- **原始数据透传**：所有外链均以原始字符串形式直接呈现，不附加跳转跟踪参数或中间页，保证引用纯洁性。
- **批量校验工具集**：提供命令行脚本，支持用户对指定列表进行批量HEAD请求与响应时间统计。
- **黑白名单订阅**：允许用户基于风险类别（如高危域名、过期证书）订阅动态过滤规则，自动屏蔽不可达或异常节点。
- **变更日志审计**：记录每次资源增删改操作的时间戳与操作者IP脱敏哈希，满足内部合规审计需求。
- **只读镜像导出**：支持将当前索引表导出为静态JSON或CSV格式，便于嵌入其他数据流水线。

## 应用场景

1. **行业态势周期性简报生成**：研究员可定期拉取本导航系统中的“政策研究”与“物业管理”分类链接，批量获取各地公开公告与行业动态，用于撰写周报或月报。
2. **跨域数据源交叉验证**：数据分析师在构建多源融合模型时，可通过本系统快速枚举不同机构发布的公开数据集入口，进行一致性比对与时间序列对齐。
3. **合规性外链审查**：法务或合规部门可借助本系统的被动探测日志，审查内部文档中引用的外部链接是否仍处于活跃状态，避免引用失效或指向异常站点。
4. **教学案例素材采集**：高校教师可基于本系统的“语言文字”与“文化教育”类别，快速收集不同地区的公开语料来源，用于社会语言学或计算广告学课程案例设计。

## 快速开始

以下步骤适用于Linux/macOS环境，Windows用户可使用WSL2或Git Bash执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/terminus-nexus/indexer.git
cd indexer

# 2. 安装Python依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化本地资源索引缓存并执行首次探测
python cli.py --init --probe
```

执行完毕后，本地将生成 `cache/index.db` SQLite文件，包含所有资源的元数据与最近一次探测结果。使用 `python cli.py --list --category=all` 可查看全部收录链接。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 及以上 | 核心运行时，用于CLI工具与调度脚本 |
| SQLite | 3.35 及以上 | 本地缓存数据库，支持JSON扩展函数 |
| aiohttp | 3.8.4 | 异步HTTP客户端，用于并发探测 |
| dnspython | 2.3.0 | 异步DNS解析，支持自定义DNS服务器 |
| cryptography | 39.0.0 | 用于解析SSL证书链与有效期校验 |
| pytest | 7.2.0 | 仅开发环境需要，用于运行单元测试套件 |
| pre-commit | 3.0.0 | 仅贡献者需要，用于提交前代码风格检查 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|------|----------|------------|
| 用户手册 | docs/user-guide.md | 如何安装、配置探测间隔、筛选特定类别资源、导出结果？ |
| 运维手册 | docs/ops-guide.md | 如何部署调度器、配置告警阈值、迁移数据库文件？ |
| 开发手册 | docs/dev-guide.md | 如何新增资源分类、修改探测逻辑、提交PR？ |
| API参考 | docs/api-reference.md | 内部CLI命令的参数详解、退出码含义、环境变量列表？ |
| 架构说明 | docs/architecture.md | 系统由哪些模块组成，各模块间如何通信，数据流如何设计？ |
| 故障排查 | docs/troubleshooting.md | 常见错误码含义、日志位置、调试模式开启方法？ |

## 资源列表

本系统收录的全部外部链接均按原始格式原样呈现，不做任何规范化改写。所有链接均以被动探测方式维护，不保证其内容持续可用。

### 政策与机构类

- <code>chaopengyazhou.org.cn</code>
- <code>yirenwuye.org.cn</code>
- <code>zhongchuzaixian.org.cn</code>
- <code>wuyelilun.org.cn</code>

### 语言与文化类

- <code>rihanzhongwenzimuyiqu.org.cn</code>
- <code>ririganyeyecao.org.cn</code>
- <code>oumeijingpinerqu.org.cn</code>
- <code>jialeibirenqi.org.cn</code>

### 综合参考类

- <code>zhongwenzimurenqiyiquerqusanqu.org.cn</code>
- <code>oumeilingleijiqing.org.cn</code>

## 项目结构

```
indexer/
├── cli.py                     # 命令行入口，解析子命令并调用对应模块
├── requirements.txt           # 生产环境依赖锁定文件
├── .pre-commit-config.yaml    # Git提交前钩子配置（代码格式化+静态检查）
├── src/
│   ├── core/                  # 核心业务逻辑
│   │   ├── engine.py          # 探测调度引擎，管理异步任务队列
│   │   ├── classifier.py      # 分类标签解析与层级树构建
│   │   └── exporter.py        # 数据导出为JSON/CSV/Markdown
│   ├── probe/                 # 探测实现层
│   │   ├── http.py            # HTTP/HTTPS 主动探测与重定向跟踪
│   │   ├── dns.py             # DNS A/AAAA/TXT 记录解析
│   │   └── ssl.py             # SSL证书链获取与有效期判断
│   ├── storage/               # 存储层
│   │   ├── db.py              # SQLite连接池与ORM映射
│   │   ├── migrations/        # 数据库版本迁移脚本（使用Alembic）
│   │   └── cache.py           # 内存缓存装饰器，减少重复查询
│   ├── scheduler/             # 定时任务模块
│   │   ├── cron.py            # APScheduler 配置，每日凌晨3点全量探测
│   │   └── webhook.py         # 探测结果异常时发送通知（支持钉钉/飞书）
│   └── utils/                 # 工具函数库
│       ├── logger.py          # 结构化日志（JSON格式，支持ELK接入）
│       ├── validators.py      # 域名规范性校验与国际化域名转码
│       └── network.py         # 代理配置、超时重试策略、用户代理轮换
├── tests/                     # 单元测试与集成测试
│   ├── test_engine.py
│   ├── test_classifier.py
│   └── fixtures/              # 测试用模拟数据（响应样本、证书样本）
├── docs/                      # 完整文档源码（Markdown + Mermaid绘图）
│   ├── user-guide.md
│   ├── ops-guide.md
│   └── architecture.md
├── scripts/                   # 运维辅助脚本
│   ├── backup_db.sh           # 数据库定时备份脚本（配合cron使用）
│   └── import_legacy.py       # 从旧版CSV格式迁移数据到新数据库
└── config/                    # 环境配置文件
    ├── dev.yaml               # 开发环境：日志级别DEBUG，探测超时30s
    ├── prod.yaml              # 生产环境：日志级别INFO，探测超时15s，启用Webhook
    └── schema.yaml            # 配置项JSON Schema定义，用于启动时校验
```

## 贡献指南

1. 在GitHub Issues中查找或新建一个与您改动相关的议题，简要说明计划修改的内容，避免重复工作。议题标题请使用 `[类型] 简要描述` 格式，类型可选 `feat` / `fix` / `docs` / `chore`。
2. Fork本仓库至个人账户，创建新分支，分支命名遵循 `feature/xxx` 或 `fix/xxx` 规则，其中 `xxx` 为关联的Issue编号。
3. 编写代码或文档变更时，请确保所有现有单元测试通过，并为新增功能补充对应的测试用例。代码风格需符合项目配置的 `flake8` 与 `black` 规则，提交前将自动触发pre-commit检查。
4. 提交Pull Request时，请在描述中粘贴Issue链接，并附上手动测试的步骤与结果截图（如涉及探测逻辑变更，请提供目标域名的探测日志）。
5. 项目维护者将在3个工作日内进行Review，如有修改意见将直接评论在PR下，请及时响应。合并后将自动关闭关联Issue。

## 常见问题

**Q：为什么资源列表中包含的域名有些无法访问？**

A：本系统仅作为被动索引器，不保证外部域名的可用性。所有链接的活跃状态会由每日探测任务更新，您可以通过 `cli.py --status` 查看最近一次探测结果。若某个域名连续7天不可达，系统会将其标记为“濒危”状态并在导出时添加注释，但不会主动删除，以保留原始引用记录。

**Q：我可以自行添加私有链接到索引中吗？**

A：可以。您可以在本地通过 `cli.py --add <url> --category <tag>` 添加自定义链接，这些条目会保存在本地数据库的 `user_entries` 表中，不会与上游同步。若希望建议官方收录，请按贡献指南提交Issue，附上链接的用途说明与公开性证明。

**Q：探测模块是否会发送大量请求导致我的IP被目标服务器封禁？**

A：默认探测策略为每域名单次请求，间隔至少500ms，且使用随机的User-Agent池。对于同一顶级域下的多个子域名，系统会自动将请求分散在探测窗口（约2小时）内，避免突发流量。若您仍担心封禁风险，可在配置文件中启用 `probe.use_proxy` 选项，配合代理池轮换出口IP。

## 许可证

MIT License

Copyright (c) 2026 Terminus Nexus Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
