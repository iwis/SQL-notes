The repository contains notes about parts of SQL that differ the most in **PostgreSQL**, **MySQL**, **Oracle**, **SQL Server**, and **SQLite**. Currently there are notes about:
 - organization of DBMSs (databases, schemas, users, connecting to DBMS, the `SET ROLE` statement, referencing database objects, synonyms, tablespaces),
 - string, mathematical, and time built-in functions,
 - access control,
 - triggers (I didn't describe triggers in SQL Server, because their syntax differs significantly from other DBMSs),
 - sequences,
 - paging the result of a SELECT query,
 - query optimization (indexes and query execution plan).

The notes are quite complete. At the same time, they are concise, because I wrote information common for all DBMS, and marked the differences.

# DBMS organization
Sources of information:
 - https://stackoverflow.com/questions/7942520/relationship-between-catalog-schema-user-and-database-instance
 - the documentations of PostgreSQL, MySQL, Oracle, and SQL Server

# Built-in functions
Sources of information:
 - [syntax](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html) and [description](https://crate.io/docs/sql-99/en/latest/) of the SQL Standard,
 - draft of the SQL:2011 Standard - drafts of all parts are linked as "SQL:20nn Working Draft Documents" at http://www.wiscorp.com/SQLStandards.html,
 - the documentations of PostgreSQL, MySQL, Oracle, SQL Server, and SQLite - I checked them in November 2020

# DDL - Triggers
Sources of information:
 - syntax of [trigger definition](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#_11_49_trigger_definition) in the SQL Standard and its [description](https://crate.io/docs/sql-99/en/latest/chapters/24.html),
 - PostgreSQL, MySQL, and SQLite documentation about triggers.
 I already knew how triggers work in Oracle, so I haven't read Oracle documentation.

The `triggers-additional-info.md` file contains additional notes about DML triggers in PostgreSQL and about system triggers.

# DDL - Sequences
Sources of information:
 - syntax of [sequence definition](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#_11_72_sequence_generator_definition) and [its usage](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#_6_14_next_value_expression) in SQL Standard,
 - PostgreSQL, MySQL, Oracle, SQL Server, and SQLite documentation about sequences,
 - additionally, I read about the alternative of a sequence - an *"identity"* field generated automatically from an implicit sequence - both in [SQL Standard](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#identity-column-specification) and in PostgreSQL, MySQL, Oracle, SQL Server and SQLite documentation.

# SQL - Paging
Sources of information:
 - syntax of [OFFSET](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#result-offset-clause) and [FETCH FIRST](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#fetch-first-clause) clauses in SQL Standard,
 - PostgreSQL, MySQL, Oracle, SQL Server, and SQLite documentation.

# Access control - DCL
Sources of information:
 - [syntax](https://jakewheat.github.io/sql-overview/sql-2016-foundation-grammar.html#_12_access_control) in the SQL Standard and its [description](https://crate.io/docs/sql-99/en/latest/chapters/15.html),
 - the tutorials and documentations of PostgreSQL, MySQL, Oracle, and SQL Server,
 - [Security: Access Rights in SQL](http://users.informatik.uni-halle.de/~brass/db06/db_secur.pdf) slides (they are available also in https://web.archive.org/).

# Query optimization
Sources of information:
 - Wikipedia articles about [indexes](https://en.wikipedia.org/wiki/Database_index) and [query plans](https://en.wikipedia.org/wiki/Query_plan),
 - PostgreSQL, MySQL, SQL Server, and SQLite documentation about indexes. I only read the most essential information in the SQL Server documentation. I already knew how indexes work in Oracle, so I haven't read Oracle documentation.
 - [use-the-index-luke.com/sql/explain-plan](https://use-the-index-luke.com/sql/explain-plan) and subpages.

# Symbols and marking used in the notes
The following marking are used in the notes:
 - green underscore - syntax or behavior defined by SQL Standard
 - orange underscore - differences in RDBMS
 - blue underscore - when was a syntax introduced to a RDBMS?
 - purple underscore - this information is related to transactions
 - `P` `M` `O` `S` `L` - each letter means respectively: PostgreSQL, MySQL, Oracle, SQL Server, SQLite; they are used on the left margin or in parentheses: (`PMOSL`: ...)
 - `[..]` - an option
 - `{..|..}` - a choice (sometimes also: `..|..` if it isn't ambiguous, e.g. `[..|..]` - an optional choice)
 - `∨` - logical "or"
 - `=>` - logical implication
 - `≡` - equality (used for example for aliases)

All SQL keywords are written in `UPPERCASE`.

# Generating PDF files
The PDF files were generated from the DOCX files, which are available at the `src` directory, using Microsoft Word 2016.
