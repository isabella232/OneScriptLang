# Fields
A key feature of OneScript is to define questions and answers structures to be stored in the interview. Fields can be one of the basic types:

Type | Description
---- | -----------
`info` | An information field type that is just used to present a question that expects no response.
`int` | A integer value.
`float` | A floating value.
`string` | A test question to store single words, phrases and or general free text.
`categorical` | A multiple choice single answer and multiple choice multiple answer type question.
`define` | A like the categorical field, but reuseable many times in place of a categorical list.
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

## Controls
Field definition can include a specific reference to a control to use by the presentation of the question. The ability to present the desired control is up to the presentation layer the environment that the OneScript Virtual Machine is running in.

The following example shows a multiple choice single answer categorical type question that is traditionally presented as a list of radio buttons with labels:

```
intro_choice "Choose an option" [1] categorical
{
    _1 "Choice 1",
    _2 "Choice 2",
    _3 "Choice 3"
};
```

By applying a control style this can be changed to a drop down list:

```
intro_choice "Choose an option" [1] categorical
style 
( 
    control 
    (
        type = droplist
    ) 
)
{
    _1 "Choice 1",
    _2 "Choice 2",
    _3 "Choice 3"
};
```

The following set of controls are available:

```
button              checkbutton             date
datetime            dtoplist                listbox
listcontrol         multilineedit           password
radiobutton         singlelineedit          static
time                slider                  barcode
geocode             media                   draganddrop
star                email
```

## Categoricals
The categoricals clause for categorical and loop type fields can be expanded into the following part:

```
'{' categorical { , categorical } '}'
[ rot[ate]  | ran[domise] | rev[erse] | asc[ending] | desc[ending] ]
[ fix ]
```

The optional clauses to the categories are describes as follows:

Name | Description
---- | -----------
rotate | The categorical list is rotated by one before each presentation
randomize | The categorical list is presented in a random order each time
reverse | The categorical list is presented in reverse order to the order it was coded in
ascending | The categorical list is presented in ascending order based on the name of the categorical
descending | The categorical list is presented in descending order based on the name of the categorical
fix | If the categorical list is a sub list then its position remains fixed regardless of the overall clauses defined to set the categoricals. 

A categorical can be described in the following way:

```
identifier
[ label ]
[ <other> | DK | REF | NA ]
[ exclusive ]
[ factor (factor_value) ]
[ fix ]
[ nofilter ]
```

Name | Description
---- | -----------
identifier | The name of the categorical as an identifier
label | The categorical label that is displayed to the user
other	| Implemented by the compiler not implemented by the runtime
DK, REF and NA | Indicates that the enumerator is special of a special type referring to "Don't Know", "Refused to Answer" and "Not Applicable" respectively. These are automatically made immune from any ordering applied to the enumerator list and placed at the end of enumerator list.
exclusive | Indicates that if the enumerator is selected then it cannot be combined with any other enumerator selections.
factor (factor_value) | Used to define a numerical value to associate with the enumerator. The enumerator value must be numeric.
fix | Fixes the enumerator's position in the category list regardless of the ordering applied to the enumerator list.
nofilter | Prevents the enumerator from being filtered out of the list of enumerators in OneScript.

It is also possible to create a sub list of enumerators in two ways - as direct list of enumerators:

```
identifier
[ label ]
<enumerators>
```

Or you can use a defined list:

```
identifier
use list-name
[ sublist [ rot[ate] | ran[domize] | rev[erse] | asc[ending] | desc[ending] ]
label
[ fix ] 
```
## Helper Fields
Helper fields are used to support additional features and characteristics of a survey, allowing control at the question/field level. Currently Helper fields support the ability to override error messages for specific questions. This adds an additional level of personalisation. The example below shows a date field with the range error message overridden to be more helpful.

```
Date1  "Please select a date and time for your call."
  style(Control(Type="date"))
  date ["2018-01-01 09:00am".."2100-12-31 05:00pm"]
  helperfields (
    StandardTexts block fields (
        NotInRange "The date cannot be earlier than 1st Jan 2018" info;
    )
  );
```

## Properties
Properties are a simple way of storing additional data in the Fields area. Properties can be associated with fields and the enumerators within fields. It is really easy to define properties for a field or enumerator. The example below shows a text field with some properties:

```
example "Example property field"
    [ show = false ]
    info;
```

This could be used during the main logic of the script in the following way:

```
if (example.Properties["show"].Value.ToBool() {
    example.show()
}
```

The field properties could be altered to influence the main logic of the script without having to change the main logic.

To add properties to the main interview model there is a special info field called "interview". This can be used in the following way:

```
interview
    [ checkQuota = true ]
    info;
```

To access this property the main scripting would need to include:

```
if interview.Properties["checkQuota"].Value.ToBool() {
    checkQuota(Interview)
}
```

The script above checks the value of the checkQuota property and if it is true it performs the checkQuota method.


## Field Definitions

### Info Field
The info field is for display only and not designed to collect an answer from the participant. For example:

```
hello "How are you" info;
```

### Text Field
A string field defines a question that holds a text value. The length of the string is limited to around 2 billion.

```
identifier
[ label ]
[ [ <properties> ] ]
[ <styles and templates> ]
string
[ [ range ] ]
[ <categoricals> ]
[ <codes> ]
[ ( initial | default ) (text) ]
[ fix ]
[ <usage-type> ]
[ <helperfields> ]
[ nocasedata ]
```

### 

