# FEMCourseEigen ON WINDOWS

***Author:*** Pedro Lima 

***Date:*** March 2021  

## Notes

---

- **Note 0:** This tutorial assumes you have `forked` this repository from [https://github.com/labmec/FEMCourseEigen](https://github.com/labmec/FEMCourseEigen). If you haven't forked it, or don't know what a fork is, you should ask your professor or check course syllabus, then come back here.
- **Note 1:** C++ development with CMake on Windows is tricky. If this is your introduction to programming with C++ and you never heard of CMake, you should probably go for **Ubuntu** or **MacOS**.  Your course instructor probably recommended you to go for Ubuntu, and **you should listen to him**. Finite Element approximations will prove challanging enough on their own. Figuring these stuff out on your own will not be trivial. Proceed at your own risk.
- **Note 2:** I’m writing this after I got it working with **Visual Studio Community 2019 as my compiler**, and **VSCode as IDE**. I did not try anything else, but made an effort not to assume any code editor from the reader. As a result, this tutorial feels general enough that others can adapt it to their needs. If you’d like the adventure yourself, here are some other popular options: 
 
    - Visual Studio Community as compiler & editor;
    - CLion;
    - MinGW+VSCode; 
    - Cygwin+VSCode;
> If you manage, though,  please write up a similar tutorial and submit it so others can benefit from your accomplishments.

- **Note 3:** Don't be alarmed by error messages when installing Eigen and Boost. As long as the build ends successfully with error code 0, you're fine.
- **Note 4:** Things that are different for each reader were written with the placeholder `${thing}` and you should, obviously, replace it for whatever you have on your side. 
`${thing} = thing-in-my-pc`
e.g. my name is Nina Simone so, in my computer, I'm logged in as a user named `nina` <br>
 `${your-username}` = `nina`<br>
NOT `${nina}` JUST `nina`
- **Note 5:** I left some micro-steps and little details unwritten. I judged the instructions of the package providers (Eigen, CMake, git, …) were clear enough for the reader to figure out what option should suit their own machine.

---

## Steps

1. Download and install Visual Studio [https://visualstudio.microsoft.com/vs/community/](https://visualstudio.microsoft.com/vs/community/)
    - Open the downloaded *Visual Studio Installer* and configure your Visual Studio installation to your preferences;
    - *“C++ for desktop development”* should have more than enough packages for this course;

    ---

    - **Note:** If you know what you’re doing, you can tweak the configuration a bit to get Visual Studio to install CMake & git for you. If so, you could possibly skip steps 2 and 3. 
    (I’ve added them anyway, just in case.)

    ---

2. Download and install CMake (Binary distribution)
    - [https://cmake.org/download/](https://cmake.org/download/)
    - `Windows x64 Installer` is probably what you want, but you have to chose the one for your machine;
    - During installation, make sure you select **“add CMake to path”**, for convenience.
3. Download and install git
    - [https://git-scm.com/downloads](https://git-scm.com/downloads)
4. Create the following directories on your disk:

    (If you know what you're doing, you don't have to follow this step perfectly, but I'll assume you did)

    REPLACE `${your-username}` for your username on your computer.

    `C:\Users\${your-username}\projects`

    `C:\Users\${your-username}\projects\lib`

5. Download Eigen (optional)

    If Eigen is not found by CMake, it will then be downloaded automatically. In case you would rather install it anyway, you can follow these instructions:
    
    - [https://gitlab.com/libeigen/eigen/-/releases/3.3.9](https://gitlab.com/libeigen/eigen/-/releases/3.3.9)
    - You want the `Source code (zip)`

    ---
    
    **Note:** Eigen is a header-only library, so you could just copy the `/Eigen` folder from within the zip you downloaded and paste it into your `/headers2021` directory, but the course `CMakeLists.txt` assumes you've properly installed it, so:
    
    ---

    - Unpack it inside the directory `projects/lib` that you created few steps ago
    - Open your preferred terminal (`cmd` or `WindowsPowerShell`) and don't forget to change the placeholder `${your-username}`

    ```bash
    cd C:\Users\${your-username}\projects\lib
    mkdir eigen-build
    mkdir Eigen3
    cd eigen-3.3.9
    cmake -S . -B ..\eigen-build -DCMAKE_INSTALL_PREFIX:PATH=C:/Users/${your-username}/projects/lib/Eigen3
    cd ..\eigen-build
    cmake --build . --target install
    ```
6. Install Catch2 (optional)

[https://github.com/catchorg/Catch2](Catch2) is used for the Unit Tests. It is also automatically downloaded by CMake if not found.

7. Clone course repository.

    Assuming you have already forked the repository, open your preferred terminal and run:

    ```bash
    cd projects
    git clone https://github.com/${your-github-username}/FEMCourseEigen
    ```

8. Configure
    - Open the CMake GUI;
    - Select your project root directory in `Where is the source code:`

        If you've been following, it'll be at
         `C:\Users\${your-username}\projects\FEMCourseEigen`

    - Select your preferred build directory in `Where to build the binaries:`

        If this is your first time, you might want to use
         `C:\Users\${your-username}\projects\FEMCourseEigen\build`

    - Press **configure**.

        (If you're doing this for the first time, CMake will ask you what type of *MakeFiles* you want it to generate. This is compiler dependent, and this tutorial expects you to choose VisualStudio 2019)

    - Resolve any path CMake couldn't automatically find (there shouldn't be any if you followed this tutorial correctly);
    - Keep pressing **configure** until there are no more error messages;
    - Press **generate**
9. Build
    - Go to your preferred IDE, or command line and build.
    
    <details><summary> IF YOU ARE USING VSCode click the triangle to the left to unfold more instructions </summary>
    - Download the following extensions:

        1. C/C++ [by Microsoft]
        2. CMake [by twxs]
        3. CMake Tools [by Microsoft]
        4. C/C++ Themes [by Microsoft]
        5. Better C++ Syntax [by Jeff Hykin]

    - Press `ctrl`+`shift`+`P`
    - In the prompted box at the top, type

        `CMake: Delete Cache and Reconfigure`

        the search should autocomplete before you can finish

    - Execute the command.
    - If you're prompted for a kit, you probably want

        `Visual Studio Community 2019 Release - x86_amd64`

        if that doesn't work, you can try the other kits. There's a button at the bar at the bottom. You can also leave [non specified] and have CMake try to guess it (that didn't work for me).

    - Press `ctrl`+`shift`+`P` again
    - now type `CMake: Clean Rebuild` and run the command to build all targets.
    </details>

10.  Paraview
    [https://www.paraview.org/download/](https://www.paraview.org/download/)
    
   - Pick windows and version 5.9 (which is the latest release as I'm writing this).
   - Download the installer <br>
   **ParaView-5.9.0-Windows-Python3.8-msvc2017-64bit.exe**

---
---
---
