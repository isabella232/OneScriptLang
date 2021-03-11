# Macro Instruction Reference

## Exception Handlers

Macro has exception handling built in as a set of instructions. They manage the exception stack that runs alongside the thread it is associated with. If the exception handler fails to capture an exception then the operating system exception handler takes over.

The instructions are as follows:

### throw
#### Operation
Throw an exception to the exception handler stack
#### Format
`throw` extended_ident
#### Forms
`throw NullException`
#### Description
