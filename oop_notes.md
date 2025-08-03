
# OOP Notes

## OOP has Four Core Pillars:
1. **Inheritance**
2. **Polymorphism**
3. **Encapsulation**
4. **Abstraction**

---

## 1. **Inheritance**

### **Definition:**
Inheritance allows a class (child/subclass) to inherit properties and methods from another class (parent/superclass). This promotes **code reuse** and **hierarchical classification**.

### **Key Concepts:**
- The child class **inherits** fields and methods of the parent.
- It can **override** or **extend** behavior.
- Dart supports **single inheritance** (one parent per class).

### **Code Example:**

```dart
// Base class (Parent)
class Animal {
  void eat() {
    print("Animal is eating");
  }
}

// Derived class (Child)
class Dog extends Animal {
  void bark() {
    print("Dog is barking");
  }

  // Overriding the parent method
  @override
  void eat() {
    print("Dog is eating dog food");
  }
}

void main() {
  Dog dog = Dog();
  dog.bark();     // Output: Dog is barking
  dog.eat();      // Output: Dog is eating dog food
}
```

### **Usage in Real Life:**
- `Vehicle` → `Car`, `Bike`
- `Employee` → `Manager`, `Developer`

---

## 2. **Polymorphism**

### **Definition:**
Polymorphism means **many forms**. It allows objects to be treated as instances of their **parent class**, but the **actual method invoked depends on the runtime object type**.

### **Key Concepts:**
- Achieved via **method overriding** (runtime polymorphism).
- Promotes **flexibility** and **scalability**.
- Dart uses **dynamic dispatch** to call overridden methods at runtime.

### **Code Example:**

```dart
class Animal {
  void makeSound() {
    print("Animal makes a sound");
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Dog barks");
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print("Cat meows");
  }
}

void main() {
  List<Animal> animals = [Dog(), Cat()];

  for (var animal in animals) {
    animal.makeSound();
    // Output: Dog barks
    //         Cat meows
  }
}
```

### **Real-World Analogy:**
- A remote control can operate different devices (TV, AC) – **same interface, different behavior**.

---

## 3. **Encapsulation**

### **Definition:**
Encapsulation is about **hiding internal details** and exposing only what's necessary. It helps in **data protection** and **code maintainability**.

### **Key Concepts:**
- Dart uses **private fields** with `_` prefix.
- Use **getters** and **setters** to control access.
- Promotes **data hiding** and **modularity**.

### **Code Example:**

```dart
class BankAccount {
  // Private field
  double _balance = 0.0;

  // Getter
  double get balance => _balance;

  // Setter with validation
  void deposit(double amount) {
    if (amount > 0) {
      _balance += amount;
    } else {
      print("Invalid deposit amount");
    }
  }

  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount;
    } else {
      print("Insufficient funds or invalid amount");
    }
  }
}

void main() {
  BankAccount account = BankAccount();
  account.deposit(100);
  print(account.balance); // Output: 100.0
  account.withdraw(30);
  print(account.balance); // Output: 70.0
}
```

### **Real-World Analogy:**
- ATM machine: You interact with buttons (interface), but **don’t see the internal circuitry**.

---

## 4. **Abstraction**

### **Definition:**
Abstraction means **hiding complexity** and showing only essential features. It allows **focusing on what an object does**, rather than how it does it.

### **Key Concepts:**
- Implemented via **abstract classes** and **interfaces** in Dart.
- Abstract classes cannot be instantiated.
- Abstract methods have **no body**, must be **overridden**.

### **Code Example:**

```dart
// Abstract class
abstract class Shape {
  void draw(); // abstract method

  double area(); // abstract method
}

// Concrete class implementing Shape
class Circle extends Shape {
  double radius;

  Circle(this.radius);

  @override
  void draw() {
    print("Drawing a circle");
  }

  @override
  double area() {
    return 3.14 * radius * radius;
  }
}

void main() {
  Circle circle = Circle(5);
  circle.draw();                      // Output: Drawing a circle
  print(circle.area());               // Output: 78.5
}
```

### **Real-World Analogy:**
- Car dashboard: You can drive a car (abstract interface), but you **don’t need to know the engine mechanics**.

---

## Summary Table

| Pillar        | What It Means                            | Dart Feature Used            |
| ------------- | ---------------------------------------- | ---------------------------- |
| Inheritance   | Reuse code from parent class             | `extends`                    |
| Polymorphism  | One interface, multiple behaviors        | Method overriding            |
| Encapsulation | Hide internal details, control access    | `_private`, getter/setter    |
| Abstraction   | Show essential features, hide complexity | `abstract class`, interfaces |

---

## Final Notes:
- OOP promotes **modular, maintainable, and reusable code**.
- In Dart, **everything is an object**, even numbers and functions.
- Mastering these pillars is essential for building **scalable Flutter apps**.

---

Let me know if you want this expanded to include **interface usage**, **mixins**, or how OOP works in **Flutter widgets**.
