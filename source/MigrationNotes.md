# Migration Notes

This document summarizes the portability issues with the current code base in respect to porting
to Apple Silicon.  Note, our Xcode will only build for macOS, not iOS/tvOS/watchOS.

## Existing Code

### icdab_thread

This has x86 specific thread state.  Needs migration.

## New Code

### Fixed arg called with variadic args

Write an example program that calls a function implemented with fixed arguments, with variadic arguments on the call site, and show it crashing on ARM; see https://developer.apple.com/documentation/apple_silicon/addressing_architectural_differences_in_your_macos_code


### Dynamic calls with objc_msgSend

Write an example program that unsafely is transformed to variadic by objc_msgSend; see https://developer.apple.com/documentation/apple_silicon/addressing_architectural_differences_in_your_macos_code

### Boolean from Int failure

Since 1024 cast to BOOL is false on x86 but true on arm64 write some code which leads to a logic crash; see https://developer.apple.com/documentation/apple_silicon/addressing_architectural_differences_in_your_macos_code

### Execute data as code

Write a simple program that places assembly code in a data array and then jumps into it.  This simulates writing a JIT compiler.  The aim is to trigger execute on readonly data segments; see https://developer.apple.com/documentation/apple_silicon/porting_just-in-time_compilers_to_apple_silicon