<img src="./assets/icon.png" width="128" height="128" alt="SparkEmUp">

# SparkEmUp

A desktop workbench for Apache Spark on your own computer: write SQL, Python and Scala in notebooks, run them on a local Spark 4.1, and browse the tables, files and databases they work with. No cluster is needed.

This repository hosts **installers and release notes only**. It is the public download point for SparkEmUp. Source code is developed elsewhere; builds are published here as [GitHub Releases](../../releases).

## Download

Grab the latest installer for your platform from the [Releases page](../../releases/latest):

| Platform | File |
|---|---|
| Windows | `SparkEmUp_<version>_x64-setup.exe` |
| Linux | `SparkEmUp_<version>_amd64.deb`, `SparkEmUp-<version>-1.x86_64.rpm`, or `SparkEmUp_<version>_amd64.AppImage` |

## First run

SparkEmUp brings its own Java and Spark and uses nothing installed on your machine: no `JAVA_HOME`, `SPARK_HOME`, `HADOOP_HOME` or winutils. On first start it downloads them once (about 1 GB), checking each download's checksum:

- Eclipse Temurin Java 21
- Apache Spark 4.1.3
- the libraries for Delta Lake, Avro and Excel files, and Azure storage

They can be installed for your user only, or, with administrator rights, once **for all users** of the computer.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release history.

## License

[MIT](LICENSE)
