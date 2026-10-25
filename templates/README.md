# Claude Code 药厂统计模板

给统计师（SAS / R）在 Claude Code 里用的上下文模板：分层 CLAUDE.md + 常用命令 + subagent + 权限配置。

## 安装

把整个文件夹的内容复制到你的 study 项目根目录：

```
你的项目/
├── CLAUDE.md                  ← 根：导航地图 + 铁律
├── adam/CLAUDE.md             ← ADaM 目录约定
├── tlf/CLAUDE.md              ← TLF 目录约定
├── sdtm/CLAUDE.md             ← SDTM 只读约定
├── specs/CLAUDE.md            ← spec 只读声明
├── docs/STUDY_MAP.md          ← 全项目索引（人工维护）
└── .claude/
    ├── commands/              ← /check-log /qc-tlf /new-adam
    ├── agents/                ← study-explorer / tlf-reviewer
    └── settings.json          ← 权限与 hook
```

然后把所有 `[方括号]` 替换成你项目的实际内容。

## 第一次用：让 explorer 给你画地图

```bash
# 在项目根目录启动 Claude Code 后：
> 用 study-explorer 把这个 study 扫一遍，生成 docs/STUDY_MAP.md
```

之后每个新 session，它会自动读到根 CLAUDE.md + 当前目录的 CLAUDE.md。

## 常用工作流

```bash
# 写一个新的 ADaM 程序（按 spec 搭框架）
> /new-adam ADAE

# 跑完程序检查 log
> /check-log output/logs/adae.log

# TLF 写完做 QC
> /qc-tlf tlf/t_ae_summary.sas

# 独立复核（派 subagent，不污染主 session 上下文）
> 用 tlf-reviewer 复核 output/t_ae_summary.rtf，报告写到 docs/review_20261012.md
```

## 关键习惯

- **一次一件事**：一个 session 只做一个 dataset 或一张表，切换任务开新 session。
- **长了就 compact**：`/compact` 时加一句指令，如"保留 ADSL 衍生逻辑的关键决策"。
- **只给元数据**：define.xml、spec、数据字典可以给；原始受试者数据不进对话。
- **人审**：大改前用 Plan 模式出 plan 存档，你审完再执行；正式分析的代码必须人复核。

## 合规提醒

- 用公司 IT 批准的部署方式（如 Bedrock 上的 Claude / 企业版），不要把数据喂给公网 API。
- 保留 session 日志，审计时可追溯。
- 这套模板是效率工具，不改变你们 SOP 里"独立 QC / 双人复核"的要求。
