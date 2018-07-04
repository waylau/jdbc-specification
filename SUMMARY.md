# Summary

* [主页](README.md)
* [1. Introduction（介绍）](1.Introduction.md)
    * 1.1 The JDBC API 3
    * 1.2 Platforms 3
    * 1.3 Target Audience 4
    * 1.4 Acknowledgements 4
* [2. Goals（目标）](2. Goals.md)
    * 2.1 History 7
    * 2.2 Overview of Goals 7
* [3. Summary of New Features（新特性）](3.Summary-of-New-Features.md)
    * 3.1 Overview of changes 11
* [4. Overview（概览）](4.Overview.md)
    * 4.1 Establishing a Connection 15
    * 4.2 Executing SQL Statements and Manipulating Results 16
        * 4.2.1 Support for SQL Advanced Data Types 17
    * 4.3 Two-tier Model 17
    * 4.4 Three-tier Model 18
    * 4.5 JDBC in the Java EE Platform 20
* [5. Classes and Interfaces（类与接口）](5.Classes-and-Interface.md)
    * 5.1 The java.sql Package 21
    * 5.2 The javax.sql Package 25
* [6. Compliance（合规性）](6.Compliance.md)
    * 6.1 Definitions 29
    * 6.2 Guidelines and Requirements 30
    * 6.3 JDBC 4.2 API Compliance 31
    * 6.4 Java EE JDBC Compliance 35
* [7. Database Metadata（数据库元数据）](7.Database-Metadata.md)
    * 7.1 Creating a DatabaseMetadata Object 38
    * 7.2 Retrieving General Information 38
    * 7.3 Determining Feature Support 39
    * 7.4 Data Source Limits 39
    * 7.5 SQL Objects and Their Attributes 40
    * 7.6 Transaction Support 40
    * 7.7 New Methods 41
    * 7.8 Modified Methods 41
* [8. Exceptions（异常）](8.Exceptions.md)
    * 8.1 SQLException 43
        * 8.1.1 Support for the Java SE Chained Execeptions 44
        * 8.1.2 Navigating SQLExceptions 44
        * 8.1.2.1 Using a For-Each Loop with SQLExceptions 45
    * 8.2 SQLWarning 46
    * 8.3 DataTruncation 46
        * 8.3.1 Silent Truncation 47
    * 8.4 BatchUpdateException 47
    * 8.5 Categorized SQLExceptions 48
        * 8.5.1 NonTransient SQLExceptions 48
        * 8.5.2 Transient SQLExceptions 49
        * 8.5.3 SQLRecoverableException 50
    * 8.6 SQLClientinfoException 50
* [9. Connections（连接）](9.Connections.md)
    * 9.1 Types of Drivers 52
    * 9.2 The Driver Interface 52
        * 9.2.1 Loading a driver that implements java.sql.Driver 53
    * 9.3 The DriverAction Interface 53
    * 9.4 The DriverManager Class 54
    * 9.5 The SQLPermission Class 56
    * 9.6 The DataSource Interface 56
        * 9.6.1 DataSource Properties 57
        * 9.6.2 The JNDI API and Application Portability 58
        * 9.6.3 Getting a Connection with a DataSource Object 59
        * 9.6.4 Closing Connection Objects 59
            * 9.6.4.1 Connection.close 60
            * 9.6.4.2 Connection.isClosed 60
            * 9.6.4.3 Connection.isValid 60
* [10. Transactions（事务）](10.Transactions.md)
    * 10.1 Transaction Boundaries and Auto-commit 61
        * 10.1.1 Disabling Auto-commit Mode 62
    * 10.2 Transaction Isolation Levels 62
        * 10.2.1 Using the setTransactionIsolation Method 63
        * 10.2.2 Performance Considerations 64
    * 10.3 Savepoints 64
        * 10.3.1 Setting and Rolling Back to a Savepoint 65
        * 10.3.2 Releasing a Savepoint 65
* [11. Connection Pooling（连接池）](11.Connection-Pooling.md)
* [12. Distributed Transactions（分布式事务）](12.Distributed-Transactions.md)
* [13. Statements（语句）](13.Statements.md)
* [14. Batch Updates（批量更新）](14.Batch-Updates.md)
* [15. Result Sets（结果集）](15.Result-Sets.md)
* [16. Advanced Data Types（高级数据类型）](16.Advanced-Data-Types.md)
* [17. Customized Type Mapping（自定义类型映射）](17.Customized-Type-Mapping.md)
* [18. Relationship to Connectors（与连接器的关系）](18.Relationship-to-Connectors.md)
* [19. Wrapper Interface（包装器接口）](19.Wrapper-Interface.md)
* [A. Revision History（修订记录）](A.Revision-History.md)
* [B. Data Type Conversion Tables（数据类型转换表）](B.Data-Type-Conversion-Tables.md)
* [C. Scalar Functions（标量函数）](C.Scalar-Functions.md)
* [D. Related Documents（相关文档）](D.Related-Documents.md)

