# mvsqlite for Windows

```bat
cmd
scoop install llvm openssl-mingw llvm-mingw
cargo build --release -p mvsqlite
cd mvsqlite-sqlite3
mingw32-make.exe build-patched-sqlite3
set RUST_LOG=info
set MVSQLITE_DATA_PLANE=http://localhost:7000
sqlite3 test
.tables
```

## Check fdb status

```bash
fdbcli
status
# Force create a database
# configure new single memory
```


## Create a mvsqlite database

```bat
msys2
curl http://localhost:7001/api/create_namespace -i -d '{"key":"test"}'
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
  --raw-data-prefix m
```

## Starting mvstore with foundationdb on Windows

```bash
cmd
cargo build --release -p mvstore
set RUST_LOG=info
mvstore --data-plane 127.0.0.1:7000 --admin-api 127.0.0.1:7001 --metadata-prefix mvstore --raw-data-prefix m --cluster "C:/ProgramData/foundationdb/fdb.cluster"
```