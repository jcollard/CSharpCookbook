# C# Cookbook

This repository is meant to be used as a reference during a programming session.
It contains "recipes" for the syntax for performing various tasks in C# as well
as common error messages. 

This Cookbook is a work in progress! Feel free to make suggestions, open Issues,
and create Pull Requests.

- [C# Cookbook](#c-cookbook)
  - [Common Errors](#common-errors)
  - [Local Variables](#local-variables)
  - [If Statements](#if-statements)
  - [Basic Loops](#basic-loops)
  - [For Each Loops](#for-each-loops)
  - [Static Methods](#static-methods)

## [Common Errors](CommonErrors.md)

This is a collection of all the errors that appear in the Cookbook. If you have
an error message, you can look it up by it's error number here and find links to
relevant sections within the Cookbook.

## [Local Variables](LocalVariables.md)

A variable allows a programmer to manage the complexity of a program by naming a
location in memory.

In C#, there are two types of variables: local variables and member variables.
This section discusses local variables.

### Recipes <!-- omit in toc --> 

```csharp
<variable-type> <variable-name>; // Declaring a variable
<variable-name> = <expression>; // Assigning a variable
<variable-type> <variable-name> = <expression>; // Initializing a variable
```

## [If Statements](IfStatements.md)

An if statement is a programming construct that we use to create selections
within a program. Closely coupled with the `if` statement is the `else`
statement which can be used to create a "this" or "that" selection.

### Recipes <!-- omit in toc --> 

```csharp
if (<boolean-expression-0>)
{
    // Body to execute if boolean-expression-0 is true
} 
else if (<boolean-expression-1>)
{
    // Body to execute if boolean-expression-0 is false and boolean-expression-1 is true.
}
else if (<boolean-expression-2>)
{
    // Body to execute if boolean-expression-0 and boolean-expression1 are false and boolean-expression-2 is true.
} 
//... (any number of else if statements to follow)
else // The final else statement is optional
{
    // Body to execute if all boolean-expressions are false.
}
// All branches continue executing at the end of the decision tree.
```

## [Basic Loops](BasicLoops.md) 

There are three types of basic loops in C#: `while`, `for`, and `do`...`while`
loops.

### Recipes <!-- omit in toc --> 

```csharp
while (<boolean-expression>) // While Loop
{
    // Body to execute
}

for (<init-counter>; <boolean-expression>; <increment-counter>) // For loop
{
    // Body to execute
}

do  // Do ... While loop
{
    // Body to be executed
}
while (<boolean-expression>);
```

## [For Each Loops](ForEachLoops.md)

It is so common to iterate over each element in a list or other collection type that C# provides a
special `foreach` loop to accomplish this.

```csharp
foreach (<variable-type> <variable-name> in <iterable>)
{
    // Body to be executed for each element
}
```

## [Static Methods](StaticMethods.md)

Methods provide a way to manage the complexity of a program by breaking it into
logical chunks that can be "called". In this section, we will see the recipe for
`public static` methods which are roughly equivalent to functions in other
programming languages.

```csharp
// Declaring a public static method
public static <return-type> <method-name>(<method-parameters>)
{
    // Body of the method
}

// Calling a public static method
// Within an expression:
<method-name>(<method-arguments>);
```


## [Lists](Lists.md) <!-- omit in toc --> 

TODO:

## [Arrays](Arrays.md) <!-- omit in toc --> 

TODO:


## Custom Data Types <!-- omit in toc --> 

### Classes and Member Variables (Fields) <!-- omit in toc --> 

TODO:

### Constructors <!-- omit in toc --> 

TODO:

### Methods <!-- omit in toc --> 

TODO:

### Properties <!-- omit in toc --> 

TODO:

### Static Class Variables <!-- omit in toc --> 

TODO: