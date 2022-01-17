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
  - [If / Else Statement](#if--else-statement)
  - [If / Else-If Statements](#if--else-if-statements)
    - [Using an Else-if When You Should Use a Second If](#using-an-else-if-when-you-should-use-a-second-if)
    - [Using an If When You Should Use an Else-If](#using-an-if-when-you-should-use-an-else-if)

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

#### Forgetting Curly Brackets <!-- omit in toc -->

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
else 
{
    // Body of code to execute if the <boolean-expression> is false.
}
```

### Examples <!-- omit in toc --> 

```csharp
Console.WriteLine("How old are you?");
int age = int.Parse(Console.ReadLine());
if (age < 13) 
{
    Console.WriteLine("You are not old enough to watch PG-13 movies.");
} 
else
{
    Console.WriteLine("You are old enough to watch PG-13 movies.");
}
DisplayMovies(age);
```

### Common Errors <!-- omit in toc --> 

* An `else` statement must immediately follow the body of an if statement. If
  you do not do this, you will likely receive this error: `error CS8641: 'else'
  cannot start a statement.`
  * This often occurs if the preceding if statements curly brackets are incorrect.

### Common Mistakes <!-- omit in toc -->

Just like with if statements, there are two common mistakes that beginners will
make when writing else statements that will not manifest in an error message but
will result in an incorrect result: Using a semi-colon at the end of an if
statement and not using curly brackets to denote the body of the if statement.

## If / Else-If Statements

It can be useful to be able to several possible outcomes based on more than one
boolean expression. This can be accomplished by following the else keyword with
an if statement. Doing this is called an else-if statement. 

**Note**: This can be done any number of times. However, if you find yourself
writing more than 4 options, consider breaking your logic into multiple methods.

### Recipe  <!-- omit in toc -->

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

### Example  <!-- omit in toc -->

```csharp
Console.WriteLine("How old are you?");
int age = int.Parse(Console.ReadLine());
if (age < 13) 
{
    Console.WriteLine("You are not old enough to watch PG-13 movies.");
} 
else if (age < 18)
{
    // This body will only execute if age >= 13 and age < 18.
    // Because the first if statement was false, we know age must be >= 13.
    Console.WriteLine("You are old enough to watch PG-13 movies.");
    Console.WriteLine("You are not old enough to watch R rated movies.");
} 
else
{
    Console.WriteLine("You are old enough to see any movie!");
}
DisplayMovies(age);
```

### Common Mistakes <!-- omit in toc -->

There are three common mistake that will not manifest that will not result in an error message
but will result in incorrect behavior: Ordering your else if statements
incorrectly, using an `else if` when you should use a second `if`, and using an
`if` when you should use an `else if`.

### Incorrectly Ordering  <!-- omit in toc -->

When you use one or more `else if` statements, they are checked in the order
that they are written. As soon as one of the boolean-expressions is true, that
body will be executed and the remaining `else if` statements will be skipped.
This can result in unexpected behavior. For example:

```csharp
Console.WriteLine("How old are you?");
int age = int.Parse(Console.ReadLine());
if (age >= 13) 
{
    Console.WriteLine("You are old enough to watch PG-13 movies.");
    Console.WriteLine("You are not old enough to watch R rated movies.");
} 
else if (age >= 18) 
{
    // This body will never execute because the boolean-expression age >= 13 will always be true
    // if age > 18 is true. Because we first check if age >= 13, that body will always be executed
    // and this body will always be skipped.
    Console.WriteLine("You are old enough to see any movie!");
} 
else
{
    Console.WriteLine("You are not old enough to watch PG-13 movies.");
    
}
DisplayMovies(age);
```

### Using an Else-if When You Should Use a Second If

Often times, we will want to have two if statements that follow each other.
Beginning programmers will often always add `else` statements if there are two
sequential `if` statements. Be careful not to fall into this trap. For example:

```csharp
Console.WriteLine("How old are you?");
int age = int.Parse(Console.ReadLine());
bool canSeePG13 = false;
bool canSeeR = false;
if (age >= 18) 
{
    Console.WriteLine("You are old enough to see R rated movies.");
    canSeeR = true;
} 
else if (age >= 13) 
{
    // This body will only execute if age is between 13 and 17. However,
    // we want it to execute whenever age is greater than 13
    Console.WriteLine("You are old enough to see PG-13 movies.");
    canSeePG13 = true;
} 
DisplayMovies(canSeePG13, canSeeR);
```

### Using an If When You Should Use an Else-If

Similar to using an `else if` when you should use an `if`, it is not uncommon to
use two sequential `if` statements when you should be using an `else if`
statement. For example:

```csharp
Console.WriteLine("How old are you?");
int age = int.Parse(Console.ReadLine());
if (age < 13) 
{
    Console.WriteLine("You are not old enough to watch PG-13 movies.");
}
if (age < 18)
{
    // This body will execute for any age that is less than 18 which is 
    // not the correct result.
    Console.WriteLine("You are old enough to watch PG-13 movies.");
    Console.WriteLine("You are not old enough to watch R rated movies.");
} 
else
{
    Console.WriteLine("You are old enough to see any movie!");
}
DisplayMovies(age);
```