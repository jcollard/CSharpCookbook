# C Sharp Cookbook: Local Variables

A variable allows a programmer to manage the complexity of a program by naming a
location in memory.

In C#, there are two types of variables: local variables and member variables.
This section discusses local variables.

## Declaring a Local Variable

Declaring the variable is the process of creating a location in memory to store
data and giving that location a name. In C#, you must also specify the type of
data that will be stored in that location.

* A local variable is a variable that is declared within the body of a method. 
* A local variable is only accessible within the method it was declared.

### Recipe

```csharp
<variable-type> <variable-name>;
```

### Examples

```csharp
int age; // Declare an integer named age
float weight; // Declare a floating point number named weight
List<int> guesses; // Declare a list of integers named guesses
Random generator; // Declare a "Random" named generator
```

### Common Errors

* A variable must have a unique name for the given scope. If you create a
  variable that has a conflicting name, you will receive an error that looks
  something like: `error CS0128: A local variable or function named
  'VARIABLE_NAME' is already defined in this scope`.

## Assigning a Variable

Assigning a variable is the process of storing

### Recipe

```csharp
<variable-name> = <expression>;
```

### Examples

```csharp
int sum;
sum = 14 + 7; // Evaluate 14 + 7 then assign it to sum

float score;
score = GetScore() + GetExtraCredit(); // Evaluate GetScore() + GetExtraCredit() and assign the result to score

List<int> guesses;
guesses = new List<int>(); // Construct a new list and assign it to guesses

Random generator;
generator = new Random(); // Construct a new random generator and assign it to generator
```

### Common Errors

* The variable must be declared before it can be assigned. If you try to assign
  a variable before declaring it, you will receive an error similar to this:
  `error CS0841: Cannot use local variable '<variable-name>' before it is
  declared`

* The variable being assigned must be in scope. If this isn't the case, you will
  receive an error something like this: `CS0103: The name '<variable-name>' does
  not exist in the current context`. This often is caused by:
  * A typo in the variable name.
  * The variable being declared within the body of an if statement or loop
  * The variable being declared in a different method

* The variable being assigned must have the same data type as the expression
  being evaluated. If the types do not match, you will receive an error that
  looks something like: `error CS0029: Cannot implicitly convert type
  '<expression-type>' to '<variable-type>'`

## Declare and Initialize a Variable

Initializing a variable is occurs the first time you assign a value to a
variable. This is so common that it is possible to both declare and initialize a
variable in a single statement.

### Recipe

```csharp
<variable-type> <variable-name> = <expression>;
```

### Examples

```csharp
int age = 14; // Declare and initialize age to store the value 14
float score = GetScore() + GetExtraCredit(); // Declare and initialize score to store the result of evaluating GetScore() + GetExtraCredit()
List<bool> answers = new List<bool>(); // Declare and initialize answers to be a new list.
```

### Common Errors

See: [Declaring a Local Variable](#declaring-a-local-variable)

## Accessing a Variable

Accessing a variable is the process of retrieving the data stored in the memory
associated with a variable. 

### Recipe

As part of an expression:

```csharp
<variable-name>
```

### Examples
```csharp
Console.Write("Enter an integer: ");
int x = int.Parse(Console.ReadLine());
Console.Write("Enter another integer: ");
int y = int.Parse(Console.ReadLine());
int sum = x + y; // Access the value x and value y, then sum them together.
Console.WriteLine($"The sum of {x} and {y} is {sum}."); // Access the values sotred in x, y, and sum, and interpolate them in a string.
```

```csharp
Console.Write("Enter your name: ");
string name = Console.ReadLine();
Console.WriteLine($"Nice to meet you {name}!"); // Access the value stored in name and interpolate it in a string.
```

### Common Errors

* A variable cannot be used as a statement. If you do this, you will receive an
  error that looks like this: `error CS0201: Only assignment, call, increment,
  decrement, await, and new object expressions can be used as a statement`
    * This is often caused by having a variable on a line by itself.

* The variable must be declared before it can be accessed. If you try to access
  a variable before declaring it, you will receive an error similar to this:
  `error CS0841: Cannot use local variable '<variable-name>' before it is
  declared`

* The variable being accessed must be in scope. If this isn't the case, you will
  receive an error something like this: `CS0103: The name '<variable-name>' does
  not exist in the current context`. This often is caused by:
  * A typo in the variable name.
  * The variable being declared within the body of an if statement or loop
  * The variable being declared in a different method

* The variable being accessed must be initialized. If it has not been assigned a
  value, you will receive an error that looks like this: `error CS0165: Use of
  unassigned local variable '<variable-name>'`.
  * This is often caused by assigning a variable inside of an if statement but
    not assigning it within each of the `else` branches.
  