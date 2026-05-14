# _Klebsiella pneumoniae_ Species Complex _in silico_ serotyping databases

> [!WARNING]
> This repository is currently for testing purposes only


## Proposed layout
- Databases must be in Genbank format, with the `.gbk` suffix.
- Databases must be accompanied by a metadata file with the same name as the database but with a `.toml` suffix.
- All files must be in the repository root directory.

## Future plans
- Generate a Github workflow to automatically bump database versions on repository release.
- Develop a Python Shiny app to interactively populate the metadata TOML file from a database file.
