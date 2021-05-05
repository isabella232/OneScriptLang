# Macro Virtual Machine
The Macro Virtual Machine is designed with a Java and PDP machine in mind. The best way to understand teh virtual machine is to use the [Macro Language](Macro.md).

## Environments
The Virtual machine runs in a number of environments which is better described [here](Environemtns.md).

## Common Virtual Machine Operations
Regardless of the environment the virtual machine has a common operative level. This is describe by the following steps:

### Startup
When a virtual is started up it is given some information about the environment that it is running in. This includes the following information:

Item | Description
---- | -----------
Player | The player that is responsible for presenting question and getting the answer to and from the respondent.
Cache | The cache service that saves the answers to a result object model and makes it possible to restart a survey from where it was interrupted.

### Player
A player is responsible for the presentation of a question and the collection of the results. Depending on the presentation target the player will be simple or complex. A player for SMS is going to be far simpler than a player for mobile web or a mobile app.

Players can be plugged into the virtual machine and tailored to the target platform.

### Threads
When a virtual machine is started the main thread is responsible for processing the survey. [OneScript](OneScript.md) has the ability to handle errors and process events. It also follows that the virtual machine has the ability to process errors by creating 


### Image Structure
Image structure refers to the byte layout of a Macro Image that can be loaded by the Macro Virtual Machine. The basic structure  of a a Macro Image is split into the following:

Item | Description
---- | -----------
Header | Basic Header that provide a good starting point to check that it is a real Macro Image
Using List | A list of references to external libraries that can be loaded by the Macro Virtual Machine to resolve references.
Class List | A list of classes to load up
String List | To save space string a placed in a separate table and referenced by the image.

#### Header
The header includes a special binary pattern followed by the entry pointer.

Item | Description
---- | -----------
Pattern | a four byte pattern matching the values 1,2,3,4
Entry Point | an integer that refers to the class in the image that contains the entry point.

#### Using List
The using list is a list of external libraries that will be used to resolve references that cannot be resolved internally.




