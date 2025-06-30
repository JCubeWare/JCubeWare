![JCubeWare Logo](https://jcubeware.com/Public/Images/JCubeWare_Guidelines.png)

# Setting Up

The recommended OS for our projects should run on the Linux kernel.
OS of our choice for now is Ubuntu.

If you have Windows, you may get a virtual machine or use WSL 
(<a href="https://learn.microsoft.com/en-us/windows/wsl/install">Learn More</a>).

# Coding Convention

## File Header

Every file header should have this entire comment on top.
If in C, put the header between the comment start and commend end symbols.

Leave one empty line underneath the header.

```python
           #################################
          ###                          #####
        ###     ######################### ##
      ###     ###                   ##### ##
    ####     ########################  ## ##
  ####                          ###    ## ##
####                          ####     ## ##
################################ #     ## ##
##                     #     ##  #  ## ## ##
##                     #     ##  #  ## ## ##
##                     #     ##  #  ##### ##
##                     #     ##  # ###### ##
##                     #     ##  # #  ### ##
##                     #     ##  ###  ### ##
##                     #     ##  ##    ## ##
##########             #     ##  ##    #  ##
##       #             #     ##  ##      ###
##       #             #     ##  #      ### 
##       #             #     ##       ###   
##       ###############     ##     ####    
##                           ##   ####      
##                           ## ####        
##                           #####          
################################            

############# [J][C]ube[W]are ##############
#   Be responsible. Code for the future.   #
#         (c) 2025-2025, JCubeWare         #
############################################
```

## Formatting

### File Naming

File naming is in Pascal Case:

```
TestProgram.c
StringFunctions.h
```

### Whitespace

Be very cautious about leaving behind whitespace at the end of the line.
Carefully review your code and reduce it.
The only source of spaces at the end should be from the header

### Line length

Line length should always be maxmimum of 80 characters, as that's the most 
widely supported standard.

If you are to split a long function call, such as the following:

```c
int Result = ThisIsALongTestFunctionThatDoesStuff(FirstArgument, SecondArgument, ThirdArgument, RandomPointer);
```

Split it up so the tokens are indented one block deeper.

```c
int Result = ThisIsALongTestFunctionThatDoesStuff(
	FirstArgument,
	SecondArgument,
	ThirdArgument,
	RandomPointer
);
```

### Indentation

Indentation is always Tabs. Tab size used most by us is 4 characters long.

Tabs are flexible and permit your own indentation for convenience.

## Naming

For most things, we use a cursed mix of Pascal Case and Snake Case.
Underscores separate the context, similiar to namespace in other languages.

## Functions

Functions are the basis of C, so it's very important you get all the 
neccessary information at just a glance.

The function name should contain the context (where it's from) and
it's general purpose.

```c
int TestFunction_HandleRandomEvent
(
	float FirstArgument,
	void* SecondArgument
)
{
	return TEST_OK;
}
```

If the function has no arguments to take, define it as follows.

```c
int TestFunction_DoStuff
(
	void
);
```

Declarations should always be the same format inside the header files and in 
the files they are defined in.

```c
int TestFunction_HandleRandomEvent
(
	float FirstArgument,
	void* SecondArgument
);
```

## Control Flow

Control flow is a very important thing for the program.
To all tokens this applies, a space between the token and it's argument is good.

```
if (...)
switch (...)
while (...)
```

### if

If there is a single statement after the if, no braces are required.

```c
if (TestValue > 0)
	SingleStatement();
```

However, when there are multiple, it's required to have the braces.

```c
if (TestValue > 0)
{
	MultipleStatements();
	NextToEachOther();
}
```

If the content of the parenthesis is too big to fit in one line, split them up
like so. In this case, the space between the if and parenthesis is not required.

```c
if
(
	(LongerIf == 1)
	&& (!ThisIfHasASingleLine)
)
	DoStuff();
```

### else

else has the exact same notation as if()


```c
else
	SingleStatement();
```

```c
else
{
	MultipleStatements();
	NextToEachOther();
}
```

```c
else if
(
	(LongerIf == 1) &&
	(!ThisIfHasASingleLine)
)
	DoStuff();
```

### while

while() has the exact same notation as if()

```c
while (TestValue > 0)
	SingleStatement();
```

```c
while (TestValue > 0)
{
	MultipleStatements();
	NextToEachOther();
}
```

```c
while
(
	(LongerIf == 1) &&
	(!ThisIfHasASingleLine)
)
	DoStuff();
```

### switch

The switch is indented in the way that the cases are moved one block lower
than the switch statement itself. It's visually easier to discern.

```c
switch (TestValue)
{
	case 0:
		DoStuff();
		break;
	case 1:
		DoSomethingElse();
		break;
	default:
		DoTheDefault();
		break;
}
```

### Labels / Goto

Usually, goto is frowned upon due to it's disruptive nature in algorithms.
Should you require one, please be careful in the potential memory leaks and 
context breaking it can cause.

Place labels at the start of the line, regardless of indentation.
Always make the goto label lowercase to distinct it from the code.

```c
	int ArgumentIndex;
	goto testlabel
testlabel:
```

### Returns

Write returns without the parenthesis, unless it's a comparison.

```c
return TestValue;
return (TestValue == 5);
```

## Variables

Variables are another cornerstone of every programming langauge.
Handling them is the most important part of the program.

### Context

Context wise, each variable should be it's own line.

```c
// int x,y,z;

int XPosition;
int YPosition;
int ZPosition;
```

The variables should also be separated from the code if they are in a function.
One line is enough

```c
int TestVariable;
int AnotherOne;

TestProject_DoStuff();
```

### Naming

The name of the variables should be concise and have a point.

```c
int i; // BAD
int IteratorForTheEntireLoop; // BAD
int Iterator; // GOOD
int ArgumentIndex; // GREAT

char* string; // BAD
char* TheRequiredStringForParsing; // BAD
char* ParsingString; // GOOD
char* StringToPrase; // GREAT
```

### Order

Variable declaration should be ordered based on their size and status.

We generally tend to prefer native C before custom structs.

```
char
short
int
TestProject_t
```

Uninitialized should come first.

```
int Result;
int ArgumentIndex = 0;
```

### Pointer Asterisk

The pointer asterisk should always be right next to the type.
That makes it easier to look for all pointer variables.

```c
char * Buffer; // BAD
char *Buffer; // BAD
char* Buffer; // GOOD
```

### Structs and Unions

Structs and unions are formatted like functions.
Name on the first line, declaration on the other.

```c
struct TestProject_Test
{
	int Amount;
	void* Pointer
};

union TestProject_Value
{
	int Integer;
	float Float;
	char* Text;
}
```

### Enums

To let the user know that it's an enumerated value, we use the "_e" suffix.
Every enum must end with a member that has the context, name of the enum and 
`_COUNT_` at the end.

To separate enums and defines between each other, enums have the start context
with normal formatting and the rest with only uppercase characters.

```c
enum TestProject_ReturnState_e
{
	TestProject_OK,
	TestProject_BAD,
	TestProject_RETURNSTATE_COUNT_ // This must be always last
};
```

### Custom types

To let the user know that it's a custom type, we use the POSIX suffix.

Please keep in mind that the struct itself is best handled outside of
the typedef so you can have a pointer to itself (For things like linked lists).

```c
struct TestProject_Test
{
	int Amount;
	void* Pointer
};

typedef struct TestProject_Test TestProject_Test_t;
```

## Macros

Macro defines should be named fully uppercase so it's obvious they are macros.

```c
#define TESTPROJECT_BUFFER_SIZE 8192
```

Macros are always at the start of the line, regardless of any further
indentation in the file.

```c
#ifndef TESTPROJECT_COMMON_H
#define TESTPROJECT_COMMON_H

...

#endif
```

```c
#if TESTPROJECT_USE_PROTO_VALUE
	int TestValue = 5;
#else
	int TestValue = 10;
#endif

	TestProject_HandleTestValue(TestValue);
```

## Commenting

### File organizing

The biggest use for comments in our code is organizing the file itself.
These are used across different programming langauges too.

**C**
```c
/*##====[ BIG HEADER ]====##*/
/*#===[ SUBHEADER ]===#*/
```
**Python / Bash**
```python
##====[ BIG HEADER ]====##
#==[ SUBHEADER ]==#
```
**Assembly**
```assembly
; ##====[ BIG HEADER ]====##
; #===[ SUBHEADER ]===#
```

Headers most commonly found in the files:
```
##====[ EXTERNAL INCLUDES ]====##
##====[ INCLUDES ]====##
##====[ HELPER FUNCTIONS ]====##
##====[ FUNCTIONS ]====##
##====[ DEFINES ]====##
##====[ VARIABLES ]====##
##====[ DATA TYPES ]====##
#===[ ENUMS ]===#
#===[ TYPEDEFS ]===#
```

### Function Description

All functions in the header files MUST have a description like this.
It serves not only as a reference should you look through the includes,
it's also very helpful for IDEs like VSCode to display on hover.

```c
/*
 * []====[ DESCRIPTION ]====[]
 * 
 * This function does BLA BLA BLA...
 *
 * []====[ ARGUMENTS ]====[]
 * 
 * [] TestPointer (void*)
 * Address to the wanted structure. Modify accordingly only when updating the 
 * required number count.
 *
 * [] NewValue (int)
 * This is the new value we want to edit
 *
 * []====[ RETURNS ]====[]
 *
 * [] TESTPROJECT_OK (0)
 * Success
 *
 * [] TESTPROJECT_RETURNS (<> 0)
 * Error (Return Enumeration)
 */
```

```c
/*
 * []====[ DESCRIPTION ]====[]
 * 
 * This function returns a number
 *
 * []====[ ARGUMENTS ]====[]
 * 
 * None
 *
 * []====[ RETURNS ]====[]
 * 
 * [] <0-10>
 * Function was successfull!
 *
 * [] <10-20)
 * Function experienced an internal error.
 *
 * [] 20
 * This is a random number I decided is important.
 */
```


```c
/*
 * []====[ DESCRIPTION ]====[]
 * 
 * This function is a void function with no arguments
 *
 * []====[ ARGUMENTS ]====[]
 * 
 * None
 *
 * []====[ RETURNS ]====[]
 * 
 * None
 */
```

### Inside functions

Generally, code comments are not needed when the code is descriptive itself.
Please use them only in header files or in unclear code parts. If in code, use
them ONLY to describe WHY it's implemented that way, not HOW. That is what the
code is for.

Using the C standard commenting

```c
/* This is a single line comment. Mind your grammar, please! */
```

```c
/*
 * This is a multi line comment.
 * It has no purpose, just shows what you're up to :D
 */
```

# End

These are the current rules. Each project produced will be
carefully reviewed if the code standard is upholded as expected.