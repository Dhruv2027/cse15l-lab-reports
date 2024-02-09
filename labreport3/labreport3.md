# Lab Report - 3

## Part 1 - Bugs
In this section, I will be exploring bugs in the ArrayExamples.java file from week 4's lab session. First, I forked the `https://github.com/ucsd-cse15l-f23/lab3` repository and then used the following commands in the terminal to run and test the code.
```
local $ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
local $ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
As of now, there are only 2 tests, which ran perfectly. However, when I added more tests they failed. One of the failed tests: 
Code: 
```java
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```

```java
@Test
public void testReversedArray(){
  int[] input1 = { 1, 2, 3 };
  assertArrayEquals(new int[]{ 3, 2, 1 }, ArrayExamples.reversed(input1));
}
```

In this case, the error was that the test expected <3>, but was actually <0>. 

In another case, in the test:
```java
@Test
public void testReversed() {
  int[] input1 = { };
  assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
}
```
The test works perfectly. When there is no input, the program correctly returns no array, thus passing the test.

