# OneScript

> For more information visit the [General index](../README.md)

This provides a basic overview of the OneScript language and how it relates to the Macro Virtual Machine.

In reverence to all other languages OneScript offers the same capabilities as many other languages:
```
Console.Write("Hello World");
```

## General Terms
These general terms refer to all elements of OneScript
* `ident` - refers to an identity that can be any underscore or alpha, followed by any underscore or alphanumeric.
For example, `init` and `OneScript.Core.DateTime`.
* `literal` - a literal can refer to a value of numeric, string, boolean, date or enumerator value.
* `numeric` - numeric values can be integers or floating point values.
* `string` - string values.
* `date` - date and/or time values.
* `enumerator` - enumerator value is a special collection of values that can be used with the categorical or multiple choice type questions in a survey.
* `enum` - a value type defined by a set of named constants of the underlying integral numeric type.

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

```
enum Fluid {
    Water,
    Coke,
    Milk,
    Tea,
    Coffee
}
```

## Whitespace

OneScript programs are defined through the OneScript language which is case sensitive. It supports each keyword and associated operator can be separated with whitespace. The following can be considered to be whitespace:
* `Space`
* `Tab`
* `//` followed by a comment
* `/*` with a comment `*/`

### Keywords
The following keywords are reserved and may not be used as identifiers:

```
audio          bool         break
byte           case         catch       
class          continue     control 
date
default        define       do
else           enum         enumerator
false          fields       fix
float          for          foreach
global         goto         helperfields
if             in           int
initial        is           new
nocasedata
null           media        object
page           picture      precision
private        public       ref
return         scale        string
struct         switch       throw
time           true         try
typeof         using        while    
validation     video        void

THERE ARE MORE...
```

### Basic Data Types
The following basic data types are built into OneScript

Type | Description
---- | -----------
`bool`| a boolean value that be either true or false.
`byte` | an unsigned byte value
`int` | a signed integer value
`float` | a floating point value
`date` | a date value
`string` | a string value
`enum` | an enum numeric value.
`enumerator` | 
`object` | an object
`void` | used to define the absence of a value (for example a method with no return value)

### Objects
`object` refer to instances of classes that cannot be defined by the base types (bool, int, float, date, enum and string).

### Void
`void` refers to a 'no value' and is used to explain what is returned in a method.

### Null
`null` refer to a reference that has no value. This can be used to detect whether a value has been instantiated or not. If an object has not yet been instantiated then it is automatically set to null.

### String Constants
String constants are delimited with a double quote `"`. String constants are unicode with the ability to add encoded values from the following list:
* `\n` - new line
* `\r` - return 
* `\t` - tab
* `\\` - back slash
* `\"` - double quote
* `""` - double quote

## Program Structure
OneScript is a "Light Object Orientated Language". This means it does not support inheritance within its own language, but does support it through the objects it can create from libraries.

Basic statements and declarations in a OneScript program are added to a "Main" class if they are not declared explicitly within a class. The "Main" class is always used as the entry point to a OneScript Virtual Machine program.

### Declarations
Basic declarations take the following form:
```
int a = 0;
string b;
bool c, d;
float f = 0.2;
```

### Arrays
Declare arrays using brackets (`[]`), and create the array using the `new` statement.
```
int[] a = new int[3];
```

Access the array elements using brackets:
```
a[0] = 2;
```

### Statements
Statements are used to control the flow of a program and manipulate data defined in declarations.
The following demonstrates a simple OneScript program:
```
string hw = "Hello Word";
Console.PrintLine(hw);
```

### Blocks
Statements can be grouped into blocks by using the `{` and `}` braces. This allows statements to refer to a group of statements rather just one. For example:
```
if (a == 1) {
    a = 2;
    a = a + 1;
}
```
In some instances the a single statement can be used in place of a block. For example:
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
In this example the `int i = 0` is the declaration initializer, the `i < 5` is the test and the `i++` is the changer.

The `break` statement will force the loop to finish and move onto the next statement. The `continue` statement will force the process to jump to the next changer statement continuing the loop.

#### foreach Statements
Foreach statements are based on an iterator being implemented by the object be assessed. OneScript has a standard set of properties and methods that allow the `foreach` statement to be to  used.

```
foreach (Question question in questions) {
    question.Ask();
}
```

The `break` statement will force the loop to finish and move onto the next statement. The `continue` statement will force the process to jump to the next changer statement continuing the loop.

#### switch Statements
Switch statements supports any kind of data type and is designed to support testing for for equality of a value against other values:

```
switch (question.QuestionName) {
    case "fred":
        question.Ask();
        break;
    case otherQuestion.QuestionName:
        otherQuestion.Ask();
        break;
    default:
        break;
}
```

Like many other languages the break statement will route the logic to the next statement outside of the switch block.

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

#### Methods
Methods are declared by using parentheses and wa block of statements. For example:
```
string greet(string person, string day) {
    return "Hello" + person + " today is " + day;
}
```

#### return Statements
Return statements are used to exit methods and return to the call include method. When the end of the statements are reached in a method an automatic return is carried out. 
```
void CheckStatus(int status) {
    if (status == 1) {
        return;
    }

    question.Ask();
}
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

It is possible to force an error with the `throw` statement. for example:
```
if (a == 0) {
    throw new Exception("There is a problem with a");
}
```

### Snapshots
Snapshots are a particular feature of OneScript that supports the ability to move back and forth in an application by defining a `snapshot` of the application to jump back to later. 
```
    save snapshot "intro";
    q1.Ask();
    q2.Ask();
    if (q2.Response.Value == null) {
        restore snapshot "intro";
    }
```

A snapshot will hold information about the virtual machine position in the code and the restoration of a snapshot will automatically jump the flow of the application back to the statement directly after the save snapshot statement with the equivalent name.

> Note: The snapshots are automatically generated for questions in the Interview Model and named after the questions full name in the [Interview Model](InterviewModel.md).


## Fields
To make OneScript a researchers language it supports the definition of fields that hold the definitions of questions to be asked and results to be stored for analysis. Fields are declared in a field block:
```
    fields {
        catGRCOptIn {   ENU:"<b>Do you have a <u>Genting Rewards Card</u>?</b>", 
                       ZHA:"您是否持有<u>云尊卡</u>？" } 
            categorical [1..1] {
                r01 { ENU:"Yes" , ZHA:"是" } factor (1),
                r02 { ENU:"No" , ZHA:"否" } factor (2), 
                - "No Answer" NA factor (99)
            };
    }
```
A field can describe the options, language and controls to be used in the asking of a question, but is also accessible through the object interfaces (IInterview, IQuestion, ICategory, etc.) automatically generated for OneScript.
```
    catGRCOptIn.MustAnswer = false;
    CatGRCOptIn.Ask();
```
When the `Ask` method of a question is used a Snapshot is automatically generated to support the ability to move back and forth through questions. A feature that is supported by DIY Surveys.

For more information on Field please refer to the [Fields Reference](Fields.md)

## Classes
Classes are a way of encapsulating methods and properties together. Unlike other languages OneScript classes only have basic capabilities and cannot be inherited or used in polymorphisms.
```
    class Shape {
        public int numberOfSides = 0;
        public string SimpleDescription() {
            return "A shape with " + numberOfSides + " sides";
        }
    }
```
An instance of a class can be created in the following way:
```
    Shape shape = new Shape();
    shape.numberofides = 3;
    shape.SimpleDescription();
```
