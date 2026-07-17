# 08 — Strings

## String বানানো

```java
String s1 = "Hello";
String s2 = new String("Hello");
```

---

## সব গুরুত্বপূর্ণ Methods

```java
String s = "Hello World";

// ── LENGTH ──
s.length();                  // 11

// ── UPPERCASE / LOWERCASE ──
s.toUpperCase();             // "HELLO WORLD"
s.toLowerCase();             // "hello world"

// ── TRIM (সামনে-পিছনে space বাদ) ──
"  hello  ".trim();          // "hello"

// ── CHARACTER ──
s.charAt(0);                 // 'H'
s.charAt(6);                 // 'W'

// ── SUBSTRING ──
s.substring(6);              // "World"
s.substring(0, 5);           // "Hello"

// ── CONTAINS ──
s.contains("World");         // true
s.contains("world");         // false (case sensitive)

// ── STARTS / ENDS WITH ──
s.startsWith("Hello");       // true
s.endsWith("World");         // true

// ── REPLACE ──
s.replace("World", "Java");  // "Hello Java"
s.replace('l', 'L');         // "HeLLo WorLd"

// ── SPLIT ──
String csv = "a,b,c,d";
String[] parts = csv.split(",");  // ["a","b","c","d"]

// ── INDEX OF ──
s.indexOf('o');              // 4  (প্রথম 'o' কোথায়)
s.indexOf("World");          // 6

// ── IS EMPTY ──
"".isEmpty();                // true
"hi".isEmpty();              // false
```

---

## String Comparison

```java
String a = "hello";
String b = "hello";
String c = "HELLO";

// ✅ সঠিক উপায়
a.equals(b);                 // true
a.equals(c);                 // false

// Case ignore করে compare
a.equalsIgnoreCase(c);       // true

// ❌ ভুল উপায়
a == b;  // এটা memory address compare করে!
```

---

## String + Number

```java
String name = "Rian";
int age = 20;

System.out.println(name + " is " + age);   // Rian is 20
System.out.println("Sum: " + (5 + 3));     // Sum: 8
System.out.println("Sum: " + 5 + 3);       // Sum: 53  (ভুল!)
```

---

## Char Check করা

```java
char c = 'A';

Character.isLetter(c);       // true
Character.isDigit(c);        // false
Character.isUpperCase(c);    // true
Character.isLowerCase(c);    // false
Character.toUpperCase('a');  // 'A'
Character.toLowerCase('A');  // 'a'
```

---

## Example — Palindrome Check

```java
String s = "madam";
String rev = new StringBuilder(s).reverse().toString();

if (s.equals(rev)) {
    System.out.println("Palindrome");
} else {
    System.out.println("Not Palindrome");
}
```
