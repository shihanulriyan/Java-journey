# 05 — If-Else & Switch

## Basic If

```java
if (condition) {
    // condition true হলে চলবে
}
```

---

## If-Else

```java
if (condition) {
    // true হলে
} else {
    // false হলে
}
```

---

## If-Else If-Else

```java
if (marks >= 80) {
    System.out.println("A+");
} else if (marks >= 70) {
    System.out.println("A");
} else if (marks >= 60) {
    System.out.println("B");
} else if (marks >= 50) {
    System.out.println("C");
} else {
    System.out.println("Fail");
}
```

---

## Nested If

```java
if (age >= 18) {
    if (hasID == true) {
        System.out.println("Entry allowed");
    } else {
        System.out.println("No ID card");
    }
} else {
    System.out.println("Under age");
}
```

---

## Ternary Operator (একলাইনে if-else)

```java
// Syntax: condition ? valueIfTrue : valueIfFalse

int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println(max); // 20

// String দিয়েও
String result = (marks >= 50) ? "Pass" : "Fail";
System.out.println(result);
```

---

## Switch Statement

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Other day");
        break;
}
```

> ⚠️ `break` না দিলে পরের case-ও run হবে!

---

## Switch with String

```java
String color = "red";

switch (color) {
    case "red":
        System.out.println("Red color");
        break;
    case "blue":
        System.out.println("Blue color");
        break;
    default:
        System.out.println("Unknown color");
}
```

---

## Example — Calculator

```java
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("Enter num1: "); int a = input.nextInt();
        System.out.print("Operator (+,-,*,/): "); char op = input.next().charAt(0);
        System.out.print("Enter num2: "); int b = input.nextInt();

        switch (op) {
            case '+': System.out.println(a + b); break;
            case '-': System.out.println(a - b); break;
            case '*': System.out.println(a * b); break;
            case '/': System.out.println(b != 0 ? (double)a/b : "Error"); break;
            default:  System.out.println("Invalid operator");
        }
    }
}
```
