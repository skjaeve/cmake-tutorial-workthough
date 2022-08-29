# Step 1: A basic starting point
Tutorial link: [Step 1: A basic starting point](https://cmake.org/cmake/help/latest/guide/tutorial/A%20Basic%20Starting%20Point.html)

Straightforward enough. Go to sample directory that contains one source file, and write the `CMakeLists.txt` file the tutorial says to.

Then to build. 

There's this sentence:
> First, run the cmake executable or the cmake-gui to configure the project and then build it with your chosen build tool.

I haven't chosen a build tool. Isn't CMake a build tool? 

Make a build directory (`Step1_build`) next to the source directory, go into it. 


```
$ mkdir Step1_build
$ cd Step1_build
```

> Next, navigate to the build directory and run CMake to configure the project and generate a native build system:

Native build system? What's that mean? I thought I was gonna use CMake to build.

Run cmake from build directory, pointing it at the source directory: `cmake ../Step1`

`cmake` runs, no error messages. Apparently, it makes a Makefile. So that's what it does.

```
-- Configuring done
-- Generating done
-- Build files have been written to:...
 ```

Build time! 
```
$ cmake --build .
```
It ... (drum roll) builds! And it runs.

# Summary

## What I did

I made a CMakeLists file. It defines a project name, which I don't know what is. It defines an executable, which I know what is, and the source file that goes into building that executable.

## What I learned

CMake apparently isn't a build tool. CMake doesn't build directly, it creates Makefiles and calls Make in the background.

Building is (can be) done in a different directory from where the source files are.


## What I'm missing
I didn't choose a build tool.

# Next: [Step 2: Adding a library](step02.html)
