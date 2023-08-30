# cpp2wasm
Compile c++ codes  to WebAssembly by using Emscripten SDK.

```shell
# Generate html and js
emcc hello.c -s WASM=1 -o hello.html

# use customized htmp template
emcc -o hello2.html hello2.c -O3 -s WASM=1 --shell-file shell_minimal.html

# start web server to check result
python -m http.server
```