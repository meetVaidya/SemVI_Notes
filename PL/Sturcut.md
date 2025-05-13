advanced_java_practice/
├── .gitignore                  // To ignore IDE files, .class files, etc.
├── README.md                   // General notes about your practice project
└── src/
    └── com/                    // Your base package (e.g., com.yourname.practice)
        └── yourname/
            └── practice/
                ├── core_java/
                │   ├── collections/
                │   │   ├── arraylist/
                │   │   │   └── StudentRecordsDemo.java
                │   │   ├── linkedlist/
                │   │   │   └── PlaylistDemo.java
                │   │   │   └── TaskQueueDemo.java
                │   │   ├── hashset/
                │   │   │   └── UniqueNamesDemo.java
                │   │   ├── treeset/
                │   │   │   └── SortedNamesDemo.java
                │   │   │   └── MergeTreeSetsDemo.java
                │   │   ├── hashmap/
                │   │   │   └── StudentGradesDemo.java
                │   │   └── linkedhashmap/
                │   │       └── RecentActivitiesDemo.java
                │   ├── generics/
                │   │   ├── BoxDemo.java
                │   │   ├── SwapMethodDemo.java
                │   │   ├── BoundedNumericDemo.java
                │   │   ├── BoundedShapesDemo.java
                │   │   └── GenericStackDemo.java
                │   ├── interfaces_abstract_classes/
                │   │   ├── DefaultMethodInterfaceDemo.java
                │   │   ├── AbstractClassConstructorDemo.java
                │   │   ├── MultipleInterfacesDemo.java
                │   │   ├── CompareAbstractInterfaceDemo.java
                │   │   └── PolymorphismWithInterfaceDemo.java
                │   └── reflection/
                │       ├── InspectClassDemo.java
                │       ├── DynamicCreationDemo.java
                │       └── AccessPrivateFieldDemo.java
                │
                ├── java8_features/
                │   ├── streams/
                │   │   ├── StreamFromCollectionDemo.java
                │   │   ├── MapFilterDemo.java
                │   │   ├── ReduceSumDemo.java
                │   │   ├── CollectToListDemo.java
                │   │   ├── ParallelStreamDemo.java
                │   │   ├── VowelWordCountDemo.java
                │   │   └── GroupWordsByFirstLetterDemo.java
                │   └── default_static_methods/ // Can also be inside core_java/interfaces...
                │       └── LoggableInterfaceDemo.java // (Example from my previous answer)
                │
                ├── design_patterns/
                │   ├── creational/
                │   │   ├── singleton/
                │   │   │   └── SingletonConnectionManager.java
                │   │   │   └── SingletonAccessDemo.java
                │   │   └── factory/
                │   │       ├── shape_factory/
                │   │       │   ├── Shape.java
                │   │       │   ├── Circle.java
                │   │       │   ├── Square.java
                │   │       │   ├── ShapeFactory.java
                │   │       │   └── ShapeFactoryDemo.java
                │   │       └── furniture_factory/
                │   │           ├── Furniture.java
                │   │           ├── Chair.java
                │   │           ├── Table.java
                │   │           ├── FurnitureFactory.java
                │   │           └── FurnitureFactoryDemo.java
                │   ├── behavioral/
                │   │   ├── observer/
                │   │   │   ├── stock_tracker/
                │   │   │   │   ├── StockSubject.java
                │   │   │   │   ├── StockObserver.java
                │   │   │   │   ├── StockPriceTracker.java
                │   │   │   │   ├── PriceAlert.java
                │   │   │   │   ├── DisplayBoard.java
                │   │   │   │   └── StockDemo.java
                │   │   └── strategy/
                │   │       ├── sorting/
                │   │       │   ├── SortStrategy.java
                │   │       │   ├── BubbleSort.java
                │   │       │   ├── QuickSort.java
                │   │       │   ├── SorterContext.java
                │   │       │   └── SortingDemo.java
                │   └── structural/
                │       └── (empty for now, as none were explicitly asked)
                │
                ├── solid_principles/
                │   ├── srp/ // Single Responsibility Principle
                │   │   ├── UserInputHandler.java
                │   │   ├── DataProcessor.java
                │   │   └── SrpDemo.java
                │   ├── ocp/ // Open/Closed Principle
                │   │   ├── discount_calculator/
                │   │   │   ├── DiscountStrategy.java
                │   │   │   ├── FixedDiscount.java
                │   │   │   ├── VipDiscount.java
                │   │   │   ├── Order.java
                │   │   │   ├── DiscountCalculator.java
                │   │   │   └── OcpDemo.java
                │   ├── lsp/ // Liskov Substitution Principle
                │   │   ├── shapes/
                │   │   │   ├── Rectangle.java
                │   │   │   ├── Square.java // (The problematic one or the fixed one)
                │   │   │   └── LspDemo.java
                │   ├── isp/ // Interface Segregation Principle
                │   │   ├── printer_scanner_fax/
                │   │   │   ├── Printable.java
                │   │   │   ├── Scannable.java
                │   │   │   ├── Faxable.java
                │   │   │   ├── SimplePrinter.java
                │   │   │   ├── AllInOneDevice.java
                │   │   │   └── IspDemo.java
                │   │   └── blog_users/ // For the specific blog user ISP problem
                │   │       ├── ReadableUser.java
                │   │       ├── EditableUser.java
                │   │       ├── BlockableUser.java
                │   │       ├── Reader.java
                │   │       ├── Writer.java
                │   │       ├── Admin.java
                │   │       └── BlogUserIspDemo.java
                │   └── dip/ // Dependency Inversion Principle
                │       ├── notification/
                │       │   ├── MessageService.java
                │       │   ├── EmailService.java
                │       │   ├── SMSService.java
                │       │   ├── NotificationManager.java
                │       │   └── DipDemo.java
                │
                └── applications/ // For larger examples combining multiple concepts or specific scenarios
                    ├── library_system_solid/ // For the "Design a simple library system" questions
                    │   ├── model/
                    │   │   ├── Book.java
                    │   │   └── Member.java
                    │   ├── repository/
                    │   │   ├── BookRepository.java // Interface
                    │   │   └── InMemoryBookRepository.java // Implementation
                    │   ├── service/
                    │   │   ├── LoanService.java
                    │   │   └── NotificationService.java // Interface
                    │   │   └── EmailNotificationService.java // Implementation
                    │   └── LibraryDemo.java
                    ├── food_delivery_solid/ // For the food delivery SOLID problem
                    │   ├── model/
                    │   │   └── Order.java
                    │   ├── service/
                    │   │   ├── OrderProcessor.java
                    │   │   ├── PriceCalculator.java
                    │   │   └── notification/
                    │   │       ├── OrderNotifier.java // Interface
                    │   │       └── EmailOrderNotifier.java
                    │   └── FoodDeliveryDemo.java
                    ├── ad_agency_solid/ // For the Ad agency SOLID problem
                    │   ├── marketing/
                    │   │   └── CampaignService.java
                    │   ├── analytics/
                    │   │   └── AnalyticsService.java
                    │   └── AdAgencyDemo.java
                    └── customer_order_streams/ // For the customer order simulation with streams
                        ├── model/
                        │   ├── Item.java
                        │   └── Order.java
                        └── CustomerOrderDemo.java