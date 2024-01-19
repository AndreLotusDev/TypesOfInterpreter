# Interpreter Pattern in C#

## Overview

The Interpreter design pattern is used to define a grammatical representation for a language and provides an interpreter to deal with this grammar. The primary objective of this pattern is to define how to evaluate sentences in a language.

This pattern involves implementing an expression interface that tells to interpret a particular context. This pattern is used in SQL parsing, symbol processing engines, etc.

## Why Use the Interpreter Pattern?

- When there is a language to interpret, and you can represent statements in the language as abstract syntax trees.
- When the grammar of the language is relatively simple.
- When efficiency is not a critical concern.

## Example: Simple Mathematical Expressions Interpreter

In this example, we will create a basic interpreter for simple mathematical expressions (addition and subtraction).

### Step 1: Expression Interface

First, define an `Expression` interface with an `Interpret` method.

```csharp
public interface IExpression
{
    int Interpret();
}
```

### Step 2: Terminal Expressions

Create terminal expression classes implementing the above interface.

```csharp
public class NumberExpression : IExpression
{
    private int number;

    public NumberExpression(int number)
    {
        this.number = number;
    }

    public int Interpret()
    {
        return number;
    }
}

public class AddExpression : IExpression
{
    private IExpression firstExpression, secondExpression;

    public AddExpression(IExpression first, IExpression second)
    {
        firstExpression = first;
        secondExpression = second;
    }

    public int Interpret()
    {
        return firstExpression.Interpret() + secondExpression.Interpret();
    }
}

public class SubtractExpression : IExpression
{
    private IExpression firstExpression, secondExpression;

    public SubtractExpression(IExpression first, IExpression second)
    {
        firstExpression = first;
        secondExpression = second;
    }

    public int Interpret()
    {
        return firstExpression.Interpret() - secondExpression.Interpret();
    }
}
```

### Step 3: Using the Interpreter

Now, use these expressions.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        IExpression isTenPlusFive = new AddExpression(new NumberExpression(10), new NumberExpression(5));
        Console.WriteLine($"10 + 5 = {isTenPlusFive.Interpret()}");

        IExpression isTenMinusFive = new SubtractExpression(new NumberExpression(10), new NumberExpression(5));
        Console.WriteLine($"10 - 5 = {isTenMinusFive.Interpret()}");
    }
}
```

This will output:

```
10 + 5 = 15
10 - 5 = 5
```

---

Feel free to modify this README as needed for your specific use case and GitHub repository.
