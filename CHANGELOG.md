# Changelog

All notable changes to SparkEmUp will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.1] - 2026-10-26
### Added
- Startup steps in Spark profiles: Scala files, Python files and notebooks (all their cells, or only the ones you pick) that run before any notebook does. Scala files and the notebooks' Scala and SQL cells run once each time Spark starts. Python files and Python cells run in each notebook's Python before its first cell, so their imports and helpers are there in every notebook. A step that fails stops the ones after it, and a "Startup failed" button in the status bar shows which step failed, its error and its output. A profile's old Scala startup script carries over as its first step.
- Delta settings in Spark profiles: turn Delta Lake off for a lighter Spark, or make new tables Delta by default, and switch optimized writes, auto compaction, adding new columns on write, deletion vectors and change data feed for new tables, and VACUUM's 7-day check.
- "Size for your data" in Spark profiles: small, medium and large data presets worked out from your computer's cores and memory. Each sets the cores, the driver's memory, the largest result and the shuffle partitions, and says why.
- Settings → Maven & network: Maven repositories with a login (user and password or token), Azure Artifacts feeds with a personal access token, and a proxy (off, the system's, or set by hand). The proxy is used for Maven, runtime downloads, Azure, Databricks, Python cells, and Spark's own Azure and S3 file systems. Passwords are kept in your system's keychain or only for the current run, and Test shows what each repository answered.
- Libraries tab: every library of a profile in one list with a details pane, and an Add library… dialog that searches Maven Central as you type, flags packages built for another Scala version, and offers each package's versions with their dates.
- The Catalog and Delta tabs work on remote Spark targets too, including Databricks with Unity Catalog's catalogs. A target picker in the Catalog header connects only when asked.
- Azure: search resources by name and type across every subscription.
- Notebook tree: a filter box that finds notebooks by name, and searches inside notebooks for text in their cells. A match opens the notebook at that cell with the text selected.
- Add cells anywhere: a "+ cell" button shows between cells and before the first one, and its menu picks the language or sets the notebook's default. Cells can be moved up and down.
- Cells:
  - Tab indents (4 spaces in Python, 2 in Scala and SQL) and Shift+Tab unindents. Escape then Tab still moves the focus on.
  - Word wrap can be turned off per cell from its menu, or with Alt+Z.
  - The code and output heights can be dragged, and are saved with the cell. By default the code grows up to 60% of the window, and outputs scroll after half of it.

### Changed
- Settings: "Spark session" and "Spark profiles" are now one Spark tab. The app-wide settings come first, then the profile editor with sections (runtime, CPU, driver, executors, SQL, catalog, Delta, startup, Advanced). Cores and memory have their own inputs, Java and Spark folders are checked as you type, extra Spark settings are edited as rows, and changes wait for Save or Discard.
- Library management moved from the sidebar to the Libraries tab. The sidebar keeps a short summary of the running profile's libraries.
- Testing a Databricks target whose cluster is stopped asks before starting it, shows what the test is doing, and can be stopped. A server that doesn't answer now fails in seconds instead of a minute.

### Fixed
- A Scala cell that returns a DataFrame made by a library's own Spark session no longer fails with "table or view not found", and SQL cells can query it.
- Azure storage: when your Azure sign-in can list an account's containers but has no data role to read them, SparkEmUp now uses the account key instead, as Storage Explorer does.

## [0.2.0] - 2026-10-23
### Added
- Azure storage: connections to storage accounts with an account key, a SAS token, a service principal or the Azurite emulator. Secrets are kept in your system's keychain, or only for the current run if you prefer. Browse containers and folders, preview files, see their properties, create folders, rename, move and delete, and make SAS links. A transfers queue handles downloads, uploads and copies between accounts.
- Spark can read and write Azure storage: turn on "Use in Spark" on a connection and its credentials go into the session, kept up to date when Spark restarts or the connection changes. Account keys are hidden in the UI and the logs.
- Azure sign-in, with the Azure CLI's login or SparkEmUp's own browser sign-in. Switch tenants, browse subscriptions, resource groups and resources, and add a storage account as a connection from there.
- Remote Spark: each notebook chooses where it runs, either the local Spark or a remote target. A target is a Spark Connect server (with or without TLS and a token) or a Databricks cluster (with a personal access token or the Azure sign-in). A stopped Databricks cluster is started when you connect, and you can see its recent events. SQL and Python cells run on the target. Scala cells, Spark jobs, plans and lineage still need the local Spark.
- Jobs panel: live Spark jobs and their stages. Each cell also gets a Jobs tab that follows its run, and a stage opens to its task list and a task summary that warns about skew.
- Plans: the Plan tab shows a statement's plan as planned (without running it) and each run's final plan with its operator metrics ("As run"), as a folding tree, a graph or Spark's text. Selecting an operator opens its details, the operators it reuses, and for a run its metrics and the Spark stages it ran in.
- Lineage panel: what each cell read and wrote, and which source columns each output column comes from.
- Delta tab for Delta tables: overview, history, schema, files and health, plus optimize, vacuum, restore, delete, clone, table properties, protocol, convert and create.
- Jar check: the Libraries view warns about jars that clash with Spark's own classes or with each other, and about classes your jars need but nothing provides. The class browser names the missing dependencies of a class.
- Browse… buttons next to file and folder paths, using your system's file dialogs.
- Spark 3.5: alongside Spark 4.1, SparkEmUp can download a Spark 3.5 runtime (Java 17, Scala 2.12, with its own Python for Python cells). First start asks which runtimes to download and which one to start with; Settings → Runtimes downloads, removes and picks the default later.
- Spark profiles: named Spark setups (runtime, settings, startup script, jars and Maven packages from a shared jar pool), each with its own catalog. Switch the running profile from the status bar, and pin a notebook to a profile so it asks to switch before it runs.
- Import from Sparking 1.6.5: its saved scripts become notebooks, its setup (settings, startup scripts, jars and Maven packages) becomes a Spark 3.5 profile, and its Azure Storage connections become storage connections, with their secrets kept in your keychain.
- Files: browse local folders, page through large files, and re-encode them. EBCDIC files decode with code page profiles, an identify step and a preview. Record layouts turn fixed-width or delimited lines into typed columns (including COBOL signed numbers), and can be imported from COBOL copybooks, PL/I includes and Sparking 1.6.5's parser classes.
- Scheme viewer: turns a table's, a result's or a layout's schema into Scala case classes, a PySpark StructType, SQL DDL, Python dataclasses, Spark JSON, a SQL Server bcp format file or a MERGE upsert procedure, to copy, save or add to the notebook.
- Logs window: Spark's, the Python workers' and SparkEmUp's own logs in one place, with filters and live log levels. Each cell has a Logs tab with the lines from its last run.
- Signature help and hover in Python and Scala cells, and Scala completion of every name in scope. The Scala interpreter warms up when Spark is ready, so the first completion answers at once.
- Result tables:
  - a right-click menu copies a value, a row, a column or the page, tab-separated, with or without headers;
  - the cell under the pointer is marked with its row and column, and a click keeps the mark there;
  - Search (in the cell's tab bar, or Ctrl+F over the table) finds columns by name and values on the page or in the whole result, with match case, whole value and regular expressions, and can filter the result to the matching rows. Export then writes only those rows;
  - the pager goes to the first or last page, a page number or a row number, and pages are 100, 500 or 1,000 rows;
  - the row numbers stay in view when the table scrolls sideways.

### Changed
- The notebook header and its open panels stay at the top while the cells scroll.
- The Python and Scala variable panels open on their own and can both be open at once.
- The Logs panel at the bottom is replaced by the Logs window.

### Fixed
- On Windows, a user folder with non-ASCII letters (such as `C:\Users\Ramón`) no longer creates a wrongly named data folder.
- When a startup library breaks Spark, the start now fails at once with the error and names the startup libraries, instead of retrying for two minutes.
- Installed builds can open the system's file dialogs.
- Long column names in the catalog no longer squeeze the column type to one letter per line.

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
