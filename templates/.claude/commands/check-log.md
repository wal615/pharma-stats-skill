---
description: 扫描 SAS/R 日志中的 ERROR、WARNING 并汇总
---

扫描日志文件 `$ARGUMENTS`（不传则用 `output/logs/` 下最新的一个）。

1. 逐行找 `ERROR`、`WARNING`（SAS）或 `Error`、`Warning`（R），忽略大小写
2. 按文件分组输出：每个问题给出一行原文 + 行号
3. 常见可忽略的 NOTE（如 "MERGE 有重复 by 值"之外的普通 NOTE）不用列
4. 最后给结论：
   - 有 ERROR → 列出全部，程序算没跑通，停下来等我处理
   - 只有 WARNING → 逐条判断是否影响结果，不确定的标出来问我
   - 都没有 → 回一句"log 干净"即可，不要长篇大论
