# Dear ImGUI framework
Easy ready-to-go framework to implement a Dear ImGUI application that uses Vulkan + GLFW as backend.

## How it works
To create a new application simply include imgui_framework.hpp 

```c++
#include "imgui_framework.hpp"
```

Then call

```c++
ImGUI_f::init(width, height, "window_name");

// If you need particular fonts load them here (You need to have a TTF file saved somewhere)
// e.g.
// ImGuiIO& io = ImGui::GetIO();
// io.Fonts->AddFontFromFileTTF("../../misc/fonts/Roboto-Medium.ttf", 16.0f);

ImGUI_f::uploadFonts();
ImGUI_f::run(&update_function);
```

The update_function() will be called at each frame, place here the Dear ImGUI commands to display what you want.

You can see an example looking at [example.cpp](example.cpp).

Remember to update the values in the [CMakeLists](CMakeLists.txt) for `GLFW_DIR` and `IMGUI_DIR`.

Build the CMake project from the command line writing for example:
```cmd
mkdir build
cd build
cmake -G "Visual Studio 16 2019" ..
```

Or from the cmake-gui.