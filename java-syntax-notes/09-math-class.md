# 09 — Math Class

> Import করতে হয় না — সরাসরি ব্যবহার করা যায়।

---

## সব গুরুত্বপূর্ণ Methods

```java
// ── POWER (ঘাত) ──
Math.pow(2, 10);        // 1024.0  (2^10)
Math.pow(3, 3);         // 27.0    (3^3)

// ── SQUARE ROOT ──
Math.sqrt(25);          // 5.0
Math.sqrt(2);           // 1.4142...

// ── ABSOLUTE VALUE (|x|) ──
Math.abs(-15);          // 15
Math.abs(15);           // 15
Math.abs(-3.14);        // 3.14

// ── MAX / MIN ──
Math.max(10, 20);       // 20
Math.min(10, 20);       // 10
Math.max(5, Math.max(3, 9));  // 9  (3 এর মধ্যে max)

// ── CEILING (উপরে রাউন্ড) ──
Math.ceil(4.1);         // 5.0
Math.ceil(4.9);         // 5.0

// ── FLOOR (নিচে রাউন্ড) ──
Math.floor(4.9);        // 4.0
Math.floor(4.1);        // 4.0

// ── ROUND (নিকটতম) ──
Math.round(4.4);        // 4
Math.round(4.5);        // 5
Math.round(4.6);        // 5

// ── RANDOM (0.0 থেকে 1.0 এর মধ্যে) ──
Math.random();          // 0.0 ≤ x < 1.0

// RANDOM integer (0 থেকে 99)
int rand = (int)(Math.random() * 100);

// RANDOM integer (1 থেকে 100)
int rand2 = (int)(Math.random() * 100) + 1;

// ── LOG ──
Math.log(Math.E);       // 1.0   (natural log)
Math.log10(100);        // 2.0   (log base 10)

// ── PI ──
Math.PI;                // 3.141592653589793
Math.E;                 // 2.718281828459045
```

---

## Example Programs

```java
// বৃত্তের ক্ষেত্রফল
double r = 5;
double area = Math.PI * Math.pow(r, 2);
System.out.println("Area: " + area);  // 78.53...

// Hypotenuse বের করা (a^2 + b^2 = c^2)
double a = 3, b = 4;
double c = Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));
System.out.println("Hypotenuse: " + c);  // 5.0

// Random dice (1-6)
int dice = (int)(Math.random() * 6) + 1;
System.out.println("Dice: " + dice);
```

---

## Random Range Formula

```java
// min থেকে max এর মধ্যে random
int min = 10, max = 50;
int rand = (int)(Math.random() * (max - min + 1)) + min;
```
