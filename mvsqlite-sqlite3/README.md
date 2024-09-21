# mvsqlite

```bash
cargo build --release -p mvsqlite
cd mvsqlite-sqlite3
make build-patched-sqlite3
```

## Check fdb status

```bash
'C:\Program Files\foundationdb\bin\fdbcli.exe'
status
# Migrate the database from in-memory to ssd
configure perpetual_storage_wiggle=1 storage_migration_type=gradual
configure single ssd
# Check the status
status
```

## Start sqlite client

```cmd
export RUST_LOG=info
export MVSQLITE_DATA_PLANE=http://127.0.0.1:7000
./sqlite3 mvsqlite
.tables
```

## Fix binary

```bash
install_name_tool -add_rpath /usr/local/lib ~/Documents/mvsqlite/target/release/mvstore
RUST_LOG=info ~/Documents/mvsqlite/target/release/mvstore \
  --data-plane 127.0.0.1:7000 \
  --admin-api 127.0.0.1:7001 \
  --metadata-prefix mvstore \
  --raw-data-prefix m \
  --cluster /usr/local/etc/foundationdb/fdb.cluster
curl http://localhost:7001/api/create_namespace --include --data {\"key\":\"mvsqlite\"}
```

## Starting mvstore with foundationdb on Linux

```bash
# on Linux
wget https://github.com/apple/foundationdb/releases/download/7.1.15/foundationdb-clients_7.1.15-1_amd64.deb
sudo dpkg -i foundationdb-clients_7.1.15-1_amd64.deb
wget https://github.com/apple/foundationdb/releases/download/7.1.15/foundationdb-server_7.1.15-1_amd64.deb
sudo dpkg -i foundationdb-server_7.1.15-1_amd64.deb
cargo build --release -p mvstore
RUST_LOG=info ./mvstore \
  --data-plane 127.0.0.1:7000 \
  --admin-api 127.0.0.1:7001 \
  --metadata-prefix mvstore \
  --raw-data-prefix m \
  --cluster /etc/foundationdb/fdb.cluster
```

## Starting mvstore with foundationdb on Windows

```cmd
REM install https://github.com/apple/foundationdb/releases/download/7.1.25/foundationdb-7.1.25-x64.msi
cargo build --release -p mvstore
$env:RUST_LOG="info"
./mvstore.exe --data-plane 127.0.0.1:7000 --admin-api 127.0.0.1:7001 --metadata-prefix mvstore --raw-data-prefix m --cluster "C:/ProgramData/foundationdb/fdb.cluster"
```

## Create a mvsqlite database

```bat
scoop install curl
curl http://localhost:7001/api/create_namespace --include --data {\"key\":\"mvsqlite\"}
```

## Debugging library loading

```powershell
scoop install Dependencies 
```
