# Static Methods

Methods provide a way to manage the complexity of a program by breaking it into
logical chunks that can be "called". In this section, we will see the recipe for
`public static` methods which are roughly equivalent to functions in other
programming languages.

One major main benefit of using a method is to provide named "chunks" of code
that can be used and reused. Although naming a method well can be difficult, a
well named method can make the logic of your program easy to read and understand
without requiring the reader to understand the underlying logic.

- [Static Methods](#static-methods)
  - [Declaring a Public Static Method](#declaring-a-public-static-method)
    - [Recipe](#recipe)
    - [Example](#example)
      - [Finding the Minimum of Two Values](#finding-the-minimum-of-two-values)
    - [Common Errors](#common-errors)
  - [Calling a Public Static Method](#calling-a-public-static-method)
    - [Recipe](#recipe-1)
    - [Example](#example-1)
    - [Common Errors](#common-errors-1)
  - [More Examples](#more-examples)
    - [Breaking a Complex Method into Smaller Methods](#breaking-a-complex-method-into-smaller-methods)
      - [A Single Method TODO List Program](#a-single-method-todo-list-program)
      - [A Multi-Method TODO List Program](#a-multi-method-todo-list-program)
      Methods](#breaking-a-complex-method-into-smaller-methods)

## Declaring a Public Static Method

Just like variables, you must first declare a method.

### Recipe

```csharp
public static <return-type> <method-name>(<method-parameters>)
{
    // Body of the method
}
```

### Example

#### Finding the Minimum of Two Values

The following method has two parameters: `a` and `b`. The return type of the
following method is an `int`.

Given two `int` values, return the smaller of the two values.

```csharp
public static int Min(int a, int b)
{
    if (a < b)
    {
        return a;
    }
    else
    {
        return b;
    }
}
```

### Common Errors

    * A static method declaration cannot be followed by a semi-colon. If you do this, you will likely receive the following errors:
      * `error CS1519: Invalid token '{' in class, record, struct, or interface member declaration`
      * `error CS1022: Type or namespace definition, or end-of-file expected`
    * A method must declare a body using an open and close curly bracket. If you're missing one, you will likely receive one or more of the following errors:
      * `error CS1513: } expected`
      * `error CS1002: ; expected`
      * `error CS1022: Type or namespace definition, or end-of-file expected`
    * A method must `return` a value that is of the specified `<return-type>`. If you are returning the wrong type, you will see an error message similar to this:
      * `error CS0029: Cannot implicitly convert type '<value-type>' to '<return-type>'`
    * A method `void` method cannot return a value. If you are trying to return a value in a method that returns void, you will likely see an error message similar to this:
      * `error CS0127: Since 'ClassName.MethodName()' returns void, a return keyword must not be followed by an object expression`
    * A method that declares a return type must return a value. If it is possible for the method to reach the end of the body without encountering a return statement, you will likely see an error message similar to this:
      * `error CS0161: 'ClassName.MethodName()': not all code paths return a value`
    * A method's name must be unique among all methods and variables declared within a class. A common error is to write a method and variable with the same name. If you do this, you will likely receive an error message similar to this: 
      * `error CS0102: The type 'ClassName' already contains a definition for 'Variable/MethodName'`

## Calling a Public Static Method

After a method has been declared, you can use it. When we write code that
invokes a method, we refer to this as "calling" a method. To do this, you write
the name of the method followed by a list of arguments that match the parameters
of the method.

When the code is executing, when a method call is encountered, the current code
"pauses" and the program executes at the beginning of the called methods
declaration with the specified arguments substituted as the parameters of that
method.

When the body of the called method reaches a `return` statement, the program
will exit the method and "return" to the location where the method was called.
The value specified by the `return` is substituted in place of the method call
and the program continues to execute.

### Recipe

```csharp
// Within an expression:
<method-name>(<method-arguments>);
```

### Example

The following uses the `Min` method declared above to ensure that a player's
health does not go above the maximum allowed value.

```csharp
int health, maxHealth;
// Some other code here
// The player may or may not have taken damage.
// The player discovers a healing potion and drinks it
int healAmount = 10;
health += 10; // Increase health by 10
health = Min(maxHealth, health); // Ensures the players health does not go above maxHealth
// The program continues to execute
```

### Common Errors

    * A method can only be called within a context for which the return type is valid. If you call a method in a position with an invalid type, you will likely see an error message similar to this:
      * `error CS0029: Cannot implicitly convert type '<method-return-type>' to '<expected-type>'`
    * A method must be called with arguments that match the parameters of the method. If you call a method with the incorrect arguments, you will likely see one or more of the following error messages:
      * `error CS7036: There is no argument given that corresponds to the required formal parameter '<param-name>' of 'ClassName.MethodName(<method-parameter-types>)'`
      * `error CS1503: Argument <num>: cannot convert from '<specified-type>' to '<required-type>'`
      * `error CS1501: No overload for method 'MethodName' takes <num> arguments`
    * Calling a `non-static` method will result in the following error message. This usually means you forgot to put the keyword `static` on the method.
      * `error CS0120: An object reference is required for the non-static field, method, or property 'ClassName.MethodName(<method-arameter-types>)'`

## More Examples

### Breaking a Complex Method into Smaller Methods

As you write a program, you will often find your methods growing in size and
complexity. A good rule to follow is to keep methods short and concise. If a
method does not fit on a single screen (10 - 20 lines) consider breaking it into
smaller methods.

#### A Single Method TODO List Program

The following shows how you might write a todo list manager using one long
method. Notice how long the method is and how complex the code becomes as we add
more options.

```csharp
List<string> todoList = LoadList();

Console.WriteLine("Welcome to the TODO List!");

while (true)
{
    Console.WriteLine("Select from one of the following options: ");
    Console.WriteLine("1. Display TODO List");
    Console.WriteLine("2. Add Item to TODO List");
    Console.WriteLine("3. Remove Item from TODO List");
    Console.WriteLine("4. Save List");
    Console.WriteLine("5. Exit");

    int option = int.Parse(Console.ReadLine());

    if (option == 1)
    {
        int ix = 1;
        foreach (string item in todoList)
        {
            Console.WriteLine($"{ix}. {item}");
        }
    }
    else if (option == 2)
    {
        Console.Write("Enter an item to add: ");
        string newItem = Console.ReadLine();
        todoList.Add(newItem);
    }
    else if (option == 3)
    {
        if (todoList.Count == 0)
        {
            Console.WriteLine("The list is already empty.");
        }
        else
        {
            Console.WriteLine("Which item would you like to remove? Enter a number between 1 and ");
            // TODO: This is getting pretty long. How do I test this?
        }
    }
    else if (option == 4)
    {
        // TODO: WOW, this is getting complex
    }
    else if (option == 5)
    {
        // TODO: Yikes... I already have more than 50 lines of code!
    }
    else
    {
        Console.WriteLine("That is not a valid option.");
    }
}
```

#### A Multi-Method TODO List Program

The following program creates a TODO List program utilizing several methods to
make the program easier to understand at a glance. Additionally, it makes it
much easier to work on and debug each of the pieces of functionality in isolation.

```csharp
List<string> todoList = LoadList();

Console.WriteLine("Welcome to the TODO List!");

while (true)
{
    DisplayOptions();

    int option = int.Parse(Console.ReadLine());

    if (option == 1)
    {
        DisplayList(todoList);
    }
    else if (option == 2)
    {
        AddItem(todoList);
    }
    else if (option == 3)
    {
        RemoveItem(todoList);
    }
    else if (option == 4)
    {
        SaveList(todoList);
    }
    else if (option == 5)
    {
        Console.WriteLine("Have a great day!");
        break;
    }
    else
    {
        Console.WriteLine("That is not a valid option.");
    }
}
```