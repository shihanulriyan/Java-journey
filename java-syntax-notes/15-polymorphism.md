# 15 — Polymorphism (Overloading & Overriding)

## Polymorphism কী?
"এক নাম, অনেক রূপ।" একই নামের method আলাদা আলাদা অবস্থায় আলাদা কাজ করে।

| ধরন | কখন ঠিক হয় | কীভাবে |
|-----|-------------|--------|
| Compile-time | code compile এর সময় | Method **Overloading** |
| Runtime | program চলার সময় | Method **Overriding** |

---

## 1. Method Overloading
একই class এ একই নামের একাধিক method — **parameter আলাদা** হতে হবে (সংখ্যা বা type বা ক্রম)।

```java
class Calculator {
    int add(int a, int b)          { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c)   { return a + b + c; }
}

public class OverloadDemo {
    public static void main(String[] args) {
        Calculator c = new Calculator();

        System.out.println(c.add(5, 3));        // 8
        System.out.println(c.add(2.5, 3.5));    // 6.0
        System.out.println(c.add(1, 2, 3));     // 6
    }
}
```

> ⚠️ শুধু return type আলাদা হলে overloading হয় না:
> ```java
> int    get(int a) { return a; }
> double get(int a) { return a; }   // ❌ compile error
> ```

---

## 2. Method Overriding
Parent এর method কে Child নিজের মতো করে নতুন করে লেখে। **একই নাম, একই parameter।**

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Woof");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meow");
    }
}

public class OverrideDemo {
    public static void main(String[] args) {
        Animal a1 = new Dog();       // Parent type এর variable, Child এর object
        Animal a2 = new Cat();
        Animal a3 = new Animal();

        a1.sound();    // Woof
        a2.sound();    // Meow
        a3.sound();    // Some sound

        Animal[] zoo = { new Dog(), new Cat(), new Dog() };
        for (Animal a : zoo) {
            a.sound();             // কোন object — সেটা অনুযায়ী method চলে
        }
    }
}
```

**Output:**
```
Woof
Meow
Some sound
Woof
Meow
Woof
```

> `@Override` লেখা বাধ্যতামূলক না, কিন্তু লিখলে নামে ভুল থাকলে compiler ধরিয়ে দেয়। সবসময় লিখো।

---

## Overriding এর নিয়ম

- নাম আর parameter হুবহু এক
- Access কমানো যাবে না (`public` কে `private` করা যাবে না)
- `static`, `final`, `private` method override হয় না
- Return type একই (বা তার child type)

---

## Upcasting আর Downcasting

```java
// main এর ভেতরে
Animal a = new Dog();       // Upcasting — নিজে নিজে হয়

// a.fetch();               // ❌ Animal type এ fetch() নেই (শুধু Dog এ থাকলে)

Dog d = (Dog) a;            // Downcasting — নিজে লিখতে হয়
// d.fetch();               // ✅ এখন Dog এর method পাওয়া যাবে

// ভুল downcast
// Cat c = (Cat) a;         // ❌ ClassCastException (a আসলে Dog)
```

নিরাপদে downcast করতে আগে `instanceof` দিয়ে check:

```java
if (a instanceof Dog) {
    Dog d = (Dog) a;
}
```

---

## Overloading vs Overriding

| | Overloading | Overriding |
|--|-------------|------------|
| কোথায় | একই class | Parent ↔ Child |
| Parameter | আলাদা | একই |
| Return type | যেকোনো | একই |
| ঠিক হয় | Compile এর সময় | Runtime এ |
| `@Override` | লাগে না | লিখতে হয় |
