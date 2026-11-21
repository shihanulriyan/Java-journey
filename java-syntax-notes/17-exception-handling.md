# 17 — Exception Handling

## Exception কী?
Program চলার সময় হঠাৎ যে সমস্যা হয় (যেমন 0 দিয়ে ভাগ, array এর বাইরে index)।
Handle না করলে program **crash** করে।

---

## try-catch-finally Syntax

```java
try {
    // যে code এ সমস্যা হতে পারে
} catch (ExceptionType e) {
    // সমস্যা হলে এখানে আসবে
} finally {
    // সমস্যা হোক বা না হোক — সবসময় চলবে (ঐচ্ছিক)
}
```

---

## Example

```java
public class TryCatchDemo {
    public static void main(String[] args) {
        try {
            int a = 10, b = 0;
            int c = a / b;                    // ArithmeticException
            System.out.println(c);
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero");
        } finally {
            System.out.println("This always runs");
        }

        System.out.println("Program continues");
    }
}
```

**Output:**
```
Cannot divide by zero
This always runs
Program continues
```

> `try` এর যে line এ exception হয়, তার নিচের বাকি line গুলো আর চলে না — সোজা `catch` এ চলে যায়।

---

## একাধিক catch

```java
public class MultiCatchDemo {
    public static void main(String[] args) {
        try {
            int[] arr = new int[3];
            arr[5] = 10;                            // ArrayIndexOutOfBoundsException
        } catch (ArithmeticException e) {
            System.out.println("Math error");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Invalid index: " + e.getMessage());
        } catch (Exception e) {                     // সবার শেষে — বাকি সব exception ধরে
            System.out.println("Other error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Invalid index: Index 5 out of bounds for length 3
```

> ⚠️ `catch (Exception e)` সবার **শেষে** দিতে হয়। আগে দিলে নিচের catch গুলো কখনো পৌঁছায় না → compile error।

একই কাজ হলে এক catch এ একাধিক:

```java
catch (ArithmeticException | NullPointerException e) {
    System.out.println("Problem: " + e.getMessage());
}
```

---

## Exception এর তথ্য

```java
e.getMessage();        // কী সমস্যা — ছোট message
e.printStackTrace();   // কোন line এ হয়েছে — পুরো তথ্য (debug এর জন্য)
```

---

## সাধারণ Exception গুলো

| Exception | কখন হয় |
|-----------|---------|
| `ArithmeticException` | `int` কে 0 দিয়ে ভাগ |
| `ArrayIndexOutOfBoundsException` | array এর বাইরের index |
| `StringIndexOutOfBoundsException` | String এর বাইরের index |
| `NullPointerException` | `null` এর উপর method call |
| `NumberFormatException` | `Integer.parseInt("abc")` |
| `InputMismatchException` | Scanner এ number চাইলে text দিলে |
| `ClassCastException` | ভুল downcast |
| `FileNotFoundException` | file পাওয়া যায়নি |

> `double` কে 0 দিয়ে ভাগ করলে exception হয় না — `Infinity` আসে। শুধু `int` এ হয়।

---

## throw — নিজে exception ছোড়া

```java
public class ThrowDemo {

    static void checkAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be 18 or more");
        }
        System.out.println("Allowed");
    }

    public static void main(String[] args) {
        try {
            checkAge(20);
            checkAge(15);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Allowed
Error: Age must be 18 or more
```

---

## throws — method এর মাথায় সতর্কবার্তা

```java
static void readData() throws IOException {
    // এখানে IOException হতে পারে
    // handle করার দায়িত্ব এই method কে যে call করবে তার
}
```

---

## Checked vs Unchecked

| | Checked | Unchecked |
|--|---------|-----------|
| Compiler কী করে | handle বা `throws` না করলে **error** | কিছু বলে না |
| উদাহরণ | `IOException`, `FileNotFoundException` | `ArithmeticException`, `NullPointerException` |
| কারণ | বাইরের জিনিসের সমস্যা (file, network) | সাধারণত programmer এর ভুল |

---

## Custom Exception (নিজের exception)

```java
class InvalidMarksException extends Exception {
    InvalidMarksException(String message) {
        super(message);
    }
}

public class CustomExceptionDemo {

    static void check(int marks) throws InvalidMarksException {
        if (marks < 0 || marks > 100) {
            throw new InvalidMarksException("Marks must be 0-100");
        }
        System.out.println("Marks OK: " + marks);
    }

    public static void main(String[] args) {
        try {
            check(85);
            check(150);
        } catch (InvalidMarksException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Marks OK: 85
Error: Marks must be 0-100
```

---

## Scanner Input Validation (সবচেয়ে বেশি কাজে লাগে)

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class SafeInput {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int num = 0;
        boolean valid = false;

        while (!valid) {
            try {
                System.out.print("Enter a number: ");
                num = input.nextInt();
                valid = true;                       // সফল হলে loop শেষ
            } catch (InputMismatchException e) {
                System.out.println("That is not a number. Try again.");
                input.next();                       // ভুল input টা ফেলে দাও
            }
        }

        System.out.println("You entered: " + num);
    }
}
```

> ⚠️ `input.next()` না দিলে ভুল text Scanner এ আটকে থাকে → loop **অনন্তকাল** ঘুরবে।

---

## try-with-resources (file/Scanner নিজে নিজে বন্ধ হয়)

```java
try (Scanner sc = new Scanner(System.in)) {
    int x = sc.nextInt();
    System.out.println(x);
}   // এখানে sc নিজে নিজে close হয়ে যায়
```

File নিয়ে বিস্তারিত → `19-file-readwrite.md`
