# OneScript

> For more information visit the [General index](../README.md)

This provides a basic overview of the OneScript language and how it relates to the Macro Virtual Machine.

## General Terms
These general terms refer to all elements of OneScript
* `ident` - refers to an identity that can be any underscore or alpha, followed by any underscore or alphanumeric.
For example, `init` and `OneScript.Core.DateTime`.
* `literal` - a literal can refer to a value of numeric, string, boolean, date or enumerator value.
* `numeric` - numeric values can be integers or floating point values.
* `string` - string values.
* `date` - date and/or time values.
* `enumerator` - enumerator value is a special collection of values that can be used with the categorical or multiple choice type questions in a survey.
* `enum` - a enum value.

### Numeric Constants
Numerical constants can be in decimal, hexidecimal, binary, octal or float point. 
These can take the following forms:

Type | Example
---- | -------
`decimal-value` | 1, 2, -3
`hexadecimal-value` | ^X12F
`binary-value` | ^B10111
`octal-value` | ^O1234567
`floating-point-value` | 0.23, -.12, -123.45

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

### enumerator Constants
Enumerator constants can be an alpha optionally followed by an alphanumeric separated by a comma and surrounded by braces.
For example:
* `{a}`
* `{_1,_2}`
* `{a1}`
* `{a,b1}`
* `{abc}`

For more information on Enumerators [check here](Enumerators.md).

### enum Constants
Enum constants (not to be confused with enumerators) are a way to using an identifier to reference a constant value rather that placing the constant value everywhere in the code. For example:


### Keywords
The following keywords are reserved and may not be used as identifiers:

```
audio       bool         break       block       byte        case        
catch       class        continue    date        datetime    default
define      do           else        enum        enumerator  false
field       fix          float       for         foreach     global
goto        helperfields if          in          int         internal
is          new          nocasedata  null        media       object
page        picture      precision   private     public      ref
return      scale        string      struct      switch      throw
time        true         try         typeof      using       while    
validation  video        void

THERE ARE MORE...
```

### Objects
`object` refer to instances of classes that cannot be defined by the base types (bool, int, float, date, enum and string).

### Void
`void` refers to a 'no value' and is used to explain what is returned in a method.

### Null
`null` refer to a reference that has no value. This can be used to detect whether a value has been instantiated or not. If an object has not yet been instantiated then it is automatically set to null.

### String Constants
String constants are unicode with the ability to add encoded values from the following list:
* `\n` - new line
* `\r` - return 
* `\t` - tab

## Program Structure
OneScript is a light object orientated language. This means it does not support inheritance within its own language, but does support it through the objects it can create.

Basic statements and declarations in a OneScript program are added to a "Main" class if they are not declared explicitly within a class. The "Main" class is always used as the entry point to a OneScript Virtual Machine program.

### Declarations
Basic declarations take the following form:
* `int a = 0;`
* `string b;`
* `bool c, d;`

### Statements
Statements are used to control the flow of a program and manipulate data defined in declarations.
The following demonstrates a simple OneScript program:
```
string hw = "Hello Word";
Console.PrintLine(hw);
```

### Blocks
Statements can be grouped into blocks by using the `{` and `}` braces.
This allows statements to refer to a group of statements rathen just one.
For example:
```
if (a == 1) {
    a = 2;
    a = a + 1;
}
```
In some instances the a single statement can be used in place of a block.
For example:
```
if (a == 1)
    a = 2;
```

### Flow Control
OneScript contains the following program flow controls.

#### if Statements
A basic `if` statement requires a condition and a block referring to a statement that is executed 
if the statement results in a boolean value of `true`. For example:
```
bool b = true;
if (b) {
    // Perform this block.
}
```
A more extensive `if` statement includes the `else` statement. For example:
```
int b = 2;
if (b == 1) {
    // Perform this block
}
else {
    // Perform this block
}
```

#### do..while Statements
Do while statements follow the flow of performing a statement or block while an expression is true.
For example:

```
int a = 0;
do {
    a++;
} while (a < 30)
```

#### while Statements
While statements will perform the following statement or block whilst an expression is true.
For example:
```
int a = 0;
while (a < 20) {
    a++;
}
```

#### for Statements
For statements consist of a set of statements that control a loop.
1. A declaration initializer
1. A test
1. A changer

The simplest form of this is:
```
for (int i = 0; i < 5; i++) {
    Console.Write(i);
}
```
In this example the 

#### foreach Statements
Foreach statements are based on an iterator being implemented by the object be assessed. OneScript has a standard set of properties and methods that allow the `foreach` statement to be to  used.

```
foreach (Question question in questions) {
    question.Ask();
}
```

#### goto Statements
Goto statements rely on a label. They are basic representation of branching to a new statement. The following is an example:
```
b = 0;
start:
if (b == 10) {
    goto exit;
}

b = b + 1;
goto start;
exit:
...
```

#### return Statements
Return statements are used to exit methods and return to the call include method. 
```
Need some examples
```

### Error Handling
Error handling automatically handled by the Macro Virtual Machine. By default, when the application generates an error it will fail with unpredicted results and the user of the application must deal with it.

To take control of any errors it will be necessary to implement a `try..catch` coding control. For example:
```
try {
    if (a == 1) {
        ...
    }
}
catch(Exception e) {
    ...
}
```

It is possible to provide a set of catch clauses for different errors. For example:
```
try {
    if (a == 1) {
        ...
    }
}
catch(NullParameterException ne) {

}
catch(Exception e) {
    ...
}
```

Ultimately if the errors are not met then the error falls through to the next error handler in the stack. The catch statement can optional declare a variable that is store at the private method block level.



