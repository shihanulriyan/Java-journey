# 04 — Type Casting

## দুই ধরনের Casting

### 1. Widening (Automatic) — ছোট → বড়
Java নিজেই করে, কিছু লিখতে হয় না।

```java
int    a = 10;
long   b = a;      // int → long ✅
double c = a;      // int → double ✅
float  d = a;      // int → float ✅

System.out.println(c); // 10.0
```

**ক্রম:** `byte → short → int → long → float → double`

---

### 2. Narrowing (Manual) — বড় → ছোট
নিজে লিখতে হয়, data হারিয়ে যেতে পারে।

```java
double d = 9.99;
int    i = (int) d;     // 9 — দশমিক কাটা যাবে!

long   l = 1000L;
int    a = (int) l;     // 1000

float  f = 3.14f;
int    b = (int) f;     // 3
```

---

## int ↔ char Casting

```java
char c = 'A';
int  i = c;             // 65 (ASCII value)
System.out.println(i);  // 65

int  n = 66;
char ch = (char) n;
System.out.println(ch); // B
```

---

## int ↔ String Convert

```java
// int → String
int    num = 100;
String s1  = String.valueOf(num);     // "100"
String s2  = Integer.toString(num);   // "100"
String s3  = "" + num;                // "100"  (সবচেয়ে সহজ)

// String → int
String s   = "42";
int    n   = Integer.parseInt(s);     // 42
```

---

## double ↔ String Convert

```java
// double → String
double d = 3.14;
String s = String.valueOf(d);         // "3.14"

// String → double
String s2 = "3.14";
double d2 = Double.parseDouble(s2);   // 3.14
```

---

## Division এ দশমিক পেতে

```java
int a = 7, b = 2;

System.out.println(a / b);             // 3   (ভুল!)
System.out.println((double) a / b);    // 3.5 (সঠিক)
System.out.println(a / (double) b);    // 3.5 (সঠিক)
```

---

## Example Program

```java
public class CastingDemo {
    public static void main(String[] args) {
        double price = 99.99;
        int    intPrice = (int) price;       // 99

        int    score = 85;
        double percent = (double) score / 100 * 100;

        String numStr = "250";
        int    num = Integer.parseInt(numStr);

        System.out.println("Int Price: " + intPrice);
        System.out.println("Percent: " + percent);
        System.out.println("Parsed: " + num);
    }
}
```
