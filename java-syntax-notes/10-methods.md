# 10 — Methods (Function)

## Method কী?
কোডের একটা block যেটা বারবার ব্যবহার করা যায়।

---

## Syntax

```java
returnType methodName(parameter1, parameter2, ...) {
    // body
    return value;  // returnType void হলে লাগে না
}
```

---

## ৪ ধরনের Method

```java
// 1. কিছু নেয় না, কিছু দেয় না
static void greet() {
    System.out.println("Hello!");
}

// 2. কিছু নেয়, কিছু দেয় না
static void greetUser(String name) {
    System.out.println("Hello " + name);
}

// 3. কিছু নেয় না, কিছু দেয়
static int getNumber() {
    return 42;
}

// 4. কিছু নেয়, কিছু দেয় (সবচেয়ে বেশি ব্যবহৃত)
static int add(int a, int b) {
    return a + b;
}
```

---

## Method Call করার নিয়ম

```java
public class MethodDemo {

    static int add(int a, int b) {
        return a + b;
    }

    static boolean isEven(int n) {
        return n % 2 == 0;
    }

    static String getGrade(int marks) {
        if (marks >= 80) return "A+";
        else if (marks >= 70) return "A";
        else if (marks >= 60) return "B";
        else return "Fail";
    }

    public static void main(String[] args) {
        int result = add(5, 3);
        System.out.println(result);          // 8

        System.out.println(isEven(10));      // true
        System.out.println(isEven(7));       // false

        System.out.println(getGrade(85));    // A+
        System.out.println(getGrade(55));    // Fail
    }
}
```

---

## Return Types

```java
static int    getInt()     { return 10; }
static double getDouble()  { return 3.14; }
static boolean getBool()   { return true; }
static String getString()  { return "Hello"; }
static char   getChar()    { return 'A'; }
static void   doSomething(){ System.out.println("done"); }
```

---

## Method Overloading (একই নাম, আলাদা parameter)

```java
static int add(int a, int b) {
    return a + b;
}

static double add(double a, double b) {
    return a + b;
}

static int add(int a, int b, int c) {
    return a + b + c;
}

// Call
add(5, 3);          // 8
add(2.5, 3.5);      // 6.0
add(1, 2, 3);       // 6
```

---

## Recursive Method (নিজেকে নিজে call করে)

```java
// Factorial
static int factorial(int n) {
    if (n == 0) return 1;        // base case
    return n * factorial(n - 1); // recursive call
}

// Fibonacci
static int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

---

## Common Utility Methods

```java
// Swap
static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Array sum
static int arraySum(int[] arr) {
    int sum = 0;
    for (int x : arr) sum += x;
    return sum;
}

// isPrime
static boolean isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i < n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```
