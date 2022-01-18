# Basic Loops

There are three types of basic loops in C#: `while`, `for`, and `do`...`while`
loops.

## While Loop

Similar to an if statement, a while loop first checks a boolean-expression, then
if that boolean-expression is true, executes the body of the while loop. If the
boolean-expression is false, the body of the while loop is skipped and the
program continues.

However, unlike an if statement, when the body of a while loop has finished
executing the code returns to the top of the while loop and the condition is
checked again. This process continues until the boolean-expression evaluates to
false OR the body of the while loop encounters a `break` statement.

### Recipe

```csharp
while (<boolean-expression>)
{
    // Body to execute
}
```

### Examples

#### Validating User Input

```csharp
Console.Write("Enter a positive integer: ");
int value = int.Parse(Console.ReadLine());
while (value <= 0)
{
    // This body is skipped if the value entered is positive
    // Otherwise, we prompt the user to enter another value.
    Console.WriteLine("The value must be positive.");
    Console.Write("Enter a positive integer: ");
    value = int.Parse(Console.ReadLine());
}
Console.WriteLine($"{value} is a positive integer.");
```

#### Using a Break to Exit a Loop

```csharp
int value = 0;
while (true) // The body of this while loop will always execute
{
    Console.Write("Enter a positive integer: ");
    value = int.Parse(Console.ReadLine());
    if (value > 0)
    {
        // If the value is positive, we "break" and exit the body
        // of the loop, skipping anything that comes after the break
        // statement
        break;
    }
    
    Console.WriteLine("The value must be positive.");
}
Console.WriteLine($"{value} is a positive integer.");
```

#### Printing Out Integers Between Two Values

```csharp
Console.Write("Enter the lower bound: ");
int low = int.Parse(Console.ReadLine());
Console.Write("Enter the upper bound: ");
int high = int.Parse(Console.ReadLine());
int value = low;
while (value <= high)
{
    // The body of this loop will execute as long
    // as value is less than high.
    Console.WriteLine(value);
    value++;
}
```

### Common Errors

* The `<boolean-expression>` must in fact result in a `boolean`. If this is not
  the case, you will receive an error similar to this: `error CS0029: Cannot
  implicitly convert type '<data-type>' to 'bool'`

### Common Mistakes

There are three common mistakes that occur when writing basic loops that do not
manifest in an error message but will result in behavior that is incorrect:

* Adding a semi-colon at the end of the loop
* Forgetting to use curly brackets for the body of the loop
* Creating an infinite loop

#### Adding a semi-colon at the end of the loop

When you're learning to program in C#, you learn that "every line ends with a
semi-colon". If you add a semi-colon to the end of a loop, the body of the loop
is empty. This is almost never the desired result. For example:

```csharp
while (value <= high); // Oops, we have a semi-colon here
{
    // This code is not attached to the preceding while loop.
    // If `value <= high` is true, this code will never be executed
    // If `value <= high` is false, this code will be executed exactly once.
    Console.WriteLine(value);
    value++;
}
```

#### Forgetting to use curly brackets for the body of the loop

The body of a while loop may be a single statement without curly brackets. This
can lead to very confusing run time bugs which often result in infinite loops.
For example:

```csharp
while (value <= high)
    Console.WriteLine(value);
    value++; // This line is not part of the preceding while loop.
```

In the above example, we have potential for an infinite loop because value is
never updated during the body of the loop. Although the line `value++` is
indented, it is not part of the body. For this reason, it is considered poor
practice to exclude curly brackets from a loop.

#### Writing Infinite Loops

It is very easy to write a loop that never exits. Even the most experienced
programmers will unintentionally write an infinite loop. In the two examples
above, we demonstrated two ways in which infinite loops can occur. However,
there are countless ways to unintentionally write an infinite loop. When this
occurs, you can press `CTRL+C` in the terminal to interrupt the program and ask
it to exit. Sometimes, you may have to press this multiple times. And in rare
cases, this will not work.

## For Loop

It is very common in programming to write a loop which iterates through a
sequence of numbers. The [Printing Out Integers Between Two
Values](#printing-out-integers-between-two-values) in the while loop section
above demonstrates how to do this with a while loop. However, this is so common
that there is special syntax for doing this called a `for` loop.

### Recipe

```csharp
for (<initialize-a-counter-variable>; <boolean-expression>; <increment-the-counter-variable>)
{
    // Body to execute
}
```

### Examples

```csharp
// Write the numbers 0 to 9 to the console.
for (int ix = 0; ix < 10; ix++)
{
    Console.WriteLine(ix);
}
```

```csharp
string toCapitalize = Console.ReadLine();
// Writes each letter in a string on a separate line
for (int j = 0; j < toCapitalize.Length; j++)
{
    char ch = toCapitalize[j];
    Console.WriteLine(ch);
}
```

```csharp
string toCapitalize = Console.ReadLine();
// Writes every other letter in a string on a separate line
for (int j = 0; j < toCapitalize.Length; j += 2)
{
    char ch = toCapitalize[j];
    Console.WriteLine(ch);
}
```

### Common Errors with For Loops

For loops have the same common errors as [While Loops](#common-errors).

In addition to these common errors, there is another common error that beginning
programmers often encounter:

* Trying to use the counter variable outside of the for loop

#### Trying to use the counter variable outside of the for loop

When we write for loops, we typically declare and initialize a counter variable
as part of the for loop. When we do this, that variable is only in scope during
the body of the for loop. For example:

```csharp
for (int i = 0; i < 10; i++) // i is declared here
{
    Console.WriteLine(i);
}
Console.WriteLine(i); // The variable i is not in scope here
```

When this happens, you will usually receive the following error message: `error
CS0103: The name '<variable-name>' does not exist in the current context`

### Bad Habits / Weird Behavior

It turns out that each of the components of a for loop are optional and
variadic. This means that you do not need to specify a counter variable,
boolean-expression, nor do you need to increment the counter variable. For
example, this is valid code:

```csharp
for(;;);
```

The above example is the same as writing `while (true);`. 

There are certain situations where it makes sense to omit one or more of the
components, however, by doing this you are writing code in an unconventional way
which results in extra effort being placed on a reader. When you do this, you
should make sure you have a good reason and be sure that you leave a comment
explaining why you chose to write it that way.

## Do ... While Loops

Sometimes it is useful to guarantee an action is performed at least once before
checking to see if it should be looped. When this is the case, a `do` ...
`while` loop can be used.

### Recipe

```csharp
do 
{
    // Body to be executed
}
while (<boolean-expression>);
```

### Examples

```csharp
int value;
do
{
    Console.Write("Enter a positive integer: ");
    value = int.Parse(Console.ReadLine());
    if (value <= 0)
    {
        Console.WriteLine($"{value} is not positive.");
    }
} while (value <= 0);

Console.WriteLine($"{value} is a positive integer.");
```

### Common Errors and Mistakes

Do while loops are prone to the same common errors and mistakes as [While Loops](#common-errors)