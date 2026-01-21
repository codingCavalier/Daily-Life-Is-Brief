<img width="668" height="519" alt="image" src="https://github.com/user-attachments/assets/a8c39959-9e55-4e55-98e5-d22603efa099" />### 一些入门的文章
- https://zhuanlan.zhihu.com/p/568908494
- https://zhuanlan.zhihu.com/p/579253989

- OpenGL 是一套跨语言、跨平台，支持 2D、3D 图形渲染接口。这套接口由一系列的函数组成，定义了如何对简单及复杂的图形进行绘制。这套接口涉及到对设备的图像硬件进行调用，因此在不同的平台基于这套统一接口做了对应的实现。
- OpenGL ES 是 OpenGL 的子集，是针对手机和游戏主机等嵌入式设备而设计，去除了许多不必要和性能较低的 API 接口。
- Metal 是苹果为了解决 3D 渲染性能问题而推出的框架，该技术将 3D 图形渲染性能提高了 10 倍。
- Vulkan 是一套新的跨平台支持 2D、3D 图形渲染的接口。Vulkan 针对全平台即时 3D 程序（如电子游戏和交互媒体）设计，并提供高性能与更均衡的 CPU/GPU 使用。
- **谷歌则是从 2016 年的 Android N（安卓 7.0）开始支持 Vulkan API。当然 OpenGL ES 也仍是持续支持的。**
- 在日常开发中，开发者一般通过使用上层 API 来构建和绘制界面，而调用 API 时系统最终还是通过 OpenGL/Metal/Vulkan 来实现视图的渲染。开发者也可以直接使用 OpenGL/Metal/Vulkan 来驱动 GPU 芯⽚⾼效渲染图形图像以满足一些特殊的需求。
- OpenGL 的渲染架构是 Client/Server 模式
- OpenGL 提供了 3 个通道来让我们从 Client 向 Server 中的顶点着色器（Vertex Shader）和片元着色器（Fragment Shader）传递参数和渲染信息：**Attribute、Uniform、Texture Data**
- **一个巨大的状态机**
- **图形渲染管线**：顶点着色器 → 图元装配 → 几何着色器 → 光栅化 → 片段着色器 → 测试与混合。
- <img width="641" height="435" alt="image" src="https://github.com/user-attachments/assets/43db120a-9fcc-4c22-8d0f-1df6e00ff602" />
- 现代 OpenGL 转变为可编程（Programmable）渲染管线，而这里的编程语言就是 GLSL 语言，它是一种类 C 的语言，专为图形计算量身定制，包含了一些针对向量和矩阵操作的有用特性，我们用它编写我们自己的顶点着色器和片段着色器。
- **着色器**就是一段运行在 GPU 中的程序，这段程序由开发者编写，所以说为开发者提供了很大的灵活度和可掌控度。现在 OpenGL 主要有三种着色器：顶点着色器、几何着色器、片段着色器，其中顶点着色器和片段着色器为开发者必须提供，几何着色器为可选提供。

### EGL
- 如果我们了解了 OpenGL ES 就会知道，虽然它定义了一套移动设备的图像渲染 API，但是并没有定义窗口系统。为了让 GLES 能够适配各种平台，GLES 需要与知道如何通过操作系统创建和访问窗口的库结合使用，这就有了 EGL，EGL 是 OpenGL ES 渲染 API 和本地窗口系统之间的一个中间接口层，它主要由系统制造商实现。EGL 提供如下机制：
  - 与设备的原生窗口系统通信；
  - 查询绘图图层的可用类型和配置；
  - 创建绘图图层；
  - 在 OpenGL ES 和其他图形渲染 API 之间同步渲染；
  - 管理纹理贴图等渲染资源。
- **EGL 是 OpenGL ES 与设备的桥梁，以实现让 OpenGL ES 能够在当前设备上进行绘制。**
- <img width="668" height="519" alt="image" src="https://github.com/user-attachments/assets/8190b9ec-2e0c-4753-8566-b49111b76afa" />
- Display 是对实际显示设备的抽象。在 Android 上的实现类是 **EGLDisplay**。
- Surface 是对用来存储图像的内存区域 FrameBuffer 的抽象，包括 Color Buffer、Stencil Buffer、Depth Buffer。在 Android 上的实现类是 **EGLSurface**。
- Context 存储 OpenGL ES 绘图的一些状态信息。在 Android 上的实现类是 **EGLContext**。
- 这里需要注意的是 EGL 的工作模式是双缓冲模式，其内部有两个 FrameBuffer（帧缓冲区）：BackFrameBuffer 和 FrontFrameBuffer，当 EGL 将一个 FrameBuffer 显示到屏幕上的时候，另一个 FrameBuffer 就在后台等待 OpenGL ES 进行渲染输出。直到调用了 eglSwapBuffer() 这条指令的时候，才会把前台的 FrameBuffer 和后台的 FrameBuffer 进行交换，这时界面呈现的就是 OpenGL ES 刚刚渲染的内容了。
