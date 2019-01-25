# Entity Component Systems FAQ
Frequently asked questions about Entity Component Systems (ECS). Disclaimer: I am the author of the open source [reflecs framework](https://github.com/SanderMertens/reflecs). Some of the answers below refer to documentation or features of reflecs, in which case this will be clearly indicated.

## General questions

### What is an Entity Component System?
ECS is an architecture paradigm for writing and organizing code. The key principles that define an ECS are a strict separation between data and logic (and therefore a lack of encapsulation) and the prominent role of composition in modeling data.

### What are examples of ECS implementations?
Here is a list of both open source and closed source ECS frameworks:

- [Unity ECS](https://unity3d.com/learn/tutorials/topics/scripting/introduction-ecs) (C#)
- [Entitas](https://github.com/sschmid/Entitas-CSharp) (C#, support for others)
- [AFRAME](https://aframe.io/) (HTML5 / JS)
- [Specs](https://slide-rs.github.io/specs/) (Rust)
- [Artemis](https://github.com/junkdog/artemis-odb) (Java, support for others)
- [EnTT](https://github.com/skypjack/entt) (C++)
- [EntityX](https://github.com/alecthomas/entityx) (C++)
- [Reflecs](https://github.com/SanderMertens/reflecs) (C)

### Where is ECS being used?
ECS is mostly used in gaming and simulation.

### Why should I use ECS?
ECS is often considered to promote code reusability and good performance.

### Where can I find ECS example code?
These projects are ECS examples written in Reflecs ECS:
- https://github.com/SanderMertens/ecs_nbody
- https://github.com/SanderMertens/ecs_collisions
- [Reflecs examples](https://github.com/SanderMertens/reflecs/tree/master/examples)

This is a page with Entitas examples:
- https://github.com/sschmid/Entitas-CSharp/wiki/Example-projects

This is an example of a Pong game written in EnTT:
- https://github.com/DomRe/EnttPong

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

### What is the difference between EC and ECS?
Confusingly, Entity Component is closer to OOP than to ECS. EC is the native architecture found in many game engines, and is essentially OOP with a larger emphasis on composition. Components in EC do contain behavior, where in ECS systems and components are strictly separated.

### Is ECS a subset or superset of OOP?
No. It is strictly possible to implement the rules of ECS in OOP, but this would not be very efficient, nor would it conform to the rules of OOP (like encapsulation).

### Is ECS a subset or superset of EC?
No, for the same reasons as OOP.

### Where should I start when I want to write an ECS application?
You have to decide whether you want to write your own ECS framework, or select an existing framework. Building your own ECS can be very educational but you should count on working for it for some time, as ECS frameworks internally can be quite complex. 

Make sure to read as much as you can about ECS, and try writing a simple project first. Trivial ECS examples are easy to follow though actually writing an application in it requires a bit of a shift in mindset (if you are used to OOP).

### Where can I find resources to learn more about ECS?
Unity has a few excellent introduction videos on ECS: https://unity3d.com/learn/tutorials/topics/scripting/introduction-ecs. If you found a good resource, let me know in an issue and I will add it here.

## Technical questions

### What is an entity?
An entity is a unique identifier (often a 32bit or 64bit integer) that identifies a list of components.

### What is a component?
A component can be any data type. Components can be added and removed to entities.

### What is a system?
A system is a function (code) that subscribes for a combination of components. If an entity has all the components that a system subscribes for, it will be matched with that system, and the system logic will be evaluated for that entity.

### How are entities stored in memory?
This depends on the ECS framework. Typically entities are stored in internal tables (arrays) that are organized by a combination of components. For example, all entities with components (A, B) will be stored in the table (A, B), all entities with components (A, C) will be stored in table (A, C) and so on.

### How are entities matched to systems?
Systems are matched against tables instead of individual entities (if this is how the ECS stores the entities). The set of tables typically stabilizes fast in an application, and thus matching happens very infrequently, even if entities are created / deleted often. If components are added or removed from entities, they will move to a different table.

### Can I add / remove components to entities at any moment in time?
This depends on the ECS framework. As systems are iterating over an array, making modifications to that array can have undesired side effects. It is important to understand how an ECS framework handles this.

[Reflecs](https://github.com/SanderMertens/reflecs) allows you to add/remove components at any time.

### Can I create / delete entities at any moment in time?
This depends on the ECS framework. As systems are iterating over an array, adding or deleting rows from that array can have undesired side effects. It is important to understand how an ECS framework handles this.

[Reflecs](https://github.com/SanderMertens/reflecs) allows you to create/delete entities at any time.

### Can ECS be used in multithreaded applications?
This depends on the framework. Some ECS frameworks explicitly support multithreading (Unity, Specs, [Reflecs](https://github.com/SanderMertens/reflecs)) while others are not thread safe and leave this up to the application.

ECS frameworks that are multithreaded often take advantage of the fact that, since all data is stored in arrays, work can be easily distributed to worker threads.

### Can you define entity types?
This depends on the framework, though usually ECS frameworks have the notion of "archetype" entites, or "tags". An archetype is a named group of components that a certain kind of entity always has. A tag is an empty component that is just there to be able to quickly identify entities.

Care must be taken to not lend to much importance to entity types. A properly designed ECS application does not emphasize what an object _is_, but what an object _has_. If you find yourself in a situation where adding one component should prevent adding another component, you are probably trying to impose OOP on ECS (after all, an object can't be two things at once!).

Reflecs supports tags and archetypes (they are called "families"). Additionally, [Reflecs](https://github.com/SanderMertens/reflecs) supports "prefabs", which in addition to specifying a named list of components, also store component values. This mechanism is similar to how prefabs work in Unity EC.

### Can I reuse the same component for multiple purposes?
No. Entity Component Systems have a nominal type system, which is a fancy way of saying that types (components) are identified by name, and you should not reuse the same structure for different purposes. The reason for this is that a system subscribes for a component, and needs to be able to process the component data without context. Therefore, the meaning of a component must be consistent across all entities.

### How do I run a system?
This depends on the ECS framework. Some ECS frameworks require you to run your systems manually, whereas others run the systems for you. In [Reflecs](https://github.com/SanderMertens/reflecs), you declare the systems, after which they will be automatically invoked in the main loop.

### Can I run systems periodically?
This depends on the ECS framework. In [Reflecs](https://github.com/SanderMertens/reflecs), you can specify a time interval at which a system needs to be ran.

### Can I run systems when component values change?
This depends on the ECS framework. In [Reflecs](https://github.com/SanderMertens/reflecs), you can specify that a system should be invoked when a component value is set.

### Can I run systems when I'm adding / removing components?
This depends on the ECS framework. In [Reflecs](https://github.com/SanderMertens/reflecs), you can specify that a system should be invoked when a component is added or removed.

### How do I specify the ordering of my systems?
This depends on the ECS framework, but is an important part of ECS design. In an ideal world, systems have no dependencies and can be ran in any order. In practice however, this is seldomly the case. Each ECS framework approaches this problem differently. In Unity ECS for example, you can specify the dependencies of a system (systems that should run before the system).

[Reflecs ECS](https://github.com/SanderMertens/reflecs) promotes a design in which systems are decoupled as much as possible. It is not possible to specify per-system dependencies, as this would mean that a system requires knowledge about other systems. Instead, reflecs has two strategies for defining system order. First of all, systems can specify a stage in which they should be ran. There are five stages (OnLoad, PreFrame, OnFrame, PostFrame, OnStore), each with a specific purpose. Within a stage, systems are executed in order of declaration.

### Do I have to read/write component data inside systems?
No, though it is recommended to do so. When you access a component outside of a system, an ECS framework needs to do a lookup to first see if the entity has the component, and where it is stored. When components are accessed inside a system, the ECS framework knows the interest of the system beforehand, and since data is stored in an array, can precompute the locations of the components for you, which improves performance. 

### How do I specify parent-child relationships in ECS?
This depends on the ECS framework. In Reflecs ECS, you can add "Container" entities to entities.

### How many entities, components and systems does a typical application have?
This highly depends on the application. Anywhere between a dozen, hundreds, or maybe even thousands of components and systems. The number of entities is tightly coupled with how many objects your game or simulation has.

### How do I initialize component data?
This depends on the ECS framework and programming language. An OOP language may let you initialize components in constructors. In [Reflecs ECS](https://github.com/SanderMertens/reflecs), you can initialize components with systems that are invoked when a component is added to an entity, or with prefabs.
