## Introduction
V8 is bascially consists of the memory management of the heap and the execution stack (very simplified but helps
make my point). Things like the callback queue, the event loop and other things like the WebAPIs (DOM, ajax, 
setTimeout etc) are found inside Chrome or in the case of Node the APIs are Node.js APIs:
```
    +------------------------------------------------------------------------------------------+
    | Google Chrome                                                                            |
    |                                                                                          |
    | +----------------------------------------+          +------------------------------+     |
    | | Google V8                              |          |            WebAPIs           |     |
    | | +-------------+ +---------------+      |          |                              |     |
    | | |    Heap     | |     Stack     |      |          |                              |     |
    | | |             | |               |      |          |                              |     |
    | | |             | |               |      |          |                              |     |
    | | |             | |               |      |          |                              |     |
    | | |             | |               |      |          |                              |     |
    | | |             | |               |      |          |                              |     |
    | | +-------------+ +---------------+      |          |                              |     |
    | |                                        |          |                              |     |
    | +----------------------------------------+          +------------------------------+     |
    |                                                                                          |
    |                                                                                          |
    | +---------------------+     +---------------------------------------+                    |
    | |     Event loop      |     |          Callback queue               |                    |
    | |                     |     |                                       |                    |
    | +---------------------+     +---------------------------------------+                    |
    |                                                                                          |
    |                                                                                          |
    +------------------------------------------------------------------------------------------+
```
The execution stack is a stack of frame pointers. For each function called that function will be pushed onto 
the stack. When that function returns it will be removed. If that function calls other functions
they will be pushed onto the stack. When they have all returned execution can proceed from the returned to 
point. If one of the functions performs an operation that takes time progress will not be made until it 
completes as the only way to complete is that the function returns and is popped off the stack. This is 
what happens when you have a single threaded programming language.

So that describes synchronous functions, what about asynchronous functions?  
Lets take for example that you call setTimeout, the setTimeout function will be
pushed onto the call stack and executed. This is where the callback queue comes into play and the event loop. The setTimeout function can add functions to the callback queue. This queue will be processed by the event loop when the call stack is empty.

TODO: Add mirco task queue
