# Setting Up OpenGL and GLFW in Visual Studio Code 2022

For this, I am using **Visual Studio Code 2022**. If you don’t already have the setup for using **C++**, that should be your first step.

If you already have it, that’s good.

## Installing OpenGL and GLFW

As you may or may not know, **OpenGL is a cross-platform, low-level API for rendering 2D and 3D graphics**. This is not something you can just download and use immediately; it depends on your **GPU**. This means that not all programs will run on all computers—it depends on your GPU and the drivers provided by its manufacturer.

You need to install **GLFW (Graphics Library Framework)**:

- **Download the Windows precompiled binaries** from the GLFW website.
- GLFW is a **library that helps create windows, handle input, and manage OpenGL contexts**.

## How They Work Together

- Since OpenGL itself does not handle window creation, **GLFW is often used to create a window and OpenGL context**.
- Developers use GLFW to set up the environment and OpenGL to render graphics within that environment.

## Creating the Project in Visual Studio Code

1. **Create an empty C++ project** in Visual Studio Code.
2. **In the root directory**, create a folder named `src`.
3. Inside `src`, create a file named `Application.cpp`.
4. You can copy and paste the source code from the documentation.

## Setting Up Dependencies

1. Open the **solution folder** in **File Explorer** and create a new folder named `Dependencies`.
2. Inside `Dependencies`, **copy and paste** the `include` and `lib-vc2022` (this version may change—use the latest one) folders from the GLFW download.
3. In the `lib-vc2022` folder, **keep only `glfw3.lib` and delete the other files**.

## Configuring Visual Studio Code

1. **Right-click the root folder** and select **Build**.
    - It will give you a bunch of errors, but that’s okay because we haven’t done the proper setup yet.
2. **Right-click the root folder again** and go to **Properties**.
3. Click on `C/C++`, then in **Additional Include Directories**, paste this:
    
    ```
    $(SolutionDir)Dependencies\GLFW\include
    ```
    
    - This simply sets a relative path to the GLFW include files.
4. Next, go to `Linker` → `General` and paste this in the **Additional Library Directories** field:
    
    ```
    $(SolutionDir)Dependencies\GLFW\lib-vc2022
    ```
    
5. Lastly, go to `Linker` → `Input`, and in the **Additional Dependencies** field, replace the existing content with:
    
    ```
    glfw3.lib; opengl32.lib; User32.lib; Gdi32.lib; Shell32.lib
    ```
    
Now press `Ctrl + F5` and you will see a black window.