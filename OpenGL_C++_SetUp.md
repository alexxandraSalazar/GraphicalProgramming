# Setting Up OpenGL and GLFW in Visual Studio  2022

For this, I am using **Visual Studio  2022**. If you don’t already have the setup for using **C++**, that should be your first step.

If you already have it, that’s good.

## Installing OpenGL and GLFW

As you may or may not know, **OpenGL is a cross-platform, low-level API for rendering 2D and 3D graphics**. This is not something you can just download and use immediately; it depends on your **GPU**. This means that not all programs will run on all computers—it depends on your GPU and the drivers provided by its manufacturer.

You need to install **GLFW (Graphics Library Framework)**:

- **Download the Windows precompiled binaries** from the GLFW website.
- GLFW is a **library that helps create windows, handle input, and manage OpenGL contexts**.

## How They Work Together

- Since OpenGL itself does not handle window creation, **GLFW is often used to create a window and OpenGL context**.
- Developers use GLFW to set up the environment and OpenGL to render graphics within that environment.

## Creating the Project in Visual Studio 

1. **Create an empty C++ project** in Visual Studio .
2. **In the root directory**, create a folder named `src`.
3. Inside `src`, create a file named `Application.cpp`.
4. You can copy and paste the source code from the documentation.

## Setting Up Dependencies

1. Open the **solution folder** in **File Explorer** and create a new folder named `Dependencies`.
2. Inside `Dependencies`, **copy and paste** the `include` and `lib-vc2022` (this version may change—use the latest one) folders from the GLFW download.
3. In the `lib-vc2022` folder, **keep only `glfw3.lib` and delete the other files**.

## Configuring Visual Studio 

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

---

## Installing GLEW

1. **Download the GLEW precompiled binaries**.
2. Add them to the `Dependencies` folder and rename the folder to `GLEW` for better organization.

### Configuring GLEW in Visual Studio 

1. Go to **Properties** → `C/C++` → `General` → **Additional Include Directories** and add:

    ```bash
    $(SolutionDir)Dependencies\GLEW\include
    ```

2. Go to **Properties** → `Linker` → `General` and add this to the **Additional Library Directories**:

    ```bash
    $(SolutionDir)Dependencies\GLEW\lib\Release\x64
    ```

3. In **Properties** → `Linker` → `Input`, add:

    ```bash
    glew32s.lib
    ```

4. At the top of `Application.cpp`, add:

    ```cpp
    #include <GL/glew.h>
    #include <iostream>
    ```

5. Go to **Properties** → `C/C++` → `Preprocessor` and add:

    ```bash
    GLEW_STATIC;WIN32;
    ```

### Setting Up GLEW Initialization

To properly initialize GLEW, it must be set up **after** creating the OpenGL context. Modify the OpenGL setup to include:

```cpp
/* Make the window's context current */
glfwMakeContextCurrent(window);

// Initialize GLEW
if (glewInit() != GLEW_OK)
    std::cout << "Error!" << std::endl;

---
# Setting Up OpenGL and GLFW in Visual Studio 2022

For this guide, we will be using **Visual Studio 2022**. If you haven’t set up C++ development yet, install the **Desktop development with C++** workload via the **Visual Studio Installer**.

If you already have it installed, you’re good to go.

---

## Installing OpenGL and GLFW

As you may or may not know, **OpenGL is a cross-platform, low-level API for rendering 2D and 3D graphics**. OpenGL is not something you can just download and install directly—it relies on your **GPU** and its **drivers**. This means that not all programs will run on every computer; compatibility depends on your GPU manufacturer and driver support.

To simplify window management, we will use **GLFW (Graphics Library Framework)**.

### Installing GLFW

1. Download the **Windows precompiled binaries** from the [GLFW official site](https://www.glfw.org/download.html).
2. GLFW is a **library that helps create windows, handle input, and manage OpenGL contexts**.

---

## How They Work Together

- OpenGL does **not** provide functionality for window creation or input handling.
- **GLFW** is commonly used to create a window and an OpenGL rendering context.
- Developers use GLFW to manage the environment and OpenGL to render graphics within that environment.

---

## Creating the Project in Visual Studio

1. **Create an empty C++ project** in Visual Studio.
2. In the project directory, **create a new folder** named `src`.
3. Inside `src`, create a file named `Application.cpp`.
4. You can copy and paste example source code from the GLFW documentation to test the setup.

---

## Setting Up Dependencies

1. **Open the solution folder** in **File Explorer**.
2. **Create a new folder** named `Dependencies`.
3. Inside `Dependencies`, **copy and paste** the `include` and `lib-vc2022` (or the latest version) folders from the GLFW download.
4. In the `lib-vc2022` folder, **keep only `glfw3.lib` and delete the other files**.

---

## Configuring Visual Studio

1. **Right-click the project in Solution Explorer** and select **Build**.
   - This will produce errors because we haven’t configured dependencies yet.
2. **Right-click the project again** and go to **Properties**.

### Adding Include Directories

- Navigate to **C/C++** → **General** → **Additional Include Directories**.
- Add the following path:

    ```
    $(SolutionDir)Dependencies\GLFW\include
    ```

This tells Visual Studio where to find GLFW's header files.

### Linking the GLFW Library

- Navigate to **Linker** → **General** → **Additional Library Directories**.
- Add the following path:

    ```
    $(SolutionDir)Dependencies\GLFW\lib-vc2022
    ```

### Linking OpenGL and GLFW Libraries

- Navigate to **Linker** → **Input** → **Additional Dependencies**.
- Replace the existing content with:

    ```
    glfw3.lib; opengl32.lib; User32.lib; Gdi32.lib; Shell32.lib
    ```

Now, **press `Ctrl + F5`**, and you should see a black window appear.

---

# Installing and Configuring GLEW

To use modern OpenGL features, we need **GLEW (OpenGL Extension Wrangler Library)**.

### Installing GLEW

1. Download the **Windows precompiled binaries** from the [GLEW official site](http://glew.sourceforge.net/).
2. Extract the files, then move the `include` and `lib` folders to `Dependencies`.
3. Rename the extracted folder to `GLEW` for better organization.

### Configuring GLEW in Visual Studio

1. Go to **Properties** → **C/C++** → **General** → **Additional Include Directories** and add:

    ```
    $(SolutionDir)Dependencies\GLEW\include
    ```

2. Go to **Properties** → **Linker** → **General** → **Additional Library Directories** and add:

    ```
    $(SolutionDir)Dependencies\GLEW\lib\Release\x64
    ```

3. Navigate to **Properties** → **Linker** → **Input**, then add:

    ```
    glew32s.lib; opengl32.lib; glfw3.lib; User32.lib; Gdi32.lib; Shell32.lib
    ```

4. In your `Application.cpp` file, add the following at the top:

    ```cpp
    #include <GL/glew.h>
    #include <iostream>
    ```

5. Finally, go to **Properties** → **C/C++** → **Preprocessor** and add:

    ```
    GLEW_STATIC; WIN32;
    ```

> ⚠️ **Important:**  
> The `GLEW_STATIC` definition should **only** be added if linking against the **static** GLEW library (`glew32s.lib`). If using the dynamic library (`glew32.lib`), **do not define `GLEW_STATIC`**.

---

## Initializing GLEW in Code

After setting up OpenGL, GLEW must be initialized **after creating the OpenGL context**. Modify your OpenGL setup as follows:

```cpp
/* Make the window's context current */
glfwMakeContextCurrent(window);

// Initialize GLEW
if (glewInit() != GLEW_OK)
    std::cout << "Error initializing GLEW!" << std::endl;
