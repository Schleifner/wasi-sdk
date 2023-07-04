The default wasi sdk build enable -mbulk-memory, but it's still a proposal of Wasm, some compilers still doesn't support this feature.
To run wasm sdk on those compilers, -mbulk-memory must be disabled and build the wasi-sdk from source again

## Install deps
### Ubuntu
```shell
sudo apt install git clang ninja cmake make
```

### Windows
Build on Windows need msys2
```shell
pacman -Sy base-devel git  mingw-w64-clang-x86_64-toolchain  mingw-w64-clang-x86_64-cmake  mingw-w64-clang-x86_64-ninja
export PATH=/clang64/bin:/usr/bin:/c/Windows/System32
```

## Build
```shell
git clone https://github.com/Schleifner/wasi-sdk.git
cd wasi-sdk
git switch without-bulk-memory
git submodule update --init --recursive --progress
(cd src/wasi-libc && git apply ../../wasi-sdk-without-bulk-memory/bulk-memory.patch)
make package -j $(nproc)
```
