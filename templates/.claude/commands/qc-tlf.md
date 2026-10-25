---
description: 按 QC 清单核对 TLF 程序与输出
---

对 `$ARGUMENTS`（TLF 程序路径，如 `tlf/t_demog.sas`）做 QC：

1. 找到它在 `docs/STUDY_MAP.md` 里对应的编号和 shell 位置，读 shell
2. 逐项核对输出（`output/tlf/` 下同名文件）：
   - [ ] 标题、脚注与 shell 逐字一致
   - [ ] 分组、排序、分析人群与 SAP/spec 一致
   - [ ] N 数、分母与 ADaM 对得上（抽查至少一组）
   - [ ] 小数位、单位、四舍五入符合 SAP
   - [ ] 程序 log 干净（调 `/check-log`）
   - [ ] 没有硬编码的日期、路径、临时测试代码
3. 输出 QC 报告：通过项打勾，不通过项说明问题 + 定位到代码行号
4. 不通过的不许标"完成"，修完重跑再 QC
