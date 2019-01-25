# Entity Component Systems FAQ
Frequently asked questions about Entity Component Systems (ECS). Disclaimer: I am the author of the open source [reflecs framework](https://github.com/SanderMertens/reflecs). Some of the answers below refer to documentation or features of reflecs, in which case this will be clearly indicated.

## General questions

### What is an Entity Component System?
ECS is an architecture paradigm for writing and organizing code. The key principles that define an ECS are a strict separation between data and logic (and therefore a lack of encapsulation) and the prominent role of composition in modeling data.

### What are examples of ECS implementations?
Here is a list of both open source and closed source ECS frameworks:

- Unity ECS (C#)
- Entitas (C#)
- AFRAME (HTML5 / JS)
- Specs (Rust)
- Artemis (Java)
- EnTT (C++)
- Reflecs (C)

### Where is ECS being used?
ECS is mostly used in gaming and simulation.

### Why should I use ECS?
ECS is often considered to promote code reusability and good performance. 

### What is the difference between ECS and OOP?
In OOP, business logic is built around objects and what objects _are_. The identity and class of an object are central to how the business logic is organized. Code is literally "oriented" around objects. Inheritance and polymorphism are mechanisms that at the core capture what an object is and what an object does. Encapsulation further emphasizes this, as the logic that mutates data is colocated on the object that stores the state.

ECS on the other hand has no notion of what an object is, but emphasizes what an object (entity) _has_, with composition taking a central role in ECS designs. Furthermore, data and business logic in ECS are strictly separated in components and systems, thus there is no notion of interaction. Business logic in ECS is executed on entities that match certain components, rather than invoking logic upon specific entities explicitly. Because of these differences, ECS is sometimes referred to as the "opposite of OOP".

### Can I mix ECS and OOP in the same application?
Yes.

### Is ECS considered to be faster than OOP?
In most cases, yes, although this highly depends on the ECS implementation. An ECS implementation that is implemented in a data-oriented way will be faster than the OOP equivalent. This is due component data being stored in contiguous arrays, which minimizes CPU cache misses. Business logic in ECS is expressed in "systems", which iterate over these arrays. Systems are executed consecutively on each entity in an array, which also reduces cache misses in the instruction cache.

Contrary to ECS, objects in OOP are often located in different parts of the heap, rather than being stored in arrays. This makes it harder for a CPU to predict where the next piece of data is going to be read from, which results in cache misses. Furthermore, polymorphism and the usage of virtual/overridable methods introduce indirections, and can cause the instruction cache to be flushed often, which can further reduce performance.

### Are ECS and Data Oriented Programming the same?
They are not the same, but they are related. ECS is often combined with data oriented programming to produce performant code.

### What is the different between Entity Component (EC) and Entity Component System (ECS)?
Confusingly, Entity Component is closer to OOP than to ECS. EC is the native architecture found in many game engines, and is essentially OOP with a larger emphasis on composition. Components in EC do contain behavior, where in ECS systems and components are strictly separated.

### Is ECS a subset or superset of OOP?
No. It is strictly possible to implement the rules of ECS in OOP, but this would not be very efficient.

### Is ECS a subset or superset of EC?
No, for the same reasons as OOP.

### Where should I start when I want to write an ECS application?
You have to decide whether you want to write your own ECS framework, or select an existing framework. Building your own ECS can be very educational but you should count on working for it for some time, as ECS frameworks internally can be quite complex. Make sure to read as much as you can about ECS, and try writing a simple project first. Trivial ECS examples are easy to follow and reason about, though actually writing an application in it requires a bit of a shift in mindset (if you are used to OOP).

### Where can I find resources to learn more about ECS?

## Technical questions

### What is an entity?

### What is a component?

### What is a system>?

### How are entities matched to systems?

### How are entities stored in memory?

### Can I add / remove components to entities at any moment in time?

### Can I create / delete entities at any moment in time?

### Can ECS be used in multithreaded applications?

### Can you define entity types?

### Can I reuse the same component for multiple purposes?

### How do I run my systems?

### Can I run systems periodically?

### Can I run systems when component values change?

### Can I run systems when I'm adding / removing components?

### How do I specify the ordering of my systems?

### Do I have to read/write component data inside systems?

### How do I specify parent-child relationships in ECS?

### How many entities, components and systems does a typical application have?

### How do I initialize component data?
