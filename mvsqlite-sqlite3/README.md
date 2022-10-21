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