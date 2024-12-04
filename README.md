# Get CPM

CMake script for bootstrapping [CPM.cmake](https://github.com/cpm-cmake/CPM.cmake) with a CMake function.

## Usage

1. Clone this file into your repo.
2. Include it in your `CMakeLists.txt` file. 
3. Call the defined `get_cpm(VERSION)` function.

e.g.
`CMakeLists.txt`
```CMake
cmake_minimum_required(VERSION 3.10)

project(ProjectFoo)

# include and call get_cpm
include(get_cpm.cmake)
get_cpm(VERSION "v0.40.2")

# use CPM like usual beyond this point
CPMAddPackage("gh:fmtlib/fmt#7.1.3")

add_executable(foo main.cpp)

target_link_libraries(foo
	PRIVATE
		fmt::fmt
)
```


If the `CPM_SOURCE_CACHE` env variable is set, it will download it into the directory specified there.

The function will avoid re-downloading a version of CPM if it has already been downloaded.

You may also specify `"master"` for the `VERSION` argument to get the latest in the source repo, this will mean that a new latest version is downloaded on every Configure instead of being cached.
