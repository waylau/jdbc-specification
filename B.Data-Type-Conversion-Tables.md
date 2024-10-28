# B. Data Type Conversion Tables（数据类型转换表）


本附录描述了驱动程序必须支持的映射和转换。以下是涵盖的映射和转换内容：

- JDBC 类型映射到 Java 类型
- Java 类型映射到 JDBC 类型
- JDBC 类型映射到 Java 对象类型
- Java 对象类型映射到 JDBC 类型
- `setObject` 和 `setNull` 方法从 Java 对象类型到 JDBC 类型的转换
- `ResultSet` 获取方法支持的类型转换


## B.1 JDBC 类型映射到 Java 类型

**表 B-1** 显示了 JDBC 类型与 Java 类型之间的概念对应关系。程序员在编写代码时应考虑这一映射。例如，如果数据库中的值是 SMALLINT，则在 JDBC 应用程序中应使用 short 数据类型。

除了 `getObject` 外，所有 `CallableStatement` 的 getter 方法都使用此映射。`CallableStatement` 和 `ResultSet` 接口的 `getObject` 方法使用 **表 B-3** 中的映射。

**表 B-1** JDBC 类型映射到 Java 类型

| JDBC 类型 | Java 类型 |
| --- | --- |
| CHAR | String |
| VARCHAR | String |
| LONGVARCHAR | String |
| NUMERIC | java.math.BigDecimal |
| DECIMAL | java.math.BigDecimal |
| BIT | boolean |
| BOOLEAN | boolean |
| TINYINT | byte |
| SMALLINT | short |
| INTEGER | int |
| BIGINT | long |
| REAL | float |
| FLOAT | double |
| DOUBLE | double |
| BINARY | byte[] |
| VARBINARY | byte[] |
| LONGVARBINARY | byte[] |
| DATE | java.sql.Date |
| TIME | java.sql.Time |
| TIMESTAMP | java.sql.Timestamp |
| CLOB | java.sql.Clob |
| BLOB | java.sql.Blob |
| ARRAY | java.sql.Array |
| DISTINCT | 基础类型的映射 |
| STRUCT | java.sql.Struct |
| REF | java.sql.Ref |
| DATALINK | java.net.URL |
| JAVA_OBJECT | 基础 Java 类 |
| ROWID | java.sql.RowId |
| NCHAR | String |
| NVARCHAR | String |
| LONGNVARCHAR | String |
| NCLOB | java.sql.NClob |
| SQLXML | java.sql.SQLXML |


## B.2 Java 类型映射到 JDBC 类型

**表 B-2** 显示了驱动程序应使用的映射规则，用于 `ResultSet` 接口中的更新方法和 IN 参数。`PreparedStatement` 的 setter 方法以及 `RowSet` 的 setter 方法使用此表将 Java 类型的 IN 参数映射到将发送到数据库的 JDBC 类型。请注意，这两个接口的 `setObject` 方法使用 **表 B-4** 中所示的映射。

**表 B-2** 从 Java 类型到 JDBC 类型的标准映射

| Java 类型 | JDBC 类型 |
| --- | --- |
| String | CHAR, VARCHAR, LONGVARCHAR, NCHAR, NVARCHAR 或 LONGNVARCHAR |
| java.math.BigDecimal | NUMERIC |
| boolean | BIT 或 BOOLEAN |
| byte | TINYINT |
| short | SMALLINT |
| int | INTEGER |
| long | BIGINT |
| float | REAL |
| double | DOUBLE |
| byte[] | BINARY, VARBINARY 或 LONGVARBINARY |
| java.sql.Date | DATE |
| java.sql.Time | TIME |
| java.sql.Timestamp | TIMESTAMP |
| java.sql.Clob | CLOB |
| java.sql.Blob | BLOB |
| java.sql.Array | ARRAY |
| java.sql.Struct | STRUCT |
| java.sql.Ref | REF |
| java.net.URL | DATALINK |
| Java 类 | JAVA_OBJECT |
| java.sql.RowId | ROWID |
| java.sql.NClob | NCLOB |
| java.sql.SQLXML | SQLXML |

## B.3 JDBC 类型映射到 Java 对象类型

`ResultSet.getObject` 和 `CallableStatement.getObject` 使用 **表 B-3** 所示的标准映射。

---

注意 – JDBC 1.0 规范将 `SMALLINT` 和 `TINYINT` JDBC 类型的 Java 对象映射定义为 `Integer`。由于在 JDBC 1.0 规范最终确定时，Java 语言中没有 `Byte` 和 `Short` 数据类型，因此将 `SMALLINT` 和 `TINYINT` 映射到 `Integer` 是为了保持向后兼容性。

---

**表 B-3** 从 JDBC 类型到 Java 对象类型的映射

| JDBC 类型       | Java 对象类型                          |
| ------------- | ---------------------------------- |
| CHAR          | String                             |
| VARCHAR       | String                             |
| LONGVARCHAR   | String                             |
| NUMERIC       | java.math.BigDecimal               |
| DECIMAL       | java.math.BigDecimal               |
| BIT           | Boolean                            |
| BOOLEAN       | Boolean                            |
| TINYINT       | Integer                            |
| SMALLINT      | Integer                            |
| INTEGER       | Integer                            |
| BIGINT        | Long                               |
| REAL          | Float                              |
| FLOAT         | Double                             |
| DOUBLE        | Double                             |
| BINARY        | byte[]                             |
| VARBINARY     | byte[]                             |
| LONGVARBINARY | byte[]                             |
| DATE          | java.sql.Date                      |
| TIME          | java.sql.Time                      |
| TIMESTAMP     | java.sql.Timestamp                 |
| DISTINCT      | 底层类型的对象类型                          |
| CLOB          | java.sql.Clob                      |
| BLOB          | java.sql.Blob                      |
| ARRAY         | java.sql.Array                     |
| STRUCT        | java.sql.Struct 或 java.sql.SQLData |
| REF           | java.sql.Ref                       |
| DATALINK      | java.net.URL                       |
| JAVA_OBJECT   | 底层的 Java 类                         |
| ROWID         | java.sql.RowId                     |
| NCHAR         | String                             |
| NVARCHAR      | String                             |
| LONGNVARCHAR  | String                             |
| NCLOB         | java.sql.NClob                     |
| SQLXML        | java.sql.SQLXML                    |


## B.4 Java 对象类型映射到 JDBC 类型

`PreparedStatement.setObject`、`PreparedStatement.setNull`、`RowSet.setNull` 和 `RowSet.setObject` 在没有提供目标 JDBC 类型参数的情况下，使用 **表 B-4** 中的映射。

**表 B-4** 从 Java 对象类型到 JDBC 类型的映射

| Java 对象类型 | JDBC 类型 |
| --- | --- |
| String | CHAR, VARCHAR, LONGVARCHAR, NCHAR, NVARCHAR 或 LONGNVARCHAR |
| java.math.BigDecimal | NUMERIC |
| Boolean | BIT 或 BOOLEAN |
| Byte | TINYINT |
| Short | SMALLINT |
| Integer | INTEGER |
| Long | BIGINT |
| Float | REAL |
| Double | DOUBLE |
| byte[] | BINARY, VARBINARY 或 LONGVARBINARY |
| java.math.BigInteger | BIGINT |
| java.sql.Date | DATE |
| java.sql.Time | TIME |
| java.sql.Timestamp | TIMESTAMP |
| java.sql.Clob | CLOB |
| java.sql.Blob | BLOB |
| java.sql.Array | ARRAY |
| java.sql.Struct | STRUCT |
| java.sql.Ref | REF |
| java.net.URL | DATALINK |
| Java 类 | JAVA_OBJECT |
| java.sql.RowId | ROWID |
| java.sql.NClob | NCLOB |
| java.sql.SQLXML | SQLXML |
| java.util.Calendar | TIMESTAMP |
| java.util.Date | TIMESTAMP |
| java.time.LocalDate | DATE |
| java.time.LocalTime | TIME |
| java.time.LocalDateTime | TIMESTAMP |
| java.time.OffsetTime | TIME_WITH_TIMEZONE |
| java.time.OffsetDateTime | TIMESTAMP_WITH_TIMEZONE |

## B.5 通过 `setObject` 和 `setNull` 将 Java 对象类型转换为 JDBC 类型

**表 B-5** 显示了可以作为目标 JDBC 类型传递给 `PreparedStatement.setObject`、`PreparedStatement.setNull`、`RowSet.setNull` 和 `RowSet.setObject` 方法的 JDBC 类型。

**表 B-5** 由 `setObject` 和 `setNull` 在 Java 对象类型与目标 JDBC 类型之间进行的转换

| Java 对象类型 | 支持的 JDBC 类型 |
| --- | --- |
| String | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, DATE, TIME, TIMESTAMP, NCHAR, NVARCHAR, LONGNVARCHAR |
| java.math.BigDecimal | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Boolean | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Byte | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Short | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Integer | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Long | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Float | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| Double | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR |
| byte[] | BINARY, VARBINARY, 或 LONGVARBINARY |
| java.math.BigInteger | BIGINT, CHAR, VARCHAR, LONGVARCHAR |
| java.sql.Date | CHAR, VARCHAR, LONGVARCHAR, DATE, TIMESTAMP |
| java.sql.Time | CHAR, VARCHAR, LONGVARCHAR, TIME, TIMESTAMP |
| java.sql.Timestamp | CHAR, VARCHAR, LONGVARCHAR, DATE, TIME, TIMESTAMP |
| java.sql.Array | ARRAY |
| java.sql.Blob | BLOB |
| java.sql.Clob | CLOB |
| java.sql.Struct | STRUCT |
| java.sql.Ref | REF |
| java.net.URL | DATALINK |
| Java 类 | JAVA_OBJECT |
| java.sql.RowId | ROWID |
| java.sql.NClob | NCLOB |
| java.sql.SQLXML | SQLXML |
| java.util.Calendar | CHAR, VARCHAR, LONGVARCHAR, DATE, TIME, TIMESTAMP, ARRAY |
| java.util.Date | CHAR, VARCHAR, LONGVARCHAR, DATE, TIME, TIMESTAMP, ARRAY |
| java.time.LocalDate | CHAR, VARCHAR, LONGVARCHAR, DATE |
| java.time.LocalTime | CHAR, VARCHAR, LONGVARCHAR, TIME |
| java.time.LocalDateTime | CHAR, VARCHAR, LONGVARCHAR, DATE, TIME, TIMESTAMP |

## B.6 ResultSet getter 方法支持的类型转换

**表 B-6** 列出了 `ResultSet` getter 方法可能返回的 JDBC 类型。此表还显示了 `SQLInput` 读取方法使用的转换方式，但后者仅使用推荐的转换方式。

**表 B-6** 使用 `ResultSet` getter 方法检索 JDBC 数据类型

| Java 对象类型           | 推荐的 JDBC 类型         | 支持的 JDBC 类型                                                                                                                                                                                                                                                                                                                           |
| ------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| getByte             | TINYINT             | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR, ROWID                                                                                                                                                                                                            |
| getShort            | SMALLINT            | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getInt              | INTEGER             | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getLong             | BIGINT              | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getFloat            | REAL                | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getDouble           | FLOAT, DOUBLE       | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getBigDecimal       | DECIMAL, NUMERIC    | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getBoolean          | BIT, BOOLEAN        | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR                                                                                                                                                                                                                   |
| getString           | CHAR, VARCHAR       | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, DATE, TIME, TIMESTAMP, DATALINK, NCHAR, NVARCHAR, LONGNVARCHAR                                                                                                                 |
| getNString          | NCHAR, NVARCHAR     | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, DATE, TIME, TIMESTAMP, DATALINK, NCHAR, NVARCHAR, LONGNVARCHAR                                                                                                                 |
| getBytes            | BINARY, VARBINARY   | BINARY, VARBINARY, LONGVARBINARY                                                                                                                                                                                                                                                                                                      |
| getDate             | DATE                | CHAR, VARCHAR, LONGVARCHAR, DATE, TIMESTAMP                                                                                                                                                                                                                                                                                           |
| getTime             | TIME                | CHAR, VARCHAR, LONGVARCHAR, TIME, TIMESTAMP                                                                                                                                                                                                                                                                                           |
| getTimestamp        | TIMESTAMP           | CHAR, VARCHAR, LONGVARCHAR, DATE, TIME, TIMESTAMP                                                                                                                                                                                                                                                                                     |
| getAsciiStream      | LONGVARCHAR         | CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, CLOB, NCLOB                                                                                                                                                                                                                                                             |
| getBinaryStream     | LONGVARBINARY       | BINARY, VARBINARY, LONGVARBINARY                                                                                                                                                                                                                                                                                                      |
| getCharacterStream  | LONGVARCHAR         | CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, CLOB, NCHAR, NVARCHAR, LONGNVARCHAR, NCLOB, SQLXML                                                                                                                                                                                                                      |
| getNCharacterStream | LONGNVARCHAR        | CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, CLOB, NCHAR, NVARCHAR, LONGNVARCHAR, NCLOB, SQLXML                                                                                                                                                                                                                      |
| getClob             | CLOB                | CLOB, NCLOB                                                                                                                                                                                                                                                                                                                           |
| getNClob            | NCLOB               | CLOB, NCLOB                                                                                                                                                                                                                                                                                                                           |
| getBlob             | BLOB                | BLOB                                                                                                                                                                                                                                                                                                                                  |
| getArray            | ARRAY               | ARRAY                                                                                                                                                                                                                                                                                                                                 |
| getRef              | REF                 | REF                                                                                                                                                                                                                                                                                                                                   |
| getURL              | DATALINK            | DATALINK                                                                                                                                                                                                                                                                                                                              |
| getObject           | STRUCT, JAVA_OBJECT | TINYINT, SMALLINT, INTEGER, BIGINT, REAL, FLOAT, DOUBLE, DECIMAL, NUMERIC, BIT, BOOLEAN, CHAR, VARCHAR, LONGVARCHAR, BINARY, VARBINARY, LONGVARBINARY, DATE, TIME, TIMESTAMP, CLOB, BLOB, ARRAY, REF, DATALINK, STRUCT, JAVA_OBJECT, ROWID, NCHAR, NVARCHAR, LONGNVARCHAR, NCLOB, SQLXML, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE |
| getRowId            | ROWID               | ROWID                                                                                                                                                                                                                                                                                                                                 |
| getSQLXML           | SQLXML              | SQLXML                                                                                                                                                                                                                                                                                                                                |