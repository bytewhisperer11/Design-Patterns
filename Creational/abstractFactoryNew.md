# Abstract Factory Pattern

## Definition
The Abstract Factory Pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It allows a client to create objects that belong to a specific family, ensuring compatibility among them.

## Intent
- To provide a way to create objects without specifying the exact class of the object that will be created.
- To allow the creation of families of related or dependent objects.

## Problem
- You need to create objects that are part of a family, and you want to ensure they work well together.
- The client code needs to be independent of the specific classes being instantiated.
- You want to manage a complex system of interrelated objects without tightly coupling the code to concrete implementations.

## Solution
- Define an abstract factory interface that declares methods for creating abstract products.
- Create concrete factory classes that implement the abstract factory interface, providing implementations for the product creation methods.
- The client interacts with the factory to create objects without needing to know their specific classes.

## Key Components
- **Abstract Factory:** The interface that declares methods for creating abstract products.
- **Concrete Factory:** The classes that implement the abstract factory interface and instantiate specific products.
- **Abstract Product:** The interface that defines the product type to be created.
- **Concrete Product:** The classes that implement the abstract product interface, representing specific products.
- **Client:** The code that uses the abstract factory to create products without depending on their concrete implementations.

## Coding Example

```typescript
// Abstract Products
interface Button {
    render(): void;
}

interface Checkbox {
    render(): void;
}

// Concrete Products
class WindowsButton implements Button {
    render() {
        console.log("Rendering a Windows button.");
    }
}

class MacButton implements Button {
    render() {
        console.log("Rendering a Mac button.");
    }
}

class WindowsCheckbox implements Checkbox {
    render() {
        console.log("Rendering a Windows checkbox.");
    }
}

class MacCheckbox implements Checkbox {
    render() {
        console.log("Rendering a Mac checkbox.");
    }
}

// Abstract Factory
interface GUIFactory {
    createButton(): Button;
    createCheckbox(): Checkbox;
}

// Concrete Factories
class WindowsFactory implements GUIFactory {
    createButton(): Button {
        return new WindowsButton();
    }
    createCheckbox(): Checkbox {
        return new WindowsCheckbox();
    }
}

class MacFactory implements GUIFactory {
    createButton(): Button {
        return new MacButton();
    }
    createCheckbox(): Checkbox {
        return new MacCheckbox();
    }
}

// Client Code
function clientCode(factory: GUIFactory) {
    const button = factory.createButton();
    const checkbox = factory.createCheckbox();
    
    button.render();
    checkbox.render();
}

// Usage
let factory: GUIFactory;

const isWindows = true; // Change to false for Mac
if (isWindows) {
    factory = new WindowsFactory();
} else {
    factory = new MacFactory();
}

clientCode(factory);
