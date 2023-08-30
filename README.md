# cpp2wasm
Compile c++ codes  to WebAssembly by using Emscripten SDK.

```shell
# Generate html and js
cd emsdk\
# run emcmdprompt.bat  to open a win terminal with Emscripten env.
emcc hello.c -s WASM=1 -o hello.html

# use customized htmp template
emcc -o hello2.html hello2.c -O3 -s WASM=1 --shell-file shell_minimal.html

# 如果需要调用一个在 C 语言自定义的函数，你可以使用 Emscripten 中的 ccall() 函数，以及 EMSCRIPTEN_KEEPALIVE 声明（将你的函数添加到导出函数列表中）
# 默认情况下，Emscripten 生成的代码只会调用 main() 函数，其他的函数将被视为无用代码。在一个函数名之前添加 EMSCRIPTEN_KEEPALIVE 能够防止这样的事情发生。你需要导入 emscripten.h 库来使用 EMSCRIPTEN_KEEPALIVE。
# 备注： 为了保证万一你想在 C++ 代码中引用这些代码时代码可以正常工作，我们添加了 #ifdef 代码块。由于 C 与 C++ 中名字修饰规则的差异，添加的代码块有可能产生问题，但目前我们设置了这一额外的代码块以保证你使用 C++ 时，这些代码会被视为外部 C 语言函数。

emcc -o hello3.html hello3.c -O3 -s WASM=1 -s "EXTRA_EXPORTED_RUNTIME_METHODS=['ccall']" --shell-file shell_minimal.html

# start web server to check result
python -m http.server
```