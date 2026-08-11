# CloudLink 聚合网关

CloudLink 聚合网关是一个轻量级的技术资源导航与外部链接聚合中间件，面向开发者、运维工程师与技术内容策展人，用于将分散在多个域名下的外部参考资源、文档站点、示例仓库与社区入口统一收敛至同一可维护的访问前缀下，并提供基础的访问日志、健康检查与静态资源缓存能力。

该项目本身不存储、不转发、不代理任何用户生成内容，仅作为公开可访问的链接汇总表（Link Manifest）的展示层与跳转辅助层，适用于内部技术团队的知识库入口整合、开源项目的外部依赖索引，以及个人技术博客的“友情链接”或“推荐阅读”面板的自托管替代方案。

## 功能概览

- **集中式链接清单管理**：通过单一 YAML 配置文件维护所有外部链接的标题、描述、分类与活跃状态，无需修改代码即可增删改查。
- **按分类与标签动态渲染**：支持为每个链接分配多个标签，前端页面自动按标签分组展示，并支持客户端即时筛选。
- **链接可用性被动探测**：在页面加载时通过异步请求对每个外部链接进行轻量级 HEAD 探测，并在 UI 上以颜色标记可用状态（绿色可用、灰色超时、红色拒绝连接）。
- **自定义重定向短链**：支持为常用或长尾链接配置短别名（如 `/r/docs`），访问时返回 302 临时重定向，便于口头传播与文档引用。
- **访问统计与来源追踪**：记录每次跳转的时间戳、客户端 IP 脱敏哈希、User-Agent 精简字段与 Referer，便于分析流量构成。
- **静态资源本地缓存策略**：对常见的图标库、字体文件与框架 CSS 提供可配置的本地缓存副本，减少外部 CDN 不稳定带来的页面渲染阻塞。
- **完全容器化部署**：提供 Dockerfile 与 docker-compose 示例，支持一键启动，并默认绑定非特权端口 8080，适配容器编排环境。
- **健康检查与就绪探针**：暴露 `/health` 与 `/ready` 端点，返回标准的 JSON 状态信息，方便接入 Kubernetes 或 Prometheus 监控体系。

## 应用场景

- **企业内部技术文档门户的依赖索引**：将团队常用的数据库管理工具、监控面板、日志检索入口、内部 Git 服务等链接统一汇总，减少收藏夹混乱，并利用可用性探测快速发现故障依赖。
- **开源项目的资源推荐页**：在项目 README 中仅放置一个指向 CloudLink 实例的链接，即可在独立页面中集中展示官方文档、社区论坛、贡献者指南、第三方插件列表等，保持 README 简洁。
- **个人技术博客的外部链接聚合**：作为博客侧边栏的增强替代方案，独立页面可承载更多分类与描述，同时支持短链重定向，便于在不同文章中引用同一外部资源的最新地址。
- **线下技术分享会的资料发放页**：通过配置临时链接清单，将演讲 PPT 云盘链接、示例代码仓库、反馈问卷、参考论文 DOI 等集中发布，并利用访问统计了解资料触达情况。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，要求已安装 Git、Node.js 18.x 及以上版本，以及 npm 或 yarn。

```bash
# 1. 克隆项目仓库
git clone https://github.com/cloudlink-io/cloudlink-gateway.git
cd cloudlink-gateway

# 2. 安装项目依赖
npm install

# 3. 复制示例配置文件并编辑链接清单
cp config/links.example.yaml config/links.yaml
# 根据需要修改 links.yaml，替换为实际的外部链接列表

# 4. 以开发模式启动服务
npm run dev
# 服务默认监听 http://localhost:8080
# 访问 / 查看链接汇总页面，访问 /health 检查服务状态
```

生产环境建议使用 `npm run build` 构建静态资源后，通过 `npm start` 启动，并使用 Nginx 或 Caddy 作为前置反向代理。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，使用原生 fetch 与 Promise API |
| npm | 8.x 或 9.x | 依赖管理工具，用于安装第三方包 |
| 可用磁盘空间 | ≥ 200 MB | 包含源代码、依赖及缓存资源文件 |
| 可用内存 | ≥ 512 MB | 开发模式建议 1GB，生产模式约 256MB 峰值 |
| 操作系统 | Linux / macOS / Windows 10+ | 支持主流 Unix 风格文件路径及符号链接 |
| DNS 解析能力 | 需可解析公网域名 | 用于链接探测与重定向目标解析 |
| 时区数据 | 系统默认 | 访问日志时间戳依赖于系统时区配置 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user-guide/configuration.md` | 如何编写 links.yaml 配置文件、支持哪些字段、如何设置分类与标签 |
| 用户手册 | `/docs/user-guide/short-links.md` | 如何配置自定义短链别名、重定向状态码选择、以及短链的优先级规则 |
| 运维手册 | `/docs/operations/deployment.md` | 如何通过 Docker、Kubernetes 或 Systemd 部署，以及环境变量配置清单 |
| 运维手册 | `/docs/operations/monitoring.md` | 如何接入 Prometheus 指标、解读健康检查返回值、设置告警阈值 |
| 开发指南 | `/docs/development/architecture.md` | 项目的模块划分、核心数据流、中间件设计原则 |
| 开发指南 | `/docs/development/testing.md` | 单元测试与集成测试的运行方法、Mock 外部请求的策略 |
| 常见问题 | `/docs/faq.md` | 汇总了链接探测超时、页面渲染异常、短链冲突等高频问题及解决方案 |

## 资源列表

以下为当前版本外部参考资源及关联站点的原始链接汇总，按类别整理。所有链接均保留用户提供的原始格式，不做任何协议或域名改写。

官方与社区入口

- <code>jiujiujiujiure.org.cn</code>

中文技术内容索引

- <code>chengrenzipaishipin.org.cn</code>
- <code>renqishaofuzhongwen.org.cn</code>
- <code>taosewuyuetian.org.cn</code>

多媒体与学习资源

- <code>tingtingrihanyiquerqusanqu.org.cn</code>
- <code>youcuyoudashipin.org.cn</code>
- <code>qingqingcaochengrenwang.org.cn</code>

图库与素材参考

- <code>yazhousetuzipai.org.cn</code>
- <code>shunvrenqizhongwenzimu.org.cn</code>

动漫与番剧相关

- <code>yinghuadongmanzhengbanguanwangderukou.org.cn</code>

## 项目结构

```
cloudlink-gateway/
├── config/                         # 配置目录
│   ├── default.yaml                # 默认框架配置（端口、缓存、日志级别）
│   └── links.example.yaml          # 链接清单示例文件（含字段说明）
├── src/                            # 源代码主目录
│   ├── server/                     # HTTP 服务启动与中间件链
│   │   ├── app.js                  # Express 应用初始化
│   │   ├── middleware/             # 请求日志、CORS、请求限速等中间件
│   │   └── routes/                 # 路由定义：首页、重定向、健康检查、静态资源
│   ├── core/                       # 核心业务逻辑
│   │   ├── manifestLoader.js       # 加载并校验 links.yaml 配置文件
│   │   ├── probeManager.js         # 管理外部链接的异步探测任务与缓存状态
│   │   ├── shortLinkResolver.js    # 短链别名匹配与 302 重定向处理器
│   │   └── statsCollector.js       # 访问记录的轻量级内存存储与脱敏处理
│   ├── views/                      # 模板引擎及静态页面组装
│   │   ├── layout.ejs              # 基础 HTML 骨架
│   │   ├── index.ejs               # 链接汇总主页面（含分类与过滤逻辑）
│   │   └── error.ejs               # 错误提示页（404 / 500 等）
│   ├── public/                     # 前端静态资源
│   │   ├── css/                    # 基础样式与响应式布局
│   │   ├── js/                     # 客户端探测脚本、筛选器、状态更新逻辑
│   │   └── assets/                 # 图标、字体、默认占位图片
│   └── utils/                      # 通用工具函数
│       ├── logger.js               # 结构化日志封装（支持 JSON 与彩色输出）
│       └── validator.js            # URL 格式校验、域名黑名单检查
├── test/                           # 单元测试与集成测试用例
│   ├── unit/                       # 核心模块的独立测试
│   └── integration/                # 端点测试与模拟外部请求
├── docker/                         # 容器化相关文件
│   ├── Dockerfile                  # 基于 Alpine 的多阶段构建
│   └── docker-compose.yml          # 本地编排示例（含 Redis 可选缓存）
├── scripts/                        # 运维辅助脚本
│   ├── healthcheck.sh              # 容器内健康检查调用脚本
│   └── backup-links.sh             # 定期备份 links.yaml 到本地快照
├── .env.example                    # 环境变量示例（覆盖默认配置）
├── package.json                    # npm 项目描述与依赖声明
├── README.md                       # 项目说明文档（即本文档）
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。建议在 `develop` 分支上新建特性分支，命名格式为 `feature/简短描述` 或 `fix/问题编号`。
2. 运行 `npm install` 安装依赖，并执行 `npm run lint` 检查代码风格（使用 ESLint + Prettier）。所有新提交必须通过 lint 检查，且不引入额外的控制台警告。
3. 若新增或修改配置文件字段，需同步更新 `config/links.example.yaml` 中的注释说明，并在 `/docs/user-guide/configuration.md` 中补充对应文档。
4. 提交代码前，运行 `npm run test` 确保所有单元测试与集成测试通过。若涉及前端页面改动，请附带简单的手动测试截图或描述。
5. 发起 Pull Request 到主仓库的 `main` 分支，并在描述中清晰说明改动目的、影响范围以及是否包含破坏性变更。PR 合并后会自动触发 Docker 镜像构建流程。

## 常见问题

**问：链接清单中的域名无法被探测，页面一直显示为红色状态，如何调整？**

答：默认探测超时时间为 3000 毫秒，且使用 HEAD 请求。部分站点可能禁止 HEAD 方法或响应较慢，您可以在 `config/default.yaml` 中调整 `probe.timeout` 和 `probe.method`（可改为 GET）。另外，若站点要求特定的 User-Agent，可在 `probe.headers` 中自定义。请注意，频繁探测大量链接可能导致客户端浏览器限制并发请求数，可适当调低 `probe.concurrency` 值。

**问：我可以将 CloudLink 部署在子路径下（如 `/links`）而不是根路径吗？**

答：可以。在环境变量中设置 `BASE_PATH=/links`，或在配置文件中修改 `server.basePath`。所有内部路由与静态资源引用会自动添加此前缀。但请注意，短链重定向功能也会继承该前缀，即短链 `docs` 的实际访问路径为 `/links/r/docs`。

**问：访问统计会记录完整的用户 IP 和 User-Agent 吗？是否涉及隐私合规问题？**

答：默认实现中，IP 地址在记录前会经过 SHA-256 哈希加盐处理（盐值在启动时随机生成），仅保留哈希值用于独立访客去重，不会存储原始 IP。User-Agent 仅保留前 64 个字符且移除具体的版本号字段。所有统计数据保存在内存中，服务重启即清空。如需持久化存储，请自行接入外部数据库并评估合规风险。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:26
