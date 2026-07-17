# 06 — Loops

## For Loop

```java
// Syntax
for (initialization; condition; update) {
    // body
}

// Example: 1 থেকে 5 print
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}

// উল্টো দিকে
for (int i = 5; i >= 1; i--) {
    System.out.println(i);
}

// দুই করে বাড়ানো
for (int i = 0; i <= 10; i += 2) {
    System.out.println(i);  // 0 2 4 6 8 10
}
```

---

## While Loop

```java
// Syntax
while (condition) {
    // body
}

// Example
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

---

## Do-While Loop (কমপক্ষে একবার চলবেই)

```java
// Syntax
do {
    // body
} while (condition);

// Example
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

---

## For vs While vs Do-While

| | For | While | Do-While |
|--|-----|-------|----------|
| কবে ব্যবহার | কতবার চলবে জানা | কতবার জানা নেই | কমপক্ষে ১ বার |
| Check কখন | আগে | আগে | পরে |

---

## Break & Continue

```java
// break — loop বন্ধ করে
for (int i = 1; i <= 10; i++) {
    if (i == 5) break;
    System.out.println(i);  // 1 2 3 4
}

// continue — এই step skip করে
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.println(i);  // 1 2 4 5
}
```

---

## Nested Loop (loop এর ভেতরে loop)

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.print(i * j + " ");
    }
    System.out.println();
}
```

**Output:**
```
1 2 3
2 4 6
3 6 9
```

---

## Common Loop Patterns

```java
// ── Sum of 1 to n ──
int sum = 0;
for (int i = 1; i <= n; i++) {
    sum += i;
}

// ── Factorial ──
int result = 1;
for (int i = 1; i <= n; i++) {
    result *= i;
}

// ── Digit বের করা ──
while (num != 0) {
    int r = num % 10;   // শেষ digit
    num = num / 10;     // digit বাদ দাও
}

// ── Input নেওয়া যতক্ষণ সঠিক না হয় ──
Scanner input = new Scanner(System.in);
int num;
do {
    System.out.print("Enter positive number: ");
    num = input.nextInt();
} while (num <= 0);
```
