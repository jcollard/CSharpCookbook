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