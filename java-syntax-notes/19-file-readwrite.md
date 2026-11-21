# 19 — File Read / Write

## Import

```java
import java.io.File;
import java.io.FileWriter;
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.PrintWriter;
import java.io.IOException;
import java.util.Scanner;
```

(সবগুলো একসাথে চাইলে `import java.io.*;`)

---

## File এ লেখা — FileWriter

```java
// নতুন file বানায় (আগে থাকলে পুরনো লেখা মুছে নতুন করে লেখে)
try (FileWriter writer = new FileWriter("data.txt")) {
    writer.write("Hello\n");
    writer.write("Java\n");
} catch (IOException e) {
    System.out.println("Write error: " + e.getMessage());
}
```

পুরনো লেখার নিচে **যোগ** করতে (append) — দ্বিতীয় argument `true`:

```java
try (FileWriter writer = new FileWriter("data.txt", true)) {
    writer.write("New line\n");
} catch (IOException e) {
    System.out.println("Write error: " + e.getMessage());
}
```

---

## File এ লেখা — PrintWriter (println/printf সহ)

```java
try (PrintWriter pw = new PrintWriter("out.txt")) {
    pw.println("Line 1");
    pw.printf("%d + %d = %d%n", 2, 3, 5);
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
```

---

## File থেকে পড়া — Scanner

```java
try (Scanner reader = new Scanner(new File("data.txt"))) {
    while (reader.hasNextLine()) {
        String line = reader.nextLine();
        System.out.println(line);
    }
} catch (IOException e) {
    System.out.println("File not found: " + e.getMessage());
}
```

শব্দ/সংখ্যা ধরে ধরে পড়তে `hasNext()` + `next()` / `nextInt()`।

---

## File থেকে পড়া — BufferedReader

```java
try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {     // শেষ হলে null আসে
        System.out.println(line);
    }
} catch (IOException e) {
    System.out.println("Read error: " + e.getMessage());
}
```

---

## File class এর কাজ

```java
File f = new File("data.txt");

f.exists();             // আছে কিনা — true/false
f.getName();            // "data.txt"
f.length();             // size (byte এ)
f.getAbsolutePath();    // পুরো path — file কোথায় তৈরি হলো দেখতে
f.delete();             // মুছে ফেলা — সফল হলে true
```

---

## ⚠️ File কোথায় তৈরি হয়?

শুধু নাম দিলে (`"data.txt"`) file তৈরি হয় **যে folder থেকে program চালাচ্ছো** সেখানে।
পড়তে গিয়ে `FileNotFoundException` এলে প্রথমে `getAbsolutePath()` print করে দেখো — file ঠিক জায়গায় আছে কিনা।

---

## Example Program — লিখে আবার পড়া

```java
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class FileDemo {
    public static void main(String[] args) {
        String fileName = "students.txt";

        // ── লেখা ──
        try (FileWriter writer = new FileWriter(fileName)) {
            writer.write("Rian 85\n");
            writer.write("Karim 72\n");
            writer.write("Anis 90\n");
            System.out.println("File written");
        } catch (IOException e) {
            System.out.println("Write error: " + e.getMessage());
        }

        // ── পড়া ──
        try (Scanner reader = new Scanner(new File(fileName))) {
            int total = 0;
            while (reader.hasNext()) {
                String name = reader.next();
                int marks = reader.nextInt();
                System.out.println(name + " -> " + marks);
                total += marks;
            }
            System.out.println("Total: " + total);
        } catch (IOException e) {
            System.out.println("Read error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
File written
Rian -> 85
Karim -> 72
Anis -> 90
Total: 247
```

---

## Input নেওয়ার জন্য file ব্যবহার (Competitive Programming style)

Code এ কিছু বদলাতে হয় না — `Scanner(System.in)` ই থাকে। Terminal থেকে file কে keyboard এর জায়গায় বসানো হয়।

```bash
# Command Prompt (cmd) এ
java Main < input.txt > output.txt

# PowerShell এ '<' চলে না — pipe ব্যবহার করো
Get-Content input.txt | java Main
```

> VS Code এর terminal এ ডানদিকের dropdown (`+` এর পাশে) থেকে **Command Prompt** বেছে নিলে `<` চলবে।
