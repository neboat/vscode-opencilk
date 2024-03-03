# Cilk README

This langauge extension provides syntax-highlighting for Cilk programs.  This extension adds the **Cilk/C** and **Cilk/C++** language modes, which extend the C and C++ langauge modes, respectively, with support for syntax-highlighting the Cilk keywords `cilk_for`, `cilk_spawn`, `cilk_scope`, `cilk_sync`, and `cilk_reducer`.

You can enable more powerful VS code capabilities to work on Cilk programs using the [clangd VS Code extension](vscode:extension/llvm-vs-code-extensions.vscode-clangd) configured to use [OpenCilk](https://www.opencilk.org/)'s custom version of [clangd](https://clangd.llvm.org/).

## Features

This extension introduces the Cilk/C and Cilk/C++ language modes, which add support for syntax-highlighting the Cilk keywords to the C and C++ language modes.  This extension only adds support for syntax-highlighting C/C++ programs that use Cilk.  VS Code uses other extensions to provide more powerful programming features, including code completions, cross references, and hover and inlay hints.

To enable advanced VS Code capabilities to work on Cilk programs, use and configure the [clangd VS Code extension](vscode:extension/llvm-vs-code-extensions.vscode-clangd) as follows:

- Install the [clangd VS Code extension](vscode:extension/llvm-vs-code-extensions.vscode-clangd), and set it up in the usual manner.  In particular, make sure that clangd is set up to build your program with the OpenCilk compiler and the `-fopencilk` flag.  See the [clangd documentation](https://clangd.llvm.org/installation#project-setup) for more information on setting up clangd.
- Update the `clangd.path` setting to point to a copy of the clangd binary built or shipped with OpenCilk, e.g., `"clangd.path": "/path/to/opencilk/bin/clangd"`.

After that, you should be able to VS Code's advanced programming capabilities on Cilk programs, as illustrated here:

![Example of VS Code's support for code refactoring on a `cilk_for` loop.](images/cilk_for-refactor-example.png)

## Requirements

To enable advanced VS Code features, you will need OpenCilk's custom version of clangd, which adds support for Cilk.

To get OpenCilk's custom version of clangd, [build and install OpenCilk](https://www.opencilk.org/doc/users-guide/build-opencilk-from-source/) with the `clang-tools-extra` project enabled.

If you are building OpenCilk using the `tools/build` script in the [OpenCilk/infrastructure repository](https://github.com/OpenCilk/infrastructure), modify the script as follows before running it:

```diff
--- a/tools/build
+++ b/tools/build
@@ -72,7 +72,7 @@ cd "${BUILD_DIR}"

 : "${OPENCILK_RELEASE:=Release}" # RelWithDebInfo to debug the compiler
 : "${OPENCILK_ASSERTIONS:=On}"   # Off to disable assertions in the compiler
-OPENCILK_COMPONENTS="clang"      # Required components; edit to add extra LLVM projects
+OPENCILK_COMPONENTS="clang;clang-tools-extra"      # Required components; edit to add extra LLVM projects
 OPENCILK_RUNTIMES="cheetah;cilktools" # Required runtimes
 # Add compiler-rt project to enable support for Google sanitizers.
 case "${OS}" in

```

## Known Issues

Found a bug or a missing feature, either with this language extension or OpenCilk's clangd?  Please post an issue on the [issue tracker](https://github.com/neboat/vscode-opencilk/issues).

## Release Notes

This extension is based on the [Better C++ Syntax extension](vscode:extension/jeff-hykin.better-cpp-syntax) and extends the syntaxes in that extension to support the Cilk keywords.

### 1.0.0

Initial release of the OpenCilk VS Code language extension, with basic instructions on how to setup the clangd VS Code extension for Cilk programs.
