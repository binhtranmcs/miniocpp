
# miniocpp

This repo purpose is to link [minio-cpp SDK](https://github.com/minio/minio-cpp) to a project without using vcpkg. Also, this can be compiled with cxx_abi=0.

To include in a project:

```
cd my_project
git clone git@github.com:binhtranmcs/miniocpp.git
add_subdirectory(miniocpp)
target_link_libraries(my_project PRIVATE miniocpp)
```
