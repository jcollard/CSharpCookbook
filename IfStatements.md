# C Sharp Cookbook: If Statements

An if statement is a programming construct that we use to create selections
within a program. Closely coupled with the `if` statement is the `else`
statement which can be used to create a "this" or "that" selection.
Additionally, you can string multiple `if-else-if` statements together to create
complex branching selections. However, be careful when doing this as it become
unruly to manage if you have too many conditions. When this happens, you should
consider breaking your decision down into smaller components and using
[Methods](Methods.md) to manage the complexity.

- [C Sharp Cookbook: If Statements](#c-sharp-cookbook-if-statements)
  - [A simple If Statement](#a-simple-if-statement)
      - [Forgetting Curly Brackets](#forgetting-curly-brackets)
  - [If / Else Statement](#if--else-statement)

## A simple If Statement

A simple if statement checks if a boolean expression (condition) is `true`. If
it is `true` it executes its `body` of code. If it is `false`, it skips its
`body`.

### Recipe <!-- omit in toc --> 

```csharp
if (<boolean-expression>)
{
    // Body of code to execute if the <boolean-expression> is true.
}
```

### Examples <!-- omit in toc --> 

```csharp
Console.Write("Enter your name: ");
string name = Console.ReadLine();
if (name == "Joseph") 
{
    // Only runs if the user types in "Joseph"
    Console.WriteLine("Wow! That's my name too!");
}
Console.WriteLine($"Nice to meet you, {name}.");
```

### Common Errors <!-- omit in toc --> 

* The `<boolean-expression>` must in fact result in a `boolean`. If this is not
  the case, you will receive an error similar to this: `error CS0029: Cannot
  implicitly convert type 'string' to 'bool'`
  * Often times this occurs when you are checking for equality and use the
    assignment operator (`=`) rather than the equality operator (`==`)


### Common Mistakes <!-- omit in toc -->

There are two common mistakes when learning to write if statements that will not
manifest in an error message but will result in an incorrect result: Using a
semi-colon at the end of an if statement and not using curly brackets to denote
the body of the if statement.

#### Adding a Semi-colon <!-- omit in toc -->

Adding a semi-colon `;` at the end of the if statement. C# is happy to let you
add a `;` at the end of an if statement. This means the body of that if
statement is empty! For example:

```csharp
if (hasKey); // Ooops, semi-colon
{
    // This body will always execute as it is not actually connected to the preceding if statement
    Console.WriteLine("You open the chest and acquire the sword!");
    hasSword = true;
}
```

#### Forgetting Curly Brackets

Forgetting to add curly brackets `{`, `}` around the body of the if statement.
It turns out you can have a single statement as a body in an if statement. You
must explicitly use curly brackets if you would like to have more than one
statement. It is considered bad practice to use single-statement bodies for if
statements. For example:

```csharp
if (hasKey)
    Console.WriteLine("You open the chest and acquire the sword!"); // This line is the entire body of the if statement.
    hasSword = true; // This code will always execute because it is not part of the if statement
```

**Exceptions to the Rule:**

During error checking, we often check a condition and throw an exception at the
start of a method. It can help with readability to use single-statement bodies
in this case. When you do this, the body of the if statement should **always**
be on the same line as the if statement. For example:

```csharp
public static string CheckGuess(string guess)
{
    if (guess == null) throw new ArgumentNullException("The guess cannot be null.");
    if (guess.Length > 5) throw new ArgumentException("The length of the guess should not exceed 5 characters.");
    // Perform CheckGuess
}
```
## If / Else Statement

Often, we want to make a branching selection if the boolean expression is
`false`. This can be accomplished using an `else` statement.

### Recipe <!-- omit in toc --> 

```csharp
if (<boolean-expression>)
{
    // Body of code to execute if the <boolean-expression> is true.
}
```

### Examples <!-- omit in toc --> 

```csharp
Console.Write("Enter your name: ");
string name = Console.ReadLine();
if (name == "Joseph") 
{
    // Only runs if the user types in "Joseph"
    Console.WriteLine("Wow! That's my name too!");
}
Console.WriteLine($"Nice to meet you, {name}.");
```

### Common Errors <!-- omit in toc --> 

* The `<boolean-expression>` must in fact result in a `boolean`. If this is not
  the case, you will receive an error similar to this: `error CS0029: Cannot
  implicitly convert type 'string' to 'bool'`
  * Often times this occurs when you are checking for equality and use the
    assignment operator (`=`) rather than the equality operator (`==`)