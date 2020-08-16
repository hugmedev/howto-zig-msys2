# Setting up development environment from zero

1. install windows
1. install msys2
1. from msys2 install mingw-w64-x86_64-toolchain mingw-w64-x86_64-glfw mingw-w64-x86_64-glew
1. download master version of zig from official site
1. from msys2 set `export PATH="/path/to/zig:$PATH"` in ~/.bashrc
1. from msys2 create a directory for your project and cd there.
1. zig init-exe
1. do exe.linkSystemLibrary("c") since we're using c libs that need standard library.
1. if you're building for windows, set:
    ```
    if (target.os_tag) |tag| { 
        if (tag == .windows) {
            //exe.linkSystemLibrary("setupapi");
            //exe.linkSystemLibrary("winmm");
            exe.linkSystemLibrary("gdi32");
            //exe.linkSystemLibrary("imm32");
            //exe.linkSystemLibrary("version");
            //exe.linkSystemLibrary("oleaut32");
            //exe.linkSystemLibrary("ole32");
            exe.linkSystemLibrary("opengl32");
        }
    }
    ```
    Inspiration has been taken from https://github.com/andrewrk/zig-sdl/blob/13cb642ba827bb069c5b66a912dd26a072dfe9b0/build.zig#L100
1.  Now you can do zig build -Dtarget=x86_64-windows-gnu

# To distribute your binaries,
from msys2 use `ldd /path/to/your/binary`

This will list all dlls you depend on. You should copy only ones that are not in your windows system folder, because 

1. they are probably already installed in windows of humans
1. probably distribution of dlls from inside of your windows system folder has some licensing weakness


When you have your executable and all dlls it need in on directory, you can distribute it as zip or package it the way you want
