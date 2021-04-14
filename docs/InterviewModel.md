# Interview Model

> For more information visit the [General index](../README.md)

The Interview Model is a set of classes that allow the customization of a survey experience:
1. The Interview Model supports the representation of the questions defined through the fields statements in OneScript.
1. The Interview Model supports access to every properties and feature of a question or field to be stored with the results of a survey.
1. The Interview Model supports the ability to route between questions depending on the results collected.
1. The interview handles saving questions in a format be loaded into a DB for analysis.

## Interview Cycle
To run an interview a OneScript Image is loaded and creates an Interview State used to maintain a session for the interview to processed. The Interview State provide access to a context value which in turn provides access to the Interview Model for the current interview.

## Cache File
As an interview is run a cache is generated that contains the result of the survey. These cache files can be loaded into a database for analysis. In cases where an interview times out a cache file is also used to restart a survey.

## Interview State
The interview state is used to access the state of the current interview from within a OneScript application. Interview State is only created when fields are defined in OneScript. Form more information on this please refer to [Fields](Fields.md).

When a field is declared the Interview Model is generated and set up in the Interview State.

## Interview Model
The interview model contains a summary of the interview status and a list of the questions together with their responses.

## Question Model
Each field created in OneScript will have a Question Model added to the Interview Model. The Question Model contains a list of 

## Categorical Model
For complex type questions (for example, those with multiple choices) Categorical Models are generated.

## Response Model
Each Question Model contains a reference to the response made at the data entry point of the survey.

## Label Model
Where text can be displayed a label model is referenced. This allows access to piping and multiple languages for questions, options and navigation.

## Navigation Model
The navigation model describes the navigation of a survey and manages what controls (buttons and dropdowns) appear to manage the navigation back and forth through a survey.
