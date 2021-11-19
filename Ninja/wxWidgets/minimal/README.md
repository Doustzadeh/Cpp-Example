# Build C++ project with wxWidgets , MinGW & Ninja

#### Downloading the last stable CMake and Ninja build system

The last stable Ninja build system at the website ([Releases · ninja-build/ninja · GitHub](https://github.com/ninja-build/ninja/releases)).

Unzip download file to "C:\ninja-win".

Add this folder to the %PATH% variable.

```shell
ninja --version
```



The last stable CMake build system at the website ([Download | CMake](https://cmake.org/download/)).

Unzip download file to "C:\cmake-x.x.x".

Add this folder to the %PATH% variable.

```shell
cmake --version
```



#### Building wxWidgets project

```shell
mkdir build
```

```shell
cd build
```

- 
  ##### Debug Mode


```shell
cmake -G Ninja -DCMAKE_BUILD_TYPE:STRING=Debug ..
```

```shell
cmake --build . --config Debug
or
cmake --build .
or
ninja
```

- ##### Release Mode


```shell
cmake -G Ninja -DCMAKE_BUILD_TYPE:STRING=Release ..
```

```shell
cmake --build . --config Release
or
cmake --build .
or
ninja
```

