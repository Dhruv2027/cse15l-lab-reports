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

![Image](SS1.png)

As can be seen in the above screenshot, 2 tests are run with one passing and one failing. The symptom here is that something that was expected is not mirrored in what was actually produced. The test expected the value of 3, but got a value of 0. The bug here is that the new array which is to be returned is not getting reversed. Instead, each value in the original array is being replaced with 0. To fix the error, I updated the old code to remove the bug.

```java
//old, buggy code
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}

//new, bug-less code
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[arr.length - i - 1];
  }
  return newArray;
}
```

All I changed here was replacing the `arr` on the left hand side with `newArray` and `newArray` on the right with `arr`. This fixes the code as when I run the java test again, I get the following output: 

```
(base) dhruvsharma@Dhruvs-MacBook-Pro-2 lab3 % javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java                              
(base) dhruvsharma@Dhruvs-MacBook-Pro-2 lab3 % java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
..
Time: 0.014

OK (2 tests)
```

***
## Part 2 - Researching Commands
I will be talking about the `grep` command. I will explore how the `-i`, `-r`, `-n`, and `"[A-Z]"` commands in `grep` work. I am starting from the `/docsearch/` directory and will change the directory to `/docsearch/technical/` and search for the files in the `plos` folder.

### `grep -i` function

I entered the command `grep -i "plos" plos/pmed.0020203.txt` while in the `/docsearch/technical/` directory to search for each occurrence of the `plos` keyword in the file `pmed.0020203.txt`. The output I received is shown below: 

```
dhruvsharma@Dhruvs-MacBook-Pro-2 technical % grep -i "plos" plos/pmed.0020203.txt 
      PLoS Medicine is a sufficiently new journal that we are often doing
      PLoS Medicine ? Although our journal's focus is on human studies, we have
      PLoS Medicine . These include studies that explore off-label uses of
      PLoS Medicine . Instead, we encourage submission of important advances
      PLoS Biology , our flagship open-access biology journal
      (www.plosbiology.org).
      PLoS Medicine has published a number of Perspectives on research articles
      PLoS Biology , and 
      PLoS Biology regularly highlights papers from 
      PLoS Medicine on its home page. In this way, because all our journals are
      PLoS Medicine and any other PLoS journal, is just a rodent click.
```

Here, each line of the output shows the line where the keyword "plos" is used. This function is particularly useful as the developer may never know when the keyword has been capitalized or has a mix of capital letters and non capital letters. The `-i` function removes this uncertainty as it gives an output regardless of capitalisation. 

In the next scenario, it may be beneficial to find out which part of the document in `government/About_LSC/ODonnell_et_al_v_LSCdecision.txt` contains the word "legal" as part of the arguement or if it is part of a legal services company. It makes searching for the context of the word "legal" a lot easier. The output: 

```
dhruvsharma@Dhruvs-MacBook-Pro-2 technical % grep -i "legal" government/About_LSC/ODonnell_et_al_v_LSCdecision.txt 
HUGH F. O'DONNELL, Executive � Director of Client Centered Legal
Services of Southwest Virginia, Incorporated; CLIENT CENTERED LEGAL
JOHN EIDLEMAN, Program Specialist for the Legal Services
Corporation; LEGAL SERVICES CORPORATION; JOHN MCKAY, President of
the Legal Services Corporation,
Client Centered Legal Services of Southwest Virginia,
granting judgment in favor of the Legal Services Corporation and
In 1974, Congress enacted the Legal Service Corporation Act
("LSCA"), which created the LSC for the purpose of providing legal
2996 (West 1994). The LSC does not itself provide legal services,
but rather grants federal funds to legal services programs across
the country. CCLS, which provides legal services to indigent people
In our recent decision in Regional Management Corp. v. Legal
specifically intended the LSCA to benefit "indigents who have legal
grievances but who are unable to afford the legal means necessary
the "especial benefit" of indigent persons in need of legal
services. Although legal services programs such as CCLS are an
affect grantees. See Tex. Rural Legal Aid, Inc. v. Legal Servs.
(D.C. Cir. 1991); San Juan Legal Servs., Inc. v. Legal Servs.
Corp., 655 F.2d 434, 438-39 (1st Cir. 1981); Spokane County Legal
Servs., Inc. v. Legal Servs. Corp., 614 F.2d 662, 668-69 (9th Cir.
```
