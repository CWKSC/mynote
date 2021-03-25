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

### Open-Closed Principle (OCP)

Open for Extension

but Closed for Modification

