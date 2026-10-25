# sdtm/ 目录约定

- SDTM 是上游交付数据，统计**只读不改**
- 需要确认映射问题时，去看 `specs/` 下的 SDTM mapping spec，不要直接改数
- 发现数据疑问：记录到 `docs/data_queries.md`（有疑问就记，不要自己"修"数据）
- 做 ADaM 前先用 `/new-adam` 框架里的输入检查段核对 SDTM 变量是否存在
