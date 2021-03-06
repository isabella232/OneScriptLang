# Macro

> For more information visit the [General index](../README.md)

Macro is the Macro virtual machine assembly language that maps directly to its machine code.

## General Terms
These general terms refer to all elements of Macro
* `ident` - refers to an identity that can be any alpha, `$`, `^` or `.`, followed by an alphanumeric, , `$`, `^` or `.`.
For example, `$init` and `OneScript.Core^DateTime`.
* `literal` - a literal can refer to a value of numeric, string, boolean, date or enumerator value.
* `numeric` - numeric values can be integers or floating point. 
* `string` - string values.
* `date` - date and/or time values.
* `set` - enumerator value is a special collection of values that can be used with the categorical or multiple choice type questions in a survey.

### Numeric Constants
Numerical constants can be in decimal, hexadecimal, binary, octal or float point. These can take the following forms:
* [ `^D` ]`decimal-value`
* `^X` `hexadecimal-value`
* `^B` `binary-value`
* `^O` `octal-value`
* `^F` `floating-point-value`

### Date Constants
Date constants must be prefixed `^T` (For example `^T01-12-2020`) and take the following form:
* `DD-MM-YYYY`
* `DD-MM-YY`
* `DD/MM/YYYY`
* `DD/MM/YY`
* `DD-MMM-YYYY`
* `YYYY-MM-DD`

A date value can also hold a time in the following form:
* `hh:mm:ss.ssss`
* `hh:mm`
* `hh:mm:ss`

### set Constants
Set constants can be an alpha optionally followed by an alphanumeric separated by a comma and surrounded by braces.
For example:
* `{a}`
* `{a1}`
* `{a,b1}`
* `{abc}`

### Objects
`object` refer to instances of classes that cannot be defined by the base types (bool, int, float, date, enum and string).

### Void
`void` refers to a 'no value', which is different to a null that is not currently support in Macro.

### String Constants
String constants are unicode with the ability to add encoded values from the following list:
* `\n` - return
* `\r`
* `\t`

## Whitespace

Macro programs are defined through the Macro language which is case sensitive. It supports each keyword and associated
operator can be separated with whitespace. The following can be considered to be whitespace:
* `Space`
* `Tab`
* `//` followed by a comment
* `/*` with a comment `*/`

## Directives

A Macro program is controlled though a set of directives that are denotes with a full stop ('.'). 
Directives start an directive area and remain in control until the next directive is encountered.
These are as follows:

Directive | Description
--------- | -----------
`.import` | the import directive refers to libraries that should imported to resolve external references.
`.name` | the name of main class included in the Macro source file
`.table` | a table directive section includes data elements that can be referenced. A table
`.class` | a class directive section includes tables and methods to declare a class. Multiple classes can be contained in one Macro source file to save time.
`.method` | a method can be included in the main source file or within a class. After a method directive there can be a table directive reflecting local data to the method and a code directive referring to the code within the method.
`.code` | a code section can only be held within the a method directive section and refers to the Macro code for the method.
`.end`| refers to the end of the source code and optionally an entry point in the list of methods defined at the top level.

### Program Structure
Program structure is achieved using directives. A simple application might take the following form:

```
.import OneScript.Core
.name Sample
.table
    string helloWorld
.method void G^$Main()
.code
    sload "Hello World"
    store helloWorld
    invokestatic Console.Write(string);
.end G^Main(0)
```

It is possible to create applications tht can be run and libraries that can be reused a number of times by Macro and OneScript applications.

### .import
In order to ensure the Macro compiler understands where to search for external references.
These references can refer to one of the following:
* Classes, methods, constants and enumerators in a DLL declared in the Macro system configuration.
* Classes, table entries declared in other pre-compiled objects found in an opgo (OneScript object) files.

```
.import import-reference
```

### .name
The name of the module used when it is referenced in the .import director if ths the object file generated is used by the
Linker.

```
.name name-ident
```

### .table
Macro allows for data declaratives that can later be used in the code. Following a `.table` directive data declaratives and methods can be defined.The `.table` directive can be used either at the top level along side other directives or
after a `.method` directive that implies the data declarations are local to the method.

#### Data Declaratives
Data declaratives must take the following form:
```
[ modifier ] data-type ident [ = expression ]
```
The `modifier` can be any one of the following:

Name | Description
---- | -----------
`global` | A global data declarative means that it is available for external libriaries to see.
`local` | A local data declarative means that it is avilable for either the local library or the method depending where the table is defined.

By default a data declarative is said to `local` to its position within the 

The `data-type` can be any one of the following:

Type | Description
---- | -----------
`bool`| a boolean value that be either true or false.
`byte` | an signed byte value
`int` | a signed integer value
`float` | a floating point value
`date` | a date value
`string` | a string value
`set` | a set value
`object` | an object
`void` | used to define the absence of a value (for example a method with no return value)

The `data-type` can also be a type held within an imported library. For example:

`IException exception`

Examples of a data declaration are as follows:
```
.table
    int temp
    string stringValue
```
It is possible to assign an initial value to a data declaration using an expression. For example
```
    int temp = 1
```
The assignment value can be any expression that can be calculated at compile time. For example
```
    int temp = 1 * 3
```
but not:
```
    int initialValue
    int temp = 1 * initialValue
```
because `initialValue` cannot be calculated.

### .method
The method directive is used to declare a method that can contain it's own table and code sections.
The method directive takes the following form:
```
.method data-type ident([data-type { ',' data-type }])
```
It is usually followed by an optional table directive and a code directive. For example:
```
.method void Test()
.table
    int temp
.code
    iload temp
    ireturn
```

The Macro virtual machine operates on a stack based processor. When a method is called a 'Call Frame' is created and all primitive data-types are passed by value with other value passed by reference. It is generally recommended that a method be completed with a return type operator to ensure that the 'Call Frame' is removed from the 'Call Frame Stack' and control is correctly returned to the called method.

### .code
The code directive is used within the method section to declare the code section. It must be followed by instructions that form the code of a method. For example:
```
.code
    iload temp
    ireturn
```
For more information on the instructions and operands please [check here](Instructions.md).

### Operands
Operands are the parameters for instructions. They can be one of the following:

#### Immediate
Denoted by prefixing the hash ('#') to the value and refers to constant value or an expression that can result in a constant value.
```
    iload #23
    addi #50
```
The above will push an integer value of 23 onto the stack, add an integer value of 50 to it and push the result onto the stack.

##### Reference
A reference to a declaration in the Macro source code or an external value to be found in the imported libraries.
```
    iload initial
    addi #23
```
The above will push the integer value of `initial`, add an integer value of 23 to it and push the result onto the stack.

##### Indexed Reference
A reference to a indexed value with a further integer value pulled off the stack to reference a specific index of the value.
```
    iload values[0]
    addi values[index]
```
The above will load the integer value referenced by `values` and indexed by 0, add the integer value referenced by `values` and indexed by `index` and push the result onto the stack.

#### Registers
Macro has 12 registers that allow provide an alternative to storing temporary data in a table or on the stack and access to processor status values

Name | Description
---- | -----------
r0 - r9 | Registers that can hold any object
pc (r10) | The program counter of the current instruction
sp (r11) | The stack pointer for the current stack
ps (r12) | The processor status

## Scope
Scope refers to whether a declaration (method or table declaration) is local to the table it is within or made available
to external references. For methods this is denoted by prefixing the `ident` with `g^`. For example:
```
.method void g^$init()
```
For declarations it is denoted by the using the modifier `global` or `local` (`local` is the default). For example:
```
    global int starter
```

## Constants
It is possible to define a table declaration as a constant. This allows the compiler to use potentially compile the code that uses it in a different way (However at this point in time there is no affect). For example:
```
    global constant int starter = 0
````
