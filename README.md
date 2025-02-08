## jakoch/rasterizers [![Build on Windows: Mesa llvmpipe](https://github.com/jakoch/rasterizers/actions/workflows/build-mesa.yml/badge.svg?branch=main)](https://github.com/jakoch/rasterizers/actions/workflows/build-mesa.yml) [![Build on Windows: Swiftshader](https://github.com/jakoch/rasterizers/actions/workflows/build-swiftshader.yml/badge.svg?branch=main)](https://github.com/jakoch/rasterizers/actions/workflows/build-swiftshader.yml)

#### What is this?

This repository automates the process of building and releasing ready-to-use
drivers for Windows of two software rasterizers: Mesa's **LLVMpipe** and
Google's **Swiftshader**.

Both rasterizers are designed to enable rendering in CPU environments,
which is particularly valuable in CI (Continuous Integration) systems for
automated testing and validation of graphics applications.

Neither Mesa's LLVMpipe nor Google's SwiftShader offer official downloads for
these packages as of February 2025.

This repository aims to provide prebuilt versions of these drivers for integration with
[jakoch/install-vulkan-sdk-action](https://github.com/jakoch/install-vulkan-sdk-action),
which automates the installation of the Vulkan SDK during GitHub Action CI runs.
The drivers are compiled using GitHub Actions CI, ensuring automated compilation,
and distributed through GitHub Releases, providing a standardized download
mechanism for developers.

By using the software rasterizers from this repository, developers can
effectively test their Vulkan applications on CPU-only or GPU-less platforms,
such as CI environments.

#### What is a Software Rasterizer?

A software rasterizer is a software-based implementation of a graphics
rendering pipeline that executes entirely on the CPU, without relying on
dedicated GPU hardware acceleration. It performs tasks such as vertex
processing, primitive assembly, rasterization (converting geometric shapes
into pixels), and pixel shading entirely through software algorithms and
CPU computations.

#### What is Mesa LLVMpipe?

[Mesa's LLVMpipe](https://docs.mesa3d.org/drivers/llvmpipe.html)  is a component
of the Mesa 3D Graphics Library that leverages the LLVM compiler infrastructure
to perform rendering tasks on the CPU. It provides a flexible and robust
solution for environments without dedicated GPU hardware. Specifically, all
graphics-related processing, including shaders, rasterization of points, lines,
and triangles, and vertex processing, is converted into LLVM intermediate
representation (IR) and then translated into CPU machine code for the target
platform, such as x86, x86_64, or ppc64le.

#### What is Swiftshader?

[Swiftshader](https://github.com/google/swiftshader), developed by Google,
delivers a high-performance CPU-based implementation of the Vulkan and
OpenGL ES APIs, ensuring graphics rendering on systems without GPU acceleration.

#### Why does this repo exist?

1. Neither project offers precompiled binaries.
   - According to Mesa's documentation:
      - > In general, precompiled Mesa libraries are not available.
      - Referencing [Mesa Documentation on Precompiled Libraries](https://docs.mesa3d.org/precompiled.html).
   - According to Google's SwiftShader repo:
      - > No releases published
      - Referencing [Google's Swiftshader Github Repository](https://github.com/google/swiftshader)
1. Various precompiled libraries from anonymous users are available on GitHub,
   but they lack regular updates and, more importantly, CI builds.
2. I needed a reliable download source for integration into my
   [jakoch/install-vulkan-sdk-action](https://github.com/jakoch/install-vulkan-sdk-action).

#### Links

##### Mesa

- Website: https://mesa3d.org
- Documentation: https://docs.mesa3d.org/
- LLVMpipe: https://docs.mesa3d.org/drivers/llvmpipe.html
- Issue Tracker: https://issuetracker.google.com/issues?q=componentid:408190&pli=1
- Main Repository: https://gitlab.freedesktop.org/mesa/mesa/
- Demos: https://gitlab.freedesktop.org/mesa/demos

##### Swiftshader

- Main Repository: https://swiftshader.googlesource.com/SwiftShader
- Github Mirror: https://github.com/google/swiftshader

##### Arch Linux

- https://wiki.archlinux.org/title/Vulkan
- https://archlinux.org/packages/?name=vulkan-swrast
- https://archlinux.org/packages/?name=lib32-vulkan-swrast
