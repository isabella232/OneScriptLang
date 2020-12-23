# Fields
A key feature of OneScript is to define questions and answers structures to be stored in the interview. Fields can be one of the basic types:

Type | Description
---- | -----------
`info` | An information field type that is just used to present a question that expects no response.
`int` | A integer value.
`float` | A floating value.
`string` | A test question to store single words, phrases and or general free text.
`categorical` | A multiple choice single answer and multiple choice multiple answer type question.
`date` | The ability to ask a question that refers to a date and/or time.
`image` | The ability to store media in response to a question.
`struct` | A structure containing a combination of field types from the above list.
`page` | This field type supports the idea of structuring a number of of the above field types into a page for presentation that responds to the navigation of the page it may be displayed on.
`loop` | A field type that combines the other field types into a set of categories or numerical loops so as to ask the same questions a number of times.

## Field Definitions
A field definition takes the following basic format:

```
name [ label ] type ';'
```
Each element can be described as follows:

Name | Description
---- | -----------
`name` | The name of the field
`label` | The text to display to the respondent.
`type` | The type of field. For more information on this please read below.


For example an information field could take the following format:

```
welcome "Welcome to the interview" info;
```

## Initial and Default Answer
For questions that expect a response it is possible to set up what you would like to display as the initial answer for the respondent to see and what we should set the answer to if they do not select anything. For example:

```
name "What is your name?" text initial("Doug")
```



## Field Definitions

### Info Field
The info field is for display onlyy and not designed to collect an answer from the participant. For example:

```
hello "How are you" info;
```


