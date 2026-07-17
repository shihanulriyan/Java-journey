# 02 — Operators

## Arithmetic Operators (গণিত)

```java
int a = 10, b = 3;

System.out.println(a + b);   // 13  (যোগ)
System.out.println(a - b);   // 7   (বিয়োগ)
System.out.println(a * b);   // 30  (গুণ)
System.out.println(a / b);   // 3   (ভাগ — দশমিক কাটা যাবে!)
System.out.println(a % b);   // 1   (ভাগশেষ)
```

> ⚠️ `10 / 3 = 3` (integer division — দশমিক পাবে না)
> দশমিক পেতে: `10.0 / 3` অথবা `(double) 10 / 3`

---

## Relational Operators (তুলনা → true/false দেয়)

```java
int a = 10, b = 5;

System.out.println(a > b);    // true
System.out.println(a < b);    // false
System.out.println(a >= b);   // true
System.out.println(a <= b);   // false
System.out.println(a == b);   // false  (সমান কিনা)
System.out.println(a != b);   // true   (অসমান কিনা)
```

---

## Logical Operators (যুক্তি)

```java
// && (AND) — দুটোই true হলে true
System.out.println(5 > 3 && 10 > 7);   // true
System.out.println(5 > 3 && 10 < 7);   // false

// || (OR) — যেকোনো একটা true হলে true
System.out.println(5 > 3 || 10 < 7);   // true
System.out.println(5 < 3 || 10 < 7);   // false

// ! (NOT) — উল্টো করে
System.out.println(!true);    // false
System.out.println(!false);   // true
```

---

## Assignment Operators

```java
int a = 10;

a += 5;   // a = a + 5 = 15
a -= 3;   // a = a - 3 = 12
a *= 2;   // a = a * 2 = 24
a /= 4;   // a = a / 4 = 6
a %= 4;   // a = a % 4 = 2
```

---

## Increment / Decrement

```java
int a = 5;

a++;   // a = 6  (পরে বাড়ায়)
++a;   // a = 7  (আগে বাড়ায়)
a--;   // a = 6  (পরে কমায়)
--a;   // a = 5  (আগে কমায়)
```

> ⚠️ পার্থক্য:
> ```java
> int a = 5;
> System.out.println(a++);  // 5 print হবে, তারপর a=6
> System.out.println(++a);  // আগে a=7, তারপর 7 print
> ```

---

## Example Program

```java
public class OperatorDemo {
    public static void main(String[] args) {
        int a = 15, b = 4;

        System.out.println("যোগ: " + (a + b));
        System.out.println("ভাগশেষ: " + (a % b));
        System.out.println("সমান?: " + (a == b));
        System.out.println("AND: " + (a > 10 && b < 10));
    }
}
```

**Output:**
```
যোগ: 19
ভাগশেষ: 3
সমান?: false
AND: true
```
