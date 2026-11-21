# 20 — Useful Code Patterns

> Assignment এ বারবার আসে এমন program গুলোর ছাঁচ।
> প্রতিটা `static` method — class এর ভেতরে বসিয়ে `main` থেকে call করলেই চলবে।

---

## Prime Number

```java
static boolean isPrime(int n) {
    boolean prime = true;

    if (n < 2) {
        prime = false;                       // 0, 1 prime না
    } else {
        for (int i = 2; i * i <= n; i++) {   // √n পর্যন্ত দেখলেই যথেষ্ট
            if (n % i == 0) {
                prime = false;
                break;                       // একটা ভাগ হলেই আর দেখার দরকার নেই
            }
        }
    }
    return prime;
}

// m থেকে n এর মধ্যে সব prime + মোট কতটা
static void primesInRange(int m, int n) {
    int count = 0;

    for (int i = m; i <= n; i++) {
        if (isPrime(i)) {
            System.out.println(i);
            count++;
        }
    }
    System.out.println("Total = " + count);
}

// isPrime(7)  → true
// isPrime(10) → false
// isPrime(1)  → false
// primesInRange(1, 10) → 2, 3, 5, 7 (আলাদা আলাদা line এ), তারপর Total = 4
```

> ⚠️ Nested loop এ প্রতিবার ভুল হয়: flag/count **reset না করা**, আর result print `break` এর পরে loop এর **ভেতরে** রাখা।
> Method বানালে প্রতিবার নতুন variable পাওয়া যায় — তাই reset এর ভুল হয় না।

---

## Factorial

```java
static long factorial(int n) {
    long fact = 1;                    // 0 না — 1 দিয়ে শুরু (গুণের শুরু সবসময় 1)

    for (int i = 1; i <= n; i++) {
        fact = fact * i;
    }
    return fact;
}

// factorial(5) → 120
// factorial(0) → 1   (আলাদা if লাগে না)
```

> `int` এ 12! পর্যন্ত ধরে, 13! থেকে overflow। তাই `long` নিয়েছি (20! পর্যন্ত ঠিক)।

---

## Fibonacci (প্রথম n টা term)

```java
static void fibonacci(int n) {
    int a = 0, b = 1;

    for (int i = 1; i <= n; i++) {
        System.out.print(a + " ");
        int next = a + b;
        a = b;
        b = next;
    }
    System.out.println();
}

// fibonacci(7) → 0 1 1 2 3 5 8
```

> প্রথম দুইটা আলাদা print করা লাগে না — এভাবে `n = 1` হলেও ঠিক চলে।
> প্রতি লাইনে চাইলে `print(a + " ")` এর জায়গায় `println(a)`।

---

## Reverse & Palindrome (number)

```java
static int reverse(int num) {
    int rev = 0;

    while (num != 0) {
        int r = num % 10;           // শেষ digit
        rev = rev * 10 + r;         // reverse এর পিছনে বসাও
        num = num / 10;             // শেষ digit বাদ
    }
    return rev;
}

static boolean isPalindrome(int num) {      // positive number ধরে
    return reverse(num) == num;             // original num এর সাথে তুলনা
}

// reverse(123)      → 321
// isPalindrome(121) → true
// isPalindrome(123) → false
```

> ⚠️ Loop এর ভেতরে যে variable বদলাতে থাকে (`temp`), loop শেষে সেটা `0` হয়ে যায়।
> তাই তার সাথে তুলনা করা যায় না — তুলনা হবে **original number** এর সাথে।
> String palindrome → `08-strings.md`

---

## Sum of Digits / Count Digits

```java
static int sumOfDigits(int num) {
    int sum = 0;

    while (num != 0) {
        sum += num % 10;
        num /= 10;
    }
    return sum;
}

static int countDigits(int num) {
    if (num == 0) return 1;         // 0 তেও 1 টা digit

    int count = 0;
    while (num != 0) {
        count++;
        num /= 10;
    }
    return count;
}

// sumOfDigits(1234) → 10
// countDigits(1234) → 4
// countDigits(0)    → 1
```

---

## Armstrong Number (যেকোনো digit এর জন্য)

```java
static int power(int base, int exp) {
    int result = 1;

    for (int i = 1; i <= exp; i++) {
        result = result * base;
    }
    return result;
}

static boolean isArmstrong(int num) {
    int len = countDigits(num);         // countDigits ওপরের section এ আছে
    int temp = num, sum = 0;

    while (temp != 0) {
        sum += power(temp % 10, len);   // প্রতিটা digit কে (digit সংখ্যা) ঘাত
        temp /= 10;
    }
    return sum == num;
}

// 0 থেকে 10000 এর মধ্যে Armstrong:
// 0 1 2 3 4 5 6 7 8 9 153 370 371 407 1634 8208 9474
```

- `153` → 1³ + 5³ + 3³ = 153 (3 digit, তাই ঘন)
- `1634` → 1⁴ + 6⁴ + 3⁴ + 4⁴ = 1634 (4 digit, তাই চতুর্থ ঘাত)

> শুধু `r*r*r` নিলে 3 digit এ ঠিক, কিন্তু 1 digit (0–9) আলাদা `if` দিয়ে ধরতে হয়।
> `len` ঘাত নিলে সব digit এর জন্য নিজে নিজেই ঠিক আসে।

---

## Perfect Number

```java
static boolean isPerfect(int n) {
    if (n < 2) return false;

    int sum = 0;
    for (int i = 1; i < n; i++) {
        if (n % i == 0) {
            sum += i;               // n এর নিজেকে বাদে সব উৎপাদক যোগ
        }
    }
    return sum == n;
}

// isPerfect(6)  → true   (1 + 2 + 3)
// isPerfect(28) → true
// isPerfect(12) → false
```

---

## GCD & LCM

```java
static int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

static int lcm(int a, int b) {
    return (a / gcd(a, b)) * b;     // আগে ভাগ করলে overflow কম হয়
}

// gcd(12, 18) → 6
// lcm(12, 18) → 36
```

---

## Leap Year

```java
static boolean isLeapYear(int year) {
    return (year % 400 == 0) || (year % 4 == 0 && year % 100 != 0);
}

// isLeapYear(2024) → true
// isLeapYear(2000) → true
// isLeapYear(1900) → false
```

---

## Swap দুইটা সংখ্যা

```java
// main এর ভেতরে
int temp = a;
a = b;
b = temp;
```

> ⚠️ Swap আলাদা method এ করলে কাজ করে না — Java তে `int` এর copy যায়। Array এর ভেতরে swap করলে চলে (নিচে bubble sort)।

---

## Multiplication Table

```java
static void table(int n) {
    for (int i = 1; i <= 10; i++) {
        System.out.println(n + " x " + i + " = " + (n * i));
    }
}

// table(5) → 5 x 1 = 5 ... 5 x 10 = 50
```

---

## Star / Number Pattern

নিয়ম: **বাইরের loop = row (সারি)**, **ভেতরের loop = column (কলাম)**।
ভেতরের loop এ `print` (একই line এ), ভেতরের loop শেষে `println()` (নতুন line)।

```java
static void rightTriangle(int n) {
    for (int i = 1; i <= n; i++) {              // i = row
        for (int j = 1; j <= i; j++) {          // j = column
            System.out.print("*");
        }
        System.out.println();                   // row শেষ → নতুন line
    }
}

static void invertedTriangle(int n) {
    for (int i = n; i >= 1; i--) {
        for (int j = 1; j <= i; j++) {
            System.out.print("*");
        }
        System.out.println();
    }
}

static void pyramid(int n) {
    for (int i = 1; i <= n; i++) {
        for (int s = 1; s <= n - i; s++) {          // আগে space
            System.out.print(" ");
        }
        for (int j = 1; j <= 2 * i - 1; j++) {      // তারপর star
            System.out.print("*");
        }
        System.out.println();
    }
}

static void numberTriangle(int n) {
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            System.out.print(j + " ");
        }
        System.out.println();
    }
}
```

`n = 4` দিলে:

```
rightTriangle    invertedTriangle    pyramid    numberTriangle
*                ****                   *       1
**               ***                   ***      1 2
***              **                   *****     1 2 3
****             *                   *******    1 2 3 4
```

---

## Array Operations (নিজে লেখা, library ছাড়া)

```java
static void reverseArray(int[] arr) {
    for (int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - 1 - i];
        arr[arr.length - 1 - i] = temp;
    }
}

static void bubbleSort(int[] arr) {
    int n = arr.length;

    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];              // swap
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;                           // পাওয়া গেলে index
        }
    }
    return -1;                                  // না পেলে -1
}

static int binarySearch(int[] arr, int target) {    // arr আগে sort করা থাকতে হবে
    int low = 0, high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;                      // ডান অর্ধেকে খোঁজো
        } else {
            high = mid - 1;                     // বাম অর্ধেকে খোঁজো
        }
    }
    return -1;
}

// arr = {5, 2, 8, 1, 9}
// reverseArray(arr)    → {9, 1, 8, 2, 5}
// bubbleSort(arr)      → {1, 2, 5, 8, 9}
// linearSearch(arr, 8) → 3   (sort এর পরের arr এ)
// binarySearch(arr, 8) → 3   (sort করা arr এ)
// linearSearch(arr, 7) → -1
```

---

## Menu-Driven Program

```java
import java.util.Scanner;

public class MenuDemo {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int choice;

        do {
            System.out.println();
            System.out.println("1. Even/Odd");
            System.out.println("2. Square");
            System.out.println("0. Exit");
            System.out.print("Choice: ");
            choice = input.nextInt();

            switch (choice) {
                case 1: {                       // case এর ভেতরে variable বানালে { } দাও
                    System.out.print("Enter number: ");
                    int n = input.nextInt();
                    System.out.println(n % 2 == 0 ? "Even" : "Odd");
                    break;
                }
                case 2: {
                    System.out.print("Enter number: ");
                    int n = input.nextInt();
                    System.out.println("Square = " + (n * n));
                    break;
                }
                case 0:
                    System.out.println("Bye!");
                    break;
                default:
                    System.out.println("Invalid choice");
            }
        } while (choice != 0);              // 0 না দেওয়া পর্যন্ত ঘুরতে থাকবে
    }
}
```

---

## Common Mistakes Checklist

| ভুল | ঠিক |
|-----|-----|
| গুণের result `0` দিয়ে শুরু (factorial) | `1` দিয়ে শুরু |
| Nested loop এ `count`/flag reset না করা | ভেতরের loop শুরুর আগে reset |
| `break` এর পরেও code চলবে ভাবা | Check/print loop এর **বাইরে** |
| Prime এ `i <= num` | `i < num` অথবা `i * i <= num` |
| Palindrome এ `temp == rev` | `num == rev` |
| String compare এ `==` | `equals()` |
| `nextInt()` এর পর `nextLine()` | মাঝে একটা বাড়তি `input.nextLine()` |
| `if (a = b)` | `if (a == b)` |
| File এর নাম ≠ class এর নাম | `Test.java` ↔ `public class Test` |
| Scanner program Output panel এ চালানো | Terminal এ `javac` + `java` |
