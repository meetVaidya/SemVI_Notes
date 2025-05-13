**Summary for Oral Exam:**

- Prior to Java 8, interfaces could only have abstract methods (methods without a body).
- **Java 8 introduced two new types of methods in interfaces:**
  - **Default Methods:** These are regular instance methods with a default implementation. They allow you to add new methods to interfaces without breaking existing implementations.
  - **Static Methods:** These belong to the interface itself and are called using the interface name, not via instances. They can be used for utility or helper methods.
- **Default methods** are invoked on objects (instances), whereas **static methods** are invoked on the interface directly.
- **Static methods cannot be overridden** by implementing classes, but **default methods can be overridden**.

### Example Code for Each:
```java
interface MyInterface {
    default void show() { System.out.println("Default method"); }
    static void print() { System.out.println("Static method"); }
}

class Demo implements MyInterface { }

public class Main {
    public static void main(String[] args) {
        Demo d = new Demo();
        d.show();               // Calls default method
        MyInterface.print();    // Calls static method
    }
}
```

---

### Real-life Analogy

**Default Method Analogy:**  
Imagine a company handbook (interface) that gives a default lunch break policy ("take 1 hour for lunch").  
If a new employee joins and doesn’t specify their preference, they follow this default. But if a manager (class) wants a different policy, they can override it.

**Static Method Analogy:**  
Think of the handbook also including a static emergency contact number.  
No employee (object) can change this number-it belongs to the handbook (interface) itself, and everyone refers to the same, unchangeable number.

---

Say "next" and I’ll proceed to **Design Patterns**.

Citations:
[1] Module_2_Collections.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/baf89d05-3849-46e2-9a7e-b8cb8bd37901/Module_2_Collections.pdf
[2] Module_2_Generics.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/16c7600d-ba5f-4cc8-85e9-8a8800fbdf07/Module_2_Generics.pdf
[3] Module_3.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/b50431c8-ac00-4a97-8d07-eff31e95e1b9/Module_3.pdf
[4] Module_1.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/5364e01d-2a7b-403b-af99-2a702f0f3761/Module_1.pdf
[5] Module_2_Collections.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/baf89d05-3849-46e2-9a7e-b8cb8bd37901/Module_2_Collections.pdf
[6] Module_2_Generics.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/16c7600d-ba5f-4cc8-85e9-8a8800fbdf07/Module_2_Generics.pdf
[7] Module_3.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/b50431c8-ac00-4a97-8d07-eff31e95e1b9/Module_3.pdf
[8] Module_1.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/62938491/5364e01d-2a7b-403b-af99-2a702f0f3761/Module_1.pdf
