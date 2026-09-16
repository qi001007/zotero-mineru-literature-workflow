# Zotero + MinerU Literature Workflow

[中文](#中文) · [English](#english)

## 中文

一个面向科研文献管理的 Codex Skill。它把“找到了题录”变成可验证的全文工作流：

```text
Zotero 父条目
├─ 本地 PDF 链接
└─ MinerU full.md 链接
```

每篇完成的论文同时具备：

- 合法获取、通过 `%PDF` 文件头校验的本地 PDF；
- 由 MinerU 转换得到的 Markdown 主文件 `full.md`；
- Zotero 父条目下对应的两个**链接文件**附件。

只有满足这三个条件，论文才会被计入“已完成”；单纯的 DOI、标题或元数据条目始终只是候选文献。

### 这个 Skill 会做什么

1. 检查 Zotero、MinerU、Zotero 写入能力与本地可写目录是否可用；
2. 如果缺少 Zotero 或 MinerU，明确提示缺失能力及官方安装渠道；
3. 在下载或转换前询问研究文件的保存位置，并区分 Zotero 程序、Zotero 数据目录与研究文件目录；
4. 从合法开放来源获取 PDF，并拒绝把登录页、HTML 错页或 CAPTCHA 当成论文；
5. 将每个 PDF 交给 MinerU，保留独立的 Markdown/图片输出目录；
6. 为 Zotero 中的对应父条目建立 PDF 和 Markdown 两个本地链接附件；
7. 回读验证磁盘文件和 Zotero 附件，分别报告题录、PDF、Markdown、双链接条目的数量。

### 推荐目录

```text
<research-root>/
├─ 学术论文/                      # 原始且通过校验的 PDF
└─ MinerU/
   └─ <paper-slug>/
      ├─ full.md                  # MinerU 主文档
      └─ ...                      # 图片与其他提取资源
```

PDF 与 MinerU 文件夹使用同一个 `<paper-slug>`，便于迁移、备份和排查。

### 前置条件

- [Zotero Desktop](https://www.zotero.org/download/)；
- [MinerU](https://github.com/opendatalab/MinerU) 或可用的 MinerU MCP/CLI 集成；
- 一个可以创建 Zotero 条目和链接附件的 Zotero 集成方式；
- 用户确认的本地研究目录。

本 Skill 不会自动安装软件、移动 Zotero 数据库，或绕过付费墙。Zotero 本地 API 密钥、用户 ID、分类 ID 和本地绝对路径均不得提交到仓库。

### 使用方式

将此目录作为 Codex Skill 安装或放入可发现的 Skills 目录。随后可以这样请求：

> 为我的毕业设计建立 Zotero + MinerU 文献工作流。先检查 Zotero 和 MinerU，询问我希望把研究文件放在哪个盘；确认后，整理这些论文并给每个 Zotero 条目添加 PDF 与 MinerU Markdown 的链接附件。

详细执行规则见 [SKILL.md](SKILL.md)。

## English

A Codex Skill for building a **verifiable, local full-text research library** with Zotero and MinerU.

Each completed paper must have:

- a legally obtained and validated local PDF;
- a MinerU-generated Markdown document, normally `full.md`;
- two linked-file attachments under the matching Zotero parent item: one PDF and one Markdown file.

Metadata-only citations are never counted as completed papers.

### What it does

- checks Zotero, MinerU, writable storage, and Zotero attachment-write capability;
- asks the user to choose a research-file location before writing files;
- keeps PDFs and MinerU output in parallel folders;
- validates downloaded files before treating them as PDFs;
- converts verified PDFs with MinerU;
- attaches both local files to the Zotero parent record as **linked files**;
- reads back the result and reports verifiable completion counts.

### Safety and scope

This Skill uses legal open-access, repository, author-preprint, or arXiv sources only. It does not bypass paywalls, write directly to `zotero.sqlite`, relocate a Zotero library without approval, or publish local credentials and paths.

## Repository layout

```text
.
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
└─ references/
   ├─ storage-and-preflight.md
   └─ zotero-linking.md
```

## License

Please add a license appropriate for your intended distribution before publishing a release.
