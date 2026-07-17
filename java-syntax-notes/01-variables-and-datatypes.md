# 01 — Variables & Data Types

## Variable কী?
মেমোরিতে data রাখার জায়গা।

---

## Syntax
```java
dataType variableName = value;
```

---

## সব Data Types

```java
// ── INTEGER (whole number) ──
byte   b = 10;           // -128 to 127
short  s = 1000;         // -32768 to 32767
int    i = 100000;       // সবচেয়ে বেশি ব্যবহৃত
long   l = 9999999999L;  // শেষে L লাগবে

// ── DECIMAL ──
float  f = 3.14f;        // শেষে f লাগবে
double d = 3.14159;      // সবচেয়ে বেশি ব্যবহৃত

// ── CHARACTER ──
char c = 'A';            // single quote

// ── BOOLEAN ──
boolean isPass = true;   // true অথবা false

// ── STRING ──
String name = "Rian";    // double quote
```

---

## Multiple Variables একসাথে

```java
int a = 10, b = 20, c = 30;
```

---

## Default Values (declare করলে value না দিলে)

| Type | Default |
|------|---------|
| int | 0 |
| double | 0.0 |
| boolean | false |
| char | '\u0000' |
| String | null |

---

## Constants (পরিবর্তন হবে না)

```java
final double PI = 3.14159;
final int MAX = 100;
```

---

## নামকরণের নিয়ম

```java
// ✅ সঠিক
int age = 20;
String studentName = "Rian";
double totalMarks = 95.5;

// ❌ ভুল
int 1age = 20;       // সংখ্যা দিয়ে শুরু
int class = 10;      // keyword ব্যবহার
int my age = 20;     // মাঝে space
```

---

## Example Program

```java
public class VariableDemo {
    public static void main(String[] args) {
        String name = "Rian";
        int age = 20;
        double cgpa = 3.75;
        boolean isStudent = true;

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("CGPA: " + cgpa);
        System.out.println("Student: " + isStudent);
    }
}
```

**Output:**
```
Name: Rian
Age: 20
CGPA: 3.75
Student: true
```
