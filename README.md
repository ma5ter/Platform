# Platform
CMake Embedded Platform Toolchain Framework

*Being mature and popular CMake is not always clearly understood and not easily can be tuned when dealing with non standard environments.*

The only existing 'official way' to use an usupported by the CMake embedded compiler is to define `CMAKE_SYSTEM_NAME` as `Generic`.<br> 
But there are many pitfalls inside this approach and it is nearly unavailable to get a nice working mechanism instead of ugly compromise.

This framework is intended to help using CMake based projects with various embedded compilers, be a cross-platform solution and became easily extensible.

## Which is supported
Now this framework supports these embedded compilers:

1. Microchip XC8

### Some extras
For the supported compilers the framework provides native CMake custom targets to produce `custom_compiler.yaml` files for the CLion IDE.<br>
Note that support of custom compiler was implemented in CLion starting version `213.4928.11`.

## Installation
First of all just clone this repository into your project's folder (side by side to the main `CMakeLists.txt` file)

    git clone --depth 1 https://github.com/ma5ter/Platform.git

Make sure that folder name with the content is unchanged and named as `Platform`

Add into the project's `CMakeLists.txt` file following required variables:

    set(CMAKE_SYSTEM_NAME Embedded)
    set(EMBEDDED_C_COMPILER XC8)

At least for the Microchip XC8 compiler a chip's part number should be supplied to properly generate default macros and other stuff: 

    set(CHIP 18f87j60)

When you need to use specific version of the compiled also add:

    set(EMBEDDED_C_COMPILER_VERSION X.XX)

where `X.XX` is a compiler version.

## Usage

Build works without any other efforts.

Run and debug is not supported by this framework and should be implemented as custom targets now.

### Usage with CLion

Prior to be recognized as custom compiler a proper `custom_compiler.yaml` file should be created.<br>
This is done by building custom target of `CLion-YAML` which is supplied by the framework and produces compiler's yaml file in the project's folder.

Next a custom compiler should be set up in the IDE as described here:
> https://blog.jetbrains.com/clion/2021/10/clion-2021-3-eap-custom-compiler/#using_a_custom_compiler_in_clion

After that CLlion recognizes all the predefined macros and system include paths of the compiler and stops arguing about unsupported compiler.
