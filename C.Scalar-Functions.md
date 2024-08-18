# C. Scalar Functions（标量函数）


JDBC API 支持对标量值进行数值、字符串、时间、日期、系统和转换函数的转义语法。这些标量函数可以按照 [13.4.1 节 "标量函数"](13-114 页) 中描述的方式在 SQL 字符串中使用。Open Group CLI 规范提供了关于标量函数语义的更多信息。以下列出了这些标量函数供参考。

如果 DBMS 支持某个标量函数，驱动程序也应支持该函数。由于不同的 DBMS 支持的标量函数的语法略有不同，因此驱动程序的任务是将它们映射到适当的语法，或者直接在驱动程序中实现这些函数。

用户可以通过调用元数据方法来查询支持的函数。例如，`DatabaseMetaData.getNumericFunctions` 方法返回支持的数值函数的 Open Group CLI 名称的逗号分隔列表。同样，`DatabaseMetaData.getStringFunctions` 方法返回支持的字符串函数列表，依此类推。

标量函数按类别列出如下:

## C.1 数值函数

|函数名称 | 函数返回值|
|--- | --- |
|ABS(number) | number 的绝对值|
|ACOS(float) | float 的反余弦，以弧度表示| 
|ASIN(float) | float 的反正弦，以弧度表示|
|ATAN(float) | float 的反正切，以弧度表示| 
|ATAN2(float1, float2) | float2 / float1 的反正切，以弧度表示|
|CEILING(number) | 大于或等于 number 的最小整数|
|COS(float)| float 弧度的余弦值|
|COT(float)| float 弧度的余切值|
|DEGREES(number)| number 弧度的度数|
|EXP(float)| float 的指数函数|
|FLOOR(number)| 小于或等于 number 的最大整数|
|LOG(float)| float 的自然对数（以 e 为底）|
|LOG10(float) | float 的常用对数（以 10 为底）|
|MOD(integer1, integer2)| integer1 / integer2 的余数|
|PI()| 常量 pi|
|POWER(number, power)| number 的 power 次幂|
|RADIANS(number)| number 度数的弧度|
|RAND(integer)| 基于种子 integer 的随机浮点数|
|ROUND(number, places)| number 四舍五入到 places 位小数|
|SIGN(number)| -1 表示 number < 0；<br/> 0 表示 number = 0；<br/> 1 表示 number > 0|
|SIN(float) | float 弧度的正弦值|
|SQRT(float) | float 的平方根|
|TAN(float) | float 弧度的正切值|
|TRUNCATE(number, places) | number 截断到 places 位小数|


## C.2 字符串函数

|函数名称 | 函数返回值|
|---|---|
|ASCII(string)| 返回字符串 string 中最左边字符的 ASCII 码值的整数表示|
|CHAR(code) | 返回 ASCII 码值为 code 的字符，code 的取值范围在 0 到 255 之间|
|CHAR_LENGTH(string [,CHARACTERS\|OCTETS]) | 如果 string 是字符数据类型，则返回字符串表达式的字符长度；否则返回字符串表达式的字节长度，其结果为不小于位数除以 8 的最小整数|
|CHARACTER_LENGTH(string [,CHARACTERS\|OCTETS]) | CHAR_LENGTH(string) 的同义词|
|CONCAT(string1, string2) | 通过将 string2 附加到 string1 后形成的字符字符串；如果字符串为空，则结果取决于 DBMS|
|DIFFERENCE(string1, string2) | 返回表示 string1 和 string2 的 SOUNDEX 函数值之间差异的整数|
|INSERT(string1, start, length, string2) | 通过从 string1 中删除从 start 开始的 length 个字符，并将 string2 插入 string1 的 start 位置，形成一个字符字符串|
|LCASE(string)| 将字符串 string 中的所有大写字符转换为小写字符|
|LEFT(string, count) | 返回字符串 string 的最左边 count 个字符|
|LENGTH(string [,CHARACTERS\|OCTETS]) | 返回字符串 string 中的字符数，不包括尾部空格|
|LOCATE(string1, string2[, start]) | 返回 string2 中第一次出现 string1 的位置，从 string2 的开头开始搜索；如果指定了 start，则从 start 位置开始搜索。如果 string2 不包含 string1，则返回 0。位置 1 是 string2 中的第一个字符|
|LTRIM(string) | 返回去除前导空格的字符串 string|
|OCTET_LENGTH(string) | 返回字符串表达式的字节长度，其结果为不小于位数除以 8 的最小整数|
|POSITION(substring IN string[, CHARACTERS\|OCTETS]) | 返回子字符串 substring 在字符串 string 中首次出现的位置，结果为 NUMERIC，具有实现定义的精度和 0 的小数位|
|REPEAT(string, count) | 返回由重复 string count 次形成的字符字符串|
|REPLACE(string1, string2, string3) | 将 string1 中的所有 string2 替换为 string3|
|RIGHT(string, count) | 返回字符串 string 的最右边 count 个字符|
|RTRIM(string) | 返回去除尾部空格的字符串 string|
|SOUNDEX(string) | 返回一个字符字符串，它依赖于数据源，表示字符串 string 中单词的发音；这可能是一个四位数的 SOUNDEX 代码，每个单词的语音表示等|
|SPACE(count) | 返回由 count 个空格组成的字符字符串|
|SUBSTRING(string, start, length [,CHARACTERS\|OCTETS]) | 返回通过从字符串 string 的 start 位置开始提取 length 个字符形成的字符字符串|
|UCASE(string) | 将字符串 string 中的所有小写字符转换为大写字符|

---

注意 – SQL 2003 特性 T061，“UCS 支持”，是数据库支持 OCTETS 所必需的。

---


## C.3 时间和日期函数

|函数名称 | 函数返回值|
|--- | --- |
|CURRENT_DATE[()] | CURDATE() 的同义词|
|CURRENT_TIME[()] | CURTIME() 的同义词|
|CURRENT_TIMESTAMP[()] | NOW() 的同义词|
|CURDATE() | 作为日期值的当前日期|
|CURTIME() | 作为时间值的当前本地时间|
|DAYNAME(date) | 表示日期 date 中“天”部分的字符字符串；天的名称是数据源特有的|
|DAYOFMONTH(date) | 介于 1 到 31 之间的整数，表示日期 date 中的月份中的天|
|DAYOFWEEK(date) | 介于 1 到 7 之间的整数，表示日期 date 中的星期几；1 代表星期日|
|DAYOFYEAR(date)| 介于 1 到 366 之间的整数，表示日期 date 中的年份中的天|
|EXTRACT(field FROM source)| 从源中提取字段部分。源是一个日期时间值。字段的值可以是以下之一：YEAR、MONTH、DAY、HOUR、MINUTE、SECOND|
|HOUR(time) | 介于 0 到 23 之间的整数，表示时间 time 的小时部分|
|MINUTE(time)| 介于 0 到 59 之间的整数，表示时间 time 的分钟部分|
|MONTH(date) | 介于 1 到 12 之间的整数，表示日期 date 的月份部分|
|MONTHNAME(date)| 表示日期 date 中月份部分的字符字符串；月份的名称是数据源特有的|
|NOW() | 表示当前日期和时间的时间戳值|
|QUARTER(date) | 介于 1 到 4 之间的整数，表示日期 date 中的季度；1 代表 1 月 1 日到 3 月 31 日|
|SECOND(time)| 介于 0 到 59 之间的整数，表示时间 time 的秒部分|
|TIMESTAMPADD(interval, count, timestamp) | 通过将 count 数量的 interval 添加到时间戳 timestamp 中计算得出的时间戳；interval 可以是以下之一：SQL_TSI_FRAC_SECOND、SQL_TSI_SECOND、SQL_TSI_MINUTE、SQL_TSI_HOUR、SQL_TSI_DAY、SQL_TSI_WEEK、SQL_TSI_MONTH、SQL_TSI_QUARTER 或 SQL_TSI_YEAR|
|TIMESTAMPDIFF(interval, timestamp1, timestamp2) | 表示时间戳 timestamp2 大于时间戳 timestamp1 的 interval 数量的整数；interval 可以是以下之一：SQL_TSI_FRAC_SECOND、SQL_TSI_SECOND、SQL_TSI_MINUTE、SQL_TSI_HOUR、SQL_TSI_DAY、SQL_TSI_WEEK、SQL_TSI_MONTH、SQL_TSI_QUARTER 或 SQL_TSI_YEAR|
|WEEK(date)| 介于 1 到 53 之间的整数，表示日期 date 中的年份中的第几周|
|YEAR(date) | 表示日期 date 中年份部分的整数|


## C.4 系统函数

| 函数名称 | 函数返回值 |
| --- | --- |
| DATABASE() | 数据库名称 |
| IFNULL(expression, value) | 如果 expression 为 null，则返回 value；如果 expression 不为 null，则返回 expression |
| USER() | DBMS 中的用户名 |

## C.5 转换函数

| 函数名称 | 函数返回值 |
| --- | --- |
| CONVERT(value, SQLtype) | 将 value 转换为 SQLtype，SQLtype 可以是以下 SQL 类型之一：SQL_BIGINT、SQL_BINARY、SQL_BIT、SQL_BLOB、SQL_BOOLEAN、SQL_CHAR、SQL_CLOB、SQL_DATE、SQL_DECIMAL、SQL_DATALINK、SQL_DOUBLE、SQL_FLOAT、SQL_INTEGER、SQL_LONGVARBINARY、SQL_LONGNVARCHAR、SQL_LONGVARCHAR、SQL_NCHAR、SQL_NCLOB、SQL_NUMERIC、SQL_NVARCHAR、SQL_REAL、SQL_ROWID、SQL_SQLXML、SQL_SMALLINT、SQL_TIME、SQL_TIMESTAMP、SQL_TINYINT、SQL_VARBINARY 或 SQL_VARCHAR |

---

**注意** – 早期版本的 JDBC 规范定义了不带 SQL_ 前缀的 SQLtype，例如 BIGINT 和 BINARY。JDBC 驱动程序应继续支持这种形式的 SQLtype。

---