# CSE 15L lab report 3
---

## **Part 1**

The bug I will be testing or working with is the bugs involved in `ArrayExamples.java`. Specifically, the bug found in the `reveresed` method.

A failure inducing input for the buggy program as a JUnit test:
```
@Test
  public void testReversed3Ints() {
    int[] input3Ints = {1,2,3};
    assertArrayEquals(new int[]{3,2,1}, ArrayExamples.reversed(input3Ints));
  }
```
A non-failure inducing input for the program as a JUnit test:
```
@Test
  public void testReversedNothing() {
    int[] inputEmpty = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(inputEmpty));
  }
```
