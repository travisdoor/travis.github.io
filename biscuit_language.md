---
layout: page
title: Biscuit Language
permalink: /biscuit-language/
---
## About

{: style="text-align: justify;"}
Opensource game engine created from scratch in C with C# scripting interface inspired by Unity and Unreal engines.
Source code can be found [here](https://github.com/travisdoor/biscuit). This project is currently under development
and improved only in my free time.

{: style="text-align: justify;"}
The Biscuit engine is now completely migrated to the object oriented design in separate branch (features/bobject) and 
it will be merged into develop branch in few days.

## Currently implemented features

- **Render API abstractions**

  OpenGL is not used directly, render api interface is used for making rendering independent on API used by application.
  Rendering via Vulkan, DX or the other APIs can be implemented later without any major changes needed.
 
- **Simple 3D rendering**
  
  Renderable objects can be submitted for current frame and rendered later with use of render API abstracted interface.

- **Window creation and user input handling**
  
  SDL2 is used for system environment depend features.

- **Simple game loop**
- **Event system**
  
  Game or engine events can be passed around with event manager. There are two event types supported: immediate handled
  event (processed immediately) or events saved into queue and processed in next frame. Event system also helps
  to keep my engine modules more independent.

- **Resource loading**

  Every resource can be loaded with use of proper loader and it's instance can be shared around the engine.

- **Basic C# interface**
- **C# scripting**
- **Mathematics**
- **Component and Entity system**
- **Scene and game level loadings**
- **Error handling and error context**

  Biscuit engine use crash first philosophy, in most cases error causes termination of an application. Error context is 
  a concept helping to track the error.

- **Basic physics** (colisions and raycasting)
- **Multiplatform support** (MacOS, Linux, Windows)
- **Unit testting**

  Currently I'm trying to use Google test framework where it is possible.

## Dependencies
- thirdparty
    - SDL2
    - libpng
    - freetype
    - OpenGL
    - json-c
- internal
    - biscuit model
    - biscuit object
    - talloc
