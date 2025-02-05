# UPSTREAM ISSUES

## Swiftshader

- cmake build + cmake install do not build vk_swiftshader.dll
  - Building in the main folder builds third-party tools, but not the library itself.
  - To build the main library one has to specify `--target "vk_swiftshader"`.
  - Expected: configure + make + install, drops the main library into the install folder.


```
        - name: 📦 CMake ➔ Install Release
        working-directory: ${{env.BUILD_DIR}}
        run: cmake --install . --config Release
```


- broken `cmake --install` steps for main library and third-party libs..



```
cmake --install D:\a\rasterizers\rasterizers/swiftshader/build --prefix D:\a\rasterizers\rasterizers/swiftshader/install --verbose

-- Install configuration: "Release"
-- Installing: D:\a\rasterizers\rasterizers/swiftshader/install/lib/SPIRV-Tools-opt.lib
-- Installing: D:\a\rasterizers\rasterizers/swiftshader/install/SPIRV-Tools-opt/cmake/SPIRV-Tools-optTargets.cmake
-- Installing: D:\a\rasterizers\rasterizers/swiftshader/install/SPIRV-Tools-opt/cmake/SPIRV-Tools-optTargets-release.cmake
-- Installing: D:\a\rasterizers\rasterizers/swiftshader/install/SPIRV-Tools-opt/cmake/SPIRV-Tools-optConfig.cmake
CMake Error at swiftshader/build/third_party/SPIRV-Tools/source/reduce/cmake_install.cmake:36 (file):
  file INSTALL cannot find
  "D:/a/rasterizers/rasterizers/swiftshader/build/third_party/SPIRV-Tools/source/reduce/SPIRV-Tools-reduce.lib":
  File exists.
Call Stack (most recent call first):
  swiftshader/build/third_party/SPIRV-Tools/source/cmake_install.cmake:42 (include)
  swiftshader/build/third_party/SPIRV-Tools/cmake_install.cmake:42 (include)
  swiftshader/build/cmake_install.cmake:40 (include)
```


## Mesa

- Mesa uses non standard version tag scheme: "mesa-maj.min.patch".
  - Expected: standard scheme "v1.2.3" or "1.2.3".

- Missing dependecy check for directx/d3d12, compilation possible.
  - Expected: compilation not possible, with indication that dependency directx/d3d12 is missing.
  - Solved by: building and installing https://github.com/microsoft/DirectX-Headers


```
[55/703] Compiling C++ object src/vulkan/wsi/libvulkan_wsi.a.p/wsi_common_win32.cpp.obj
FAILED: src/vulkan/wsi/libvulkan_wsi.a.p/wsi_common_win32.cpp.obj
"sccache" "cl" "-Isrc\vulkan\wsi\libvulkan_wsi.a.p" "-Isrc\vulkan\wsi" "-I..\src\vulkan\wsi" "-Iinclude" "-I..\include" "-Isrc" "-I..\src" "-Isrc\vulkan\util" "-I..\src\vulkan\util" "-Isrc\vulkan\runtime" "-I..\src\vulkan\runtime" "-Isubprojects\zlib-1.3.1" "-I..\subprojects\zlib-1.3.1" "-DNDEBUG" "/MT" "/nologo" "/showIncludes" "/utf-8" "/Zc:__cplusplus" "/W2" "/EHsc" "/std:c++17" "/permissive-" "/O2" "/Gw" "-D__STDC_CONSTANT_MACROS" "-D__STDC_FORMAT_MACROS" "-D__STDC_LIMIT_MACROS" "-DPACKAGE_VERSION=\"24.1.3\"" "-DPACKAGE_BUGREPORT=\"https://gitlab.freedesktop.org/mesa/mesa/-/issues\"" "-DHAVE_OPENGL=1" "-DHAVE_OPENGL_ES_1=0" "-DHAVE_OPENGL_ES_2=0" "-DHAVE_SWRAST" "-DVIDEO_CODEC_VC1DEC=0" "-DVIDEO_CODEC_H264DEC=0" "-DVIDEO_CODEC_H264ENC=0" "-DVIDEO_CODEC_H265DEC=0" "-DVIDEO_CODEC_H265ENC=0" "-DVIDEO_CODEC_AV1DEC=1" "-DVIDEO_CODEC_AV1ENC=1" "-DVIDEO_CODEC_VP9DEC=1" "-DHAVE_WINDOWS_PLATFORM" "-DENABLE_ST_OMX_BELLAGIO=0" "-DENABLE_ST_OMX_TIZONIA=0" "-DGLAPI_EXPORT_PROTO_ENTRY_POINTS=0" "-DALLOW_KCMP" "-DMESA_DEBUG=0" "-D_WINDOWS" "-D_WIN32_WINNT=0x0A00" "-DWINVER=0x0A00" "-DPIPE_SUBSYSTEM_WINDOWS_USER" "-D_USE_MATH_DEFINES" "-DVC_EXTRALEAN" "-D_CRT_SECURE_NO_WARNINGS" "-D_CRT_SECURE_NO_DEPRECATE" "-D_SCL_SECURE_NO_WARNINGS" "-D_SCL_SECURE_NO_DEPRECATE" "-D_ALLOW_KEYWORD_MACROS" "-D_HAS_EXCEPTIONS=0" "-DNOMINMAX" "-DUSE_SSE41" "-DMISSING_64BIT_ATOMICS" "-DHAVE_STRTOF" "-DHAVE_QSORT_S" "-DHAVE_STRUCT_TIMESPEC" "-DHAVE_ZLIB" "-DHAVE_COMPRESSION" "-DWIN32_LEAN_AND_MEAN" "-DMESA_LLVM_VERSION_STRING=\"18.1.8\"" "-DLLVM_IS_SHARED=0" "-DLLVM_AVAILABLE=1" "-DDRAW_LLVM_AVAILABLE=1" "-DTHREAD_SANITIZER=0" "/wd4018" "/wd4056" "/wd4244" "/wd4267" "/wd4305" "/wd4351" "/wd4756" "/wd4800" "/wd4996" "/wd4291" "/wd4146" "/wd4200" "/wd4624" "/wd4309" "/wd4838" "/wd5105" "/we4020" "/we4024" "/we4189" "/Zc:__cplusplus" "-DNO_REGEX" "-DVK_USE_PLATFORM_WIN32_KHR" "/Fdsrc\vulkan\wsi\libvulkan_wsi.a.p\wsi_common_win32.cpp.pdb" /Fosrc/vulkan/wsi/libvulkan_wsi.a.p/wsi_common_win32.cpp.obj "/c" ../src/vulkan/wsi/wsi_common_win32.cpp
../src/vulkan/wsi/wsi_common_win32.cpp(38): fatal error C1083: Cannot open include file: 'directx/d3d12.h': No such file or directory
```
