# cpp2wasm
Compile c++ codes  to WebAssembly by using Emscripten SDK.

```shell
# Generate html and js
cd emsdk\
# run emcmdprompt.bat  to open a win terminal with Emscripten env.
emcc hello.c -s WASM=1 -o hello.html

# use customized htmp template
emcc -o hello2.html hello2.c -O3 -s WASM=1 --shell-file shell_minimal.html

# �����Ҫ����һ���� C �����Զ���ĺ����������ʹ�� Emscripten �е� ccall() �������Լ� EMSCRIPTEN_KEEPALIVE ����������ĺ�����ӵ����������б��У�
# Ĭ������£�Emscripten ���ɵĴ���ֻ����� main() �����������ĺ���������Ϊ���ô��롣��һ��������֮ǰ��� EMSCRIPTEN_KEEPALIVE �ܹ���ֹ���������鷢��������Ҫ���� emscripten.h ����ʹ�� EMSCRIPTEN_KEEPALIVE��
# ��ע�� Ϊ�˱�֤��һ������ C++ ������������Щ����ʱ�������������������������� #ifdef ����顣���� C �� C++ ���������ι���Ĳ��죬��ӵĴ�����п��ܲ������⣬��Ŀǰ������������һ����Ĵ�����Ա�֤��ʹ�� C++ ʱ����Щ����ᱻ��Ϊ�ⲿ C ���Ժ�����

emcc -o hello3.html hello3.c -O3 -s WASM=1 -s "EXTRA_EXPORTED_RUNTIME_METHODS=['ccall']" --shell-file shell_minimal.html

# start web server to check result
python -m http.server
```