# Changelog

All notable changes to SparkEmUp will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2026-10-18
### Added
- First public release of SparkEmUp, a desktop workbench for Apache Spark that runs on your own computer.
- Runtimes: Java 21 and Spark 4.1.3, with Delta Lake, Avro and Excel support, are downloaded on first start and checked against their checksums. Install them for your user, or once for all users of the computer. SparkEmUp uses nothing from your system's Java, Spark, Hadoop or Python setup.
- Notebooks: SQL, Python and Scala cells in notebooks saved as files in a folder you choose, organised in folders and tabs. Run one cell or all of them, use `${variables}`, and refer to another cell's result by name.
- Results: a grid that pages through large results, the cell's output and its query plan, live progress, cancel, and export to Parquet, CSV, JSON, Delta or Avro.
- SQL editor with completion for tables, columns and functions.
- Python cells share one Spark session with SQL and Scala, keep their variables between runs, and have completion and a list of the variables they defined.
- Scala cells run in a Scala interpreter inside Spark, so they can use the session's jars. A startup script can run when Spark starts, for example to set up a library's keys and functions.
- Python can call Scala and Java code in the session's jars, such as a library's helper objects.
- Catalog: browse databases, tables, views and functions. Register files (Parquet, CSV, JSON, Avro, Excel, Delta, ORC, text) and JDBC tables. Databases and tables are kept between restarts.
- Libraries: add jars and Maven packages that load when Spark starts, or add jars and Python files to the running session. Well-known JDBC drivers are set up automatically. A class browser shows what each jar contains.
