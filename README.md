# Exception Handling

## Learning Goals

- Explain exception handling
- Use exception handling

## Introduction

In Java, unexpected behavior is managed through "exceptions". Exceptions are
"thrown" and "caught". The code that generates the exception "throws" it and the
code that called the code that generated the exception can choose to "catch" it
or throw it as well.

## Exception Handling in Java

Let's use an example from our user interaction code:

```java
    public static void main(String[] args) {
        System.out.println("Please enter a number:");
        Scanner inputScanner = new Scanner(System.in);
        int userNumber = inputScanner.nextInt();
        System.out.println("The user entered " + userNumber);
    }
```

The `nextInt()` method of the `Scanner` class can throw a
`InputMismatchException`. It does so when the input entered by the user cannot
be interpreted as an integer number. When it throws an exception, it creates an
object of the type of the exception and returns it as the return for the method
call instead of what it would normally return if everything worked as expected.

As the code that is using this method, we can "catch" the exception by wrapping
the call for the method that throws it in a `try` and `catch` block, like this:

```java
    public static void main(String[] args) {
        System.out.println("Please enter a number:");
        Scanner inputScanner = new Scanner(System.in);
        try {
            int userNumber = inputScanner.nextInt();
            System.out.println("The user entered " + userNumber);
        } catch (InputMismatchException ime) {
            System.out.println("The input was not a number");
        }
    }
```

A `try` block can have as many statements in it as you want and is therefore
also delimited with open and close curly braces. Any exception that are thrown
by any code inside the `try` block will:

- Cause the execution of the statements inside the `try` block to be interrupted
  immediately
- Cause the execution to jump straight passed the remaining statements (if any)
  in the `try` block into the beginning of the `catch` block
- Pass an object of the type of the exception being thrown to the `catch` block

Note that in the example above, the program will not execute the line
`System.out.println("The user entered " + userNumber);` if the user enters an
invalid number, since the exception will be thrown on the previous line,
interrupting the execution of the `try` block

The `InputMismatchException` is an "unchecked" exception, which means that the
code that could potentially cause it to be thrown does not _have_ to catch it.
This is in contrast to "checked" exceptions, which are exceptions that _must_ be
caught by any code that could potentially cause them to be thrown.

For example, Java provides methods for reading data from files. In most cases,
those methods throw a checked exception called `FileNotFoundException`, so that
the code that uses them _must_ catch that exception or it will not compile. Note
that the `try {} catch {}` block for a checked exception follows exactly the
same structure as the `try {} catch {}` block for an unchecked exception.
