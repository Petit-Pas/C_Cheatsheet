# C Cheatsheet: syntax, tools and vocabulary
This document is intended to document the C syntax that you will need to complete your C Pool.
It is written in an anlytic way, it might be confusing for you at first sight but it is intended to allow you to develop an analytic comprehension of the code.
Any word in blue or with this [Format](#Format) (depending if you read this file as a  raw text file or as a markdown file) is documented in more details somewhere else in the document, and can be clicked (in Markdown mode) to get there.
## <a name="CFile"/> C File
A [C file](#CFile) has a name that ends with .c
It contains 2 parts:
* [Includes](#Include)
* [Function definitions](#FunctionDefinition)
A [C File](#CFile) contains code as text that can be compiled using [GCC](#GCC) in order to make an [executable](#Executable).

## <a name="GCC"/> GCC
[GCC](#GCC) stands for Gnu Compiler Collection.
As it names shows, it is a program that is supposed to compile 1 or more [C Files](#CFile) into 1 [executable](#Executable)
You can use i as such:
```
gcc [-o *wanted_name_of_the_executable*] file1.c [... .c]
```
If you don't specify a specific name with the -o option, the default name will be ```a.out```.

## <a name="Include"/> Includes
[Includes](#Include) can be found at the very beginning of a [C File](#CFile).
They serve the purpose of adding a library of [function declarations](#FunctionDeclaration) to the beginning of the file, withouth having to rewrite them all by hand by "including" a [Header File](#HeaderFile) in the [C File](#CFile).
They are written as either:
```C
#include <unistd.h>
```
or
```C
#include "my_header_file.h"
```
The difference between these 2 is: 
* you always use <...> when using a system include (one that you have not written yourself)
* you always use "..." when using a personnal include (one that you have written yourself)

Always use them in that order, systems than personals!

##  <a name="FunctionDeclaration"/> Function Declaration
A [Function Declaration](#FunctionDeclaration) is 1 single line with the [function prototype](#FunctionPrototype) without the body of the [C Function](#CFunction) itself, terminated with a semicolon as such:
```C
function prototype;
```
It serves the purpose of specifying the type of a [C Function](#CFunction) that would not be in the same [C File](#CFile) to [GCC](#GCC) at [compilation time](#CompilationTime), avoiding a [compilation warning](#CompilationWarning) and potential [runtime errors](#RuntimeError). 

[Function Declarations](#FunctionDeclaration) should always be used in [Header Files](#HeaderFile) and included in [C File](#CFile) with [Includes](#Include).

## <a name="FunctionPrototype"/> Function Prototype
A [Function Prototype](#FunctionPrototype) is 1 line of code that documents:
* The [return type](#ReturnType) of a [C Function](#CFunction)
* The name of the [C Function](#CFunction)
* The [Function Parameters](#FunctionParameter) of the [C Function](#CFunction)

And is written as follows:
```C
return_type name(parameters)
```
It can be used either in a [Function Declaration](#FunctionDeclaration) or in a [Function Definition](#FunctionDefinition).

## <a name="FunctionDefinition"/> Function Definition
A [Function Definition](#FunctionDefinition) is a piece of code that first declares a [Function Prototype](#FunctionPrototype), then a [Function Body](#FunctionBody).
It is written as such:
```C
Function_prototype
{
	Function_body
}
``` 
The '\{ \}' serve to isolate the [Function Body](#FunctionBody) from the rest of the [C File](#CFile).
Note that there is a tabulation for format, is it important!

## <a name="FunctionBody"/> Function Body
A [Function Body](#FunctionBody) is always composed of 2 parts:
* The [Variable Declaration](#VariableDeclaration) part in which you declare *all* the variables you are going to need for this [C Function](#CFunction) (it can then be empty if you don't need any, or more than 1 line if you need plenty).
* The [Imperative Part of a C Function](#ImperativePart) in which you can put all the executive code of your [C Function](#CFunction).

It should be written as follows:
```C
Variable Declaration

Imperative Part
```
Note that there is a blank line between the declarative and the imperative part, it is not required for [GCC](#GCC) to compile and for your [C Function](#CFunction) to work but is it required to have a code that's easier to read.

## <a name="VariableDeclaration"/> Variable Declaration
A Variable declaration is 1 line of code in which you create a variable.
Before that line the variable *does not exist* and after that line for the rest of the function, the variable is known and no other variable can be named the same.

It is composed of: 
* The [Type](#Type) of the variable.
* The name of the variable.
* A default value to the variable [optional].
* A semicolon (that ends most of the lines in a [Function Body](#FunctionBody).
It is made as such:
```C
type var_name[ = value];
```

## <a name="Type"/> Type
A [Type](#Type) is a very important concept in programmation.
When you store data in a program, it needs to be stored in a [variable](#Variable), but any data cannot be stored in any kind of "box". 
You can see [Types](#Type) as different shapes of "boxes" used to store different kind of [Variables](#Variable).
Here is a list of the most common types in C:
* int: a signed integer value encoded on 4 bytes, with value ranged between -2,147,483,648 and 2,147,483,647.
* char: a signed integer value encoded on 1 byte, with values ranged between -128 and 127. This type is often used to describe a printable character between 0 and 127 in the Ascii table. (if you are not used to the Ascii table, type ```man ascii``` in your terminal.
* char *: a special type encoded on 8 bytes that is often used to represent memory adress. This type is much more complicated than the other ones, specific days in the C Pool will be all about them and we will discuss them with you instead of with a cheatsheet. 

Please note that this is not an all-inclusive list,  they are other standard types that you might be interested to discover and these are only the standard ones! Custom types can also be created with [Structures](#Structure).

## <a name="Structure"/> Structure
 A [Structure](#Structure) is a way to create new custom (bigger) [types](#Type) by cumulating more than 1 standard [type](#Structure) or other [structures](#Structure) into 1 single new [type](#Type).
 It iscomposed of:
 * A first line declaring a new type named "struct name_s".
 * Curly brackets to isolate the structure from the rest of the file.
 * [Variable Declarations](#VariableDeclaration).
 * A shorter name that, with the starting "typedef" keyword, allows to use the new type as "name_t" and not "struct name_s" (just more practical).
```C
typedef struct name_s
{
	variable declaration;
	...
	variable declaration;	
} name_t;
```

A [Structure](#Structure) declaration should always be in a [Header File](#HeaderFile).

When Using a structure instead of a standard type, you will want to be able to access its inner members, and there is a syntax allowing that.
If a variable named "b" is inside a structure named "a", you can access it by writing ```a.b```. The point is the tool that allows to "enter" the structure to access its inner member.
So if "b" contained "c", you can also do ```a.b.c``` to access the c member inside of b, inside of a, and etc.

## <a name="Executable"/> Executable
An [executable](#Executable) file is a file generated by [GCC](#GCC) after the compilation. It is a binary file, and then absolutely non readable by a human (which you happen to be, unless Skynet has won). 
Although it cannot be read, it can of course be executed (which could have been guessed from the name though). In order to do that, use it as such:
```
./executable_file ["program argument 1" "program parameter 2" ...]
```
As you can see in the example, you can send [Program Arguments](#ProgramArgument) to your executable.

## <a name="HeaderFile"/> Header File
A [Header File](#HeaderFile) is a specific type of file often used in C development.
Its name is always to end with .h to differentiate it from a [C File](#CFile).

A [Header File](#HeaderFile) is used to contain several things:
* [Function Declarations](#FunctionDeclaration)
* [Structure Declarations](#Structure)
* Enumerations (will not be covered in this guide)
* [Macros](#Macros)
* Global Variables (will not be covered in this guide)

A [Header File](#HeaderFile) is always to be included in [C Files](#CFile) that require its content **only** using the technique described in [Include](#Include).

## <a name="CFunction"/> C Function
There is 2 main kind of [Functions](#CFunction).
* One can be compared to a mathematical function. It takes arguments as parameters, and returns a specific value. No matter the amount of times you call that function with the same arguments, the result will always be the same. For instance, an "addition" function that takes 2 and 3 as parameter will always return 5.
* One has what we call a "side effect", meaning that it does not especially create a new value (though it could) but that it affects somehow the program itself. It could then have different comportment when called twice in a row. For instance, a function in a video game that sets the video mode to full screen will work the first time it is called, but it will not do anything the second time it is called in a row. 

Whatever the kind of function is the one you are currently writing, its syntax will always be the same as seen in [Function Definition](#FunctionDefinition).

In order to use (we say "call") a function, you need to write its name, followed by its potential parameters in parenthesis, and finally a semicolon.
example:
```C
random_function(param1, param2);
```

## <a name="CompilationTime"/> Compilation Time
When we refer to something as [Compilation Time](#CompilationTime), we refer to what happens when [GCC](#GCC) is transforming all your [C Files](#CFile) into an [executable](#Executable).
It is opposed to [Runtime](#Runtime).
It's at [Compilation Time](#CompilationTime) that you can get [Compilation Errors](#CompilationError) or [Compilation Warnings](#CompilationWarning).

## <a name="CompilationError"/> Compilation Error
A [Compilation Error](#CompilationError) is an error that can occur during [Compilation Time](#CompilationTime). It will effectively prevent [GCC](#GCC) from completing the compilation, hence not creating your [Executable](#Executable).
Here is a **not limited** list of the kind of [Compilation Errors](#CompilationError) that you are gonna face.
* One of the file you asked [GCC](#GCC) to compile could not be found.
* The [Function Prototype](#FunctionPrototype) of a [Function Declaration](#FunctionDeclaration) and its [Function Definition](#FunctionDefinition) do not correspond.
* You are using an identifier that has never been declared.
* You are using the same identifier to identify 2 different things.

## <a name="CompilationWarning"/> Compilation Warning
A [Compilation Warning](#CompilationWarning) is an "error" that can occur during [Compilation Time](#CompilationTime). It will not prevent [GCC](#GCC) from completing the compilation but it could be the sign of potential cause for further [Runtime Errors](#RuntimeError).

## <a name="Runtime"/> Runtime
When we refer to something as [Runtime](#Runtime), we refer to what happen when you launch the  [executable](#Executable) that has been compiled before by [GCC](#GCC).
It is opposed to [Compilation Time](#CompilationTime).
It's at [Runtime](#Runtime) that you can get [RuntimeErrors](#RuntimeError).

## <a name="RuntimeError"/> Runtime Errors
A [Runtime Error](#RuntimeError) is an error that occur during [Runtime](#Runtime).
Usually these errors lead to a crach of your Program.
Here is a **not limited** list of the most common [Runtime Errors](#RuntimeError) that you are gonna face.
* Segmentation Fault: you basically did something wrong with memory management.
* Stack Overflow: you called a function that calls itself indefinitely, yes, a function that calls a function that calls a function, ... Inception-like.
* Killed: you tried using resource that you were not allowed to, could be due to a bad memory management too.
* Invalid Free: you tried to free resources that had already been free'd.

## <a name="ReturnType"/> Return Type
A [C Function](#CFunction) can sometimes return a value, and this value, just like a [variable](#Variable) must have a [Type](#Type).
So in the [Prototype](#FunctionPrototype) of the function, as the first keyword, you write the [Type](#type) of the variable that the function will return.
A function can only return 1 kind of variable, and it is determined by the [Return type](#ReturnType) of the function.
In the case that the function does not return value, the keyword to be used is just ```void```.

## <a name="FunctionParameter"/> Function Parameter
A [Function Parameter](#FunctionParameter) is a variable that is sent ot a function at the moment you call it.
They are copied and sent to the function, you don't send the actual variable but just a copy, which means that if you modify it in the body of the function called, they wont be modified in the function that was calling. 
Example:
```C
int a = 2;
int b = 3;

func(a, b);
```
By doing this, you send a copy of a and b to the "func" function. If that function modifes the copies it recieved, neither a nor b will be modified.
To declare them in the [Function Prototype](#FunctionPrototype), you need to give their [Type](#Type) and their name (which can differ from the name of the variable sent when calling).
After that they exist and can be used just like variables that would have been declared in the [Variable Declaration](#VariableDeclaration) part of the [Function body](#FunctionBody). 
Example:
```C
type name(type variable_name, type2 variable_name2)
```

## <a name="ImperativePart"/> Imperative Part of a Function
The imperative part of a function is the place in which the [Function](#CFunction) acutally **does** something.
The part after all the variable declaration, when everything is ready to start doing some logical work.

Here is a list of the things you can do in this part:
* [Assign a variable](#VariableAssignation)
* [Calling a Function](#CFunction)
* [Comparing variables](#Comparisons)
* [Return a result](#ReturnValue)

Appart from the "Comparing Variables" part that has a specific syntax, all these lines always need to end with a semicolon.
## <a name="Variable"/> Variable
A [Variable](#Variable) is a kind of "Box" in which you can store values. Its nothing more than that.
You usually don't want to handle lots of things as plain numbers or strings, so you just store them in variables with handy names in order to move them around easier.
See [Variable Declaration](#VariableDeclaration) to see how to declare one, and [Imperative Part of a Function](#ImperativePart) to see how you can use them. 

## <a name="VariableAssignation"/> Variable Assignation
There is not much things you can do with a variable, you can either read it or write in it.
In order to set a value to a variable, you just write the name of the variable followed by an '=' and then a new value. Plus the eternal semicolon, of course.
Example:
```C
amount = 2;
```

You can also use another variable to set one.
Example:
```C
amount = new_amount;
```
In this case, amount is now equal to the current value of new_amount, but new_amount hasn't changed, its always the value on the right hand side that is assigned to the the variable on the left hand side.
Hence, the following line cannot work:
```C
6 = amount;
```
as you can't put a value in 6, 6 not being a variable but a number.

You can also do some mathematical operations when assigning a variable.
Example:
```C
amount = old_amount + 1;
new_amount = old_amount + amount;
```

Finally you can use the [Return Value](#ReturnValue) of a function and assign it to a variable as such:
```C
amount = get_amount();
```

## <a name="ReturnValue"/> Return Value
A [Function](#CFunction) that has a [Return value](#ReturnValue) **always** return a value, wether it is the  result of a calculation or simply an indicator of how did the function go.

In order to return a value you just need to use the "return" keyword with either a value or a [Variable](#Variable).
Example:
```C
return variable;
return 0;
``` 
When you return a value in a function, the function immediately stops and the program takes the execution back where the function was called.

In order to use the return value of a [C Function](#CFunction), you need to call it and use it exactly how you would use a [Variable](#Variable).
Example:
```C
int var = addition(2, 3);
```
By doing this, you store the returned value of the call to the addition function into the "var" variable.
Beware, to avoid errors, you need to use the same [Type](#Type) to store the return value than the [Return Type](#ReturnType) of the [function](#CFunction)  called.

## <a name="Comparisons"> Comparisons
One of the thing we do the most in programming, is doing comparisons. A program will always be able to do plenty of different things, but will have to decide what to do based on certain criterias. 
A [Comparison](#Comparisons) is always used to make a certain piece of code conditional, depending on the result of the condition, the program will always either execute the said piece of code or not.

For that we use 2 things, logical operators, and keywords.
The logical operators will be used to make the comparison itself, while the keywords will enable us to control the flow of our program depending on the comparison we just made.

Here is a list of the different operators in C:
* or : ```||```
* and: ```&&```
* equal: ```==```
* not equal: ```!=```
* greater than: ```>```  
* greater than or equal: ```>=```  
* lesser than: ```<```  
* lesser than or equal: ```<=``` 

They can be used in comparisons between 2 variables or between a variable and a number.
```C
keyword (a == b)
keyword (a <= 2)
keyword (a != b || a == 2)
```

Here is a list of different keywords you can do in C, and how to use them.
### if
If allows to make a simple condition on a block of code:
```C
if (condition)
{
	things to do;
}
```
Here, the "things to do" will only be done if the "condition" is true, otherwise it will just be ignored.
Note the usage of brackets and tabs, just like when doing a [Function Definition](#FunctionDefinition).
### else
The else keyword can only be used in combination with the if keyword, it protects a block of code that will be executed only if the condition **is not** true. 
```C
if (condition)
{
	things to do;
} else 
{
	other things to do;
}
```
Only one of those 2 blocks will be executed, "things to do" if the condition is true, "other things to do" otherwise.
You can even branch more than 1 if else at the same time.
```C
if (condition1)
{
	things to do;
}
else if (condition2)
{
	other things to do;
}
else 
{
	different things to do;
}
```
In this case, either the "condition1" is true, the program execute the "things to do" and skips the rest, or "condition1" is false and the program will then check "condition2" repeating the same scheme.

### while
The while keyword is used in order to make loops. The attached block of code will be repeated "as long as" the condition is true.
```C
while (condition)
{
	some work;
}
```
The program will check the condition, if the condition is true, the program will execute the attached block of code than check the condition again, etc... until the condition becomes false.

## <a name="ProgramArgument"/> Program Argument
You can send arguments not only to a [Function](#CFunction) but only to an [executable](#Executable) by adding them at the executing command, separated by spaces:
```
./executable argument1 argument2
```
They can be used in the Main function but that will be covered at some point in the Pool.

## <a name="Macros"/> Macros
[Macros](#Macros) are kind of super short functions in one line for which we don't want to write an actual function.
They are usually used to hide something that takes 1 or more argument, does 1 simple if/else (see [Comparisons](#Comparisons)) and return a simple value.
They are to be defined in a [Header File](#HeaderFile) as such:
```C
#define NAME(param1, param2) ((condition) ? result_if_true : result_if_false)
```
and can be used an a [CFile](#CFile) as such:
```C
NAME(1, 2);
```
it will have a [Return Value](#ReturnValue) just like a normal function.

