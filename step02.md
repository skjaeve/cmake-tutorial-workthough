# Step 2: Adding a Library
Tutorial link: [Step 2: Adding a Library](https://cmake.org/cmake/help/latest/guide/tutorial/Adding%20a%20Library.html)

New directory: `Step2/`. In here' there's a subdirectory called `MathFunctions`. It cointains a C++ code file and a C++ header for said file.
This is a library, and not a part of the project proper. As I understand it, which I don't, really.

For now, I'll guess at "library" meaning "code included in the project sources, but not written specifically for this project". As opposed to, say, a pre-compiled shared library living in `/usr/lib/` or `c:\\windows\\system32`. Which is also a library, but not the same kind of library. I guess this is for when I copy for example [{fmt}](https://github.com/fmtlib/fmt) directly into my sources instead of compiling and linking it separately.

The `MathFunctions` library needs a separate `CMakeLists.txt`. It's already starting to get confusing. This is what that file contains:

```
add_library(MathFunctions mysqrt.cxx)
```

Which, if I were to guess wildly, which I am, tells CMake that this is a library with a separate build step? Compilation? Something?


# Summary
## What I did
## What I learned
## What I'm missing