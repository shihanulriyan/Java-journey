# 12 — Constructor

## Constructor কী?
`new` দিয়ে object বানানোর সময় নিজে নিজে চলে এমন বিশেষ method।
কাজ: object এর শুরুর value বসানো।

## ৩টা নিয়ম
1. নাম = class এর নাম, হুবহু (capital-small সহ)
2. কোনো return type নেই (`void` ও না)
3. `new` দিলেই চলে — আলাদা করে call করা যায় না

---

## Syntax

```java
class ClassName {
    ClassName(parameters) {
        // শুরুর কাজ
    }
}
```

---

## No-arg ও Parameterized Constructor

```java
class Student {
    String name;
    int age;

    // ১. No-arg constructor (parameter নেই)
    Student() {
        name = "Unknown";
        age = 0;
    }

    // ২. Parameterized constructor
    Student(String name, int age) {
        this.name = name;     // this.name = field, name = parameter
        this.age = age;
    }

    void display() {
        System.out.println(name + " | " + age);
    }
}

public class ConstructorDemo {
    public static void main(String[] args) {
        Student s1 = new Student();              // ১ নম্বরটা চলবে
        Student s2 = new Student("Rian", 20);    // ২ নম্বরটা চলবে

        s1.display();
        s2.display();
    }
}
```

**Output:**
```
Unknown | 0
Rian | 20
```

---

## Default Constructor — Java নিজে দেয়

তুই কোনো constructor না লিখলে Java নিজে একটা খালি constructor বানিয়ে দেয়, তাই `new Student()` চলে।

> ⚠️ **কিন্তু** যেকোনো একটা constructor লিখলেই Java আর নিজে দেয় না!
> শুধু parameterized লিখলে `new Student()` → **error**।
> দুটোই লাগলে দুটোই লিখতে হবে।

---

## Constructor Overloading
একই class এ একাধিক constructor — parameter আলাদা হলেই হয়।

```java
Student()                        // কিছু নেই
Student(String name)             // শুধু নাম
Student(String name, int age)    // নাম + বয়স
```

---

## this() — এক constructor থেকে আরেকটা call

```java
class Student {
    String name;
    int age;

    Student() {
        this("Unknown", 0);       // নিচের constructor টা ডাকছে — অবশ্যই প্রথম line
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

## Copy Constructor (নিজে লিখতে হয়)

```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    Student(Student other) {          // অন্য object এর data কপি
        this.name = other.name;
        this.age = other.age;
    }
}

public class CopyDemo {
    public static void main(String[] args) {
        Student s1 = new Student("Rian", 20);
        Student s2 = new Student(s1);     // s1 এর copy — কিন্তু আলাদা object

        s2.name = "Karim";
        System.out.println(s1.name);      // Rian  (s1 বদলায়নি)
        System.out.println(s2.name);      // Karim
    }
}
```

---

## Constructor vs Method

| | Constructor | Method |
|--|-------------|--------|
| নাম | class এর নাম | যেকোনো নাম |
| Return type | নেই | আছে (`void` সহ) |
| কখন চলে | `new` দিলে নিজে | নিজে call করলে |
| কাজ | শুরুর value বসানো | সাধারণ কাজ |
