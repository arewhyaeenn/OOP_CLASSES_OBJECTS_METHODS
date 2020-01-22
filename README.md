# COMP 150 Lab 3 - Flow of Control

In this lab:

* How to `import` classes.
* How to use the `Scanner` class to get user input.
* What is a class?
* Objects vs primitives. Reference vs value.
* What methods are, and how to write `static` methods.
* What boolean expressions are, and how to write and evaluate them.
* How to use `if`/`else` statements to decide what actions to take.
* How to use `for`, `while`, and `do while` loops to repeat actions.
* How to use the `break` and `continue` keywords.
* How to use a `switch`.
* How to visualize the flow of control in a program.
* What an array is.
* Strings and arrays.
* How to index an array.
* How to traverse an array.
* Arrays and nestability.

## Importing

**packages** contain organized sets of classes, generally with some unifying purpose. They can also contain smaller packages, known as **sub packages**.

If you check the [Java 8 API](https://docs.oracle.com/javase/8/docs/api/), you can see a list of packages available in the Java 8 Standard Edition platform (these are the packages that are available in your Java Development Kit you installed in week 1).

Classes can be imported using `import` statements, which are generally at the top of the program outside of the class definition. `import` statments consist of the `import` keywords followed by the name of the package being imported, a `.` (accessor operator) to access a member of that package, and then the class name (the package member being accessed). They look like this: `import <package>.<class>;`.

An example can be found in the previous lab, where we imported the `Scanner` class from the `util` subpackage of the `java` package with the statement:

```java
import java.util.Scanner;
```

Note that the class name `Scanner` is in `PascalCase`. This is a standard among almost all Java programmers.

## The `Scanner` Class

We used the `Scanner` class briefly in the previous lab, so you might be familiar with it already. It can be used to parse primitive data from an input source. The input source might be a text file, a `String`, or an `InputStream`. For now, we don't need to know what an `InputStream` is, we just need to now that there is one called `System.in` which corresponds to input typed in the console, so if we use that `InputStream` as a source, the `Scanner` can be used to get input from the console and parse it.

In order to use a `Scanner`, we must **construct** it. The `Scanner` class is a blueprint, which can be used to construct `Scanner` objects associated with specific input sources. The constructed `Scanner` object is said to be an **instance** of the `Scanner` class.

Object construction is done with a method called a **constructor**, which provides instructions detailing how to set up the object. A class's constructor is run with the `new` keyword, followed by the name of the class, and the parenthesis containing any **arguments** (i.e. inputs) for the constructor. The resulting object is usually then stored in a variable, so the constructor call is usually the right side of an assignment statement. For example, the statement below constructs a new `Scanner` object called `keyboard`:

```java
Scanner keyboard = new Scanner( System.in );
```

In the example above, `System.in` is specified as an argument for the `Scanner` constructor, so the `Scanner` named `keyboard` will receive its input from the console.

Once the `Scanner` has been constructed, it can be used to read and parse inputs using the methods.

Consider the following program:

```java
import java.util.Scanner;

public class FillInTheCode
{
    public static void main(String[] args)
    {
        Scanner scan = new Scanner ( System.in );
        
        System.out.println("SURVEY TIME");
        
        System.out.println("\nHow many toes do you have?");
        int nToes = scan.nextInt();

        scan.nextLine();
        System.out.println("\nWhy did the chicken cross the road?");
        String whyThough = scan.nextLine();
        
        System.out.println("\ntrue or false : Radishes are the coolest vegetable.");
        boolean radishSoCool = scan.nextBoolean();

        System.out.println("\nSURVEY SUMMARY:");
        
        System.out.println("\nYou have " + nToes + " toes...?");

        System.out.println("\nThe chicken crossed the road because \"" + whyThough + "\"");

        System.out.println("\nRadishes are the coolest vegetable : " + radishSoCool);
    }
}
```

In the program above, a `Scanner` with identifier `scan` is created, and is then used to read user's responses from the console after questions are printed to the console. Note that there is an extra call to the `nextLine` method before the second question. This is due to an oddity of how the `Scanner` interacts with its input source.

The `Scanner` essentially reads characters from the input source one at a time and parses them into the desired data types (if possible). It has methods to read all of the primitive data types, named accordingly; `nextInt` reads an `int`, `nextDouble` reads a `double` and so on... It also has methods to read different types of `String` data from its input stream; among these are `next`, which reads the next "word" (i.e. all characters up to the next white space), and `nextLine`, which reads all characters up through the next newline character (`'\n'`).

When a `Scanner` calls a method to read a primitive or the `next` method to read a word, it leaves the newline on the of the input. This will cause the next `newLine` call to be blank; it reads until the first newline, and the first character in the stream is a newline. So, that extra call to the `nextLine` method before the second question in the program above is to read this residual newline character out of the input stream, which in turn allows the following `nextLine` call to get the user's input instead of a blank line.

Here is a sample run for the program:

```
SURVEY TIME

How many toes do you have?
7

Why did the chicken cross the road?
Get off my lawn.

true or false : Radishes are the coolest vegetable.
true

SURVEY SUMMARY:

You have 7 toes...?

The chicken crossed the road because "Get off my lawn."

Radishes are the coolest vegetable : true

Process finished with exit code 0
```

## What is a Class?

The truth is, this question is a little too broad for the scope of this discussion. We are not going to all-inclusively define classes. We are going to instead talk about two common types of classes, and the significance of classes in the Object-Oriented paradigm.



## Methods

## Boolean Expressions

## `if`/`else`

## `while`

## `do while`

## `for`

## `switch`
