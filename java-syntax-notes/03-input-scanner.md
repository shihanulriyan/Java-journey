# 03 — Input (Scanner)

## Scanner Import করতে হয়

```java
import java.util.Scanner;
```

---

## Scanner Object বানানো

```java
Scanner input = new Scanner(System.in);
```

---

## সব ধরনের Input নেওয়ার Syntax

```java
Scanner input = new Scanner(System.in);

int    a = input.nextInt();        // integer
long   b = input.nextLong();       // long number
double c = input.nextDouble();     // decimal
float  d = input.nextFloat();      // float
String e = input.next();           // একটা word
String f = input.nextLine();       // পুরো line (space সহ)
char   g = input.next().charAt(0); // একটা character
boolean h = input.nextBoolean();   // true / false
```

---

## সম্পূর্ণ Template

```java
import java.util.Scanner;

public class InputDemo {
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = input.nextLine();

        System.out.print("Enter your age: ");
        int age = input.nextInt();

        System.out.print("Enter your CGPA: ");
        double cgpa = input.nextDouble();

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("CGPA: " + cgpa);
    }
}
```

---

## ⚠️ সাধারণ ভুল — nextInt() এর পরে nextLine()

```java
int age = input.nextInt();
input.nextLine();           // ← এই line টা দিতে হবে! না দিলে nextLine skip হয়
String name = input.nextLine();
```

---

## Multiple Values একই Line এ

```java
// Input: 10 20
int a = input.nextInt();
int b = input.nextInt();
System.out.println(a + b); // 30
```

---

## ⚠️ Terminal থেকে Run করতে হবে!

Scanner দিয়ে input নিলে VS Code এর Run button কাজ করে না।

```bash
# Terminal এ এই command দাও
javac InputDemo.java
java InputDemo
```
