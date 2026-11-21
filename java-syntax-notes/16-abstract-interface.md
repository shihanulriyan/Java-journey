# 16 — Abstract Class & Interface

## Abstract Class কী?
এমন class যার object বানানো যায় না। এটা Child দের জন্য একটা **অর্ধেক-তৈরি নকশা**।
কিছু method এর body থাকে, কিছু method শুধু নাম থাকে (Child কে লিখতেই হবে)।

## Syntax

```java
abstract class ClassName {
    abstract returnType methodName();      // body নেই — শেষে সোজা ;

    void normalMethod() {                  // সাধারণ method-ও রাখা যায়
        // body আছে
    }
}
```

---

## Example — Shape

```java
abstract class Shape {
    String color;

    Shape(String color) {
        this.color = color;
    }

    abstract double area();            // Child কে লিখতেই হবে

    void showColor() {
        System.out.println("Color: " + color);
    }
}

class Circle extends Shape {
    double r;

    Circle(String color, double r) {
        super(color);
        this.r = r;
    }

    @Override
    double area() {
        return Math.PI * r * r;
    }
}

class Rectangle extends Shape {
    double w, h;

    Rectangle(String color, double w, double h) {
        super(color);
        this.w = w;
        this.h = h;
    }

    @Override
    double area() {
        return w * h;
    }
}

public class AbstractDemo {
    public static void main(String[] args) {
        // Shape s = new Shape("Red");     // ❌ abstract class এর object হয় না

        Shape c = new Circle("Red", 5);
        Shape r = new Rectangle("Blue", 4, 6);

        c.showColor();
        System.out.println(c.area());      // 78.53981633974483
        System.out.println(r.area());      // 24.0
    }
}
```

**Output:**
```
Color: Red
78.53981633974483
24.0
```

> ⚠️ Child class সব abstract method না লিখলে Child ও `abstract` হতে হবে — নাহলে compile error।

---

## Interface কী?
শুধু "কী করতে পারবে" তার **চুক্তি (contract)**। কোন class এটা `implements` করলে সব method লিখতে বাধ্য।

## Syntax

```java
interface InterfaceName {
    void methodName();          // নিজে নিজে public abstract
}

class ClassName implements InterfaceName {
    @Override
    public void methodName() {  // implement করার সময় public লিখতেই হবে
        // body
    }
}
```

---

## Example — একাধিক Interface

```java
interface Drawable {
    void draw();
}

interface Resizable {
    void resize(int percent);
}

class Image implements Drawable, Resizable {    // একসাথে অনেকগুলো চলে
    @Override
    public void draw() {
        System.out.println("Drawing image");
    }

    @Override
    public void resize(int percent) {
        System.out.println("Resized to " + percent + "%");
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        Image img = new Image();
        img.draw();
        img.resize(50);

        Drawable d = img;       // interface type এর variable এও রাখা যায়
        d.draw();
    }
}
```

**Output:**
```
Drawing image
Resized to 50%
Drawing image
```

> ⚠️ Implement করার সময় `public` না লিখলে error আসবে (weaker access privileges)।

---

## Default Method (Java 8+)
Interface এ body সহ method রাখা যায় — `default` লিখে।

```java
interface Greeting {
    void sayHello();

    default void sayBye() {
        System.out.println("Bye!");
    }
}

class English implements Greeting {
    @Override
    public void sayHello() {
        System.out.println("Hello!");
    }
}

public class DefaultDemo {
    public static void main(String[] args) {
        English e = new English();
        e.sayHello();    // Hello!
        e.sayBye();      // Bye!   (লিখিনি, তবু পাচ্ছি)
    }
}
```

---

## Interface এর Constant

```java
interface Config {
    int MAX_USERS = 100;       // নিজে নিজে public static final
}
// ব্যবহার: Config.MAX_USERS
```

---

## Abstract Class vs Interface

| | Abstract Class | Interface |
|--|----------------|-----------|
| Keyword | `extends` | `implements` |
| একাধিক নেওয়া | ❌ একটাই | ✅ অনেকগুলো |
| Constructor | ✅ আছে | ❌ নেই |
| Field | সাধারণ variable রাখা যায় | শুধু constant |
| Method | abstract + সাধারণ | abstract (+ default, static) |
| কখন | কিছু common code + কিছু বাধ্যতামূলক method | শুধু "কী পারবে" এর চুক্তি |
