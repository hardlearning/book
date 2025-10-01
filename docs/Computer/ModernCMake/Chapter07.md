# Chapter 7: Managing Dependencies with CMake

## How to find installed packages

```bash
apt update
apt install protobuf-compiler libprotobuf-dev
```

CMake has a list of paths which can be scanned for filenames matching the following pattern:

- <CamelCasePackageName>Config.cmake
- <kebab-case-package-name>-config.cmake

chapter07/01-find-package-variables/message.proto

```
syntax = "proto3";
message Message {
    int32 id = 1;
}
```

chapter07/01-find-package-variables/main.cpp

```cpp
#include "message.pb.h"
#include <fstream>
using namespace std;
int main()
{
    Message m;
    m.set_id(123);
    m.PrintDebugString();
    fstream fo("./hello.data", ios::binary | ios::out);
    m.SerializeToOstream(&fo);
    fo.close();
    return 0;
}
```

chapter07/01-find-package-variables/CMakeLists.txt

```
cmake_minimum_required(VERSION 3.20.0)
project(FindPackageProtobufVariables CXX)

# find_package asks CMake to run the bundled FindProtobuf.cmake find-module and set up the Protobuf library.
find_package(Protobuf REQUIRED)
# protobuf_generate_cpp is a custom function defined in the Protobuf find-module.
# We use this function by providing two variables that will be filled with paths to the generated source (GENERATED_SRC) and header (GENERATED_HEADER) files, and a list of files to compile (message.proto).
protobuf_generate_cpp(GENERATED_SRC GENERATED_HEADER
                      message.proto)

add_executable(main main.cpp
                    ${GENERATED_SRC} ${GENERATED_HEADER})
# target_link_libraries adds libraries found by find_package() to the linking command of our main target.
target_link_libraries(main PRIVATE ${Protobuf_LIBRARIES})
# target_include_directories() adds to include paths the necessary INCLUDE_DIRS provided by the package and CMAKE_CURRENT_BINARY_DIR.
target_include_directories(main PRIVATE
                                ${Protobuf_INCLUDE_DIRS}
                                ${CMAKE_CURRENT_BINARY_DIR})
```

chapter07/02-find-package-targets/CMakeLists.txt

```
cmake_minimum_required(VERSION 3.20.0)
project(FindPackageProtobufTargets CXX)

find_package(Protobuf REQUIRED)
protobuf_generate_cpp(GENERATED_SRC GENERATED_HEADER
                      message.proto)

add_executable(main main.cpp
                    ${GENERATED_SRC} ${GENERATED_HEADER})
# If a package supports so-called "modern CMake", it will provide those IMPORTED targets instead of these variables, which allows for cleaner, simpler code.
# The protobuf::libprotobuf imported target implicitly specifies include directories.
target_link_libraries(main PRIVATE protobuf::libprotobuf)
target_include_directories(main PRIVATE
                                ${CMAKE_CURRENT_BINARY_DIR})
```

**Command**: find_package(<Name> [version] [EXACT] [QUIET] [REQUIRED])

- [version], which allows us to optionally request a specific version. Use the major.minor.patch.tweak format (such as 1.22) or provide a range – 1.22...1.40.1 (use three dots as a separator).
-  The EXACT keyword means that we want an exact version (a range is not supported here). 
- The QUIET keyword silences all messages about a found/not found package. 
- The REQUIRED keyword will stop execution if a package is not found and print  a diagnostic message (even if QUIET is enabled). 
- More information on the command can be found on the documentation page here: https://cmake.org/cmake/help/latest/command/find_package.html.