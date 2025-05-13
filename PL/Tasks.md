Okay, this is a great list of practical exercises! You're right, there's a lot of overlap and some questions are quite broad. Let's break them down into a more ergonomic and topic-focused structure, adding sample questions where the originals are a bit vague.

Here's a proposed structure:

**I. Core Java Concepts**
    A. Interfaces and Abstract Classes
    B. Collections Framework
    C. Generics
    D. Reflection

**II. Java 8+ Features**
    A. Lambda Expressions & Functional Interfaces (Implicit in Streams)
    B. Stream API
    C. Default and Static Methods in Interfaces

**III. Design Patterns**
    A. Creational Patterns
    B. Behavioral Patterns
    C. Structural Patterns (Not explicitly asked, but good to be aware of)

**IV. SOLID Principles**
    A. Single Responsibility Principle (SRP)
    B. Open/Closed Principle (OCP)
    C. Liskov Substitution Principle (LSP)
    D. Interface Segregation Principle (ISP)
    E. Dependency Inversion Principle (DIP)
    F. Applying Multiple SOLID Principles (System Design)

**V. Problem Solving & Application Design (Integrating multiple concepts)**

Let's populate this structure with your questions and add some clarifications/sample questions.

---

**I. Core Java Concepts**

**A. Interfaces and Abstract Classes**

1.  **Interface with Default Method:**
    *   **Original:** Use Interface with Default Method. Create an interface with a default greeting method and override it in implementing class.
    *   **Sample Task:** Create an interface `Loggable` with an abstract method `log(String message)` and a default method `logInfo(String message)` that prefixes "[INFO]" to the message and calls `log()`. Implement this in a `ConsoleLogger` class, overriding `logInfo` to also print to console directly.

2.  **Abstract Class with Constructor:**
    *   **Original:** Abstract Class with Constructor. Create an abstract class with a constructor and extend it in a subclass with additional logic.
    *   **Sample Task:** Create an abstract class `Vehicle` with a constructor that accepts `String registrationNumber` and stores it. It should also have an abstract method `startEngine()`. Create a `Car` subclass that calls the parent constructor and implements `startEngine()` to print "Car engine started."

3.  **Multiple Interfaces in One Class:**
    *   **Original:** Multiple Interfaces in One Class. Implement two interfaces in a single class and invoke their methods.
    *   **Sample Task:** Create interfaces `Flyable` (with `fly()`) and `Swimmable` (with `swim()`). Create a `Seaplane` class that implements both interfaces. Demonstrate calling both `fly()` and `swim()` on a `Seaplane` object.

4.  **Compare Abstract Class and Interface:**
    *   **Original:** Compare Abstract Class and Interface. Create a program showing key differences in features and usage of both.
    *   **Sample Task:** Create an abstract class `Animal` with a protected field `name`, a constructor to initialize `name`, a concrete method `eat()`, and an abstract method `makeSound()`. Create an interface `Pet` with a method `play()`. Create a `Dog` class that extends `Animal` and implements `Pet`. Demonstrate how `Dog` uses features from both. Discuss when you would choose one over the other.

5.  **Interface for Polymorphism:**
    *   **Original:** Use Interface for Polymorphism. Demonstrate how different implementations of an interface can be used interchangeably.
    *   **Sample Task:** Create an interface `Shape` with a method `draw()`. Implement `Circle`, `Square`, and `Triangle` classes that implement `Shape`. Create a list of `Shape` objects containing instances of `Circle`, `Square`, and `Triangle`. Iterate through the list and call `draw()` on each object.

**B. Collections Framework**

1.  **ArrayList: CRUD Operations**
    *   **Original:** Perform CRUD using ArrayList. Add, retrieve, update, and remove student records using ArrayList.
    *   **Sample Task:** Create a `Student` class (with `id`, `name`, `grade`). Use an `ArrayList<Student>` to store student records. Implement methods to:
        *   Add a new student.
        *   Retrieve a student by ID.
        *   Update a student's grade by ID.
        *   Remove a student by ID.
        *   Display all students.

2.  **LinkedList: Playlist Management**
    *   **Original:** LinkedList Example for Playlist. Manage songs in a playlist using LinkedList and show add/remove operations.
    *   **Sample Task:** Create a `Song` class (with `title`, `artist`). Use a `LinkedList<Song>` to represent a music playlist. Implement methods to:
        *   Add a song to the end of the playlist.
        *   Add a song at a specific position.
        *   Remove a song by title.
        *   Skip to the next song (move current song to end, or similar logic).
        *   Display the current playlist.

3.  **HashSet: Remove Duplicates**
    *   **Original:** Remove Duplicates using HashSet. Input a list of names and store unique ones using HashSet.
    *   **Sample Task:** Write a program that takes a `List<String>` of names (which may contain duplicates) as input. Use a `HashSet<String>` to store only the unique names from the input list and then print the unique names.

4.  **TreeSet: Sorted Data**
    *   **Original:** Sort Data using TreeSet. Insert names in TreeSet and show sorted order output.
    *   **Sample Task:** Create a `TreeSet<String>` and add several names to it in a random order. Iterate through the `TreeSet` and print the names to demonstrate they are stored and retrieved in natural (alphabetical) sorted order.
    *   **Combined Task:** (from your list) Merge Two TreeSets of Integers: Implement a method that takes two `TreeSet<Integer>` objects as parameters, merges them into one, and returns the merged set without duplicates. Demonstrate this with sample data.

5.  **HashMap: Key-Value Storage**
    *   **Original:** HashMap Example - Student Grades. Store and retrieve students' grades using roll numbers as keys.
    *   **Sample Task:** Use a `HashMap<Integer, String>` to store student grades, where the key is the student's roll number (integer) and the value is their grade (e.g., "A", "B+"). Implement functionality to:
        *   Add a student's grade.
        *   Retrieve a student's grade by roll number.
        *   Update a student's grade.
        *   Display all roll numbers and their grades.

6.  **LinkedHashMap: Insertion Order**
    *   **Original:** LinkedHashMap for Recent Activities. Record user activity timestamps while maintaining insertion order.
    *   **Sample Task:** Use a `LinkedHashMap<String, LocalDateTime>` to store user activities. The key should be a description of the activity (e.g., "Logged In", "Viewed Profile") and the value should be the timestamp. Add several activities and then iterate through the map to display them, demonstrating that they are retrieved in the order they were inserted.

7.  **Queue (using LinkedList): Task Simulation**
    *   **Original:** Implement Queue with LinkedList. Simulate a task queue with enqueue, dequeue operations using LinkedList.
    *   **Sample Task:** Use `java.util.LinkedList` to implement a `java.util.Queue<String>` for a task processing system. Implement methods to:
        *   `enqueueTask(String taskDescription)`: Adds a task to the queue.
        *   `dequeueTask()`: Removes and returns the task from the front of the queue.
        *   `peekTask()`: Returns the task at the front without removing it.
        *   `isQueueEmpty()`: Checks if the queue is empty.
        Simulate adding several tasks and processing them one by one.

**C. Generics**

1.  **Generic Class:**
    *   **Original:** Create a Generic Box Class. Create a class that stores objects of any type and prints the content.
    *   **Sample Task:** Implement a generic class `Box<T>` that can hold an object of any type `T`. It should have methods `setItem(T item)` and `T getItem()`. Demonstrate its usage with `Integer`, `String`, and a custom object.

2.  **Generic Method:**
    *   **Original:** Write a Generic Swap Method. Create a method that swaps two elements of any type (e.g., integers, strings).
    *   **Sample Task:** Write a static generic method `swapElements<T>(T[] array, int index1, int index2)` that swaps the elements at the given indices in an array of any type. Test it with an array of `Integer` and an array of `String`.

3.  **Bounded Generics (Upper Bound):**
    *   **Originals:**
        *   Bounded Generics Example. Create a generic method to print numeric values only using bounded type parameters.
        *   Demonstrate Bounded Parameters with Shapes: Write a generic method that accepts any type that extends the `Shape` class (which you will define). The method should calculate the total area of all shapes passed in as a list.
    *   **Sample Task (Numeric):** Create a generic method `calculateSum(List<? extends Number> numbers)` that iterates through a list of any objects that are subtypes of `Number` (e.g., `Integer`, `Double`) and returns their sum as a `double`.
    *   **Sample Task (Shapes):** Define an interface `Shape` with a method `double getArea()`. Create classes `Circle` and `Rectangle` implementing `Shape`. Write a generic method `printTotalArea(List<? extends Shape> shapes)` that calculates and prints the total area of all shapes in the list.

4.  **Generic Stack Implementation:**
    *   **Original:** Implement a Generic Stack Class: Design a class `Stack<T>` that uses an `ArrayList<T>` to implement stack behavior (push, pop, and peek methods). Include error handling for popping from an empty stack.
    *   **Task:** As described in the original.

**D. Reflection**

1.  **Inspect Class Metadata:**
    *   **Original:** Inspect Class using Reflection. Write a program to get class name, fields, and method names using reflection.
    *   **Sample Task:** Create a simple `Person` class with a few private/public fields and methods. Write a separate program that takes the `Person` class (e.g., `Person.class` or by name `Class.forName("com.example.Person")`) and uses reflection to:
        *   Print its fully qualified name.
        *   List all declared fields (name and type).
        *   List all declared methods (name, parameter types, return type).

2.  **Dynamic Object Creation:**
    *   **Original:** Dynamic Object Creation using Reflection. Create an object of a class using `Class.forName()` and `newInstance()` (or `getDeclaredConstructor().newInstance()`).
    *   **Sample Task:** Using the `Person` class from above (ensure it has a public no-arg constructor), dynamically create an instance of `Person` using `Class.forName("com.example.Person").getDeclaredConstructor().newInstance()`. If it has methods, try invoking one using reflection.

3.  **Access/Modify Private Fields:**
    *   **Original:** Access Private Field with Reflection. Use reflection to modify and access a private field of a class.
    *   **Sample Task:** In your `Person` class, add a private field `String secret` initialized to "initial_secret". Write code using reflection to:
        *   Access the value of this private `secret` field.
        *   Modify the value of this private `secret` field to "modified_secret".
        *   Verify the modification by accessing it again.

---

**II. Java 8+ Features**

**A. Lambda Expressions & Functional Interfaces**
    *(These are often used implicitly with Streams, but understanding them is key)*
    *   **Sample Task (Illustrative):** Create a functional interface `Calculator` with a single abstract method `operate(int a, int b)`. Implement this interface using lambda expressions for addition, subtraction, and multiplication.

**B. Stream API**

1.  **Stream Creation & Basic Operations:**
    *   **Original:** Stream from Collection. Convert a list of integers to stream and print all elements.
    *   **Sample Task:** Given a `List<Integer>`, create a stream from it and use `forEach()` to print each element.

2.  **Filtering and Mapping:**
    *   **Original:** Map and Filter Stream Operations. Given a list of names, filter names starting with 'A' and convert them to uppercase.
    *   **Sample Task:** Given `List<String> names = Arrays.asList("Alice", "Bob", "Anna", "Charlie", "Amanda");`, use streams to filter names that start with 'A', convert them to uppercase, and print them.

3.  **Reduction Operations:**
    *   **Original:** Use Reduce for Sum. Use `reduce()` to calculate the sum of a list of integers.
    *   **Sample Task:** Given `List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);`, use the `reduce()` operation to calculate their sum.

4.  **Collecting Results:**
    *   **Original:** Collect Stream to List. Convert a list of strings into a stream, modify, and collect it back to list.
    *   **Sample Task:** Given `List<String> words = Arrays.asList("apple", "banana", "cherry");`, convert them to a stream, transform each word to its uppercase version, and collect the results back into a new `List<String>`.

5.  **Parallel Streams:**
    *   **Original:** Parallel Stream Usage. Use `parallelStream()` to process a large dataset and compare time taken with normal stream.
    *   **Sample Task:** Create a large `List<Integer>` (e.g., 1 million random numbers). Perform a somewhat complex operation on each element (e.g., calculate `Math.sqrt(Math.log(number))`). Time this operation using a sequential stream (`stream()`) and a parallel stream (`parallelStream()`). Print the time taken for both. *Note: Actual speedup depends on the task, data size, and hardware.*

6.  **Advanced Stream Operations (Grouping, Counting):**
    *   **Originals:**
        *   Count Words Starting with Vowels from a File. Write a method that reads an array of strings representing words and returns the count of words that start with vowels.
        *   Group Words by First Letter into a Map. Write a program that uses streams to group words from an array by their first letter into a map where keys are letters and values are lists of words starting with those letters. Extend this to sort the words within each list alphabetically.
        *   Simulate Customer Orders with Item Categories. Create an application that simulates customer orders, where each order has items with prices and categories (e.g., electronics, groceries). Use streams to calculate total sales for each item category, displaying results in a user-friendly format.
    *   **Sample Task (Vowel Count):** Given `String[] words = {"apple", "banana", "orange", "grape", "umbrella", "ice"};`, use streams to count how many words start with a vowel (a, e, i, o, u, case-insensitive).
    *   **Sample Task (Group by First Letter):** Given `String[] words = {"Apple", "Banana", "Avocado", "Blueberry", "Cherry", "Apricot"};`, use streams and `Collectors.groupingBy` to create a `Map<Character, List<String>>` where keys are the first letters and values are lists of words starting with that letter. Ensure words within each list are sorted alphabetically.
    *   **Sample Task (Customer Orders):**
        Define `Item` (name, price, category) and `Order` (List<Item>). Create a list of `Order` objects.
        Use streams to:
        1.  Flatten all items from all orders.
        2.  Group items by category.
        3.  For each category, sum the prices of its items (`Collectors.summingDouble`).
        4.  Display the total sales for each category.

**C. Default and Static Methods in Interfaces**
    *   *(Covered in I.A.1. Interface with Default Method)*
    *   **Sample Task (Static Method):** Extend the `Loggable` interface (from I.A.1) with a static utility method `Loggable createConsoleLogger()` that returns a new instance of `ConsoleLogger`. Demonstrate its usage.

---

**III. Design Patterns**

**A. Creational Patterns**

1.  **Singleton Pattern:**
    *   **Original:** Implement Singleton Design Pattern. Write a Java class that ensures only one instance is created. Show how to access this instance from multiple points.
    *   **Sample Task:** Create a `DatabaseConnectionManager` class as a Singleton. It should have a method like `getConnection()` that simulates returning a database connection. Demonstrate that multiple calls to `getInstance()` return the same object. Ensure it's thread-safe (e.g., using eager initialization, or double-checked locking with `volatile`).

2.  **Factory Pattern (Simple Factory / Factory Method):**
    *   **Originals:**
        *   Implement Factory Design Pattern. Create a factory method that returns different types of shapes (e.g., Circle, Square) based on input.
        *   Create a system where a FurnitureFactory creates different types of furniture objects (e.g., Chair, Table, Sofa) based on user input.
    *   **Sample Task (Shapes):**
        Define an interface `Shape` with `draw()`. Implement `Circle`, `Rectangle`, `Triangle`.
        Create a `ShapeFactory` class with a static method `getShape(String shapeType)` which returns an instance of `Circle` if `shapeType` is "CIRCLE", `Rectangle` if "RECTANGLE", etc. Handle invalid input.
    *   **Sample Task (Furniture):**
        Define an interface `Furniture` with `getDescription()`. Implement `Chair`, `Table`, `Sofa`.
        Create a `FurnitureFactory` class with a method `createFurniture(String furnitureType)` that returns the corresponding furniture object.

**B. Behavioral Patterns**

1.  **Observer Pattern:**
    *   **Originals:**
        *   Implement Observer Design Pattern. Create a subject-observer structure where multiple observers get notified when the subject's state changes.
        *   Implement a StockPriceTracker class (subject) that notifies multiple observers (e.g., PriceAlert and DisplayBoard) when stock prices change.
    *   **Sample Task (Stock Tracker):**
        *   **Subject Interface:** `Stock` (methods: `registerObserver`, `removeObserver`, `notifyObservers`).
        *   **Observer Interface:** `StockObserver` (method: `update(String stockSymbol, double price)`).
        *   **Concrete Subject:** `StockPriceTracker` (implements `Stock`). Has a `stockSymbol` and `price`. A `setPrice(double newPrice)` method should update the price and call `notifyObservers()`.
        *   **Concrete Observers:**
            *   `PriceAlert` (prints an alert if price crosses a threshold).
            *   `DisplayBoard` (prints the new stock symbol and price).
        *   Demonstrate registering observers and seeing them notified when the price changes.

2.  **Strategy Pattern:**
    *   **Originals:**
        *   Implement Strategy Design Pattern. Create a context class that uses different sorting strategies (bubble sort, quick sort) at runtime.
        *   Implement different sorting algorithms (e.g., BubbleSort, QuickSort, MergeSort). Create a class to allow switching between these algorithms at runtime.
    *   **Sample Task (Sorting):**
        *   **Strategy Interface:** `SortStrategy` (method: `sort(int[] array)`).
        *   **Concrete Strategies:** `BubbleSortStrategy`, `QuickSortStrategy`, `MergeSortStrategy` (each implementing `SortStrategy` with its respective algorithm).
        *   **Context Class:** `SortedList` (or `SorterContext`). Has a `SortStrategy` field (set via constructor or setter) and a method `performSort(int[] array)` which delegates to the current strategy's `sort` method.
        *   Demonstrate creating a `SortedList` object, setting different sorting strategies, and sorting an array with each.

---

**IV. SOLID Principles**

*(For SOLID, many questions ask to "design a simple library system" or similar. The key is to focus on how each principle is applied within that context.)*

**A. Single Responsibility Principle (SRP)**

1.  **Originals:**
    *   Design a class that performs one specific task like handling user input or processing data.
    *   Apply SOLID Principles (S and O / S and D) - Design a simple library system... (Focus on SRP part).
2.  **Sample Task (General):** Design two classes: `UserInputHandler` responsible solely for reading and validating user input, and `DataProcessor` responsible solely for processing the validated data. The `UserInputHandler` should not know about data processing, and `DataProcessor` should not know about input sources.
3.  **Sample Task (Library - SRP):** In a library system:
    *   A `Book` class should only hold book data (title, author, ISBN).
    *   A `BookRepository` class should be responsible *only* for persisting and retrieving `Book` objects (e.g., from a list, database).
    *   A `BookPresenter` class should be responsible *only* for formatting `Book` data for display.

**B. Open/Closed Principle (OCP)**

1.  **Originals:**
    *   Create a class that can be extended for new functionality without modifying the existing code.
    *   Apply SOLID Principles (S and O) - Design a simple library system... (Focus on OCP part).
2.  **Sample Task (General - e.g., Discount Calculator):**
    Create an `Order` class. Create a `DiscountCalculator` class that calculates discounts.
    *   **Initial:** `DiscountCalculator` has a method `calculateDiscount(Order order)` that applies a flat 10% discount.
    *   **Extension:** Without modifying `DiscountCalculator`, add functionality for a "VIP Customer" discount (20%) and a "Holiday Sale" discount (15%). (Hint: Use Strategy pattern or an interface for discount types that `DiscountCalculator` can use).
3.  **Sample Task (Library - OCP):** In a library system, you have a `LoanService` that processes loans for `Book` items. How would you design it so that if you introduce new loanable item types (e.g., `Magazine`, `DVD`), the `LoanService` doesn't need to be modified? (Hint: `LoanableItem` interface).

**C. Liskov Substitution Principle (LSP)**

1.  **Originals:**
    *   Show how a subclass (e.g., Square) can be substituted for a superclass (e.g., Rectangle) without altering behavior.
    *   Apply SOLID Principles (L and I) - Design a simple library system... (Focus on LSP part).
2.  **Sample Task (Rectangle/Square - Classic Violation & Fix):**
    *   Create a `Rectangle` class with `setWidth(int w)`, `setHeight(int h)`, `getWidth()`, `getHeight()`, and `getArea()`.
    *   Create a `Square` class that inherits from `Rectangle`. Override `setWidth` and `setHeight` so that setting one also sets the other (to maintain square property).
    *   Write a client code function `useRectangle(Rectangle r)` that sets width to 5, height to 10, and asserts `r.getArea() == 50`.
    *   Show that passing a `Square` to `useRectangle` breaks the assertion.
    *   Discuss how to fix this (e.g., `Square` shouldn't inherit from `Rectangle` if their contracts differ, or make `Shape` base class and immutable properties).
3.  **Sample Task (Library - LSP):** If you have a `LibraryItem` base class and subclasses `Book` and `DigitalBook`. If `LibraryItem` has a method `getPhysicalLocation()`, this might be problematic for `DigitalBook`. Ensure that any method in `LibraryItem` makes sense and behaves consistently for all its subtypes, or redesign.

**D. Interface Segregation Principle (ISP)**

1.  **Originals:**
    *   Create separate interfaces for print, scan, and fax operations and implement only required ones. (Appears multiple times)
    *   Apply SOLID Principles (L and I) - Design a simple library system... (Focus on ISP part).
    *   Blog user scenario (IBaseUser becomes bloated).
2.  **Sample Task (Multifunction Printer):**
    *   Define interfaces: `Printable` (with `print(Document d)`), `Scannable` (with `scan(Document d)`), `Faxable` (with `fax(Document d)`).
    *   Create classes:
        *   `SimplePrinter` implements `Printable`.
        *   `Photocopier` implements `Printable`, `Scannable`.
        *   `AllInOnePrinter` implements `Printable`, `Scannable`, `Faxable`.
    *   Demonstrate that classes only implement methods relevant to them, avoiding "fat" interfaces.
3.  **Sample Task (Blog Users - ISP):**
    *   **Problem:** `IBaseUser` has `editPost()`, `readPost()`, `blockPost()`. `Reader` only needs `readPost()`. `Writer` needs `editPost()`, `readPost()`. `Admin` needs all.
    *   **Solution:**
        *   `ReadableUser` interface: `readPost()`.
        *   `EditableUser` interface: `editPost()`.
        *   `ManageableUser` interface: `blockPost()`.
        *   `Reader` implements `ReadableUser`.
        *   `Writer` implements `ReadableUser`, `EditableUser`.
        *   `Admin` implements `ReadableUser`, `EditableUser`, `ManageableUser`.

**E. Dependency Inversion Principle (DIP)**

1.  **Originals:**
    *   Demonstrate loose coupling by injecting service objects through constructors or interfaces.
    *   Apply SOLID Principles (S and D) - Design a simple library system... (Focus on DIP part).
2.  **Sample Task (Notification Service):**
    *   Create an interface `MessageService` with a method `sendMessage(String recipient, String message)`.
    *   Create concrete implementations: `EmailService` and `SMSService`.
    *   Create a `NotificationManager` class that needs to send notifications. Instead of `NotificationManager` directly creating `EmailService` or `SMSService` instances (e.g., `new EmailService()`), it should depend on the `MessageService` interface.
    *   Show how the specific service (`EmailService` or `SMSService`) can be injected into `NotificationManager` (e.g., via constructor or a setter method).
3.  **Sample Task (Library - DIP):** A `LoanProcessingService` should not depend on a concrete `OracleBookRepository` or `MySqlBookRepository`. Instead, it should depend on an `IBookRepository` interface. The concrete repository implementation can then be injected.

**F. Applying Multiple SOLID Principles (System Design Scenarios)**

1.  **Library System (General):**
    *   **Originals:** Design a simple library system following all SOLID principles with at least 2-3 classes/interfaces (appears for S+O, L+I, S+D).
    *   **Task:** Design classes/interfaces for a library (e.g., `Book`, `Member`, `Loan`, `BookRepository`, `LoanService`, `NotificationService`). For each class/interface, explain which SOLID principles were considered and how.
        *   **SRP:** e.g., `BookRepository` only handles book data access. `LoanService` handles loan business logic.
        *   **OCP:** e.g., `LoanService` can handle new types of `LoanableItem`s without modification.
        *   **LSP:** e.g., If `AudioBook` is a `Book`, it must be substitutable for `Book`.
        *   **ISP:** e.g., `Borrowable` interface for items that can be borrowed, `Reservable` for items that can be reserved.
        *   **DIP:** e.g., `LoanService` depends on `IBookRepository` and `IMemberRepository` interfaces, not concrete classes.

2.  **Food Delivery Application (OCP, SRP focus):**
    *   **Original:** Design a food delivery application... users create/view orders. New requirements: send orders via email, display total price in email, update order view. Which SOLID principle? Design application with new requirements.
    *   **Analysis:**
        *   **OCP:** Adding email notifications should not modify the core order processing logic. Use an `OrderNotifier` interface with implementations like `EmailNotifier`. The order processing system would call `orderNotifier.notify(order)`.
        *   **SRP:** `Order` class for order data. `OrderCalculator` for total price. `OrderPresenter` for displaying. `OrderEmailFormatter` for email content.
    *   **Task:** Sketch out the classes and interfaces. Show how adding email notification and updating the view (perhaps a new view format) can be done by adding new classes/implementations rather than heavily modifying existing ones.

3.  **Ad Agency Analytics (ISP/SRP focus):**
    *   **Original:** New requirements by marketing team affecting business logic of analytics team. How to tackle? Which SOLID principle violated?
    *   **Analysis:**
        *   Likely violations:
            *   **SRP:** A single module/class might be handling both marketing concerns and analytics concerns.
            *   **ISP:** If both teams consume data from a large, shared interface/data model, changes for one can break the other.
        *   **Solution:**
            *   Separate concerns. Marketing team might need a `CampaignPerformanceService`, analytics might need a `DataAggregationService`.
            *   Use separate, tailored interfaces (ISP) for data consumed by each team.
            *   Use an event-driven architecture or a mediator if they need to interact, to decouple them.
    *   **Task:** Describe a scenario (e.g., a `ReportGenerator` class used by both). Show how splitting it or using specific interfaces for each team can resolve conflicts and improve maintainability.

4.  **Blog User System (ISP focus):**
    *   **Original:** `IBaseUser` with `editPost`, `readPost`, `blockPost`. `Reader` only needs `readPost`. `Writer` needs `editPost`, `readPost`. `Admin` needs all. Problem: bloated interface.
    *   **Analysis:** Clear ISP violation.
    *   **Task:** As detailed in IV.D.3 (Blog Users - ISP section above). Implement the refined interfaces (`ReadableUser`, `EditableUser`, `ManageableUser`) and show how `Reader`, `Writer`, and `Admin` classes implement only what they need.

---

**V. Problem Solving & Application Design (Integrating multiple concepts)**

These questions are already quite good as they combine various elements.

1.  **Book Class and Library Management (Collections, OOP):**
    *   **Original:** Define a `Book` class (title, author, ISBN). Implement an `ArrayList<Book>` to manage a library. Methods: add, remove by ISBN, display all.
    *   **Task:** As described. This is a good basic collections exercise.

2.  **Simulate Customer Orders with Item Categories (Streams, OOP, Collections):**
    *   **Original:** (Duplicate, also under Streams) Create an application that simulates customer orders... calculate total sales for each item category.
    *   **Task:** As described in II.B.6.

---

This structured approach should make it easier to prepare. For each topic, understand the core concept, then try to implement the sample tasks. Good luck with your practicals!