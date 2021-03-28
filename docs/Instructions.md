# Instructions
Code instructions are made up of an operator and operands. For example
```
    iload #0
```
The above shows the operator to load an integer. This particular operator expects only one operand and in this instance is is the immediate value '0'.

Instructions usually denote the type of data it is operating upon (int, boolean, etc.) with a prefix of the type. For example:
```
    iload #0                // Refers to an integer to be loaded onto the stack
    bload #true             // Refers to a boolean value to be loaded onto the stack
    sstore localStringValue // Refers to the string on the stack to be stored in the 
                            // table declaration referenced by localStringValue
```

## Instruction Structure
Instructions are usually structured in the following way:
```
{type}{action}
```

### Type
The type can be one of the followings:
Type | Description
---- | -----------
b | boolean
d | date/time
i | integer
e | enumerator
f | float
s | string

### Action
The action can be one of the following:
Action | Description
------ | -----------
load | Load a value onto the stack
store | Store a value in a program location. This could be in a local, or global entry.
return | Return a frame off the stack returning to the current program counter location.

## Conversion Instructions
These instructions convert one type to another. They take the form:
```
{base}cvt{destination}
```
For example:
```
icvtb
```
It is possible to convert types based on the table:

- | bool (b) | byte(by) | int (i) | date (i) | enum (i) | float (f) | string (s)
- | -------- | -------- | ------- | -------- | -------- | --------- | ----------
bool (b) | x | x | | || | x
byte (by) | x | | x |||| x
int (i) | x | x | | x | x | x | x
date (d) | | | | | || x
float (f) | x | x | x | | | | x
string (s) | x | x | x | x | x | x


## Conditional Instructions
It is possible to branch from one location to another based on that value on te top of the stack.
Instruction | Description
----------- | -----------
ifeq | If equal to zero then branch
ifne | If not equal to zero then branch
ifgt | If greater than zero then branch
iflt | If less than zero then branch
ifge | If greater than or equal to zero then branch
ifle | If less than or equal to zero then branch
iftrue | If true then branch
iffalse | If false then branch
ifnull | If there is a null value on the stack then branch
ifnotnull | If there if not a null value on the stack then branch

Each on of the conditional instructions has a boolean push stack version. this is achieved by adding a `b` to the instruction. For example:
```
    ifeqb
```
The above instruction pops the integer value from the stack and converts it to a boolean value (if value equals zero then push true else push false).

## Unconditional Branching Instructions

### Goto Instruction
To support this there is also the `goto` statement that you can use to branch unconditionally to a position in the instructions. For example:
```
    ...
    load questions
    invokevirtual InitialiseLooping()
a10$:
    load questions
    invokevirtual Next()
    iffalse a20$
    load questions
    invokevirtual GetItem()
    store question
    load question
    invokevirtual Ask()
    goto a10$
a20$:
    ...
```

### Call and Return
To support code that you want to repeat it is possible to call a method and return from it.

### Calling External Libraries
To support external libraries it is possible to support


## Stack Management
Just in case you want to mange the stack independently of the rest of the instructions set you can also use the `pop` instruction to remove items from the stack.

## Error Handling
It is possible to define error management using the `pushh`, `throw` and `poph` instructions. For examples:
```
    ...
    pushh Exception,x30$ NullException,x40$
    load questions
    invokevirtual InitialiseLooping()
a10$:
    load questions
    invokevirtual Next()
    iffalse a20$
    load questions
    invokevirtual GetItem()
    store question
    load question
    invokevirtual Ask()
    goto a10$
a20$:
    ...
x30$:
    // general exception
    ...
x40$:
    // Null exception
    ...
```
The `pushh` instruction pushes a handler onto the handler task. Thew handler stack operates as a cascading exception handler, so if the error is not picked up by the handler on top of the stack the next handler is used.

The `throw` instruction will cause an exception to be thrown and the handler stack to be accessed for in search for an exception handler that will support the error.

The `poph` instruction will remove the handler off the top of the handler stack.

These three instructions allow the Macro Virtual Machine to mimic most language try, catch type error handlers.

### Exceptions
It is possible that an instruction itself can cause an exception. If this happens it will trigger access to the handler stack. An exception is based on the following list:

Exception | Description
--------- | -----------
Exception | A general exception and a catchall.
NullException | A null value was detected.
DivideByZero | Division by zero detected.


