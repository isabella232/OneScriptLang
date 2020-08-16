# OnePoint Global Virtual Machine
The OnePoint Global Virtual Machine is designed with a Java and PDP machine in mind. The best way to understand teh virtual machine is to use the [OneScript Macro Language](Macro.md).

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



