# 13 — Inheritance

## Inheritance কী?
Parent class এর field আর method Child class নিজে পেয়ে যায় — আবার লিখতে হয় না।

**উদাহরণ:** বাবার সম্পত্তি ছেলে পায়, আবার ছেলের নিজের সম্পত্তিও থাকতে পারে।

---

## Syntax

```java
class Parent {
    // field, method
}

class Child extends Parent {
    // Parent এর সব পাবে + নিজের নতুন কিছু
}
```

---

## Example

```java
class Person {
    String name;
    int age;

    void introduce() {
        System.out.println("I am " + name + ", age " + age);
    }
}

class Student extends Person {
    double cgpa;

    void showCgpa() {
        System.out.println("CGPA: " + cgpa);
    }
}

public class InheritanceDemo {
    public static void main(String[] args) {
        Student s = new Student();
        s.name = "Rian";    // Person থেকে পাওয়া
        s.age = 20;         // Person থেকে পাওয়া
        s.cgpa = 3.75;      // Student এর নিজের

        s.introduce();
        s.showCgpa();
    }
}
```

**Output:**
```
I am Rian, age 20
CGPA: 3.75
```

---

## super keyword

| ব্যবহার | মানে |
|---------|------|
| `super(...)` | Parent এর constructor call |
| `super.method()` | Parent এর method call |
| `super.field` | Parent এর field |

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
        System.out.println("Person constructor");
    }
}

class Student extends Person {
    int roll;

    Student(String name, int roll) {
        super(name);               // Parent constructor — অবশ্যই প্রথম line
        this.roll = roll;
        System.out.println("Student constructor");
    }
}

public class SuperDemo {
    public static void main(String[] args) {
        Student s = new Student("Rian", 7);
        System.out.println(s.name + " " + s.roll);
    }
}
```

**Output:**
```
Person constructor
Student constructor
Rian 7
```

> Object বানালে **আগে Parent এর constructor** চলে, তারপর Child এর।

> ⚠️ Parent এ no-arg constructor না থাকলে Child এ `super(...)` লিখতেই হবে — না লিখলে compile error।

---

## Inheritance এর ধরন

```
Single:        A → B
Multilevel:    A → B → C
Hierarchical:  A → B
               A → C
Multiple:      ❌ class দিয়ে Java তে হয় না (interface দিয়ে করা যায় — 16 নম্বর file দেখো)
```

```java
class Animal { }
class Dog extends Animal { }       // single
class Puppy extends Dog { }        // multilevel
class Cat extends Animal { }       // hierarchical (Animal এর দুইটা child)
```

---

## Method Override (Parent এর method বদলানো)

```java
class Person {
    void role() {
        System.out.println("Person");
    }
}

class Student extends Person {
    @Override
    void role() {
        System.out.println("Student");
    }
}
```

বিস্তারিত → `15-polymorphism.md`

---

## জরুরি নিয়ম

- `private` member সরাসরি Child এ পাওয়া যায় না (getter দিয়ে নিতে হয়)
- `protected` member Child এ পাওয়া যায়
- `final class` কে extend করা যায় না
- Java তে প্রতিটা class এর শেষ parent হলো `Object` class
- `instanceof` দিয়ে check করা যায় কোন type এর object:

```java
// main এর ভেতরে (উপরের Student/Person class দিয়ে)
Student s = new Student("Rian", 7);
System.out.println(s instanceof Person);    // true
System.out.println(s instanceof Student);   // true
```
