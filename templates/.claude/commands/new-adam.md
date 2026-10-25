---
description: 按 ADaM spec 为新数据集搭程序框架
---

为 `$ARGUMENTS`（数据集名，如 `ADAE`）在 `adam/` 下新建程序框架：

1. 先读 `specs/` 下的 ADaM spec，找到该 dataset 的整页定义
2. 生成程序，包含：
   - 标准头注释：目的、输入、输出、spec 版本、作者、日期
   - 输入检查段：逐个确认 spec 列的输入变量在 SDTM/ADSL 里存在，不存在就报错停下
   - 每个衍生变量一段，注释里贴 spec 原文，逻辑处留 TODO
   - 结尾：输出 xpt + 打印 `proc contents` / `str()` 摘要
3. 不要自己编衍生逻辑：spec 没写清楚的变量，逻辑留空并在文件顶部列出"待确认清单"
4. 建完告诉我：哪些变量逻辑是完整的，哪些需要我确认
