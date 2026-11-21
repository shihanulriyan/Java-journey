# 11 — OOP: Class & Object

## Class আর Object কী?

**উদাহরণ:** বাড়ির নকশা (blueprint) আর সেই নকশা দিয়ে বানানো আসল বাড়ি।

| | Class | Object |
|--|-------|--------|
| মানে | নকশা / template | নকশা থেকে বানানো আসল জিনিস |
| Memory | নিজে নেয় না | `new` দিলে নেয় |
| উদাহরণ | `Student` | `s1`, `s2` |

> একটা class থেকে যত খুশি object বানানো যায়।

---

## Class এর Syntax

```java
class ClassName {
    // Fields  → data রাখে (variable)
    // Methods → কাজ করে (function)
}
```

---

## Object বানানোর Syntax

```java
ClassName objectName = new ClassName();

objectName.fieldName = value;   // field এ value দেওয়া
objectName.methodName();        // method call
```

---

## Example Program

```java
class Student {
    String name;        // field
    int age;
    double cgpa;

    void display() {    // method
        System.out.println(name + " | " + age + " | " + cgpa);
    }
}

public class ClassObjectDemo {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Rian";
        s1.age = 20;
        s1.cgpa = 3.75;

        Student s2 = new Student();
        s2.name = "Karim";
        s2.age = 21;
        s2.cgpa = 3.50;

        s1.display();
        s2.display();
    }
}
```

**Output:**
```
Rian | 20 | 3.75
Karim | 21 | 3.5
```

> ⚠️ File এর নাম হবে `ClassObjectDemo.java` — যে class এ `public` আছে তার নামে।
> একটা file এ `public class` থাকতে পারে মাত্র একটা।

---

## Method এ Parameter ও Return

```java
class Rectangle {
    int width, height;

    void setSize(int w, int h) {    // parameter নেয়, কিছু ফেরত দেয় না
        width = w;
        height = h;
    }

    int area() {                    // কিছু ফেরত দেয়
        return width * height;
    }
}

public class RectangleDemo {
    public static void main(String[] args) {
        Rectangle r = new Rectangle();
        r.setSize(5, 4);
        System.out.println(r.area());   // 20
    }
}
```

---

## this keyword

Object নিজেকে বোঝাতে `this` ব্যবহার করে।
Parameter আর field এর নাম এক হলে `this` লাগে।

```java
class Student {
    String name;

    void setName(String name) {
        this.name = name;   // this.name = field, name = parameter
    }
}
```

---

## Reference — object copy হয় না!

```java
// main এর ভেতরে
Student a = new Student();
a.name = "Rian";

Student b = a;          // নতুন object না — একই object এর আরেকটা নাম
b.name = "Karim";

System.out.println(a.name);   // Karim  (a আর b একই object)
```

---

## static vs non-static

```java
class Counter {
    static int total = 0;   // সব object মিলে একটাই
    int id;                 // প্রতি object এর আলাদা

    Counter() {
        total++;
        id = total;
    }
}

public class CounterDemo {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();

        System.out.println(Counter.total);  // 2  (class এর নাম দিয়ে ডাকা যায়)
        System.out.println(c2.id);          // 2
    }
}
```

| | static | non-static |
|--|--------|------------|
| Object লাগে? | না | হ্যাঁ |
| কার সাথে যুক্ত | class এর | object এর |
| Call | `ClassName.method()` | `obj.method()` |

**সাধারণ error:** static `main` থেকে non-static method সরাসরি ডাকা যায় না।

```java
public class Test {
    void hello() {
        System.out.println("Hi");
    }

    public static void main(String[] args) {
        // hello();      // ❌ non-static method cannot be referenced from a static context
        Test t = new Test();
        t.hello();       // ✅ আগে object বানাও
    }
}
```

---

## Object Array

```java
// main এর ভেতরে
Student[] list = new Student[3];   // এখনো কোনো object নেই — সব null

for (int i = 0; i < list.length; i++) {
    list[i] = new Student();       // প্রতিটার জন্য আলাদা new লাগবে
    list[i].name = "Student " + (i + 1);
}

for (Student s : list) {
    System.out.println(s.name);
}
```

> ⚠️ `new Student()` না দিয়ে `list[0].name = ...` করলে `NullPointerException` আসবে।

---

## Field এর Default Value

Field এ value না দিলে নিজে নিজে default value পায়:
`int` → 0, `double` → 0.0, `boolean` → false, `String` → null।

কিন্তু **method এর ভেতরের local variable** এ default নেই — value না দিয়ে ব্যবহার করলে error।
