# 18 — ArrayList & Collections

## ArrayList কী?
Size বদলানো যায় এমন array। Array এর size fixed, ArrayList দরকার মতো বাড়ে-কমে।

| | Array | ArrayList |
|--|-------|-----------|
| Size | fixed | বাড়ে-কমে |
| Type | `int`, `double` সরাসরি চলে | শুধু object (`Integer`, `String`...) |
| Length | `arr.length` | `list.size()` |
| Access | `arr[i]` | `list.get(i)` |

---

## Syntax

```java
import java.util.ArrayList;

ArrayList<Integer> nums  = new ArrayList<>();
ArrayList<String>  names = new ArrayList<>();
```

`<>` এর ভেতরে primitive type চলে না — wrapper type লিখতে হয়:

| Primitive | Wrapper |
|-----------|---------|
| `int` | `Integer` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

---

## সব গুরুত্বপূর্ণ Method

```java
ArrayList<String> list = new ArrayList<>();

list.add("Rian");            // শেষে যোগ
list.add("Karim");
list.add("Anis");            // [Rian, Karim, Anis]

list.add(1, "Rahim");        // index 1 এ যোগ → [Rian, Rahim, Karim, Anis]
list.get(0);                 // "Rian"
list.set(2, "Sakib");        // index 2 বদলানো → [Rian, Rahim, Sakib, Anis]

list.size();                 // 4
list.contains("Anis");       // true
list.indexOf("Anis");        // 3
list.isEmpty();              // false

list.remove(1);              // index ধরে মোছা → [Rian, Sakib, Anis]
list.remove("Anis");         // value ধরে মোছা → [Rian, Sakib]

System.out.println(list);    // পুরো list একসাথে print হয়: [Rian, Sakib]

list.clear();                // সব মোছা → []
```

---

## ⚠️ Integer list এ remove এর ফাঁদ

```java
ArrayList<Integer> nums = new ArrayList<>();
nums.add(10);
nums.add(20);
nums.add(30);

nums.remove(1);                       // index 1 মোছে → [10, 30]
nums.remove(Integer.valueOf(30));     // value 30 মোছে → [10]
```

`int` দিলে Java ধরে নেয় এটা **index**। Value মুছতে চাইলে `Integer.valueOf(...)` লিখতে হয়।

---

## Loop দিয়ে ঘোরা

```java
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

for (String s : list) {              // for-each (সহজ)
    System.out.println(s);
}
```

---

## Sort, Reverse, Max, Min

```java
import java.util.ArrayList;
import java.util.Collections;

ArrayList<Integer> nums = new ArrayList<>();
nums.add(5);
nums.add(2);
nums.add(9);
nums.add(1);

Collections.sort(nums);        // [1, 2, 5, 9]
Collections.reverse(nums);     // [9, 5, 2, 1]
Collections.max(nums);         // 9
Collections.min(nums);         // 1
```

---

## Object এর ArrayList

```java
import java.util.ArrayList;

class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }
}

public class StudentListDemo {
    public static void main(String[] args) {
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student("Rian", 85));
        students.add(new Student("Karim", 72));

        for (Student s : students) {
            System.out.println(s.name + " - " + s.marks);
        }
    }
}
```

---

## Example Program

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

public class ArrayListDemo {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        ArrayList<Integer> nums = new ArrayList<>();

        System.out.println("Enter numbers (0 to stop):");
        while (true) {
            int x = input.nextInt();
            if (x == 0) break;
            nums.add(x);
        }

        if (nums.isEmpty()) {
            System.out.println("No numbers entered");
        } else {
            int sum = 0;
            for (int x : nums) sum += x;

            System.out.println("Count: " + nums.size());
            System.out.println("Sum: " + sum);
            System.out.println("Max: " + Collections.max(nums));

            Collections.sort(nums);
            System.out.println("Sorted: " + nums);
        }
    }
}
```

**Input:** `5 3 8 0`

**Output:**
```
Count: 3
Sum: 16
Max: 8
Sorted: [3, 5, 8]
```

---

## HashMap (key → value)

```java
import java.util.HashMap;

HashMap<String, Integer> marks = new HashMap<>();

marks.put("Rian", 85);              // key, value
marks.put("Karim", 72);

marks.get("Rian");                  // 85
marks.containsKey("Anis");          // false
marks.getOrDefault("Anis", 0);      // 0  (key না থাকলে default)
marks.put("Rian", 90);              // একই key আবার দিলে value বদলে যায়
marks.remove("Karim");
marks.size();                       // 1

for (String key : marks.keySet()) {
    System.out.println(key + " = " + marks.get(key));
}
```

> HashMap এ ঢোকানোর ক্রমে print হবে — এমন নিশ্চয়তা নেই।

---

## HashSet (duplicate নেয় না)

```java
import java.util.HashSet;

HashSet<Integer> set = new HashSet<>();
set.add(5);
set.add(3);
set.add(5);                      // duplicate — নেবে না

System.out.println(set.size());  // 2
System.out.println(set.contains(3));   // true
```

---

## নিজে বানানো List (DSA practice এর জন্য)

ArrayList ভেতরে কীভাবে কাজ করে সেটা বুঝতে — নিজে একটা বানিয়ে দেখো।
Array ভরে গেলে double size এর নতুন array বানিয়ে পুরনো data কপি করা হয়।

```java
class MyList {
    private int[] data = new int[2];     // শুরুতে ছোট, দরকারে বাড়বে
    private int size = 0;

    void add(int value) {
        if (size == data.length) {                    // ভরে গেছে
            int[] bigger = new int[data.length * 2];
            for (int i = 0; i < size; i++) {
                bigger[i] = data[i];                  // পুরনো data কপি
            }
            data = bigger;
        }
        data[size] = value;
        size++;
    }

    int get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Invalid index: " + index);
        }
        return data[index];
    }

    int size() {
        return size;
    }
}

public class MyListDemo {
    public static void main(String[] args) {
        MyList list = new MyList();

        for (int i = 1; i <= 5; i++) {
            list.add(i * 10);
        }

        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + " ");
        }
        System.out.println();
    }
}
```

**Output:**
```
10 20 30 40 50
```
