### use python-llama-cpp on termux

## not use docker

### change-repo !!!

you should install termux

and if use vulkan ,please install vulkan-loader

by apt : cmake libopenblas rust python-numpy vulkan-header shaderc
python-pip binutils-gold binutils llvmgold libcurl clblast openssl
patchelf

### so we should install

export PIP_CONFIG_SETTINGS="wheel.cmake=false"

//this is stop python-llama-cpp cmake build llama.cpp

pip install llama-cpp-python\[server] 
<https://github.com/abetlen/llama-cpp-python/archive/refs/heads/main.zip>

git clone --depth=1 <https://github.com/ggerganov/llama.cpp.git>

### cd llama.cpp
cmake -B build -DLLAMA_CURL=1 -DLLAMA_LTO=ON -DGGML_LTO=1 \
-DLLAMA_BUILD_TESTS=0 -DLLAMA_BUILD_EXAMPLES=1 \
-DGGML_OPENMP=1 \
-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS -DLLAMA_CLBLAST=ON \
-DGGML_VULKAN=1 \
-DLLAMA_SERVER_VERBOSE=ON -DLLAMA_BUILD_SERVER=ON -DLLAMA_SERVER_SSL=ON -DLLAMA_RPC=ON \
-DCMAKE_INSTALL_PREFIX:PATH=$PREFIX         -DCMAKE_INSTALL_BINDIR:PATH=bin \
        -DCMAKE_INSTALL_SBINDIR:PATH=sbin \
        -DCMAKE_INSTALL_LIBEXECDIR:PATH=libexec \
        -DCMAKE_INSTALL_SYSCONFDIR:PATH=etc \
 -DCMAKE_INSTALL_SHAREDSTATEDIR:PATH=$PREFIX/var/lib \
        -DCMAKE_INSTALL_LOCALSTATEDIR:PATH=var \
        -DCMAKE_INSTALL_RUNSTATEDIR:PATH=run \
        -DCMAKE_INSTALL_LIBDIR:PATH=lib \
        -DCMAKE_INSTALL_INCLUDEDIR:PATH=include \        
        -DINCLUDE_INSTALL_DIR:PATH=$PREFIX/include \
        -DCMAKE_BUILD_TYPE=RelWithDebInfo \
        -DCMAKE_C_FLAGS="${CFLAGS:--O2 -g -m64 -fmessage-length=0 -D_FORTIFY_SOURCE=2 -fstack-protector -funwind-tables -fasynchronous-unwind-tables}" \
        -DCMAKE_CXX_FLAGS="${CXXFLAGS:--O2 -g -m64 -fmessage-length=0 -D_FORTIFY_SOURCE=2 -fstack-protector -funwind-tables -fasynchronous-unwind-tables}" \
        -DCMAKE_Fortran_FLAGS="${FFLAGS:--O2 -g -m64 -fmessage-length=0 -D_FORTIFY_SOURCE=2 -fstack-protector -funwind-tables -fasynchronous-unwind-tables}" \
        -DCMAKE_EXE_LINKER_FLAGS=" -Wl,--as-needed -Wl,--no-undefined -Wl,-z,now" \
        -DCMAKE_MODULE_LINKER_FLAGS=" -Wl,--as-needed" \
        -DCMAKE_SHARED_LINKER_FLAGS=" -Wl,--as-needed -Wl,--no-undefined -Wl,-z,now" \
        -DLIB_SUFFIX=64 \
-DCMAKE_VERBOSE_MAKEFILE:BOOL=ON \
        -DBUILD_SHARED_LIBS:BOOL=ON \
        -DBUILD_STATIC_LIBS:BOOL=OFF \
        -DCMAKE_COLOR_MAKEFILE:BOOL=OFF \
        -DCMAKE_INSTALL_DO_STRIP:BOOL=OFF \
      -DCMAKE_MODULES_INSTALL_DIR=/$PREFIX/lib64/cmake/llama.cpp
cmake --build build --target all -- -j $(nproc) 

cmake --install build

#### mkdir $PREFIX/lib/python3.11/site-packages/llama_cpp/lib

ln -s $PREFIX/lib/libllama.so
$PREFIX/lib/python3.11/site-packages/llama_cpp/lib ln -s $PREFIX/lib/libggml.so
$PREFIX/lib/python3.11/site-packages/llama_cpp/lib ln -s
$PREFIX/lib/libllavashared.so
$PREFIX/lib/python3.11/site-packages/llama_cpp/lib/libllava.so

### so you can update free on llama.cpp and llama.cpp-python ??

### llama.cpp have change his symbols

