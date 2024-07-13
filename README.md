## jakoch/rasterizers [![Build on Windows: Mesa llvmpipe](https://github.com/jakoch/rasterizers/actions/workflows/build-mesa.yml/badge.svg?branch=main)](https://github.com/jakoch/rasterizers/actions/workflows/build-mesa.yml) [![Build on Windows: Swiftshader](https://github.com/jakoch/rasterizers/actions/workflows/build-swiftshader.yml/badge.svg?branch=main)](https://github.com/jakoch/rasterizers/actions/workflows/build-swiftshader.yml)

### What is this?

This repository automates the process of building and releasing ready-to-use
drivers for Windows of two software rasterizers: Mesa's LLVMmpipe and
Google's Swiftshader.

Both rasterizers are designed to enable rendering in CPU environments,
which is particularly valuable in CI (Continuous Integration) systems for
automated testing and validation of graphics applications.

The purpose of this repository is to build these drivers for integration with
[jakoch/install-vulkan-sdk-action](https://github.com/jakoch/install-vulkan-sdk-action),
which automates the installation of the Vulkan SDK during GitHub Action CI runs.
By integrating the software rasterizers from this repository,
developers can effectively test their Vulkan software on GitHub Action CI.

The drivers are compiled using GitHub Actions CI, ensuring automated compilation,
and distributed through GitHub Releases, providing a standardized download mechanism for developers.

### What is a Software Rasterizer?

A software rasterizer is a software-based implementation of a graphics
rendering pipeline that executes entirely on the CPU, without relying on
dedicated GPU hardware acceleration. It performs tasks such as vertex
processing, primitive assembly, rasterization (converting geometric shapes
into pixels), and pixel shading entirely through software algorithms and
CPU computations.

### What is Mesa LLVMmpipe?

[Mesa's LLVMmpipe](https://docs.mesa3d.org/drivers/llvmpipe.html) is a component of the Mesa 3D Graphics Library. It uses the
LLVM compiler infrastructure to perform rendering tasks on the CPU, offering
a flexible and robust solution for environments lacking dedicated GPU hardware.

### What is Swiftshader?

[Swiftshader](https://github.com/google/swiftshader), developed by Google, delivers a high-performance CPU-based
implementation of the Vulkan and OpenGL ES APIs, ensuring graphics rendering
on systems without GPU acceleration.
