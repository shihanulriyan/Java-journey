# 14 — Encapsulation (Getter & Setter)

## Encapsulation কী?
Data (field) কে `private` করে লুকিয়ে রাখা, আর `public` method (getter/setter) দিয়ে নিয়ন্ত্রিতভাবে দেওয়া-নেওয়া।

**উদাহরণ:** ATM — ব্যাংকের vault এ সরাসরি হাত দেওয়া যায় না, ATM এর button (method) দিয়েই টাকা তোলা/জমা হয়।

---

## Syntax

```java
class ClassName {
    private dataType field;                    // বাইরে থেকে সরাসরি ধরা যাবে না

    public dataType getField() {               // পড়ার জন্য (getter)
        return field;
    }

    public void setField(dataType field) {     // বদলানোর জন্য (setter)
        this.field = field;
    }
}
```

---

## Access Modifier

| Modifier | একই class | একই package | অন্য package এর Child | সব জায়গা |
|----------|-----------|--------------|------------------------|-----------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| (কিছু না) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> সাধারণ নিয়ম: **field → `private`, method → `public`**।

---

## Getter / Setter এর নাম

```java
private String name;
private boolean passed;

public String getName()          { return name; }
public void   setName(String n)  { name = n; }

public boolean isPassed()        { return passed; }   // boolean এ get এর বদলে is
public void    setPassed(boolean p) { passed = p; }
```

---

## Setter এ Validation (এটাই আসল সুবিধা)

```java
class Student {
    private int age;

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 0 && age < 120) {
            this.age = age;
        } else {
            System.out.println("Invalid age");
        }
    }
}
```

`public int age` থাকলে কেউ `s.age = -5` লিখে দিতে পারত। Setter থাকলে ভুল value আটকানো যায়।

---

## Example Program — Bank Account

```java
class BankAccount {
    private String owner;
    private double balance;

    BankAccount(String owner, double balance) {
        this.owner = owner;
        this.balance = balance;
    }

    public String getOwner() {
        return owner;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            System.out.println("Invalid amount");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Insufficient balance or invalid amount");
        }
    }
}

public class EncapsulationDemo {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount("Rian", 1000);

        acc.deposit(500);
        acc.withdraw(2000);            // balance এর চেয়ে বেশি → আটকে যাবে
        // acc.balance = 999999;       // ❌ error — balance private

        System.out.println(acc.getOwner() + ": " + acc.getBalance());
    }
}
```

**Output:**
```
Insufficient balance or invalid amount
Rian: 1500.0
```

---

## Read-only field
শুধু getter রাখো, setter রাখো না — তাহলে value শুধু constructor এ বসবে, পরে আর বদলানো যাবে না।
(এখানে `owner` সেরকম।)

---

## VS Code এ Getter/Setter নিজে নিজে বানানো
Class এর ভেতরে Right Click → **Source Action...** → **Generate Getters and Setters...**

---

## কেন Encapsulation?

- ভুল data ঢোকা আটকানো (validation)
- ভেতরের কাজ বদলালেও বাইরের code ভাঙে না
- কোন field কে কে বদলাচ্ছে সেটা এক জায়গা থেকে control করা যায়
