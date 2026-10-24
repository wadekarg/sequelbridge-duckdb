# sequelbridge-duckdb

DuckDB with its MySQL, PostgreSQL and SQLite scanner extensions built in, as static
libraries for macOS 14 or later (Apple Silicon and Intel), for
[SequelBridge](https://github.com/wadekarg/SequelBridge). DuckDB's own prebuilt
libraries leave the scanners out, to be downloaded at run time; SequelBridge links them
in instead, so it downloads no code.

Each release holds one zip and its SHA-256:

- `libs/`: universal static libraries: DuckDB, the three scanners, and the libraries
  they link (MariaDB Connector/C, libpq, OpenSSL, curl, zlib, LZ4)
- `include/duckdb.h`
- `licenses/`: the license of each library, and of each library in DuckDB's own source,
  with its NOTICE where one comes with it
- `sources/`: MariaDB Connector/C's source as it was compiled (LGPL 2.1), and the vcpkg
  port that built it

The recipe is in SequelBridge: `scripts/build-duckdb.sh` (pinned versions: DuckDB's tag,
the scanners' commits, vcpkg's tag), `scripts/package-duckdb.sh`, and the patches, vcpkg
triplets and extension list in `vendor/DuckDB/recipe/`. Each zip is built by SequelBridge's
workflow `.github/workflows/build-duckdb.yml` on GitHub Actions. SequelBridge's
`scripts/fetch-duckdb.sh` downloads a release and checks it against the SHA-256 it pins.

Releases are named `duckdb-v<DuckDB version>-sb<n>`, `n` counting rebuilds of one DuckDB
version.
