# Welcome to the OneScript Language
OneScript is a wonderful way to write programs that target running surveys. The basic language offers a powerful programming tool and the associated libraries makes it possible to access survey capabilities for different presentation layers such web desktop and mobile app.

OneScript is friendly for new programmers but also familiar to programmers to c, c#, Java, JavaScript and such languages. 

The goal of the OneScript project is to provide the best available language that works for researching. the ability to set up a set of questions and define the logic to process those  questions and ultimately store them in a data structure that can be used with the OneScript Data Analytics and/or third party data analytics.

## Status
This project is currently in development and OneScript still needs to be completed along with teh runtime.

## Features
The OnceScript features are designed to work together to make it easy for a developer to build data feedback 
and analytics solutions.

* OneScript follows a familiar language construct offered by languages such as c#, Java and JavaScript.
* Access to a common platform on Windows, Linux, MacOS, iOS and Android that support the OneScript Macro Virtual Machine
* Follows object orientated features and supports basic classes with c# properties.

## OneScript Language
The OneScript language is compiled into an object library that is based on a language called Macro that can be translated by the OneScript Linker into a image for the Macro Virtual Machine. For more information on the OneScript language please refer to the [OneScript Language Overview](docs/OneScript.md).

## Interview Model
The interview model is a part of the OneScript language that allows you to create the structure to ask and store questions for a survey. There are a number of types of questions:

Type | Description
---- | -----------
Informational | no question asked!
String | a basic free text question.
Categorical | a single or multiple choice type question.
Date | a date and time type question.
Image | a media type question.
Block | a group of questions to be plugged into a single question.
Page | a group of questions for a page.
Loop | a group of questions that can be turned into a grid.


It is backed up by a set of classes that support an interview (a single survey) experience both at the scripting level and the presentation level depending on the platform.

## Macro Virtual Machine (MacroVM)
A virtual machine based on a combination of the Java Virtual Machine and the Digital/PDP 11 Virtual Machine. 

It provides a combination instruction processing with operand specification on a stack based machine

### Macro Language
In order to help with the testing of the OneScript model the [Macro Language](docs/Macro.md) is also provided used to generate object for the Linker that are more directly associated with the OnePoint Global Virtual Machine.

## Linker
A linker of objects created by the Macro compiler and OneScript compiler into an executable suitable for the Macro Virtual
Machine contained within the OnePoint Runtime. This supports the ability to create reuseable objects across different
projects.

## Platforms
The MacroVM is available on different platforms with the aim of providing a survey with any level of complex logic that work exactly the same across the different platforms. These platforms are offered through players:
* Web
* App
* Facebook
* WhatsApp
* Desktop
* Custom App