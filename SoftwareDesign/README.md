Waterfall Model

Incremental Model

The Rapid Application Development (RAD) Model

Evolutionary Process Model

Prototyping Model

Spiral Model

Concurrent Engineering Model

Component based software engineering (CBSE)

## Class Diagram

define relationship between entity

### Composition 

A has B (Must/Compulsory)

B must included

e.g. A class contain fixed local variable link to B class

```java
class A {
    final B b = new B();
}
```

### Aggregation 

A has B (Optional)

```java
class A {
    B b;
    void setB(B b){ this.b = b; }
}
```

### Association 

A use B

more dynamic

```java
class A {
    void Foo(B b){ }
}
```

### Association and Multiplicity

[One] 1 or blank

[Zero or one] 0..1

[Zero or more] 0..*  or   *

[One or more] 1..*

[Specific range] a..b  4..7

A  1 --xxx--- 4 B

mean A xxx 4 B / B xxx 1 A

e.g Car 1 have 4 Wheel

## Roles of variable

Motivation, naming

use `i` as counter

use `sum` as accumulate

Constant / Fixed value

Stepper (Incrementor)

Most-recent holder (latest input value)

Gatherer (accumulator)

Transformation - hold value to divide compute 

One-way flag

Temporary

Organizer

## Use Case Diagrams

Objective: create semi-formal model of functional requirement

Analyze scope, external parties, interface, scenarios and reactions

define system boundary

identify primary actor, for each identify user goals

define use cases to match the goal

Secondary actor indirectly interact system or support use case to complete use case for primary actor

### \<\<Include\>\>

Must/Common include path

show lower-level task

### \<\<Extend\>\>

Option path (if then)

extension points

### Generalization (Inheritance)

 A -> B, from A to B indicate A inherit B

Actor can also be generalized

## Structure of Use Case Specification

Name

Purpose

Actor

Trigger

Preconditions

Flow of Event(Success Scenario)

Not allowed paths (if any)

Alternatives paths (if any)

Exceptions (if any)

Post conditions

Extension Points

## Sequence Diagram

Dynamic model

Class method calling sequence

Objects or Actor NOT Class

Object name before `:` (optional), `<name>:<type>`

Object, message, life-line, condition

sd stand for sequence diagram

### Message type

synchronous message - Solid triangle solid arrow left to right實線三角形實心箭咀 左指右

Reply message for synchronous message - Dotted arrow right to left 虛線箭咀 右指左

Asynchronous message - Solid arrow left to right 實線箭咀 左指右

Object creation message - Dotted arrow left to right 虛線箭咀 左指右

Return Value (Optional) - Dotted arrow right to left 右指左

### Sequence Numbering

Single Level (1, 2, 3, 4 ...)

Nested Level (1.1, 1.2, 2.2, 2.3 ...)

### Condition

`[condition]` on arrow

### Lost Message and Found Message

to and from black hole

### Reference (Ref) or InteractionUse

 

### CombinedFragments

describe control logic

Alternatives (alt)

Option (opt)

Iteration (loop)

Break (break out loop)

... etc

### Alternatives (alt)

if else 

`[condition]`

Dotted line on frame to divide then and else part

### Option (opt)

if (but no else)

### Break (break out loop)

if condition match, break out frame (inverse behavior of Option frame)

### Iteration (loop)

`loop`, `loop(3)`, `loop(1, *)`

`[condition]` to end of the loop

## Design Pattern

Class Design Principles

- Open-Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
- Dependency Inversion Principle (DIP)
- Single Responsibility Principle (SRP)
- Interface Segregation Principle (ISP)
- Law of Demeter Principle (LoD)

S.O.L.I.D

### Open-Closed Principle (OCP)

Open for Extension

but Closed for Modification

make all member private

### Liskov Substitution Principle (LSP)

subclass can be substiute of parent class

https://www.jyt0532.com/2020/03/22/lsp/

>If S is a subtype of T, then objects of type T may be replaced with objects of type S without altering any of the desirable properties of the program (correctness, task performed, etc.)

https://medium.com/@f40507777/%E9%87%8C%E6%B0%8F%E6%9B%BF%E6%8F%9B%E5%8E%9F%E5%89%87-liskov-substitution-principle-adc1650ada53

### Dependency Inversion Principle (DIP)

high level should not depend on low level

use interface for better extension

```java
// Bad
class A {
    B b = new B();
}
class B {}

// Good
class A {
    B b;
    A(B b) {
        this.b = b;
    }
}
interface B {}
```

### Single Responsibility Principle (SRP)

> Just Because You Can, Doesn't Mean You Should

Don't make function handle too many functionality

```java
// bad
class Powerful { 
    // mix function of A and B Class !
    void A_A();
    void A_B();
    // ... 100 line
    void B_A();
    void B_B();
}

// OK
class A {
    void A();
    void B();
}
class B {
    void A();
    void B();
}
```

https://medium.com/@f40507777/%E5%96%AE%E4%B8%80%E8%81%B7%E8%B2%AC%E5%8E%9F%E5%89%87-single-responsibility-principle-7b4eb03f1fff

### Interface Segregation Principle (ISP)

```java
// bad
class A {
    void B();
    void C();
    void D();
}
A a = new A();
a.B();// only use B() function

// good
class A implements IB, IC, ID { }
class IB { void B(); }
class IC { void C(); }
class ID { void D(); }
IB ib = new A();
ib.B();
```

https://www.jyt0532.com/2020/03/23/isp/

### Law of Demeter Principle (LoD)

> Don't talk to strangers

Each unity should only have limited knowledge about other units

```java
// bad
class A {
    B b;
    void Foo() {
        b.c.E();
	}
}
class B {
    C c;
}
class C {
    void E() { }
}

// Good
class A {
    B b;
    void Foo(){
        b.D()
	}
}
class B {
    C c;
    void D() { c.E(); }
}
class C {
    void E() {}
}
```

https://medium.com/@tonyhsu/%E8%BF%AA%E7%B1%B3%E7%89%B9-d2a375643b0f

## Gang-of-Four (GoF) Design Patterns

Creational

- Abstract Factory
- **Factory Method** 
- Builder
- Protoype
- **Singleton**

Structural

- **Facade**
- Adapter
- Bridge
- Composite
- Decorator
- Flyweight
- Proxy

Behavioral

- **Observer**
- Interpreter
- Template Method
- Chain of Responsibility
- **Command**
- Iterator
- Mediator
- Memento
- **State**
- **Strategy**
- Visitor

### State Pattern

object alter behavior when internal state change

object behavior depend on its state

State Interface implement by concrete class

Context Class contain State

```java
// ok
class A {
    void Foo();
}
class B : A { void Foo(); }
class C : A { void Foo(); }
class D : A { void Foo(); }
A a = new B() / C() / D();
a.Foo();

// better
class A {
    IFoo ifoo;
    A() { ifoo = new B() / C() / D(); }
    void Foo() { ifoo.Foo(); }
}
interface IFoo { void Foo(); }
class B implements IFoo { void Foo(); }
class C implements IFoo { void Foo(); }
class D implements IFoo { void Foo(); }
A a = new A();
a.Foo();
```

but number of object will increase

### Strategy Pattern

similar to state pattern, but only one function for each state

since state create a lot instance object

Strategy pass to context as parameter

State are create by context 

```java
class A {
    IFoo ifoo;
    void Foo() { ifoo.Foo(); }
}
interface IFoo { void Foo(); }
class B implements IFoo { void Foo(); }
class C implements IFoo { void Foo(); }
class D implements IFoo { void Foo(); }
A a = new A();
a.ifoo = new B() / C() / D();
a.Foo();
```

### Singleton

create a static instance in class

always only one

```java
class A {
    static final A instance = new A();
}
A.instance // access
```

provide access in everywhere

### Façade Pattern

provide simple interface to access

hide the backend detail

https://dotblogs.com.tw/jesperlai/2018/04/15/153646

### Factory Method Pattern

define interface to create object

object creation in run-time

https://carsonwah.github.io/factory-design-pattern.html

### Observer Pattern

broadcast and subscribe

notify/update 

https://notfalse.net/10/observer-pattern

### Command Pattern

log, redo, undo

Command interface

Invoker, Client, Receiver

https://notfalse.net/4/command-pattern

## Ethics

- Descriptive ethics
- Applied ethics

### Four Virtues

- Prudence
- Temperance
- Fortitude
- Justice

### Five P's

- Purpose
- Pride
- Patience
- Persistence
- Perspective



