# Sets

> For more information visit the [General index](../README.md)

Unlike many other languages, OneScript supports the ability to store, combine and test options that may represent options selected by recipient of a survey. The set type takes the following basic form:

```
{ident[,ident]}
```
For example:
```
{a,b,c}
```
It is possible to combine sets for example:
```
set e1 = {a,b,c};
set e2 = {g,h,i};
e1 = e1 + {d};                // Result is {a,b,c,d}
e1 = e1 - {a};                // Result is {b,c,d}
e1 = e1 + e2;                 // Result is {b,c,g,h,i}
```
It is also possible to test whether an set is present in a value is:
```
set e1 = {a,b,c};
set e2 = e1 & {a};            // Result is {a}
e2 = e1 & {h};                // Result {}
e2 = e1 | {h};                // Result is {a,h}
```

