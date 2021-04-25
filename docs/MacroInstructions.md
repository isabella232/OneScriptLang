# Macro Instruction Reference

## Exception Handlers

Macro has exception handling built in as a set of instructions. They manage the exception stack that runs alongside the thread it is associated with. If the exception handler fails to capture an exception then the operating system exception handler takes over.

The instructions are as follows:


### hpush
Push a handler onto the handler stack. A handler is made up of a set of exception types and label to the code to goto.

```
    ...
    hpush NullException(10$)
    loads #"Welcome"
10$:
    ...
```

### throw
Throw an exception takes the form:

```
    throw NullException, #"Null values not accepted"
```
The string reference is optional. When this instruction is used and the handler stack fails to support the exception the next handler is popped off the stack and so on. If no handlers can support the error then a general error is declared by the OneScript Runtime.

### hpop
A handler can be popped off the exception stack and discarded, so that future exceptions not longer take advantage of the handler.

```
    hpop
```




