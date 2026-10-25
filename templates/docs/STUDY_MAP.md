# docs/STUDY_MAP.md —— 全项目索引（人工维护，Claude Code 只读）

> 原则：一 dataset / 一张表一行，只写"是什么、在哪、找谁"，不复制逻辑细节。
> 每次 spec 定稿或新增程序后更新这一份文件。

## 数据流
```
SDTM → adam/*.sas → output/adam/*.xpt → tlf/*.sas → output/tlf/*.rtf
```

## ADaM 数据集

| 数据集 | 程序 | 输入 | 关键衍生变量 | spec 位置 | 状态 | 备注 |
|--------|------|------|--------------|-----------|------|------|
| ADSL | adam/adsl.sas | DM, DS, EX | TRTSDT, SAFFL, ITTFL | specs/adam_spec.xlsx#ADSL | 定稿 | - |
| ADAE | adam/adae.sas | AE, ADSL | TRTEMFL, AESER | specs/adam_spec.xlsx#ADAE | 起草 | 等 spec v0.3 |
| [ADXX] | | | | | | |

## TLF 清单

| 编号 | 程序 | 输入 ADaM | Shell 位置 | 状态 | 复核人 | 备注 |
|------|------|-----------|------------|------|--------|------|
| T1.1 | tlf/t_demog.sas | ADSL | specs/tlf_shell.pdf p.3 | 定稿 | [姓名] | - |
| F2.1 | tlf/f_ae_plot.R | ADAE | specs/tlf_shell.pdf p.12 | 起草 | - | - |
| [编号] | | | | | | |

## 关键宏

| 宏 | 位置 | 用途 | 注意事项 |
|----|------|------|----------|
| %trtdate | macros/trtdate.sas | 统一算 TRTSDT/TRTEDT | 所有含治疗日期的 dataset 都用它 |
| [宏名] | | | |

## 术语 / 约定速查
- [如：SAFFL=1 表示接受过至少一次研究药物，定义见 SAP §5.2]
