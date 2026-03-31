---
topic: "[[Agent Intelligence Framework]]"
publish: true
---
`AIF` uses a slightly different approach to function libraries. It uses a raw object with virtual functions. Then, through the project settings, we get the class default object and call the functions that way.
This approach allows users to create a child of the function library class and override the functions. All while designers and other programmers continue interacting with the functions as if it was a plain function library without making modifications to the plugin.

## Changing the function library class
Each module of `AIF` has its own developer settings, so depending on what module you're working with, you might need to subclass different function libraries.

## Using the library in C++
Depending on the context of your C++ code, it might be better to use other methods to achieve your goal. For example, if you're in a Mass processor and want to know if an entity has a tag, it's more efficient to use the `Execution Context` to evaluate it.

The libraries 2 biggest purposes is to simplify some C++ logic, and to create a bridge for blueprint developers to work with Mass. Sometimes this process leads to inefficiencies. So again, evaluate the context of your C++ code.

In some scenarios, the library provides C++-only functions, templates or macros that try to have no ineffiencies and just simplify C++ code.
