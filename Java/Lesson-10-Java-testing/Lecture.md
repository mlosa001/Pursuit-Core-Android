
---

Title: Testing using JUnit

---

## Objective

* The purpose of software tests
* Testing terminology
* Using JUnit 4
* Mocking

---


## Resources

[JUnit Homepage](http://www.junit.org/)

[JUnit 5 user guide](http://junit.org/junit5/docs/current/user-guide/)

[Unit Testing Guide by Vogella](http://www.vogella.com/tutorials/JUnit/article.html)

---


## What are software tests?

A software test is a piece of software, which executes another piece of software. It validates if that code results in the expected state (state testing) or executes the expected sequence of events (behavior testing).

---

## Why are software tests helpful?

* Software unit tests help the developer to verify that the logic of a piece of the program is correct.

* They ensure the program continues to work after modification 


---

## Testing terminology

#### Test fixture

A test fixture is a fixed state in code which is tested used as input for a test. Another way to describe this is a test precondition.

For example, a test fixture might be a a fixed string, which is used as input for a method. The test would validate if the method behaves correctly with this input.

#### Unit tests and unit testing

* A unit test targets a small unit of code, usually a method or a class. 

* The percentage of code which is tested by unit tests is typically called **test coverage**.

* Unit tests are not suitable for testing complex user interface or component interaction. For this, you should develop integration tests.

---

#### Integration tests

* An integration test aims to test the behavior of a component or the integration between a set of components. 

* Can also be referred to as Systems test or functional testing.

* The test would resemble an expected user interaction with the application.


#### Performance tests

* Performance tests are used to benchmark software components repeatedly. 

* Their purpose is to ensure that the code under test runs fast enough even if it’s under high load.

---

## Where should the test be located?

Typical, unit tests are created in a separate project or separate source folder to keep the test code separate from the real code. The standard convention from the Maven and Gradle build tools is to use:

src/main/java - for Java classes

**src/test/java** - for test classes

---

## Which part of the software should be tested?

**Hard to tell**

* You should write software tests for the critical and complex parts of your application. 

* There is such thing as over-testing and under-testing

* It is good practice to start writing tests for code in which most of the errors happened in the past. This way you can focus on the critical parts of your application.

---

## Using JUnit

JUnit is a test framework which uses annotations to identify methods that specify a test. JUnit is an open source project hosted at Github.

**Todo**: Add JUnit dependency to the LinkedList project from last week

---

### How to define a test in JUnit?

A JUnit test is a method contained in a class which is only used for testing. This is called a Test class. To define that a certain method is a test method, annotate it with the @Test annotation.

This method executes the code under test. You use an assert method, provided by JUnit or another assert framework, to check an expected result versus the actual result. These method calls are typically called asserts or assert statements.

You should provide meaningful messages in assert statements. That makes it easier for the user to identify and fix the problem. This is especially true if someone looks at the problem, who did not write the code under test or the test code.

---

## Example JUnit test
The following code shows a JUnit test using the JUnit 5 version. This test assumes that the MyClass class exists and has a multiply(int, int) method.

```java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

public class MyTests {

    @Test
    public void multiplicationOfZeroIntegersShouldReturnZero() {
        MyClass tester = new MyClass(); // MyClass is tested

        // assert statements
        assertEquals(0, tester.multiply(10, 0), "10 x 0 must be 0");
        assertEquals(0, tester.multiply(0, 10), "0 x 10 must be 0");
        assertEquals(0, tester.multiply(0, 0), "0 x 0 must be 0");
    }
}
```

---

## JUnit naming conventions
There are several potential naming conventions for JUnit tests. A widely-used solution for classes is to use the "Test" suffix at the end of test classes names.

As a general rule, a test name should explain what the test does. If that is done correctly, reading the actual implementation can be avoided.

One possible convention is to use the "should" in the test method name. For example, "ordersShouldBeCreated" or "menuShouldGetActive". This gives a hint what should happen if the test method is executed.

Another approach is to use "Given[ExplainYourInput]When[WhatIsDone]Then[ExpectedResult]" for the display name of the test method.


---


## Test execution order
JUnit assumes that all test methods can be executed in an arbitrary order. Well-written test code should not assume any order, i.e., tests should not depend on other tests.

As of JUnit 4.11 the default is to use a deterministic, but not predictable, order for the execution of the tests.

---

## Defining test methods
JUnit uses annotations to mark methods as test methods and to configure them. The following table gives an overview of the most important annotations in JUnit for the 4.x and 5.x versions. All these annotations can be used on methods.

---

## Common JUnit Annotations

**@Test**: Identifies a method as a test method.

**@Before**: Executed before each test. It is used to prepare the test environment (e.g., read input data, initialize the class).

**@After**: Executed after each test. It is used to cleanup the test environment (e.g., delete temporary data, restore defaults). It can also save memory by cleaning up expensive memory structures.

**@BeforeClass**: Executed once, before the start of all tests. It is used to perform time intensive activities, for example, to connect to a database. Methods marked with this annotation need to be defined as static to work with JUnit.


---

## Common JUnit Annotations

**@AfterClass**: Executed once, after all tests have been finished. It is used to perform clean-up activities, for example, to disconnect from a database. Methods annotated with this annotation need to be defined as static to work with JUnit.

**@Test (expected = Exception.class)**
Fails if the method does not throw the named exception.

**@Test(timeout=100)**
Fails if the method takes longer than 100 milliseconds.

---

## Assert statements

**fail([message])**: Let the method fail. Might be used to check that a certain part of the code is not reached or to have a failing test before the test code is implemented. The message parameter is optional.

**assertTrue([message,] boolean condition)**: Checks that the boolean condition is true.

**assertFalse([message,] boolean condition)**: Checks that the boolean condition is false.

**assertEquals([message,] expected, actual)**: Tests that two values are the same. Note: for arrays the reference is checked not the content of the arrays.

**assertEquals([message,] expected, actual, tolerance)**: Test that float or double values match. The tolerance is the number of decimals which must be the same.


---

## Assert statements contd.

**assertNull([message,] object)**: Checks that the object is null.

**assertNotNull([message,] object)**: Checks that the object is not null.

**assertSame([message,] expected, actual)**: Checks that both variables refer to the same object.

**assertNotSame([message,] expected, actual)**: Checks that both variables refer to different objects.

---

## Mocking (Up next)

## Test Driven Development (Up next)

---

## Summary

- Software unit tests help the developer to verify that the logic of a piece of the program is correct.

- They also verify the code is still correct after modification

- There are several different kinds of tests but unit tests are the most common and important of them.

- JUnit uses annotations to mark methods as test methods and to configure test classes

- Asserts allow you to specify the error message, the expected and the actual result.

---


## Exercises

**Question 1**:

Create a method, `splitNumber` that takes a string of the form `"12345"` and returns an int array `[1,2,3,4,5]`. The string can be of arbitrary length.

Create a JUnit test to test the method `splitNumber`.

The method signature should be `public int[] splitNumber(String input)`

---

## Exercises

**Question 2**:

Below is the code for the bubble sort algorithm, create a JUnit test for it. 
If you would like to learn more about bubble sort, see this [article](http://www.geeksforgeeks.org/bubble-sort/)

---

```java
public static void BubbleSort( int [ ] num )
{
     int j;
     boolean flag = true;   // set flag to true to begin first pass
     int temp;   //holding variable

     while ( flag )
     {
            flag= false;    //set flag to false awaiting a possible swap
            for( j=0;  j < num.length -1;  j++ )
            {
                   if ( num[ j ] < num[j+1] )   // change to > for ascending sort
                   {
                           temp = num[ j ];                //swap elements
                           num[ j ] = num[ j+1 ];
                           num[ j+1 ] = temp;
                          flag = true;              //shows a swap occurred  
                  } 
            } 
      } 
} 
```

---