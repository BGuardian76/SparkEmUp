# Changelog

All notable changes to SparkEmUp will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- Azure storage: connections to storage accounts with an account key, a SAS token, a service principal or the Azurite emulator. Secrets are kept in your system's keychain, or only for the current run if you prefer. Browse containers and folders, preview files, see their properties, create folders, rename, move and delete, and make SAS links. A transfers queue handles downloads, uploads and copies between accounts.
- Spark can read and write Azure storage: turn on "Use in Spark" on a connection and its credentials go into the session, kept up to date when Spark restarts or the connection changes. Account keys are hidden in the UI and the logs.
- Azure sign-in, with the Azure CLI's login or SparkEmUp's own browser sign-in. Switch tenants, browse subscriptions, resource groups and resources, and add a storage account as a connection from there.
- Remote Spark: each notebook chooses where it runs, either the local Spark or a remote target. A target is a Spark Connect server (with or without TLS and a token) or a Databricks cluster (with a personal access token or the Azure sign-in). A stopped Databricks cluster is started when you connect, and you can see its recent events. SQL and Python cells run on the target. Scala cells, Spark jobs, plans and lineage still need the local Spark.
- Jobs panel: live Spark jobs and their stages. Each cell also gets a Jobs tab that follows its run, and a stage opens to its task list and a task summary that warns about skew.
- Plans as run: each run's final physical plan with operator metrics, in an "As run" view of the Plan tab.
- Lineage panel: what each cell read and wrote, and which source columns each output column comes from.
- Delta tab for Delta tables: overview, history, schema, files and health, plus optimize, vacuum, restore, delete, clone, table properties, protocol, convert and create.
- Jar check: the Libraries view warns about jars that clash with Spark's own classes or with each other, and about classes your jars need but nothing provides. The class browser names the missing dependencies of a class.
- Browse… buttons next to file and folder paths, using your system's file dialogs.

### Changed
- The notebook header and its open panels stay at the top while the cells scroll.
- The Python and Scala variable panels open on their own and can both be open at once.

### Fixed
- On Windows, a user folder with non-ASCII letters (such as `C:\Users\Ramón`) no longer creates a wrongly named data folder.
- When a startup library breaks Spark, the start now fails at once with the error and names the startup libraries, instead of retrying for two minutes.

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
