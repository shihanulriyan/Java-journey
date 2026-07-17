# 07 — Arrays

## 1D Array

```java
// Declare করার উপায়
int[] arr = new int[5];              // size 5, সব 0
int[] arr = {10, 20, 30, 40, 50};   // সরাসরি value
```

---

## Access ও Modify

```java
int[] arr = {10, 20, 30, 40, 50};

System.out.println(arr[0]);     // 10 (প্রথম)
System.out.println(arr[4]);     // 50 (শেষ)
System.out.println(arr.length); // 5  (size)

arr[2] = 99;                    // value বদলানো
```

> ⚠️ Index সবসময় `0` থেকে শুরু, `length-1` পর্যন্ত।

---

## Loop দিয়ে Print

```java
int[] arr = {10, 20, 30, 40, 50};

// For loop
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// For-each (সহজ)
for (int x : arr) {
    System.out.println(x);
}
```

---

## Array Input নেওয়া

```java
Scanner input = new Scanner(System.in);
int n = input.nextInt();
int[] arr = new int[n];

for (int i = 0; i < n; i++) {
    arr[i] = input.nextInt();
}
```

---

## Common Operations

```java
int[] arr = {5, 2, 8, 1, 9, 3};

// Sum
int sum = 0;
for (int x : arr) sum += x;

// Max
int max = arr[0];
for (int x : arr) {
    if (x > max) max = x;
}

// Min
int min = arr[0];
for (int x : arr) {
    if (x < min) min = x;
}

// Search
int target = 8;
boolean found = false;
for (int x : arr) {
    if (x == target) { found = true; break; }
}
```

---

## 2D Array (Matrix)

```java
int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};

// Access
System.out.println(matrix[1][2]); // 6

// Print
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

**Output:**
```
1 2 3
4 5 6
7 8 9
```
