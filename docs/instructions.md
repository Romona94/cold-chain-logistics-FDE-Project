# Local SQL Server

The local database runs in Podman as `legacy-mssql`, using SQL Server 2022 Developer Edition and a persistent Podman volume named `legacy-mssql-data`.

This host is Apple Silicon, so the x86-64 SQL Server image runs under emulation. It has been verified with an authenticated SQL query, but this setup is for local development only; use a supported x86-64 host for production.

## Connection environment

```dotenv
SQL_SERVER_HOST=127.0.0.1
SQL_SERVER_PORT=1433
SQL_SERVER_DATABASE=master
SQL_SERVER_USER=sa
SQL_SERVER_PASSWORD=<local secret>
SQL_SERVER_ENCRYPT=true
SQL_SERVER_TRUST_SERVER_CERTIFICATE=true
```

The private environment file at `~/.config/legacy-mssql/sa.env` contains these `SQL_SERVER_*` values and the container settings. Load it with your application's environment-file support; do not commit or share it. `.env.example` contains the non-secret connection settings.

For clients that use a connection string, enable encryption and trust the local self-signed certificate, for example:

```text
Server=127.0.0.1,1433;Database=master;User Id=sa;Password=<local secret>;Encrypt=True;TrustServerCertificate=True
```

## Start and stop

```sh
podman machine start
podman start legacy-mssql
podman logs -f legacy-mssql
```

Stop the container with `podman stop legacy-mssql`. The database files remain in `legacy-mssql-data` when the container is stopped or removed.

## Source data

The logistics dataset is at `data/raw/dynamic_supply_chain_logistics_dataset.csv`. Its source URL is recorded in `data/source/data.txt`.

