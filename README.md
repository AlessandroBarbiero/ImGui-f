## Dear ImGUI framework
Easy ready-to-go framework to implement a Dear ImGUI application that uses Vulkan + GLFW as backend.

# How to run
To run a new application simply include imgui_framework.hpp and then call

```c++
ImGUI_f::init(width, height, "window_name");

// If you need particular fonts load them here
// e.g.
// ImGuiIO& io = ImGui::GetIO();
// io.Fonts->AddFontFromFileTTF("../../misc/fonts/Roboto-Medium.ttf", 16.0f);

ImGUI_f::uploadFonts();
ImGUI_f::run(&update_function);
```

The callback function will be called at each frame, place here the Dear ImGUI commands to display what you want.

Build the CMake project from the cmake-gui and run it.