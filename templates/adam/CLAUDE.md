# adam/ 目录约定

- 命名：一 dataset 一程序，如 `adsl.sas` / `adae.R`；输出同名 `.xpt` 到 `../output/adam/`
- 每个程序头必须写：目的、输入、输出、spec 版本、作者、日期
- 衍生逻辑必须和 `specs/` 下的 ADaM spec 逐条一致；不一致时停下来问我，不要自己发挥
- 关键衍生（如 TRTSDT、SAFFL、TRTEMFL）优先复用 `macros/` 下的宏，不要重写
- 新程序先用 `/new-adam` 搭框架
- 跑完必须 `/check-log`，零 ERROR 才能算完
