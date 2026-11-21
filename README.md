# ms2-sh-converter

Wrap a native resampler into a single importable .sh for OpenUtau Mobile on Android.

Turns a native resampler into a single `.sh` that **OpenUtau Mobile (Android)** can import under *Options → Custom resamplers*. The app only accepts `.sh` files or files with no extension, so the binary is embedded in the script as base64 and unpacked on first run.

```bash
# in Termux, after: pkg install git cmake make clang
cp ms2-sh $PREFIX/bin/ && chmod +x $PREFIX/bin/ms2-sh
ms2-sh                      # clone + build moresampler2, write ~/storage/downloads/moresampler2.sh
ms2-sh <git-url|folder>     # build another CMake project
ms2-sh <file>               # check a file; wrap it if it is a native ELF binary
```

- A native ELF binary is wrapped. A Windows `.exe` is rejected with an explanation, because it cannot become a script and Android cannot run it directly.
- After building on the device it runs the program once as a self-test and warns on exit code 159 (SIGSYS), 126, 127 or a crash signal.
- Environment variables: `OUT_DIR`, `NAME`, `REPO`.

## Status

Not confirmed to work end to end. Exit code 159 (SIGSYS: Android's seccomp filter killed the process) and a full render inside OpenUtau Mobile have not been verified.

## Credits

Vibe-coded with AI: written with [Claude](https://claude.com/claude-code) (Anthropic) and directed by sparky-commits1637. The default build target is [moresampler2](https://github.com/Astel123457/moresampler2); check its license before redistributing built binaries.
