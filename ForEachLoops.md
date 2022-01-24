# For Each Loops

It is so common to iterate over each element in a list or other collection type that C# provides a
special `foreach` loop to accomplish this.

- [For Each Loops](#for-each-loops)
  - [For Each Loop](#for-each-loop)
    - [Recipe](#recipe)
    - [Examples](#examples)
      - [Find the Highest Score](#find-the-highest-score)
      - [Find the Longest Name](#find-the-longest-name)
    - [Common Errors](#common-errors)
    - [Common Mistakes](#common-mistakes)
      - [Modifying the collection you are iterating over](#modifying-the-collection-you-are-iterating-over)

## For Each Loop

A `foreach` loop iterates over the elements of a list or other collection type.
In almost all instances, it is possible to write a basic loop to accomplish
this. However, a `foreach` loop makes it nearly impossible to write a loop that
doesn't access each element in the collection. Because of this, you should
typically favor using a `foreach` loop possible.

### Recipe

```csharp
foreach (<variable-type> <variable-name> in <iterable>)
{
    // Body to be executed for each element
}
```

### Examples

#### Find the Highest Score

```csharp
List<int> scores = LoadHighScores("scores.txt");
int highScore = int.MinValue;
foreach (int score in scores)
{
    if (score > highScore)
    {
        highScore = score;
    }
}
Console.WriteLine($"The highest score is {highScore}.");
```

#### Find the Longest Name

```csharp
List<string> names = LoadNames("names.txt");
string longestName = string.Empty;
foreach (string name in names)
{
    if (name.Length > longestName.length)
    {
        longestName = name;
    }
}
Console.WriteLine($"The longest name is {longestName}.");
```

### Common Errors

* You can only use a `foreach` loop on data types that are iterable (e.g. List,
  array, string). If you try to use a `foreach` loop to iterate over data that
  is not iterable, you will likely receive an error that looks like this: `error
  CS1579: foreach statement cannot operate on variables of type '<data-type-1>'
  because '<data-type-2>' does not contain a public instance or extension
  definition for 'GetEnumerator'`
  
* The type of the declared variable must match the type of the data being stored
  by the collection. For example, if you try to declare an `string` variable to
  iterate over a `List<int>` you will receive the following error: `error
  CS0030: Cannot convert type 'int' to 'string'`
  
### Common Mistakes

#### Modifying the collection you are iterating over

There are times when you would like to search for and remove elements from a
collection. If you try to use a `foreach` loop to accomplish this, you will not
receive a compilation error. But, you will receive a run time error that says
`Unhandled exception. System.InvalidOperationException: Collection was modified;
enumeration operation may not execute.`.

For example, the loop below is written such that names with more than 4 letters
should be removed. However, this will result in an error:

```csharp
List<string> names = new List<string> { "Rebecca", "John", "Emily" };
foreach (string name in names)
{
    if (name.Length > 4)
    {
        // An error happens here because you are not allowed to 
        // modify the data you are iterating over in a foreach loop
        names.Remove(name); 
    }
}
```

If you need to search for and then remove an element from a collection, you have
a few options. Here are two solutions that are common:

1. Typically the most "efficient" way is to use a basic for loop. However, this can
   be a little tricky to program as you need to make sure you adjust your index
   accordingly as the standard method of incrementing will result in a bug.
2. You can use a `foreach` loop to first find the elements to remove, then remove the
   element after the loop. **Note**: This is not the most efficient solution.
   However, it is very straight forward to write.

```csharp
List<string> names = new List<string> { "Rebecca", "John", "Emily" };
List<string> namesToRemove = new List<string> ();
foreach (string name in names)
{
    if (name.Length > 4)
    {
        // Save the name to be removed later
        namesToRemove.Add(name);
    }
}

// Iterate over all the names to be removed
foreach (string name in namesToRemove)
{
    names.Remove(name);
}
```