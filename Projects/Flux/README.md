# 🌟 Flux <!-- omit from toc -->

Game Engine to explore computer graphics and graphics programming.

`❗Note: This file is a work in progress and will be updated frequently`

## 📚 Table Of Contents

- [📚 Table Of Contents](#-table-of-contents)
- [🖥️ Graphics APIs](#️-graphics-apis)
  - [DirectX 12](#directx-12)
  - [Vulkan](#vulkan)
  - [DirectX 11](#directx-11)
  - [OpenGL 4.5+ and OpenGL ES 3.2+](#opengl-45-and-opengl-es-32)
  - [Metal](#metal)
  - [WebGPU](#webgpu)
- [📷 Rendering Hardware Interface](#-rendering-hardware-interface)
- [💻 Platform Abstraction Layer](#-platform-abstraction-layer)
- [🧵 Code Structure and Style](#-code-structure-and-style)
  - [Code Structure](#code-structure)
  - [Code Style](#code-style)

## 🖥️ Graphics APIs

| **API**          | **Platforms**                 |
| ---------------- | ----------------------------- |
| Vulkan           | Windows, Linux, macOS, Switch |
| DirectX 12       | Windows, Xbox                 |
| DirectX 11       | Windows, Xbox                 |
| OpenGL (4.5+)    | Windows, Linux, Xbox, Switch  |
| OpenGL ES (3.2+) | Windows, Linux, macOS, Switch |
| Metal            | macOS                         |
| WebGPU           | Browsers, (Also in Windows?)  |

In the end I want Flux to have the ability to use multiple modern graphics apis, such as Vulkan and DirectX 12. When I start developing Flux I will use DirectX 12, because in the beginning Flux will only support Windows. When the core systems of the engine are ready, I will start supporting other platforms. The current plan is to support Windows and Linux. I am not planning to support macOS or mobile platforms. Web support on the other hand is something I am considering. Especially because WebGPU seems very interesting.

### DirectX 12

I already have some experience with DirectX 12, but there are still some things I need to learn. For example I don't have a clear plan on how to manage descriptor heaps.

- [Raw DirectX 12](https://alain.xyz/blog/raw-directx12)
- [Managing Descriptor Heaps](https://diligentgraphics.com/diligent-engine/architecture/d3d12/managing-descriptor-heaps/)

### Vulkan

I used Vulkan in the past, but I never really got into it. It seems like that there are new extensions and features that I need to learn about, for example dynamic rendering and better synchronization.

- [Raw Vulkan](https://alain.xyz/blog/raw-vulkan)
- [VkGuide](https://vkguide.dev/)

### DirectX 11

I have experience with DirectX 11, but I don't want to use it for Flux. I want to use a more modern graphics api. Maybe in the future I will add support for DirectX 11, but for now I will focus on more modern apis.

- [Raw DirectX 11](https://alain.xyz/blog/raw-directx11)

### OpenGL 4.5+ and OpenGL ES 3.2+

The same as with DirectX 11, I have experience with OpenGL, but I don't want to use it for Flux.

- [Raw OpenGL](https://alain.xyz/blog/raw-opengl)

### Metal

I never used Metal and the fact that it is only available on macOS makes it less interesting for me. I don't have any plans to support macOS, so I don't have any plans to support Metal.

- [Raw Metal](https://alain.xyz/blog/raw-metal)

### WebGPU

WebGPU seems very interesting to me. I didn't really look into it yet, but I am planning to do so. I think it would be very cool to have Flux running in the browser in the future.

- [Raw WebGPU](https://alain.xyz/blog/raw-webgpu)

## 📷 Rendering Hardware Interface

<img src="https://i.imgur.com/9wx2DvR.png" alt="RHI Meme" width="500">

To support multiple graphics apis I will need to create a Rendering Hardware Interface (RHI).

- [An Opinionated Post on Modern Rendering Abstraction Layers](https://alextardif.com/RenderingAbstractionLayers.html)
- [Graphics API abstraction](https://wickedengine.net/2021/05/graphics-api-abstraction/)
- [Musings on cross-platform graphics engine architectures](https://www.gijskaerts.com/wordpress/?p=98)
- [Halcyon Architecture "Director's Cut"](https://media.contentapi.ea.com/content/dam/ea/seed/presentations/wihlidal-halcyonarchitecture-notes.pdf)
- [Designing a Modern Cross-Platform Low-Level Graphics Library](https://www.gamedeveloper.com/programming/designing-a-modern-cross-platform-low-level-graphics-library)

## 💻 Platform Abstraction Layer

To support multiple platforms I will need to create a Platform Abstraction Layer (PAL).
There are a lot of things to consider, such as window creation, input handling, file system, etc.
I think there should be 2 ways to abstract the platforms. The first way is to use interface classes that have virtual functions, where each platform has its own implementation. The second way is to use preprocessor directives to include the correct platform specific code. I think the first way is better, because it is more flexible and easier to maintain.
In some cases it might be easier to use the second way, for example when you want to use platform specific features that are not available on other platforms. A mix of both ways might be the best solution here.

## 🧵 Code Structure and Style

### Code Structure

I really like the modular structure of [Unreal Engine](https://www.unrealengine.com/), but there is no build system (that I know of) that makes it easy to have such a structure. Unreal Engine uses a custom build system for that. Modifying or extending a build system is quiete difficult. Maybe building some custom tooling around premake or cmake could be a solution. I will have to look into that. Other than that I think having a monolithic structure is fine too. I will start with a monolithic structure and see how it goes.

Flux should be compiled into a dynamic library that can be linked and loaded by "applications". To extend the functionality of the engine without actually modifying the engines source code, I will implement a plugin system. The plugin system should be able to load and unload plugins at runtime. The plugins should be able to add new systems, components, resources, etc. to the engine. The graphics system will probably be a plugin too, to make it easier to switch between different graphics apis and make it possible to run the engine in a headless mode (Used for dedicated servers).

### Code Style

As I mentioned before I really like Unreal Engines way of doing things. I will use [Unreal Engines Coding Standard](https://dev.epicgames.com/documentation/en-US/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine) as the base of my coding standard. I will make some changes to it to fit my needs.
