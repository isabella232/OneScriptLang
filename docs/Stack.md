# Stack Management

Macro is based on a stack based virtual machine which is key to the way programs ar managed. most instructions push values onto the stack, pop values off the stack and push values back on the stack.

### Call Frame Stack
In order to handle methods there is also a call frame stack. This is used to push values onto a stack for the method and pop off for use in the method and return a value back.

### Error Handling
To support effective error handling there is also an error handling call frame stack. That can wipe out the Call Frame Stack and local stack management.

