```bat
cmd
scoop install llvm openssl-mingw llvm-mingw
cargo build --release -p mvsqlite
cd mvsqlite-sqlite3
mingw32-make.exe build-patched-sqlite3
set RUST_LOG=info
set MVSQLITE_DATA_PLANE=http://localhost:7000
sqlite3 test
```