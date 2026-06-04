# :material-microsoft-excel: Excel的技巧

## 好用的函数

### XLOOKUP函数

+ 在 Excel 中，要保持公式中的引用在横拉时不改变列，需要使用 绝对引用符号`$`。

```excel title="excel"

    =XLOOKUP(lookup_value,lookup_array,return_array) //单条件查询

    =XLOOKUP(lookup_value1&lookup_value2,lookup_array,return_array) //多条件查询

```