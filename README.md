# Get CPM

A CMake function for auto downloading & bootstrapping [CPM.cmake](https://github.com/cpm-cmake/CPM.cmake) from within CMake itself (with caching of versions).

## Usage

1. Clone the `get_cpm.cmake` file into your repo.
2. `include` it in your `CMakeLists.txt` file. 
3. Call the defined `get_cpm(VERSION)` function.

e.g. `CMakeLists.txt`
```CMake
cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(foo)

# optional, extract the version into a cached string variable for modification by other projects that want to include this one
set(CPM_VERSION "v0.40.2" CACHE STRING "Which version of CPM to use (a git tag or \"master\")")

# include and call get_cpm (where the magic happens)
include(get_cpm.cmake)
get_cpm(VERSION ${CPM_VERSION})

# use CPM like usual beyond this point
CPMAddPackage("gh:fmtlib/fmt#7.1.3")

add_executable(bar main.cpp)

target_link_libraries(bar
	PRIVATE
		fmt::fmt
)
```

If the `CPM_SOURCE_CACHE` CMake variable or ENV variable is set, it will download it into the directory specified by it.

The function will avoid re-downloading a version of CPM if it has already been downloaded.

You may also specify `"master"` for the `VERSION` argument to get the latest in the source repo. However, this will mean that a new latest version is downloaded on every CMake configure instead of being cached (as there may have been updates to the master branch since the last download).
