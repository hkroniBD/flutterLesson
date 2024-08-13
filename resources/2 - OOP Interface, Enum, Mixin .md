## Lecture: Advanced Object-Oriented Programming in Dart

### Introduction

In this lecture, we will explore advanced OOP concepts in Dart, including interfaces, mixins, and enums. These concepts help in writing modular, reusable, and maintainable code.

### Interfaces in Dart

An interface in Dart is a way to define a contract that a class can implement. Unlike some other languages, Dart does not have a special keyword for interfaces. Instead, any class can be used as an interface.

#### Implementing Interfaces

To implement an interface, a class must provide concrete implementations for all the methods defined in the interface.

#### Example

```dart
// Defining an interface using a class
class Animal {
  void makeSound();
}

// Implementing the interface
class Dog implements Animal {
  @override
  void makeSound() {
    print('Bark');
  }
}

class Cat implements Animal {
  @override
  void makeSound() {
    print('Meow');
  }
}

void main() {
  Animal dog = Dog();
  dog.makeSound(); // Output: Bark

  Animal cat = Cat();
  cat.makeSound(); // Output: Meow
}
```

### Mixins in Dart

Mixins are a way of reusing a class's code in multiple class hierarchies. In Dart, mixins are used to add functionality to classes without using inheritance.

#### Creating and Using Mixins

Mixins are created using the `mixin` keyword. They can then be included in other classes using the `with` keyword.

#### Example

```dart
// Defining a mixin
mixin Walk {
  void walk() {
    print('Walking');
  }
}

// Defining another mixin
mixin Swim {
  void swim() {
    print('Swimming');
  }
}

// Using mixins in a class
class Animal {
  void makeSound() {
    print('Animal sound');
  }
}

class Dog extends Animal with Walk, Swim {
  @override
  void makeSound() {
    print('Bark');
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Output: Bark
  dog.walk(); // Output: Walking
  dog.swim(); // Output: Swimming
}
```

### Enums in Dart

Enums, short for enumerations, are a way to define a set of named values. They are useful when you need a fixed set of constant values.

#### Defining and Using Enums

Enums are defined using the `enum` keyword. Each value in an enum is a constant.

#### Example

```dart
// Defining an enum
enum Color {
  red,
  green,
  blue,
}

// Using enums in a class
class Car {
  String brand;
  Color color;

  Car(this.brand, this.color);

  void display() {
    print('Brand: $brand, Color: $color');
  }
}

void main() {
  Car car1 = Car('Toyota', Color.red);
  car1.display(); // Output: Brand: Toyota, Color: Color.red

  Car car2 = Car('Honda', Color.green);
  car2.display(); // Output: Brand: Honda, Color: Color.green
}
```

### Combining Concepts

You can combine interfaces, mixins, and enums to create powerful and flexible designs.

#### Example

```dart
// Interface
class CanFly {
  void fly();
}

// Mixin
mixin CanWalk {
  void walk() {
    print('Walking');
  }
}

// Enum
enum BirdType {
  sparrow,
  eagle,
}

// Class implementing interface and using mixin
class Bird implements CanFly with CanWalk {
  BirdType type;

  Bird(this.type);

  @override
  void fly() {
    print('Flying');
  }

  void display() {
    print('Bird type: $type');
    walk();
    fly();
  }
}

void main() {
  Bird bird = Bird(BirdType.eagle);
  bird.display();
  // Output: 
  // Bird type: BirdType.eagle
  // Walking
  // Flying
}
```

### Summary

- **Interfaces**: Define contracts that classes can implement.
- **Mixins**: Add functionality to classes without using inheritance.
- **Enums**: Define a set of named constant values.

### Homework

1. Create an interface `CanDrive` with a method `drive()`. Implement this interface in a `Car` class.
2. Create a mixin `CanFly` with a method `fly()`. Use this mixin in a `Bird` class.
3. Define an enum `VehicleType` with values `car`, `truck`, and `motorcycle`. Use this enum in a `Vehicle` class and create instances of different vehicle types.
4. Combine all the concepts to create a class `FlyingCar` that can drive and fly, and has a type defined using an enum.
