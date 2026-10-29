# Local SQL Server

Two SQL Server 2022 Developer Edition instances run in Podman. This Apple Silicon host runs the x86-64 images under emulation; the instances are for local development, not production.

## Connection information

| Container | Host | Port | Database | User | Private environment file | Data volume |
| --- | --- | ---: | --- | --- | --- | --- |
| `legacy-mssql` | `127.0.0.1` | `1433` | `master` | `sa` | `~/.config/legacy-mssql/sa.env` | `legacy-mssql-data` |
| `cloud-legacy-mssql` | `127.0.0.1` | `1434` | `master` | `sa` | `~/.config/legacy-mssql/cloud.env` | `cloud-legacy-mssql-data` |

Each private environment file contains its instance's `SQL_SERVER_HOST`, `SQL_SERVER_PORT`, `SQL_SERVER_DATABASE`, `SQL_SERVER_USER`, and `SQL_SERVER_PASSWORD` settings, plus the container startup settings. Both files are owner-only; load the appropriate file with your application's environment-file support. Do not commit or share them.

For a client using ADO.NET, the connection string format is `Server=127.0.0.1,<port>;Database=master;User Id=sa;Password=<secret>;Encrypt=True;TrustServerCertificate=True`, substituting `1433` or `1434` and the password from the matching private environment file.

## Start and stop

```sh
podman machine start
podman start legacy-mssql cloud-legacy-mssql
```

Stop both containers with `podman stop legacy-mssql cloud-legacy-mssql`. Their database files remain in their respective named volumes.

## Source data

The logistics dataset is at `data/raw/dynamic_supply_chain_logistics_dataset.csv`. Its source URL is recorded in `data/source/data.txt`.

