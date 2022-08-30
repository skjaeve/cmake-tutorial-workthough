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


Next step is to add an `add_subdirectory(MathFunctions)` statement to the toplevel `CMakeLists.txt`, and then "add the library to the executable", which apparently means the `target_link_libraries()` statement in the `CMakeLists.txt` snippet in the tutorial. It would be better to be explicit about this in the text. Ooh, there's that word `PUBLIC` again. Still no explanation of it.

These two new lines go on either side of `add_executable()`. No explanation.

Okay, from here on I'm going to abbreviate `CMakeLists.txt` as CML, because I can.

Next step is some code to make MathFunctions an optional library in this project. This is fair, I can absolutely see the use for optional libraries in a bigger project. Again, a new line in the middle of CML, again no explanation of placement. This is a confusing way to write files.

Hey, it feels like you forgot a conf/build step here, Mx. Tutorial. You just had me add some lines to CML, and (SPOILR) now you're gonna have me change those lines again without checking that they work?

Yup, that's exactly it. Anyway. The default for this new option is ON, but the tutorial informs me there are programs called **cmake-gui** and **ccmake** which can override the default value using the "cache". This is the first I've heard of a cache. I mean, I'm familiar with the *concept* of a cache, It just hasn't been explained to me as it relates to CMake. Yet. It probably will be explained better. Or I can guess. After all, something must have stored whatever CMake did between configure and build earlier.

Okay. Having added a variable that's supposed to control how something gets built, it makes sense to use that variable to control how something gets built. And that happens now. I am to add an `if` statement to CML. To the middle of it, of course.

Move the `add_subdirectory` statement into the `if` block. And then instead of naming the library and include file explicitly outside the block, we push their names to the lists `EXTRA_LIBS` and `EXTRA_INCLUDES`, and then we use those lists for `target_link_libraries()` and `target_include_directories()`.
And that's all fine, except for this little WTF:

> This is a classic approach when dealing with many optional components, we will cover the modern approach in the next step.

wat

why is

why do you

isn't this a tutorial

why are you even showing me the non-modern way

I don't want to learn this! I want to learn current, modern best practices. Not legacy. I mean, sure, I'll probably need to know it **later**, but not **now**! This is a tutorial! Don't teach me bad habits! Teach **me** how to do it **right**! Legacy practices is for dealing with *other* people's code!


\*breathe\*

Hokay. Modify the C++ code to use the optional library if it is enabled. Straightforward `#ifdef`s, and a thing called `#cmakedefine` which seems fairly obvious what it does in the `...h.in` template file.


Ooh, an exercise! Play with order of two CML statements and see what happens!

... nothing? Seems like it should matter, but as far as I can tell it makes no difference. 

Aha! It's because I misspelled `USE_MYMATH` when I defined it in CML. So: Good (and worrying) to know: CMake won't tell you if you don't use a variable, or use one you haven't defined. Apparently it's just implicitly false. Boo. When I fix that typo, and rebuild from scratch, I get the bevavior the exercise implies I should get.

And to clarify "from scratch": I had to remove and recreate the build directory between each rebuild. Just updating CML and rerunning `cmake` wasn't enough. So, CMake doesn't consider CML a dependency to be taken into account. This seems like a an annoying oversight. I hope there's something equivalent to `cmake clean` I haven't been told about, otherwise writing and debugging CML is going to be a major pain.

And now I am told how to change the value of USE_MYMATH from the command line: `cmake ../Step2 -DUSE_MYMATH=OFF`.

And that's the end of step 2.
# Summary
## What I did
I added a library to CML. Then I added it in a different way. Then I got upset.
## What I learned
Things can be optional. There are built-in lists that can be used for holding the names of optional things. I don't know if that knowledge is good or bad, I don't know if those lists are still used in modern CML. I have learned things and been told that I need to unlearn them. This is not good tutorialing. This is bad tutorialing.

There are if-tests.
There's a cache.
## What I'm missing
Still don't know what PUBLIC means. Still don't understand to that extent the ordering of statements in CML matters.
## Other
Twice, I was instructed to add something to CML and then modify it again without even testing if it worked.

DONTTEACHLEGACYPRACTICESINATUTORIAL


# Next: [Step 3: Adding Usage Requirements for a Library](step03.md)