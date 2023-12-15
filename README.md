# cpp-app-template

Template for a C++ application with CMake and Conan.


## Build

There are already some profiles available at ./tools/conan/.
New profiles can be added as required.

### Release Build with gcc-11

```bash
# All conan packages must be installed first
# This only needs to be done once
conan install . \
    --output-folder ./build/gcc11__x86_64-pc-linux-elf__release \
    --profile:host  ./tools/conan/gcc11__x86_64-pc-linux-elf__release \
    --profile:build ./tools/conan/gcc11__x86_64-pc-linux-elf__release \
    --build missing

# Create and enter the build directory
mkdir -p ./build/gcc11__x86_64-pc-linux-elf__release
cd ./build/gcc11__x86_64-pc-linux-elf__release

# Build the project
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_TOOLCHAIN_FILE=./conan_toolchain.cmake ../../
cmake --build . -- -j
```


## Unit Tests

In addition to the main application, a unit test application is also built.
It is located at <build-dir>/source/test and can be run from the command line.


## Benchmarks

In addition to the main application, a benchmark application is also built.
It is located at <build-dir>/source/bench and can be run from the command line.


## Static Code Analysis with Clang-Tidy

```bash
# All conan packages must be installed first
# This only needs to be done once
conan install . \
    --output-folder ./build/clang14__x86_64-pc-linux-elf__release \
    --profile:host  ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --profile:build ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --build missing

# Create and enter the build directory
mkdir -p ./build/clang14__x86_64-pc-linux-elf__release
cd ./build/clang14__x86_64-pc-linux-elf__release

# Build the project
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_TOOLCHAIN_FILE=./conan_toolchain.cmake -DANALYSIS=clang-tidy ../../
cmake --build . -- -j
```


## Sanitizers

### Address Sanitizer

```bash
# All conan packages must be installed first
# This only needs to be done once
conan install . \
    --output-folder ./build/clang14__x86_64-pc-linux-elf__release \
    --profile:host  ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --profile:build ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --build missing

# Create and enter the build directory
mkdir -p ./build/clang14__x86_64-pc-linux-elf__release
cd ./build/clang14__x86_64-pc-linux-elf__release

# Build the project
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_TOOLCHAIN_FILE=./conan_toolchain.cmake -DSANITIZER=asan ../../
cmake --build . -- -j

# Run the unit test with address sanitizer
./source/test/cpp-example-test
```

### Memory Sanitizer

```bash
# All conan packages must be installed first
# This only needs to be done once
conan install . \
    --output-folder ./build/clang14__x86_64-pc-linux-elf__release \
    --profile:host  ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --profile:build ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --build missing

mkdir -p ./build/clang14__x86_64-pc-linux-elf__release
cd ./build/clang14__x86_64-pc-linux-elf__release

# Build the project
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_TOOLCHAIN_FILE=./conan_toolchain.cmake -DSANITIZER=msan ../../
cmake --build . -- -j

# Run the unit test with address sanitizer
./source/test/cpp-example-test
```

### Thread Sanitizer

```bash
# All conan packages must be installed first
# This only needs to be done once
conan install . \
    --output-folder ./build/clang14__x86_64-pc-linux-elf__release \
    --profile:host  ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --profile:build ./tools/conan/clang14__x86_64-pc-linux-elf__release \
    --build missing

# Create and enter the build directory
mkdir -p ./build/clang14__x86_64-pc-linux-elf__release
cd ./build/clang14__x86_64-pc-linux-elf__release

# Build the project
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_TOOLCHAIN_FILE=./conan_toolchain.cmake -DSANITIZER=tsan ../../
cmake --build . -- -j

# Run the unit test with address sanitizer
./source/test/cpp-example-test
```


> [!TIP]
> To speed up your daily work, take a look at this [command line tool](https://github.com/guenterfischer/devchain)!
