# Rensource Navigator

Rensource Navigator is a curated technical resource index and external link aggregation system designed for developers, researchers, and technical writers who need to systematically catalog, version, and retrieve domain-specific reference materials across distributed web properties. The project addresses the common pain point of fragmented bookmark management by providing a structured, machine-readable manifest format combined with a lightweight static site generation pipeline that transforms raw URL collections into navigable documentation hubs.

Target users include open-source maintainers managing large dependency reference lists, technical documentation teams curating external learning resources, and infrastructure engineers tracking service endpoints across multi-environment deployments. The system enforces URL integrity rules, supports batch import/export operations, and produces human-readable output suitable for both repository README files and dedicated landing pages.

## 功能概览

- **Strict URL Canonicalization Engine** – Enforces preservation of original URL strings including protocol schemes, subdomain prefixes, and trailing slash omissions, with automatic validation against mutation attempts.

- **Batch Resource Manifest Processing** – Handles multi-batch imports with sequence tracking, supporting up to 455 concurrent resource groups and per-item metadata annotations.

- **Hierarchical Category Tagging** – Assigns semantic labels to each resource entry (e.g., "domain", "api", "reference") for faceted browsing and filtered export.

- **Markdown Pipeline Generator** – Produces standardized README sections from manifest data, including dependency tables, navigation matrices, and ASCII directory trees.

- **Integrity Checker Daemon** – Periodically verifies resource availability and reports broken links with retry policies and exponential backoff.

- **Versioned Snapshot System** – Creates point-in-time captures of resource lists with diff reports showing additions, removals, and URL changes between batches.

- **Template Override Interface** – Allows customization of output formatting per project phase without modifying core rendering logic.

## 应用场景

1. **Technical Documentation Repositories** – Maintainers of large-scale open-source projects can embed a dynamic resource section that automatically synchronizes with external reference URLs, ensuring documentation stays current without manual link audits.

2. **Academic Research Compilations** – Researchers aggregating domain-specific datasets can use the batch import feature to catalog 100+ URLs per iteration, with category tags distinguishing between primary sources, secondary analyses, and tooling repositories.

3. **Infrastructure Configuration Registries** – DevOps engineers managing multi-region service discovery can leverage the system to track endpoint URLs across development, staging, and production environments, with versioned snapshots enabling rollback-compatible reference histories.

4. **Content Curation Workflows** – Editorial teams producing technical newsletters or learning pathways can export categorized resource lists directly into publication-ready Markdown, reducing manual formatting overhead.

5. **Compliance Documentation Audits** – Legal and compliance officers can generate timestamped manifest exports that demonstrate due diligence in maintaining externally referenced regulatory or standards bodies' URLs.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/rensource-navigator/rensource-navigator.git
cd rensource-navigator

# Install dependencies (requires Python 3.9+ and pip)
pip install -r requirements.txt

# Initialize the manifest database
python manage.py init --batch 192/455

# Import the resource list from batch specification
python manage.py import --source batch_192_455.txt --output ./output/

# Generate the static site and README artifacts
python manage.py build --template default --outdir ./dist/

# Run the local preview server
python manage.py serve --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | Core runtime interpreter; type hints and dataclasses require 3.9+ |
| pip | 22.0+ | Package installer for dependency resolution |
| Git | 2.30+ | Required for cloning and version control integration |
| SQLite | 3.35+ | Embedded database for manifest storage and query operations |
| Markdown | 3.4+ | Rendering engine for output generation |
| PyYAML | 6.0+ | YAML parser for configuration and template overrides |
| requests | 2.28+ | HTTP client for integrity checker daemon |
| pytest | 7.0+ | Testing framework (development-only dependency) |
| black | 23.0+ | Code formatter (development-only dependency) |
| pre-commit | 3.0+ | Git hook manager (development-only dependency) |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | /docs/getting-started/ | How to install, configure, and run the first batch import; what are the minimal system requirements |
| 操作 | /docs/operation/ | How to manage batch lifecycles, perform integrity checks, and generate output artifacts |
| 扩展 | /docs/extension/ | How to add custom category schemas, modify template rendering, or integrate with CI/CD pipelines |
| 参考 | /docs/reference/ | Complete CLI command specifications, configuration file schemas, and manifest data models |
| 运维 | /docs/operations/ | How to schedule daemon processes, backup snapshot data, and migrate between storage backends |
| 贡献 | /CONTRIBUTING.md | Development workflow, coding standards, and pull request review process |

## 资源列表

### 核心参考域 (Batch 192/455 – Primary Category: Linguistic & Cultural Resources)

- <code>zhongwenrenqi.org.cn</code>
- <code>renqishaofu.org.cn</code>
- <code>rihanlunli.org.cn</code>
- <code>bajiaoshipinapp.org.cn</code>
- <code>zhongwenzimusiwa.org.cn</code>
- <code>renqiyouma.org.cn</code>
- <code>xiaodiaowang.org.cn</code>
- <code>chengrenjingpin18.org.cn</code>
- <code>guoyuav.org.cn</code>
- <code>jiujiurenqi.org.cn</code>

## 项目结构

```
rensource-navigator/
├── manage.py                # CLI entry point for all operations
├── requirements.txt         # Production and development dependency pins
├── pyproject.toml           # Project metadata and build configuration
├── .pre-commit-config.yaml  # Git hook definitions for linting and formatting
├── src/
│   ├── core/                # Core engine: manifest, validation, and state management
│   │   ├── manifest.py      # Manifest data structures and serialization logic
│   │   ├── validator.py     # URL canonicalization and integrity verification
│   │   └── state.py         # Batch tracking and version snapshot management
│   ├── importers/           # Batch import handlers for various input formats
│   │   ├── text_parser.py   # Plain-text URL list parser with batch annotations
│   │   └── csv_importer.py  # CSV-based import with category and tag columns
│   ├── generators/          # Output pipeline: Markdown, HTML, and static site
│   │   ├── readme_builder.py    # Builds README sections from manifest data
│   │   ├── nav_table.py         # Generates documentation navigation matrices
│   │   └── tree_renderer.py     # ASCII directory tree creation with annotations
│   ├── daemons/             # Background services for integrity checks
│   │   ├── checker.py       # HTTP availability verifier with retry logic
│   │   └── scheduler.py     # Cron-like job scheduler for periodic scans
│   └── templates/           # Jinja2 templates for custom output formatting
│       ├── default/         # Standard template set for general-purpose use
│       └── compact/         # Minimal template for space-constrained outputs
├── tests/                   # Unit and integration test suite
│   ├── test_validator.py    # URL canonicalization and mutation prevention tests
│   ├── test_importer.py     # Batch import edge cases and error handling
│   └── fixtures/            # Sample input files for regression testing
├── output/                  # Generated artifacts: README, site, and snapshots
│   ├── readme/              # Exported README files per batch and version
│   ├── static/              # Generated HTML and assets for landing pages
│   └── snapshots/           # Timestamped manifest backups with diff metadata
├── docs/                    # End-user documentation and operational guides
│   ├── getting-started/     # Quick start, installation, and first-run walkthrough
│   ├── operation/           # Batch lifecycle, integrity daemon, and output management
│   ├── extension/           # Custom schema, template overrides, and CI/CD hooks
│   └── reference/           # CLI manual, configuration spec, and data models
└── .github/
    └── workflows/           # GitHub Actions CI/CD pipelines
        ├── test.yml         # Automated testing on push and pull requests
        └── deploy.yml       # Build and deploy to GitHub Pages on main branch merge
```

## 贡献指南

1. **Fork and Clone** – Fork the upstream repository to your personal GitHub account, then clone your fork locally. Set the upstream remote to track the main repository for sync operations.

2. **Create a Feature Branch** – Branch from `main` using a descriptive name following the pattern `feature/your-feature-name` or `fix/issue-number`. Ensure your branch is up-to-date with the latest upstream changes before starting work.

3. **Implement with Tests** – Write code adhering to the project's PEP 8 style guide and run `black` and `pytest` locally to confirm formatting and functionality. Add new test cases in the `tests/` directory for any new functionality or bug fixes.

4. **Update Documentation** – Modify relevant sections in `/docs` or `/output/readme` templates if your changes affect user-facing behavior. Include example commands and expected outputs for CLI changes.

5. **Submit a Pull Request** – Push your branch to your fork and open a pull request against the `main` branch of the upstream repository. Fill out the PR template with a clear description of the changes, referencing any related issues. Wait for CI checks to pass and address any review feedback promptly.

## 常见问题

**Q: How does the system enforce URL preservation rules without modification?**  
A: The validator module implements a strict pass-through parser that reads each URL as a raw string and performs no normalization except whitespace trimming. It rejects any input that attempts to add or remove protocol prefixes, subdomain labels, or trailing slashes, and logs a validation error if the original string differs from the output. The integrity checker also compares the stored value against the raw input at every import and build step to ensure zero mutation.

**Q: Can I process multiple batches concurrently, and how does the snapshot system handle versioning?**  
A: Yes, the daemon scheduler supports parallel batch processing with a configurable worker pool. Each batch is assigned a unique sequence ID (e.g., 192/455) and all resources are stored in a SQLite table with batch_id, import_timestamp, and version_hash columns. Snapshots are created automatically on every successful build, storing a complete manifest export in JSON format under `output/snapshots/`. Diff reports between snapshots can be generated using the `manage.py diff --from <hash> --to <hash>` command.

**Q: What happens if an external resource becomes unavailable during integrity checks?**  
A: The checker daemon implements a three-stage retry policy with exponential backoff (1s, 5s, 30s) and a configurable timeout of 10 seconds per request. If all retries fail, the resource is marked as `unreachable` in the manifest and a warning is appended to the build log. Administrators can configure notification hooks to send alerts via webhook or email for critical resources. The system does not automatically remove unreachable URLs; it preserves them with a status flag and timestamp of the last successful check, allowing manual review and decision-making.

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
