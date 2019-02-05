# Entity Component Systems FAQ
Frequently asked questions about Entity Component Systems (ECS). Disclaimer: I am the author of the open source [reflecs](https://github.com/SanderMertens/reflecs) framework. Some of the answers below refer to documentation or features of reflecs, in which case this will be clearly indicated.

If you would like to submit additional questions, or otherwise make changes to the FAQ, feel free to submit an issue or PR.

**General questions:**
- [What is ECS?](#what-is-ecs)
- [Where is ECS used?](#where-is-ecs-used)
- [Why should I use ECS?](#why-should-i-use-ecs)
- [What are examples of ECS implementations?](#what-are-examples-of-ecs-implementations)
- [Where can I find ECS example code?](#where-can-i-find-ecs-example-code)
- [Where should I start when I want to write an ECS application?](#where-should-i-start-when-i-want-to-write-an-ecs-application)
- [Where can I find resources to learn more about ECS?](#where-can-i-find-resources-to-learn-more-about-ecs)
- [What is the difference between ECS and OOP?](#what-is-the-difference-between-ecs-and-oop)
- [Can I mix ECS and OOP in the same application?](#can-i-mix-ecs-and-oop-in-the-same-application)
- [Is ECS considered to be faster than OOP?](#is-ecs-considered-to-be-faster-than-oop)
- [Are ECS and Data Oriented Programming the same?](#are-ecs-and-data-oriented-programming-the-same)
- [Isn't ECS basically just arrays of structs with functions?](#isnt-ecs-basically-just-arrays-of-structs-with-functions)
- [What is the difference between EC and ECS?](#what-is-the-difference-between-ec-and-ecs)
- [Is ECS a subset or superset of OOP?](#is-ecs-a-subset-or-superset-of-oop)
- [Is ECS a subset or superset of EC?](#is-ecs-a-subset-or-superset-of-ec)

**Technical questions:**
- [What is an entity?](#what-is-an-entity)
- [What is a component?](#what-is-a-component)
- [What is a system?](#what-is-a-system)
- [How are entities stored in memory?](#how-are-entities-stored-in-memory)
- [How are entities matched to systems?](#how-are-entities-matched-to-systems)
- [Can I add / remove components to entities at any moment in time?](#can-i-add--remove-components-to-entities-at-any-moment-in-time)
- [Can I create / delete entities at any moment in time?](#can-i-create--delete-entities-at-any-moment-in-time)
- [Can ECS be used in multithreaded applications?](#can-ecs-be-used-in-multithreaded-applications)
- [Can you define entity types?](#can-you-define-entity-types)
- [Can I reuse the same component for multiple purposes?](#can-i-reuse-the-same-component-for-multiple-purposes)
- [How do I run a system?](#how-do-i-run-a-system)
- [Can I run systems periodically?](#can-i-run-systems-periodically)
- [Can I run systems when component values change?](#can-i-run-systems-when-component-values-change)
- [Can I run systems when I'm adding / removing components?](#can-i-run-systems-when-im-adding--removing-components)
- [How do I specify the ordering of my systems?](#how-do-i-specify-the-ordering-of-my-systems)
- [Do I have to read/write component data inside systems?](#do-i-have-to-readwrite-component-data-inside-systems)
- [How do I specify parent-child relationships in ECS?](#how-do-i-specify-parent-child-relationships-in-ecs)
- [How many entities, components and systems does a typical application have?](#how-many-entities-components-and-systems-does-a-typical-application-have)
- [How do I initialize component data?](#how-do-i-initialize-component-data)

## General questions

### What is ECS?
ECS is an architecture paradigm for writing and organizing code. The key principles that define ECS are a strict separation between data and logic (and therefore a lack of encapsulation) and the prominent role of composition in modeling data. ECS can be summarized with four simple rules:

- Entities are unique identifiers
- Components are plain datatypes
- Entities can contain zero or more components
- Systems are logic executed on entities with matching component sets

### Where is ECS used?
ECS is mostly used in gaming and simulation.

### Why should I use ECS?
ECS is considered to promote code reusability and good performance. If you are building a game with large numbers of objects, or want to write code that can be easily reused for other projects, ECS is worth looking into.

### What are examples of ECS implementations?
Here is a non-exhaustive list of both open source and closed source ECS frameworks:

- [AFRAME](https://aframe.io) (HTML5 / JS)
- [anax](https://github.com/miguelmartin75/anax) (C++)
- [Artemis](https://github.com/junkdog/artemis-odb) (Java, support for others)
- [ecst](https://github.com/SuperV1234/ecst) (C++)
- [Entitas](https://github.com/sschmid/Entitas-CSharp) (C#, support for others)
- [EntityX](https://github.com/alecthomas/entityx) (C++)
- [EnTT](https://github.com/skypjack/entt) (C++)
- [Esper](https://github.com/benmoran56/esper)
- [Reflecs](https://github.com/SanderMertens/reflecs) (C)
- [Specs](https://slide-rs.github.io/specs/) (Rust)
- [Unity ECS](https://unity3d.com/learn/tutorials/topics/scripting/introduction-ecs)* (C#)

* Note that Unity GameObjects are _not_ ECS. See the link for more information.

### Where can I find ECS example code?
This is a page with Entitas examples:
- https://github.com/sschmid/Entitas-CSharp/wiki/Example-projects

This is an example of a Pong game written in EnTT:
- https://github.com/DomRe/EnttPong

These are projects written in Reflecs:
- https://github.com/SanderMertens/ecs_nbody
- https://github.com/SanderMertens/ecs_collisions
- https://github.com/SanderMertens/reflecs/tree/master/examples

### Which game engines use ECS?
There are a few game engines that support ECS natively:
- [Unity](https://unity3d.com/) (C#, partially ECS)
- [Amethyst](https://amethyst.rs/) (Rust, pure ECS)
- [Reflecs](https://github.com/SanderMertens/reflecs) (C, pure ECS)

### Where should I start when I want to write an ECS application?
You have to decide whether you want to write your own ECS framework, or select an existing framework. Building your own ECS can be very educational, but count on spending a fair amount of time on it, as ECS frameworks can be quite complex internally. Regardless of what you do, try to read as much as you can about ECS. 

Once you have an ECS framework, try writing a simple game. Trivial ECS examples are easy to follow, but writing a whole game in it requires a shift in mindset, and you will likely need to try a few times before you get it right.

### Where can I find resources to learn more about ECS?
- [Unity introduction video to ECS](https://unity3d.com/learn/tutorials/topics/scripting/introduction-ecs)
- [Blog explaining performance & maintenance benefits of ECS vs. OOP](https://medium.com/ingeniouslysimple/entities-components-and-systems-89c31464240d)
- [Collection of resources on ECS](https://github.com/jslee02/awesome-entity-component-system)
- [Blog explaining how to build a simple ECS](https://blog.therocode.net/2018/08/simplest-entity-component-system)
- [https://www.youtube.com/watch?v=3-ityWN-FdE&feature=youtu.be] Video from Scott McMillan explaining CPU caching

If you found a good resource, let me know in an issue and I will add it here.

### What is the difference between ECS and OOP?
In OOP, classes describes how _objects_ behave. The responsibility of defining what an object _is_ and what an object _does_ lies only with its class, and state (members) and behavior (methods) are always tightly coupled by the class. A class therefore is a full description of the behavior of a single object. Encapsulation ensures that a method only mutates members of an object on which it is invoked. 

ECS has no notion of classes. Instead, objects (entities) are composed out of a set of simple datatypes (components). A component in ECS is data only and may not contain any behavior. Instead, behavior in ECS is organized in functions (systems) that are dynamically matched against matching entities, based on their set of components. For example, an entity may have a 'Position' and 'Speed' component, which both are plain datatypes representing a coordinate and speed. A 'Move' system could then subscribe for any entity that has 'Position' and 'Speed', and update the position according to the speed.

Because ECS promotes separation of data and behavior, it is sometimes referred to as the "opposite of OOP".

### Can I mix ECS and OOP in the same application?
Yes.

### Is ECS faster than OOP?
When the same logic is expressed in both ECS and OOP, the ECS variant is likely to be faster. This is particularly noticeable when dealing with large numbers of entities. The reason for the difference in speed is that the ECS architecture allows for more efficient data storage and retrieval by the CPU, which results in far fewer CPU cache misses.

An efficient ECS framework would store components in contiguous arrays. When a CPU requests the value from an address in RAM, it also prefetches a number of bytes that come after the requested value. If subsequent RAM requests use those prefetched values, data retrieval is very fast, since it is already in the CPU cache.

OOP in contrary, stores objects in individual RAM segments. Because objects often heavily reference each other, CPUs have to jump around in RAM, making it very difficult (if not impossible) to predict which address to fetch next. When an address is not in the CPU cache, but must be fetched from RAM, it is considered to be a "cache miss". Since accessing data from RAM directly can be up to 200x slower than accessing data from the CPU cache, OOP code can run significantly slower than ECS code.

This does assume that the ECS framework stores data in the most efficient way possible.

### Are ECS and Data Oriented Programming the same?
They are not the same, but they are related. ECS is often combined with data oriented programming to produce performant code.

### Isn't ECS basically just arrays of structs with functions?
No. ECS is a architecture paradigm, which makes no assumptions about how data is represented. Having said that, ECS frameworks often store entities in arrays, and use functions (or equivalent) to run logic.

To say that these frameworks are "just arrays of structs with functions" though would be a bit reductionist. An ECS framework lets you express at a high level which components systems are interested in. This is then matched by the ECS framework to the entity tables (arrays). This matching logic can be quite sophisticated, as frameworks can support features like excluding components, optional components, and/or matching and so on.

In addition to the matching logic, ECS frameworks often have clever strategies for storing entities in a way that is most efficient for cache efficiency. Frameworks may store each component in a dedicated table, or create tables for every occuring combination of components. Frameworks may be able to match these tables to systems once, instead of matching them in every iteration.

ECS frameworks can do these things while exposing a relatively simple set of high level operations for creating/deleting entities, adding/removing components and creating/running systems. This allows you to write high-performant code, without having to worry about managing all these arrays yourself.

### What is the difference between EC and ECS?
Entity Component (EC) is an architecture that has entities and components, like ECS, but contrary to ECS, components can have logic. EC is essentially OOP, in that it uses features like encapsulation, inheritance and polymorphism, but it puts a bigger emphasis on composition. It is a popular architecture in game engines, as it is familiar to developers that know OOP, and makes it easy to add and remove behavior to an object.

EC code is generally slower than the equivalent code in ECS, for the same reasons as mentioned [here](#is_ecs_faster_than_oop).

### Is ECS a subset or superset of OOP?
No. It is strictly possible to implement the rules of ECS in OOP, but this would not be very efficient, nor would it be canonical OOP (like encapsulation).

### Is ECS a subset or superset of EC?
No, for the same reasons as it isn't a subset or superset of OOP.

## Technical questions

### What is an entity?
An entity is a unique identifier (often a 32bit or 64bit integer) that identifies a list of components.

### What is a component?
A component can be any data type. Components can be added and removed to entities.

### What is a system?
A system is logic (typically a function) that subscribes for a combination of components. If an entity has all the components that a system subscribes for, it will be matched with that system, and the system logic will be evaluated for that entity.

### How are entities stored in memory?
This depends on the ECS framework. Typically entities are stored in internal tables (arrays) that are organized by a combination of components. For example, all entities with components (A, B) will be stored in the table (A, B), all entities with components (A, C) will be stored in table (A, C) and so on.

### How are entities matched to systems?
Systems are matched against tables instead of individual entities (if this is how the ECS stores the entities). The set of tables typically stabilizes fast in an application, and thus matching happens very infrequently, even if entities are created / deleted often. If components are added or removed from entities, they will move to a different table.

### Can I add / remove components to entities at any moment in time?
This depends on the ECS framework. As systems are iterating over an array, making modifications to that array can have undesired side effects. It is important to understand how an ECS framework handles this, as this can lead to errors that are hard to debug.

### Can I create / delete entities at any moment in time?
This depends on the ECS framework. As systems are iterating over an array, adding or deleting rows from that array can have undesired side effects. It is important to understand how an ECS framework handles this, as this can lead to errors that are hard to debug.

### Can ECS be used in multithreaded applications?
This depends on the framework. Some ECS frameworks explicitly support multithreading (Unity, Specs, [Reflecs](https://github.com/SanderMertens/reflecs)) while others are not thread safe and leave this up to the application.

ECS frameworks that are multithreaded often take advantage of the fact that, since all data is stored in arrays, work can be easily distributed to worker threads.

### Can you define entity types?
This depends on the framework, though usually ECS frameworks have the notion of "archetype" entites, or "tags". An archetype is a named group of components that a certain kind of entity always has. A tag is an empty component that is just there to be able to quickly identify entities.

Care must be taken to not lend to much importance to entity types. A properly designed ECS application does not emphasize what an object _is_, but what an object _has_. If you find yourself in a situation where adding one component should prevent adding another component, you are probably trying to impose OOP on ECS (after all, an object can't be two things at once!).

### Can I reuse the same component for multiple purposes?
No. Entity Component Systems require a nominal type system, which is a fancy way of saying that types (components) are identified by name, and you should not reuse the same structure for different purposes. The reason for this is that a system subscribes for a component, and needs to be able to process the component data without context. Therefore, the meaning of a component must be consistent across all entities.

Note however that while an _ECS framework_ must be able to uniquely identify components, you can still reuse the same _programming language_ type for different components. For example, if your application has a _type_ called `Vector2D`, you could register that type under the `Position` and `Velocity` _component_ identifiers.

### How do I run a system?
This depends on the ECS framework. Some ECS frameworks require you to run your systems manually, whereas others run the systems for you. 

### Can I run systems periodically?
This depends on the ECS framework. Some ECS frameworks let you specify an interval at which systems are ran.

### Can I run systems when component values change?
This depends on the ECS framework. Some ECS frameworks let you define systems that are executed when components are assigned a value.

### Can I run systems when I'm adding / removing components?
This depends on the ECS framework. Some ECS frameworks let you define systems that are executed when components are added or removed.

### How do I specify the ordering of my systems?
This depends on the ECS framework, but is an important part of ECS design. In an ideal world, systems have no dependencies and can be ran in any order. In practice however, this is seldomly the case. Each ECS framework approaches this problem differently. In Unity ECS for example, you can specify the dependencies of a system (systems that should run before the system).

Different strategies for ordering systems are:
- Specify system dependencies, and let the ECS framework do automatic ordering
- Specify system order manually
- Assign systems to different stages, and execute the stages in a well-defined sequence

### Do I have to read/write component data inside systems?
No, though it may be faster to do so. When you access a component outside of a system, an ECS framework needs to do a lookup to first see if the entity has the component, and where it is stored. When components are accessed from inside a system, the ECS framework knows the interest of the system beforehand, and since data is stored in an array, it can precompute the locations of the components for you, which improves performance.

Note that different ECS implementations may or may not choose to implement this optimization.

### How do I specify parent-child relationships in ECS?
This depends on the ECS framework. In Reflecs ECS, you can add "Container" entities to entities.

### How many entities, components and systems does a typical application have?
This highly depends on the application. Anywhere between a dozen, hundreds, or maybe even thousands of components and systems. The number of entities is tightly coupled with how many "things" your game or simulation has.

### How do I initialize component data?
This depends on the ECS framework and programming language. An OOP language may let you initialize components in constructors. Other ECS frameworks may offer custom mechanisms for initializing data.
