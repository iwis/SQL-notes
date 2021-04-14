Scalar SQL functions differ quite significantly among RDBMS. The following steps can be done to reduce this difference:

 1. **In SQL Server add the `LENGTH` alias for the `LEN` function**
    
    **Explanation**: All the following databases: PostgreSQL, Oracle, SQLite, and MySQL have the `LENGTH(s)` function. Only SQL Server doesn't have it.
    
    **Issue**: https://feedback.azure.com/forums/908035-sql-server/suggestions/35327518-create-an-command-alias-length-for-len

 2. **In SQL Server add the `SUBSTR` alias for the `SUBSTRING` function**
    
    **Explanation**: This is the current syntax of the `SUBSTR[ING]` functions in ANSI standard and in different RDBMS:

        ANSI standard:      SUBSTRING  (s FROM start [FOR length])
        PostgreSQL & MySQL: SUBSTR[ING](s, start [,length])
        Oracle & SQLite:    SUBSTR     (s, start [,length])
        SQL Server:         SUBSTRING  (s, start  ,length )

      To unify the syntax, I propose to make the last attribute (`length`) optional, and to add the `SUBSTR` alias. Thanks to this, we will be able to use the `SUBSTR(s, start [,length])` syntax in all above-mentioned RDBMS.

    **Issue**: https://feedback.azure.com/forums/908035-sql-server/suggestions/38443486-to-enhance-sql-s-code-compatibility-and-ease-devel

 3. **In Oracle and SQLite add the `SUBSTRING` alias for the `SUBSTR` function**
    
    **Explanation**: This is the current syntax of the `SUBSTR[ING]` functions in ANSI standard and in different RDBMS:

        ANSI standard:      SUBSTRING  (s FROM start [FOR length])
        PostgreSQL & MySQL: SUBSTR[ING](s, start [,length])
        Oracle & SQLite:    SUBSTR     (s, start [,length])
        SQL Server:         SUBSTRING  (s, start  ,length )

      To unify the syntax, I propose to add the `SUBSTRING` alias to the `SUBSTR` function. If both Oracle and SQLite do the same, we will be able to use the `SUBSTRING(s, start, length)` syntax in all above-mentioned RDBMS.

    **Issues**:
     - https://community.oracle.com/tech/developers/discussion/4477919/proposal-add-the-substring-alias-for-the-substr-function/
     - https://www.sqlite.org/forum/info/5e23745f14d22a94 - **will be implemented in [SQLite 3.34](https://sqlite.org/draft/releaselog/3_34_0.html)**

 4. **In Oracle add an optional argument `c` after a comma in the `TRIM(s)` function (the space `' '` by default)**
    
    **Explanation**: We can now call the following functions in Oracle:

        LTRIM(s [,c])
        RTRIM(s [,c])
        TRIM (s)

      We can pass the argument c after the comma in the `LTRIM` and `RTRIM` functions, but not in the `TRIM` function. For the `TRIM` function we have to use the SQL standard syntax: `TRIM(c FROM s)`. This is an odd limitation. In PostgreSQL and SQLite calling `TRIM(s, c)` is possible.
      
    **Issues**: https://community.oracle.com/tech/developers/discussion/4477917/proposal-add-an-optional-argument-c-after-a-comma-in-the-trim-s-function/

 5. **In MySQL add an optional argument `c` after a comma in the `[L|R]TRIM(s)` functions (the space `' '` by default)**
    
    **Explanation**: Currently, you can call the following functions in MySQL: `[L|R]TRIM(s)`. In PostgreSQL and SQLite we can also call `[L|R]TRIM(s, c)`.
    
    **Issues**: https://bugs.mysql.com/bug.php?id=101719

 6. **In MySQL make the last argument of the `{L|R}PAD(s, length, c)` functions optional (the space `' '` by default)**
    
    **Explanation**: The last argument `c` is optional in PostgreSQL and Oracle.

    **Issues**: https://bugs.mysql.com/bug.php?id=101720

 7. **Add the `CEIL` alias for the `CEILING` function in SQL Server, and the `CEILING` alias for the `CEIL` function in Oracle**

    **Explanation**: Both the `CEIL` and `CEILING` functions are defined in ANSI SQL Standard, and implemented in PostgreSQL and MySQL. However Oracle implements only `CEIL` function, and SQL server implements only `CEILING` function.

    **Issues**:
     - https://feedback.azure.com/forums/908035-sql-server/suggestions/42027004-add-the-ceil-alias-for-the-ceiling-function
     - https://community.oracle.com/tech/developers/discussion/4479182/add-the-ceiling-alias-for-the-ceil-function/

 8. **Implement ANSI SQL standard `TRIM`, `SUBSTRING` and `POSITION` string functions in Oracle, SQL Server and SQLite**

    **Explanation**: The SQL Standard defines, among others, these functions operating on text strings:

        TRIM([[LEADING|TRAILING|BOTH] [c] FROM] s)
        SUBSTRING(s FROM start [FOR length])
        POSITION(s2 IN s)

    They are already implemented by PostgreSQL and MySQL. Oracle implements only `TRIM` function according to SQL Standard. I propose to implement these 3 functions in Oracle, SQL Server and SQLite as well.

    Currently, SQL Server implements the following functions that work identically to the ANSI SQL Standard:

        [L|R]TRIM([c FROM] s)
        SUBSTRING(s, start, length)
        CHARINDEX(s2, s)

    SQLite implements the following functions that work identically to the ANSI SQL Standard:

        [L|R]TRIM(s [,c])
        SUBSTR(s, start [,length])
        INSTR(s, s2)

    and Oracle implements the following functions that work identically to the ANSI SQL Standard:

        SUBSTR(s, start [,length])
        INSTR(s, s2)

    **Issues**:
     - https://community.oracle.com/tech/developers/discussion/4479181/implementing-substring-and-position-standard-sql-string-functions/
     - https://feedback.azure.com/forums/908035-sql-server/suggestions/42319423-implementing-trim-substring-and-position-standard
     - https://www.sqlite.org/forum/forumpost/ec40559580

 9. **Add the `MOD` function in SQL Server and SQLite**

    **Explanation**: The ANSI SQL Standard defines `MOD(x, y)` function which returns division remainder. It is already implemented in PostgreSQL, MySQL, and Oracle.
    Currently, SQL Server and SQLite implement only modulo operator: `x % y`.

    **Issues**:
     - https://feedback.azure.com/forums/908035-sql-server/suggestions/42325678-implement-the-mod-x-y-function
     - https://www.sqlite.org/forum/forumpost/cec68c38f0

These steps will reduce the number of exceptions described in parentheses in the [Functions.txt](Functions.txt) file.
