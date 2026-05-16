# _Klebsiella pneumoniae_ Species Complex _in silico_ serotyping databases

> [!WARNING]
> This repository is currently for testing purposes only

## Proposed layout
- Databases must be in Genbank format, with the `.gbk` suffix.
- Databases must be accompanied by a metadata file with the same name as the database but with a `.toml` suffix.
- All files must be in the repository root directory.

## Database Versioning & Release Workflow
This repository uses a fully automated Continuous Integration / Continuous Deployment (CI/CD) pipeline to manage database versions.

You do not need to manually edit version numbers or create Git tags. The pipeline relies on Semantic Versioning (SemVer) and reads your 
commit messages to automatically calculate the correct version bump, update the corresponding .toml files, and generate 
database-specific release tags.

### How It Works: Conventional Commits
The automation script decides how to version a database based on the language used in your commit messages. We follow the Conventional Commits standard.

When you commit changes to a database file (e.g., .gbk, .units, .logic), prefix your commit message with one of the following:

`fix:` (Patch Bump): Use this for correcting typos, fixing broken logic rules, or minor backwards-compatible bug fixes.

- Example: `fix: correct wcaJ truncation rule in Klebsiella`
- Result: `v3.2.1 ➡️ v3.2.2`

`feat:` (Minor Bump): Use this when adding new features, such as adding a new locus, a new glycosidic linkage, or expanding the phenotype logic in a backwards-compatible way.

- Example: feat: add KL102 locus to Acinetobacter
- Result: `v3.2.1 ➡️ v3.3.0`

`feat!:` or `[major]` (Major Bump): Use this for breaking changes, such as overhauling the TOML schema, changing existing core 
nomenclature, or deleting previously supported loci.

- Example: `feat!: restructure JSON schema for phenotype logic`
- Result: `v3.2.1 ➡️ v4.0.0`

`chore:`, `docs:`, `style:` (No Bump): Changes to `README`s, generic repository maintenance, or formatting will not trigger a version bump.
