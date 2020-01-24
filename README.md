# COMP 150 Lab 3 - Flow of Control

# lab exercise make times table setup

In this lab:

* How to `import` classes.
* How to use the `Scanner` class to get user input.
* What is a class?
* Wrapper classes. TODO
* What methods are, and how to write `static` methods.
* How to use the Debugger in IntelliJ.
* What boolean expressions are, and how to write and evaluate them.
* How to use `if`/`else` statements to decide what actions to take.
* How to use `for`, `while`, and `do while` loops to repeat actions.
* How to use the `break` and `continue` keywords.
* How to use a `switch`.
* How to visualize the flow of control in a program.
* What an array is.
* Strings and arrays.
* Objects vs primitives. Reference vs value.
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

class FillInTheCode
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

The truth is, this question is a little too broad for the scope of this discussion. We are not going to all-inclusively define classes. We are going to instead talk about a few common types of classes, and the significance of classes in the Object-Oriented paradigm.

### Object Blueprints

Most classes will serve as a blueprint for a new type of Object. Classes like this can then be used to create Objects (called **instances** of the class) which behave as the class defines. That is, the class defines how its **instance** Objects store, mutate and provide access to their stored data, and how they interacts with that data.

The `Scanner` class is a perfect example; it provides a blueprint for `Scanner` objects, defining how they are created and how they function. We've used this definition to create and use `Scanner` objects.

Another way to think of an object-blueprint class is as a definition of a new data type and of the necessary methods to use that data type and allow it to interact in whatever context is necessary.

In future labs, we will be exploring how to create classes that serve as object blueprints. These types of classes are the heart of Object-Oriented Programming.

### Collections of `static` Methods and Constants

Some classes will serve as collections of related `static` methods. We'll talk more about `methods` in the next section, but they are essentially sequences of statements whose purpose is either to calculate a value or to perform an action. 

`static` methods are called directly from a class, and do not require a reference to an individual instance of the class. Nonstatic methods, on the other hand, are called from an individual instance of the class and may reference data stored by that instance.

Consider, for example, the `Math` class. It consists of:

* methods that are called directly from the class itself, like `Math.pow` used in the last lab.
* constants, also accessed directly through the class, like `Math.PI`.

An Object of type `Math` is never created; we never make a `new Math()` like we did with the `Scanner`.

### Client Classes

Some classes consist of little more than a main method, in which data and methods defined in other classes are accessed and used. These classes are sometimes referred to as program **entry points**. Small client classes are a very common part of software development; they are used to test components of (often quite large) systems of software.

## TODO String Class

## Class Variables and Constants

Constants and variables can be declared and initialized in the class body.

Consider the following class:

```java
class TemperatureConversion
{
    final static double CELC_FAHREN_RATIO = 9.0/5;
    final static int FAHREN_FREEZE_POINT = 32;
}
```

The `TemperatureConversion` class above consists of two constant numbers which are useful in conversions between temperatures in Fahrenheit and Celcius. These constants can be accessed for use in other classes.

## Methods

As mentioned in the previous section, a **method** is essentially sequences of statements whose purpose is either to calculate a desired value or to perform a desired action or sequence of actions.

### Declaring and Defining `static` Methods

`static` method declarations and definitions appear in the **scope** of the class body. Recall, a class definition looks like this:

```java
class <identifier> { <body }
```

(althought for readability's sake we usually write it like this:

```java
class <identifier>
{
	<body>
}
```

Something is said to be in the **scope** of the class body if it is in the curly braces `{}` denoting the boundaries of the class body. Specifically, `static` method declarations appear in the class body but not inside any nested blocks.

The simplest `static` method definitions look like this:

```java
static <returnType> <identifier> ( <argument_list> )
{
	<body>
}	
```

where:

* `<returnType>` is the desired data type for the output.
* `<identifier>` is the name that will be used to **call** (i.e. reference, perform) the method.
* The `<argument_list>` is, well, a list of **arguments**, separated by commas. 

Recall that **arguments** are the input data for the function. They are structured much like declarations; the consist of a data type followed by an identifier.

Consider the method definition in the `Calculator` class below:

```java
class Calculator
{
	static int subtract (int operand_1, int operand_2)
	{
		return (operand_1 - operand_2);
	}
}
```

We can tell from the header `static int subtract (int operand_1, int operand_2)`
that:

* The method is `static`, so it will be called directly through the `Calculator` class as `Calculator.subtract`.
* It's return (i.e. output) is an `int` value.
* It takes two `int` values as inputs, and refers to them as `operand_1` and `operand_2` during its calculation.

The body of the method above consists of a single statement: `return (operand_1 - operand_2);`

The `return` keywords means "leave the method" or "return to the line from which the method was called". If it is followed by an expression, then the value of that expression is the output or product of the method.

[EXERCISE] What is the output of the method above?

### Classes with Methods and Data

Classes can contain a mix of data (in the form of constants and variables) and methods, and these pieces can interact. Below, we expand the `TemperatureConversion` class from the previous section to include methods for performing conversions:

<a name="exTempClass"></a>

```java
class TemperatureConversion
{
    final static double CELC_FAHREN_RATIO = 9.0/5;
    final static int FAHREN_FREEZE_POINT = 32;

    // takes as an argument (input) the temperature in celcius (as a double)
    // returns (outputs) the temperature in fahrenheit (as a double)
    static double celcToFahren(double tempInCelc)
    {
        return tempInCelc * CELC_FAHREN_RATIO + FAHREN_FREEZE_POINT;
    }

    // argument : temperature in fahrenheit, as a double
    // return : temperature in celcius, as a double
    static double fahrenToCelc(double tempInFahren)
    {
        return (tempInFahren - FAHREN_FREEZE_POINT) / CELC_FAHREN_RATIO;
    }
}
```

Classes like this generally do not have main methods; they instead provide a collection of constants, variables and methods to facilitate some tasks in other programs. The `TemperatureConversion` class above can be accessed by other classes in the same project.

Create a new IntelliJ project, and in create two new Java classes in the src folder. The first class should be the `TemperatureConversion` class above. The second should be called `Client`. In it, put the `Client` class definition below. This `Client` class defines a main method and uses (**calls**) a method defined in `TemperatureConversion`.

<a name="exClientClass"></a>

```java
class Client
{
    public static void main(String[] args)
    {
        double tempInCelcius = 100;

        double tempInFahrenheit = TemperatureConversion.celcToFahren( tempInCelcius );

        System.out.println("Celcius : " + tempInCelcius);
        System.out.println("is equivalent to");
        System.out.println("Fahrenheit : " + tempInFahrenheit);
    }
}
```

If you run the `Client` class above, it should use the `celcToFahren` method from the `TemperatureConversion` class to convert the Celcius temperature of `100` to the corresponding Fahrenheit (`212`) and print both temperatures.

### `void` Methods

Methods can also simply **do something** and not have an output. Methods like this are called `void` methods because their return type is `void`.

Consider the example below of a class containing a `void` method:

<a name="exStringSlinger"></a>

```java
/*
    The StringSlinger class will consist of data and methods to print random nonsense.

    It is intended to facilitate the printing of bad, uninformative debug messages.
 */

// import a class for generating random primitive data
import java.util.Random;

class StringSlinger
{
    // define an array of 4 Strings, called nonsense.
    final static String[] nonsense = {
            "YEW WOT",
            "Karen please...",
            "oof",
            "No, Patrick, the lid..."
    };

    // construct a Random object to serve as a generator of random indexes
    final static Random generator = new Random();

    // select a random string from the nonsense array above and print it
    static void hurlRandomNonsense()
    {
        // Generate a random index to access the nonesense array
        int index = generator.nextInt( nonsense.length );

        // Print the message located at the specified index in the nonsense array
        System.out.println( nonsense[index] );
    }
}
```

The class above is significantly has a few things we haven't discussed yet, so let's go through them.

Let's first look at the constant `nonsense`. `nonsense` is a `String[]` (i.e. an array of `String`s). We'll discuss arrays in more detail later; for now it is sufficient to understand that the array stores the four `String`s seen in its assignment, and that they are associated with (and can be accessed using) the integers `0`, `1`, `2`, and `3`.

There is also an `import` statement, which imports the `Random` class from `java.util`. Instances of the `Random` class can be used to generated random primitive values.

In the `hurlRandomNonsense` method, the instantiated `Random` object (called `generator`) is used to generate random integers. Specifically, it is used to generate random non-negative integers less than `nonsense.length`, i.e. less than `4` (the length of the `nonsense` array). That is, it is used to generate random integers from the list `0`, `1`, `2`, and `3`.

These random integers are then used to access the corresponding `String` in the `nonsense` array, so it can be printed. The end result is: `hurlRandomNonsense` selects a random element from the `nonsense` array and prints it.

Note that `hurlRandomNonsense` is of type `void`; it does not `return` anything. In fact, it doesn't even have a `return` keyword, so its execution ends when it reaches the closing curly braces `}` denoting the end of the method body.

### Class Methods vs Instance Methods

All of the methods we've defined so far have been `static`; these methods are associated with a class, and are accessed through the class. Instance methods are instead accessed through a class instance. For example, the `nextInt` method of the `Random` class is an instance method, and is accessed through an instantiated object as you can see in [this example](#exStringSlinger). We will discuss instance methods in much more detail in future labs.

### Methods vs Functions

In most languages, there are both **methods** and **functions**. The two are similar; they are both essentially sequences of statements which may or may not reference input data to perform an action or set of actions or to output a result. The difference is that methods are associated with an object or class, whereas functions are standalone processes.

In Java, there is no such thing as a function; nothing can be defined outside of a class, so every definition is associated with either a class or with instances of that class.

[EXERCISE] Create a `Client` class to test the `StringSlinger` class.

[EXERCISE] Write a method.

## Using IntelliJ's Debugger

IntelliJ has a built-in debugger, which lets you step through your code line by line and check the values of variables and constants in the current scope.

In the project consisting of the [`TemperatureConversion`](#exTempClass) class and its [`Client`](#exClientClass) class, set a **break point** on the line with the statement `double tempInCelcius = 100;`. You can set a break point on any line by clicking in between the editor pane's line numbers and the text editor itself. A red dot will appear on the line, denoting that there is a break point there:

![Break Point](./figures/breakPoint.png)

The break point tells the debugger **where to stop** to wait for your instruction; once you run the debugger, the program will run until it hits a break point, and then stop and wait. You can then use the debugger controls to move the program forward step by step.

Once you've placed the break point, go to the `Run` menu, select `Debug...` and in the dialog that pops up select your `Client` class.

The program should begin running, and stop at the break point. The break point will now be highlighted in blue, denoting where the debugger is stopped in its execution of the program:

![Stop at Break Point](./figures/stopAtBreakPoint.png)

The line highlighted in blue **has not yet been executed**. Program execution stopped just **before** the statement on this line could run. You can think of the break point as being at the start of the line, before the statement itself.

The debugger pane should have popped up at the bottom of the IntelliJ window, where the console normally is for normal runs:

![Debugger Pane](./figures/debuggerPane.png)

You can mouse over any of the buttons in this debugger pane, and a small tooltip will appear in the bottom left of the IntelliJ window briefly describing the button's function:

![Debugger Tooltips](./figures/debuggerTooltips.png)

There is a vertical toolbar on the left, outlined in red below. From top to bottom, these buttons:

* **Rerun Program**: Run the program again from the beginning.
* **Continue Program Execution**: Run the program until it hits the next break point.
* **Pause Program**: Pauses the program wherever it is in execution. This button is useful when the program is stuck in a loop somewhere, so it's just running forever, and you'd like to find out where the offending code is.
* **Stop Program Execution**: Pretty straightforward, terminate the program.
* **Show Breakpoints**: Breakpoints are displayed in a new window which pops up, specifying what files the breakpoints are in and which lines they're on, among other things.
* **Mute Breakpoints**: The debugger will not stop at breakpoints while they are muted.
* **Get Thread Dump**: Outside of the scope of what we'll be using the debugger for.

![Execution Toolbar](./figures/executionToolbar.png)

In the variables pane, you can see a list of all variables which are accessinle from the scope of the current statement:

![Debugger Variables](./figures/debuggerVariables.png)

Currently, the statement declaring `tempInCelcius` has not been executed yet, so it is not visible in the variables pane. The only variable that we can see in the pane is the `args` variable (which you can see is the only input for the main method). We'll talk more about the `args` list, and what data is contained in it, when we cover arrays in a future lab.

Finally, the debugger controls can be used to follow the program through its execution as desired. From left to right, the buttons outlined in red in the picture below do the following:

* **Show Execution Point**: Opens the file at which execution is currently stopped, and moves your cursor to the line it is stopped on.
* **Step Over**: Steps to the next line in the current file; if the current line uses another file (say, it calls a method defined in another file), you will not enter that function definition to step through it.
* **Step Into**: Steps to the next line executed, in this file or a different file. If the current execution line calls a method defined in another file, the debugger will step into that method, so you can go through it line by line.
* **Force Step Into**: A more inclusive "step into". Step into will not step into some library functions, where force step into will.
* **Step Out**: Continue execution until leaving the current method / scope, then stop.
* **Drop Frame**: Leaves the current method by returning to where it was called, essentially allowing you to step "back in time" to just before the method being executed was called. Use this carefully, as there are some changes that will not be reversed, and we won't discuss what these changes are until a future lab.
* **Run To Cursor**: Continue execution until reaching the line where the cursor is.
* **Expression Calculator**: Opens a window which allows you to type expressions (using variables in the current scope) and see what those expressions evaluate to.

![Debugger Controls](./figures/debuggerControls.png)

Try using the **Step Into** button to move to the next line. You should end up here:

![Debugger Step Into](./figures/debuggerStepInto.png)

Execution has now stopped just before the statement on line 7 in the picture above. The statement on line 5 has been executed, and the `tempInCelcius` variable is now visible in the variables pane.

Notice that line 7 contains a call to the method `TemperatureConversion.celcToFahren`. On this line, we are faced with a choice. If we hit the **Step Into**, we will step into the `celcToFahren` function, where we can go through it line by line. If we hit **Step Over** we will fully execute this call to `celcToFahren` without walking through it, and continue executing until reaching the next line in `Client.java`, which is line 9 in the image above.

Hit **Step Into**. You should end up here:

![Debugger Step Into 2](./figures/debuggerStepInto2.png)

Note that the `tempInCelc` variable now in the variables pane is **not** the same one that we could see back in the `Client`. This is a new variable, an **argument** for the `celcToFahren` method, which has been given the value of the variable that was passed into the method in the `Client`.

If you hit the **Drop Frame** button, you can step back into the `Client`, just before the `celcToFahren` was called. This is useful if you want to start the `celcToFahren` execution over to step through it again.

If you hit **Step Over**, **Step Into**, or **Step Out**, the result will be to finish the execution of the `celcToFahren` function (because we are already on its last line) and return to the `Client`, where execution will resume on the line after the method call. Hit one these three buttons, and you should end up here:

![Debugger Step Out](./figures/debuggerStepOut.png)

(If you chose **Step Out** above you would actually end up back on line 7, but **after** the method call was completed, and you'd need to **Step Into** or **Step Over** to get to where the image above is).

Now, the variable `tempInFahrenheit` is visible in the variables pane. It has been assigned the value that was output by the `celcToFahren` call. Moreover, we already know that water boils at 100 degrees Celcius and 212 degrees Fahrenheit, so it appears that `celcToFahren` returned the correct result! This doesn't necessarily mean that `celcToFahren` is **always** correct, just that it is correct when converting 100 degrees Celcius to Fahrenheit.

Many programmers are tempted to debug their software by printing status messages to the console stating the values of variables and other pertinent information. This is generally bad practice except in niche cases where the debugger isn't helpful for one reason or another. It's bad practice for a few reasons, but the primary one is that it is **tedious** and **slow**, whereas using the debugger is **easy** and **fast** once you're used to it!

## Boolean Expressions

Recall that an **expression** is a combination of variables, operations and values that yields a resulting value, and that the primitive data type `boolean` stores **truth values** (`true` or `false`).

A **boolean expression** is an expression which evaluates to a `boolean` value of `true` or `false`.

The simplest boolean expressions are the `boolean` literal values themselves, `true` and `false`. Next in line are the identifiers of `boolean` variables, which evaluate to the value of said variables.

### Relational Operators

Java includes **relational operators** which return `true` or `false` depending on the values of their operands (which must be numerical primitives):

**OPERATOR** | **SAMPLE EXPRESSION** | **VALUE**
:----------: | :-------------------: | :-------:
`<`          | `x < y`               | `true` if `x` is less than `y`; `false` otherwise
`<=`         | `x <= y`              | `true` if `x` is less than or equal to `y`; `false` otherwise
`==`         | `x == y`              | `true` if `x` equals `y`; `false` otherwise
`!=`         | `x != y`              | `true` if `x` does not equal `y`; `false` if `x` does equal `y`
`>=`         | `x >= y`              | `true` if `x` is greater than or equal to `y`; `false` otherwise
`>`          | `x > y`               | `true` if `x` is greater than `y`; `false` otherwise

[EXERCISE] comparisons

### Boolean Operators

Java also includes **boolean operators**, which allow calculation of `boolean` values using boolean logic. Each boolean operator takes boolean expressions as operands, and outputs a boolean value based on the values of those expressions. In the following table, `a` and `b` are both assumed to be placeholders for boolean values or for boolean expressions.

**OPERATOR** | **MEANING** | **SAMPLE EXPRESSION** | **VALUE**
:----------: | :---------: | :-------------------: | :-------:
`&&`         | *and*       | `a && b`              | `true` if `a` and `b` are both `true`; `false` otherwise
`||`         | *or*        | `a || b`              | `false` if `a` and `b` are both `false`; `true` otherwise
`!`          | *not*       | `!a`                  | `true` if `a` is `false`; `false` if `a` is `true`

If you refer to the [Java 8 operator precedence](https://github.com/arewhyaeenn/COMP_150_LAB_2_JAVA_FUNDAMENTALS/blob/master/figures/operatorPrecedence.png) you'll see that, when evalutating logical expressions, first *not* operations (`!`) are performed from right to left, then *and* (`&&`) operations from left to right, and finally *or* (`||`) from left to right. Of course, parenthesis can be used to specify a different order.

[EXERCISE] boolean operations on boolean literals and boolean variables

[EXERCISE] boolean operations with relational operators

### TODO Short Circuit Evaluation

## `if`/`else`

`if` and `else` statements can be used in coalition with boolean expressions to perform different actions based on properties of data. We will cover the format of `if` and `else` statements, but first consider this example:

```java
import java.util.Scanner;

class MyClass
{
	public static void main(String[] args)
	{
		Scanner scan = new Scanner( System.in );
		
		System.out.println("Enter an integer : ")
		long userInput = scan.nextLong();
		
		if (userInput > 10)
		{
			System.out.println("Your input was greater than 10.");
		}
		else
		{
			System.out.println("Your input was not greater than 10.");
		}
	}
}
```

The program above prompts the user for an integer, and stores their response in a variable called `userInput`. It then prints out a message, telling the user whether their input was greater than `10` or not.

[EXERCISE] Edit the program above to tell the user whether their response equals `10`.

###<a name="if"></a>`if` Statements

The simplest `if` statements look like: `if ( <boolean_expression> ) { <true_block> }`.

If the boolean expression in the parenthesis is true, then the statements in the true block are executed; otherwise they are not. In the snippet below, `x` has value `5`. So, when the `if` statement's boolean expression, `x == 5`, is evaluated, it evaluates to `true`. Because the boolean expression is true, the print statement in the true block runs.

```java
int x = 5;
if (x == 5)
{
	System.out.println("mmhmmm");
}
```

### `if`/`else` Statements

An `if` statement can include a second block, called the `else` block, with instructions to execute if the boolean expression is `false`:

```java
if ( <boolean_expression> )
{
	<true_block>
}
else
{
	<false_block>
}
```

The `else` keyword precedes the false block, i.e. the instructions to execute if the boolean expression is `false`. We can expand the example `if` statement above to include an `else`:

```java
int x = <int_literal>;
if (x == 5)
{
	System.out.println("mmhmmm");
}
else
{
	System.out.println("nuh uh");
}
```

Here if the value assigned to `x` is `5`, then the message "mmhmmm" is printed; otherwise "nuh uh" is printed.

In an `if` statement, the block(s) which may or may not be executed depending on the value(s) of boolean expression(s) are called **conditional blocks**. This is because they are blocks whose contained instructions are only executed if specific conditions (specifically, those defined in the boolean expression) are met.

[EXERCISE] simple boolean, complex body

[EXERCISE] complex boolean, simple body

### Statement Nestability

If statements are structured and interpreted in the following form: `if ( <boolean_expression> ) <statement> else <statement>`.

As shown above, the trailing `else <statement>` is optional. Recall that a block can be used wherever a statement can; in the examples above, the two `<statement>`s were blocks.

Because `if` statements are a type of statement, the `<statement>` slots above could be `if` statements. In other words, `if` statements are **nestable**; one `if` statement can be a part of (i.e. can be **nested in**) another `if` statement. This means that chains of `if` statements can be made as described in the next section.

### `if`/`else if`/`else` Chains

When the `<statement>` trailing the `else` keyword is, itself, an `if` statement, you end up with something like this:

```java
if ( <boolean_expression> )
{
	...
}
else if ( <boolean_expression> )
{
	...
}
else
{
	...
}
```

Consider executing a program like the one above. If the first boolean expression is `true`, then the first block is entered and executed. Then, an `else` is reached, but because the corresponding `if`'s boolean expression was `true`, the `<statement>` trailing the `else` is not executed. In the program above, this `<statement>` is an `if` statement with an `else` of its own, all of which is not executed.

In other words, in a chain of `if`/`else if` statements, only one `true` block will be entered.

Consider this example:

```java
import java.util.Scanner;

class DoorGuard
{
    static String CURRENT_PASSWORD = "password123";
    static String OLD_PASSWORD = "password";

    public static void main(String[] args)
    {
        Scanner keyboard = new Scanner( System.in );
        System.out.println("What's the password?");
        String userResponse = keyboard.next();

        if ( userResponse.equals(CURRENT_PASSWORD) )
        {
            System.out.println("Welcome back!");
        }
        else if ( userResponse.equals(OLD_PASSWORD) )
        {
            System.out.println("That's the old password...");
        }
        else
        {
            System.out.println("Get lost!");
        }
    }
}
```

Notice that the boolean expressions above don't use the relational operators; the instead make calls to the `userResponse` `String`'s `equals` method. This is because `String`s are objects, not primitives, so the `==` operator would check if they are the **same object** (i.e. if they reference the same location in memory); we want to check if they contain the same characters, which is defined in the `String` class's `equals` method.

[EXERCISE] What happens if the user enters the current password in the example above? What if they enter the old password? What if they enter something else entirely?

[EXERCISE] Go on an if-else flow adventure with the debugger

### `if` Statements, Blocks, and Nestability

The conditional blocks in `if` statements are, well, blocks; they can contain a sequence of statements. These contained statements can also be `if` statements (or any other type of statement). For example, the program below consists of an `if` statement whose conditional blocks contain more `if` statements.

```java
import java.util.Scanner;

class FreeJacket
{
    final static String YES_RESPONSE = "yes";
    final static String NO_RESPONSE = "no";

    public static void main(String[] args)
    {
        Scanner keyboard = new Scanner( System.in );
        String userResponse;

        System.out.println("Are you cold? (yes / no)");
        userResponse = keyboard.next();

        if ( userResponse.equals(YES_RESPONSE) )
        {
            System.out.println("Would you like a FREE JACKET? (yes / no)");
            userResponse = keyboard.next();
            if ( userResponse.equals(YES_RESPONSE) )
            {
                System.out.println("Here ya go!");
            }
            else if ( userResponse.equals(NO_RESPONSE) )
            {
                System.out.println("Who likes comfort anyway?");
            }
            else
            {
                System.out.println("\"yes\" or \"no\" ... ");
            }
        }
        else if ( userResponse.equals(NO_RESPONSE) )
        {
            System.out.println("Liar! Do you want a FREE JACKET? (yes / no)");
            userResponse = keyboard.next();
            if ( userResponse.equals(YES_RESPONSE) )
            {
                System.out.println("I knew you were cold...");
            }
            else if ( userResponse.equals(NO_RESPONSE) )
            {
                System.out.println("But it's free...");
            }
            else
            {
                System.out.println("\"yes\" or \"no\" ... ");
            }
        }
        else
        {
            System.out.println("\"yes\" or \"no\" ... ");
        }
    }
}
```

[EXERCISE] Read the program above. Theorize about how it should behave. When you believe you know what it will do in any case (i.e. with any sequence of user inputs) run it to test your theory. You may want to run with the debugger, so you can step through line by line and see what's happening!

[EXERCISE] Write a program to specification using nested ifs

## `while` Loops

Sometimes it is necessary to repeat an action multiple times. This can be done with a **loop**. There are several types of loops in Java. The simplest type of loop is the `while` loop. `while` loops look like this:

```java
while ( <boolean_expression> )
{
	<loop_body>
}
```

As long as the boolean expression, called the **loop condition** remains `true`, the loop will keep repeating the statements in the **loop body**. The loop essentially works as follows:

1. Evaluate the loop condition is `true`
2. If the loop condition is `true`, execute the instructions in the loop body, then start over on step 1.
3. Otherwise, resume execution on the line after the loop body.

Each repetition of the instructions in the loop body is called an **iteration**. To **iterate** is to go through an iteration.

The snippet below should iterate 10 times; it should print out the numbers `0` through `9`, and should leave `i` with value `10` after the loop has completed.

```java
int i = 0;
while (i < 10)
{
	System.out.println(i);
	++i;
}
```

[EXERCISE] Create a simple program the the while loop above in its main method. Run with debugger...

[EXERCISE] Read a while loop example and answer questions about it.

[EXERCISE] Write a program involving a while loop to meet specifications.

## `do while` Loops

The `do while` loop is very similar to the `while` loop. There are two differences. The first difference is in how the loop itself is written. A `do while` loop is written like this:

```java
do {
	<loop_body>
} while ( <boolean_expression> );
```

The second difference is that the `while` loop checks the loop condition before the first iteration, where the `do while` loop does not. In other words, a `while` loop can iterate 0 times if the loop condition is initially `false`, but a `do while` loop will **always** iterate at least once.

Anything that can be done with a `do while` loop can also be done with a `while` loop. The `do while` loop above could be written identically with a `while` loop like this:

```java
<loop_body>
while ( boolean_expression )
{
	<loop_body>
}
```

Sometimes, a loop body must iterate at least once, and it is easier (more concise) to write a `do while` loop. For example, loops are often used to get valid user inputs with the following sequence of events:

* prompt the user for a response
* read the user's response
* validate the user's response (check if it is valid)
* if the user's response is invalid, start over
* if the user's response is valid, continue

Consider for example the `UserWrangler` class:

```java
/*
    The UserWrangler class will define methods to facilitate console interactions
    with the user (prompting, interpreting responses, validating responses...).
 */

import java.util.Scanner;

class UserWrangler
{
    final static String YES_RESPONSE = "yes";
    final static String NO_RESPONSE = "no";
    final static Scanner keyboard = new Scanner( System.in );

    static boolean getYesNoResponse(String prompt)
    {
        String userResponse;

        // repeatedly ask the user for a response (and tell them what their options are)
        // until that idiot figures out how to type "yes" or "no" ;)
        do {
            System.out.println(prompt + " (" + YES_RESPONSE + " / " + NO_RESPONSE + ")");
            userResponse = keyboard.next();
        } while ( !(userResponse.equals(YES_RESPONSE) || userResponse.equals(NO_RESPONSE)) );

        return userResponse.equals(YES_RESPONSE);
    }
}
```

At the moment, the class above contains a single method, called `getYesNoResponse`. It takes as an argument a `String`, storing the prompt (i.e. what to print to request information from the user). It returns a `boolean` value; `true` if the user enters "yes" and `false` if the user enters "no". It allows a programmer to ask the user a yes or no question, and be given the result as a `boolean` with a single method call.

[EXERCISE] Use the client below to step through `UserWrangler.getYesNoResponse` with the Debugger.

```java
class Client
{
    public static void main(String[] args)
    {
        boolean userYesNoResponse;

        while (true)
        {
            userYesNoResponse = UserWrangler.getYesNoResponse("ARA YA READY, KIDS!?");
            if (userYesNoResponse)
            {
                System.out.println("OOOOOOOHHHHHHHHHHH!!!!!");
            }
            else
            {
                System.out.println("oh...");
            }
        }
    }
}
```

[EXERCISE] or maybe just a paragraph, something to point out the infinite loop in the client above

[EXERCISE] rewrite the FreeJacket client above to use StringWrangler.getYesNoResponse

## `for` Loops

`for` loops are another loop variant. Anything that can be done with a `for` loop can also be done with a `while` loop, but in some circumstances `for` loops provide more concision.

`for` loops are structured as follows:

```java
for (<initializing_statement> ; <boolean_expression> ; <end_of_iteration_statement>)
{
	<loop_body>
}
```	

The function much like `while` loops do, but come with a bit more of the setup encased in the statement syntax. The three statements in the `for` loop's parenthesis are as follows:

* `<initializing_statement>` : executed before the first iteration.
* `<boolean_expression>` : evaluated before each iteration; if `true`, keep looping; if `false`, stop looping.
* `<end_of_iteration_statement>` : executed after each iteration, before evaluating the boolean expression for the next iteration.

Consider, for example, the while loop from above:

```java
int i = 0;
while (i < 10)
{
	System.out.println(i);
	++i;
}
```

A (nearly) identical `for` loop can be constructed using the same initial setup, loop condition, and end-of-loop statement:

```java
for (int i = 0; i < 10; ++i)
{
	System.out.println(i);
}
```

These two loops are identical in output; they both print the same numbers. There is  difference, however. The `while` loop example declares `i` outside of the scope of the loop, so `i` still exists outside of the loop (it has a value of `10` when the loop completes). The `for` loop, on the other hand, declares `i` inside the scope of the loop, so `i` doesn't exist after the loop finishes iterating.

[EXERCISE] print i after the while loop, find out what happens when you try after the for loop

[EXERCISE] modify the for loop above so it behaves exactly like the while loop (i is still accessible afterwards).

## `break` and `continue`

A `break` statement can be used to stop a loop's iterating, without finishing the current iteration. Consider this snippet:

```java
int i = 0;
while (true)
{
	if (i == 10)
	{
		break;
	}
	System.out.println(i);
	++i;
}
```

Note that in the loop above, the loop condition is simply `true`. This means that, in theory, the loop could keep iterating forever. It will only stop iterating if it encounters a `break` statement or a `return` statement.

`i` starts at `0`, and is incrememented by `1` at the end of each iteration with `++i;`; eventually, it will be `10`, at which time the `if` condition `i == 10` will be `true`, and the `break;` statement will execute. When this happens, the `while` loop ceases looping without finishing the current iteration.

[EXERCISE] what is the first number printed by the loop above? what is the last? verify by running...

A `continue` statement will cause the loop to start iteration again from the beginning of the loop body if the loop condition is still `true`.

```java
int i = 0;
while (i < 10)
{
	++i;
	if (i % 2 == 0)
	{
		continue;
	}
	System.out.println(i);
}
```

The loop above starts `i` at `0` and increments `i` by `1` at the beginning of each iteration, so eventually the loop condition `i < 10` will be `false`. In each iteration, if `i` is even (i.e. if the remainder when `i` divided by `2` is `0`) after being incremented then the loop body starts over; otherwise, the loop body continues to print `i` before starting over.

[EXERCISE] What values are printed by the loop above? verify by running...

## `switch`

`switch` statements can be used to when a `byte`, `short`, `int`, `char` or `String` expression has one of a finite number of values and the action taken that needs to be taken depends on that value.

Essentially, the `switch` take an input that is an expression with one of these types, and 

`switch`s also works with the accepted primitives' respective wrapper classes `Byte`, `Short`, `Integer` and `Character`, as well as with enumerated types (`enum`s) which we will discuss in a future lab.

#BOOKMARK

### `switch` and `if` Statements

## Arrays

### Visualizing

### Indexing

### Strings and Arrays

### Traversing

## Objects vs Primitives; Reference vs Value

### Strings again...











