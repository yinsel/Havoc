# Havoc

MSYS2 编译 Windows 客户端。

## 安装依赖

1. 打开`MinGW64`, 执行以下命令: 

```
pacman -S --needed --noconfirm python python-devel mingw-w64-x86_64-qt-creator mingw-w64-x86_64-qt5-static mingw-w64-x86_64-spdlog mingw-w64-x86_64-cmake base-devel mingw-w64-x86_64-toolchain git subversion mercurial mingw-w64-x86_64-nasm mingw-w64-x86_64-lld mingw-w64-x86_64-python-pkgconfig autoconf automake
```

2. 修改`client\CMakeLists.txt`文件, 根据说明添加`Python`包含库的绝对路径，建议使用`3.10.x`:

```
if(APPLE)
    execute_process( COMMAND brew --prefix OUTPUT_VARIABLE BREW_PREFIX ) #this because brew install location differs Intel/Apple Silicon macs
    string( STRIP ${BREW_PREFIX} BREW_PREFIX ) #for some reason this happens: https://gitlab.kitware.com/cmake/cmake/-/issues/22404
    include_directories( "${BREW_PREFIX}/bin/python3.10" )
    include_directories( "${BREW_PREFIX}/Frameworks/Python.framework/Headers" )
elseif(UNIX)
    include_directories( ${PYTHON_INCLUDE_DIRS} )
else()
  include_directories( "<Msys2的Python include目录的绝对路径>" )
endif()
```

3. 编译

```
make client-build-win
```

