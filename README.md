# Entity Component System FAQ
This FAQ is for anyone interested in ECS & modern, high performance game development. The goal is for answers to be short & correct, but not necessarily complete. The [Resources section](#Resources) contains more in-depth articles.

If you find anything missing or incorrect in the FAQ, feel free to create an issue or PR!

## About me
I'm the author of [Flecs](https://github.com/SanderMertens/flecs), an Entity Component System for C & C++. I'm always experimenting with better ways to implement ECS features, and write about it if I can. If you're interested in discussing ECS, [join the Discord](https://discord.gg/BEzP5Rgrrp)!

## General Questions
- [What is ECS?](#what-is-ecs)
- [When is something an ECS?](#when-is-something-an-ecs)
- [Why is ECS used?](#why-is-ecs-used)
- [Who is using ECS?](#who-is-using-ecs)
- [How is ECS different from OOP?](#how-is-ecs-different-from-oop)
- [How is ECS different from Entity-Component frameworks?](#how-is-ecs-different-from-entity-component-frameworks)
- [Is ECS hard to learn?](#is-ecs-hard-to-learn)
- [Is ECS a lower level of abstraction?](#is-ecs-a-lower-level-of-abstraction)
- [Does ECS require writing more code?](#does-ecs-require-writing-more-code)
- [Is ECS good for low-level code?](#is-ecs-good-for-low-level-code)
- [Can ECS be implemented in any language?](#can-ecs-be-implemented-in-any-language)
- [Should I write my own ECS?](#should-i-write-my-own-ecs)
- [Is ECS fast?](#is-ecs-fast)
- [Is ECS code more reusable?](#is-ecs-code-more-reusable)
- [Is ECS good for multithreading?](#is-ecs-good-for-multithreading)
- [Can ECS be used outside of gaming?](#can-ecs-be-used-outside-of-gaming)
- [How do I start with ECS?](#how-do-i-start-with-ecs)
- [How do I design for ECS?](#how-do-i-write-for-ecs)
- [What are the different ways to implement an ECS?](#what-are-the-different-ways-to-implement-an-ecs)
- [How are components modified?](#how-are-components-modified)
- [How are entities matched with systems?](#how-are-entities-matched-with-systems)
- [What are entity relationships?](#what-are-entity-relationships)

## How-to
- [How to create a hierarchy in ECS?](#how-to-create-a-hierarchy-in-ecs)
- [How to store spatial data in ECS?](#how-to-store-spatial-data-in-ecs)

## Data Oriented Design Questions
- [What is Data Oriented Design?](#what-is-data-oriented-design)
- [Is ECS the same as DoD?](#is-ecs-the-same-as-dod)
- [What is Random Access Memory?](#what-is-random-access-memory)
- [What is a CPU cache?](#what-is-a-cpu-cache)
- [What is a cache line](#what-is-a-cache-line)
- [What is locality of reference?](#what-is-locality-of-reference)
- [What is SIMD?](#what-is-simd)
- [What is vectorization?](#what-is-vectorization)
- [What is false sharing?](#what-is-false-sharing)
- [What is AoS?](#what-is-aos)
- [What is SoA?](#what-is-soa)
- [What is branch prediction?](#what-is-branch-prediction)

## Glossary
- [Entity](#entity)
- [Component](#component)
- [Tag](#tag)
- [System](#system)
- [Query](#query)
- [World](#world)
- [Registry](#registry)
- [Table](#table)
- [Archetype](#archetype)

## ECS frameworks
The current list includes both open and closed source ECS implementations, and engines that have adopted ECS pattern. Projects that had no activity in the past year are not included.

- [AFRAME](https://aframe.io) (HTML5/JS, MIT)
- [Artemis](https://github.com/junkdog/artemis-odb) (Java, custom license)
- [Bevy ECS](https://github.com/bevyengine/bevy) (Rust, MIT)
- [Dominion](https://github.com/dominion-dev/dominion-ecs-java) (Java, MIT)
- [EntityX](https://github.com/alecthomas/entityx) (C++11, MIT)
- [Entitas](https://github.com/sschmid/Entitas-CSharp) (C#, MIT)
- [Entitas-Redux](https://github.com/jeffcampbellmakesgames/Entitas-Redux) (C#, MIT)
- [EnTT](https://github.com/skypjack/entt) (C++17, MIT)
- [Esper](https://github.com/benmoran56/esper) (Python, MIT)
- [Fireblade](https://github.com/fireblade-engine/ecs) (Swift, MIT)
- [Flecs](https://github.com/SanderMertens/flecs) (C/C++11, MIT)
- [Hecs](https://github.com/Ralith/hecs) (Rust, Apache/MIT)
- [Legion](https://github.com/amethyst/legion) (Rust, MIT)
- [LeoECS](https://github.com/Leopotam/ecs) (C#, MIT)
- [Nu](https://github.com/bryanedds/Nu) (F#, MIT)
- [Our Machinery](https://ourmachinery.com/) (C, commercial license)
- [Photon Quantum](https://doc.photonengine.com/en-us/quantum/current/getting-started/quantum-intro) (C#, Commercial license)
- [Shipyard](https://github.com/leudz/shipyard) (Rust, Apache/MIT)
- [Specs](https://github.com/amethyst/specs) (Rust, Apache/MIT)
- [Svelto](https://github.com/sebas77/Svelto.ECS) (C#, MIT)
- [tiny-ecs](https://github.com/bakpakin/tiny-ecs) (Lua, MIT)
- [Unity DOTS](https://unity.com/dots) (C#, commercial license)
- [Zig ECS](https://github.com/prime31/zig-ecs) (Zig, MIT)
- [luaecs](https://github.com/cloudwu/luaecs) (C/Lua, MIT)

## Resources
- [Overwatch Gameplay Architecture and Netcode](https://www.youtube.com/watch?v=W3aieHjyNvw) (Blizzard, GDC)
- [Data-Oriented Design and C++](https://www.youtube.com/watch?v=rX0ItVEVjHc) (Mike Acton, CppCon)
- [CPU caches and why you care](https://vimeo.com/97337258) (Scott Meyers, NDC)
- [Culling the Battlefield: Data Oriented Design in Practice](https://www.gdcvault.com/play/1014491/Culling-the-Battlefield-Data-Oriented) (DICE, GDC)
- [Game Engine Entity/Object systems](https://www.youtube.com/watch?v=jjEsB611kxs) (Bobby Anguelov, presentation)
- [Understanding Data Oriented Design for Entity Component Systems](https://www.youtube.com/watch?v=0_Byw9UMn9g) (Unity, GDC)
- [Understanding Data Oriented Design](https://learn.unity.com/tutorial/part-1-understand-data-oriented-design?courseId=60132919edbc2a56f9d439c3&signup=true&uv=2020.1) (Unity, Tutorial)
- [Data Oriented Design](https://www.dataorienteddesign.com/dodbook/dodmain.html) (Richard Fabian, book)
- [Entities, Components and Systems](https://medium.com/ingeniouslysimple/entities-components-and-systems-89c31464240d) (Mark Jordan, blog)
- [Awesome Entity Component System](https://github.com/jslee02/awesome-entity-component-system) (Jeongseok Lee, link collection)
- [Why Vanilla ECS is not enough](https://ajmmertens.medium.com/why-vanilla-ecs-is-not-enough-d7ed4e3bebe5) (Sander Mertens, blog)
- [Formalisation of Concepts behind ECS and Entitas](https://medium.com/@icex33/formalisation-of-concepts-behind-ecs-and-entitas-8efe535d9516) (Maxim Zaks, blog)
- [Entity Component System and Rendering](https://ourmachinery.com/post/ecs-and-rendering/) (Our Machinery, blog)
- [Specs and Legion, two very different approaches to ECS](https://csherratt.github.io/blog/posts/specs-and-legion/) (Cora Sherrat, blog)
- [Where are my Entities and Components](https://ajmmertens.medium.com/building-an-ecs-1-where-are-my-entities-and-components-63d07c7da742) (Sander Mertens, blog)
- [Archetypes and Vectorization](https://medium.com/@ajmmertens/building-an-ecs-2-archetypes-and-vectorization-fe21690805f9) (Sander Mertens, blog)
- [Building Games with Entity Relationships](https://ajmmertens.medium.com/building-games-in-ecs-with-entity-relationships-657275ba2c6c) (Sander Mertens, blog)
- [Making the most of Entity Identifiers](https://ajmmertens.medium.com/doing-a-lot-with-a-little-ecs-identifiers-25a72bd2647) (Sander Mertens, blog)
- [Why Storing State Machines in ECS is a Bad Idea](https://ajmmertens.medium.com/why-storing-state-machines-in-ecs-is-a-bad-idea-742de7a18e59) (Sander Mertens, blog)
- [ECS back & forth](https://skypjack.github.io/2019-02-14-ecs-baf-part-1/) (Michele Caini, blog series)
- [Sparse Set](https://www.geeksforgeeks.org/sparse-set/) (Geeks for Geeks)
- [Hibitset](https://docs.rs/hibitset/0.6.3/hibitset/) (DOCS.RS)

## General Questions

### What is ECS?
ECS ("Entity Component System") describes a design approach which promotes code reusability by separating data from behavior. Data is often stored in cache-friendly ways which benefits performance. An ECS has the following characteristics:

- It has entities, which are unique identifiers
- It has components, which are plain datatypes without behavior
- Entities can contain zero or more components
- Entities can change components dynamically
- It has systems, which are functions matched with entities that have a certain set of components.

The ECS design pattern is often enabled by a framework. The term "Entity Component System" is often used to indicate a specific implementation of the design pattern.

### When is something an ECS?
The most rigid interperation of an ECS is something that has entities, components and systems, according to the definitions in the previous question.

In practice ECS is used a bit more liberally. Some ECS frameworks do not have systems, and only provide methods for querying entities. Other frameworks may allow for adding things to entities than are not components. These implementations are still considered ECS by many people.

A framework that lets you add "things" to entities, with a way to query for entities that have some things but not other things, is generally considered to be an ECS.

### Why is ECS used?
There are a number of reasons why ECS is gaining popularity amongst game developers:

- ECS can typically support larger numbers of game objects
- ECS code tends to be more reusable 
- ECS code is easier to extend with new features
- ECS allows for a more dynamic coding style

### Who is using ECS?
A number of commercial projects and engines today use or have used ECS. If you know of other projects that uses ECS, let me know!

- [Unity DOTS](https://unity.com/dots) (Engine)
- [Unreal (Sequencer)](https://www.unrealengine.com/en-US/tech-blog/performance-at-scale-sequencer-in-unreal-engine-4-26) (Engine)
- [Our Machinery](https://ourmachinery.com/) (Engine)
- [Photon Quantum](https://doc.photonengine.com/en-us/quantum/current/getting-started/quantum-intro) (Engine)
- [Bevy](https://bevyengine.org/) (Engine)
- [Amethyst](https://amethyst.rs/) (Engine)
- [Overwatch](https://playoverwatch.com/en-us/) (Game, uses custom ECS)
- [Xenonauts](https://store.steampowered.com/app/223830/Xenonauts/) (Game, uses custom ECS)
- [Survival City](https://play.google.com/store/apps/details?id=com.playstack.survivalcity&hl=en&gl=US) (Game, uses Entitas)
- [Penko Park](https://store.steampowered.com/app/852090/Penko_Park) (Game, uses Entitas)
- [Doomsday Vault](https://apps.apple.com/us/app/doomsday-vault/id1457773760) (Game, uses Entitas)
- [Phantom Brigade](https://www.youtube.com/watch?v=uHsh9kWQeDc&ab_channel=BraceYourselfGames) (Game, uses Entitas)
- [Minecraft Bedrock](https://minecraft.gamepedia.com/Bedrock_Edition) (Game, uses EnTT)
- [War of Rights](https://store.steampowered.com/app/424030/War_of_Rights/) (Game, uses EnTT)
- [ArcGIS](https://developers.arcgis.com/arcgis-runtime/) (Framework, uses EnTT)
- [Aether Engine](https://hadean.com/spatial-simulation/) (Framework, uses EnTT)
- [FastSuite](https://www.fastsuite.com/) (Simulation, uses EnTT)
- [RoboCraft](https://robocraftgame.com/) (Game, uses Svelto)
- [GameCraft](https://store.steampowered.com/app/1078000/Gamecraft/) (Game, uses Svelto)
- [CardLife](http://cardlifegame.com/) (Game, uses Svelto)
- [Bebylon](https://bebylon.world/) (Game, uses Flecs)
- [The Forge](https://github.com/ConfettiFX/The-Forge) (Rendering Engine, uses Flecs)
- [Territory Control](https://store.steampowered.com/app/690290/Territory_Control_2/) (Game, uses Flecs)
- [Sol Survivor](https://nicok.itch.io/sol-survivor-demo) (Game, uses Flecs)

### How is ECS different from OOP?
ECS is often described as an alternative to Object Oriented Programming. While ECS and OOP overlap, there are differences that impact how applications are designed:

- Inheritance is a 1st class citizen in OOP, composition is a 1st class citizen in ECS.
- OOP encourages encapsulation of data, ECS encourages exposed POD (plain old data) objects.
- OOP colocates data with behavior, ECS separates data from behavior.
- OOP Object instances are of a single static type, entities can have multiple, dynamically changing components

It should be noted that some have argued that ECS fits the characterisics of _Object Oriented Design_ (see https://www.gamedev.net/blogs/entry/2265481-oop-is-dead-long-live-oop/) and should therefore be considered a subset. 

However, in practice the design process of an ECS application is sufficiently different from that of what most people would recognize as OOP. As such it is at least useful to approach it as a separate approach towards design.

### How is ECS different from Entity-Component frameworks?
Confusingly, ECS and Entity-Component frameworks (EC) are not the same. EC frameworks, as typically found in game engines, are similar to ECS in that they allow for the creation of entities and the composition of components. However, in an EC framework, components are classes that contain both data and behavior, and behavior is executed directly on the component.

A simple EC framework would look something like this:

```cpp
class IComponent {
public:
    virtual void update() = 0;
};

class Entity {
    vector<IComponent*> components;
public:
    void addComponent(IComponent *component);
    void removeComponent(IComponent *component);
    void updateComponents();
};
```

Building features in an EC framework generally means inheriting from an `IComponent` interface, and composing entities from multiple components. An example of EC in practice is Unity's `GameObject` system.

### Is ECS hard to learn?
The small number of concepts and rules of an ECS are generally easy to learn. Applying them correctly however can take practice. Some aspects of ECS design go against intuition, especially when coming from an OOP background.

Anecdotally, users have reported that once ECS "clicked", it made it easier to write, reuse and scale code.

### Is ECS a lower level of abstraction?
Not necessarily. While some ECS designs can leverage low-level machine optimizations, the code written for an ECS is not necessarily lower or higher level than other approaches.

### Does ECS require writing more code?
There is not a single answer to this, and highly depends on the ECS framework and engine that is used. 

When an ECS framework is integrated with an engine, it can result in pretty compact and concise code that can be even shorter than non-ECS alternatives. Examples of engines with integrated ECS are Bevy, Amethyst and Our Machinery.

When ECS is not integrated with an engine, the additional glue-code to bridge between the native engine types and the ECS can cause an application to have to write more code.

Having said that, the time spent on writing ECS code is offset by time savings as the result of a more maintainable code base.

### Is ECS good for low level code?
Low level engine code such as rendering and physics may want to use advanced features of the underlying hardware such as vectorization, while optimizing cache locality. Some ECS frameworks are better suited for this than others. 

Generally speaking, when an ECS provides access to raw component arrays, it lends itself better towards low-level optimizations. Another deciding factor, especially in modern games, is how easy it is to multithread such systems.

### Can ECS be implemented in any language?
Yes.

### Should I write my own ECS?
Because of its small set of concepts and rules, building a functional ECS is not hard. There are many benefits to building your own, like the freedom to add new features, and only building features that you really need.

If you write your own implementation however, you should fully expect that it will not outperform established implementations. There are a lot of tricks that have been invented over time to provide a balanced performance across ECS operations. It requires constant education, experimentation and iteration to stay on top of new developments.

As is the case with many things, writing an ECS is easy to learn, but hard to master.

### Is ECS fast?
Generally yes, though this of course depends on what is being measured, and the ECS implementation. Different implementations make different tradeoffs, and as such an operation that is really fast in one framework is quite slow in another. 

Things that ECS implementations are generally good at are querying and iterating sets of entities linearly, or dynamically changing components at runtime. Things that ECS implementations are generally not good at are queries or operations that require highly specialized data structures, such as binary trees or spatial structures. Knowing the tradeoffs of an implementation and levering its design ensure you get the most performance out of an ECS.

### Is ECS code more reusable?
Yes. The reason for this is that behavior in an ECS is matched with a set of components, vs. for example being tightly coupled with a class in OOP. This has a couple of implications.

The first one is obvious. Because behavior is not tied to a single class, it can be reused across entities of different classes. The typical example is that of a "Move" system that is matched with any entity that has a "Position" and "Velocity" component.

This is not impossible to achieve in other, more OOP-style designs, but this often relies on class-based inheritance. Inheritance has well-known problems, such as how difficult it can be to refactor a class hierarchy, or how low-level base classes tend to accumulate bloat over time.

However, EC frameworks can provide similar levels of reusability, where components are simply added to game entities. (see [How is ECS different from Entity-Component frameworks?](#how-is-ecs-different-from-entity-component-frameworks)).

The big advantage of ECS here however, is that new systems can be introduced at any stage of development, and will automatically get matched with any existing and new entities that have the right components. This promotes a design where systems are developed as single-responsibility, small units of functionality that can be easily deployed across different projects.

### Is ECS good for multithreading?
Generally yes. The separation of data and behavior makes it easier to identify individual systems, what their dependencies are, and how they should be scheduled. The approach towards multithreading differs between different ECS implementations, but most approaches make it easier to multithread code.

### Can ECS be used outside of gaming?
Yes. It can be (and has been) used for projects outside of gaming.

### How do I start with ECS?
I highly recommend reading existing resources on ECS and experimenting with the approaches they describe. Reading the code of example ECS projects can also be a good way to fast-track your understanding of how ECS applications are written.

### How do I design for ECS?
Designing an ECS application starts with creating the components (data structures) that contain the game data. Important things to take into account are:

- How many instances of the data will exist
- How often is data accessed
- How often is the data mutated
- When does data need to be accessed/mutated
- Which data is accessed/mutated together
- What is the cardinality of the data

It is good practice to design components and systems to have a single responsibility. This makes them easier to reuse across projects, and makes it easier to refactor code.

### What are the different ways to implement an ECS?
There are many different ways in which to implement an ECS, each with different tradeoffs. This non exhaustive list contains some of the more popular approaches:

#### Archetypes (aka "Dense ECS" or "Table based ECS")
An archetype ECS stores entities in tables, where components are columns and entities are rows. Archetype implementations are fast to query and iterate.

Examples of archetype implementations are [Flecs](https://github.com/SanderMertens/flecs), [Our Machinery](https://ourmachinery.com/), [Unity DOTS](https://unity.com/dots), [Unreal Sequencer](https://www.unrealengine.com/en-US/tech-blog/performance-at-scale-sequencer-in-unreal-engine-4-26), [Bevy ECS](https://bevyengine.org/), [Legion](https://github.com/amethyst/legion) and [Hecs](https://github.com/Ralith/hecs).

#### Sparse set ECS (aka "Sparse ECS")
A sparse set based ECS stores each component in its own sparse set which is has the entity id as key. Sparse set implementations allow for fast add/remove operations.

Examples of sparse set implementations are [EnTT](https://github.com/skypjack/entt) and [Shipyard](https://github.com/leudz/shipyard).

#### Bitset based ECS
A bitset-based ECS stores components in arrays where the entity id is used as index, and uses a bitset to indicate if an entity has a specific component. Different flavors of bitset-based approaches exist. One approach is to have an array for each component with an accompanying bitset to indicate which entities have the component. Another approach uses the [hibitset](#hibitset) data structure (see link).

Examples of bitset implementations are [EntityX](https://github.com/alecthomas/entityx) and [Specs](https://github.com/amethyst/specs).

#### Reactive ECS
A reactive ECS uses signals resulting from entity mutations to keep track of which entities match systems/queries.

An example of a reactive ECS is [Entitas](https://github.com/sschmid/Entitas-CSharp).

### How are components modified?
There are usually two ways in which an ECS allows for modifying a component, which is either by modifying the component on a single entity, or modifying the component values of many entities in a system.

An example of the first approach:
```cpp
entity.set<Position>({10, 20});
```

An example of the second approach:
```cpp
system<Position, Velocity>().each(
    [](entity e, Position& p, Velocity & v) {
        p.x += v.x;
        p.y += v.y;
    });
```

The second approach is generally faster as it requires less lookups, and can take advantage of efficient component storage methods.

### How are entities matched with systems?
There are three popular ways of implementing this.

1. In an archetype-based ECS a query stores a list of matched tables, where a table can contain many entities. This approach has as advantage that as tables stabilize quickly, query evaluation overhead is reduced to zero on average.

2. In a sparse set ECS a query iterates all entities in one of the queried for components (usually the one with the least entities) and tests for each subsequent component if the entity has it. Bitset-based ECS implementations use a similar approach.

3. In a reactive ECS a system collects entities that have the right set of components by listening for signals that could cause an entity to match.

### What are entity relationships?
Entity relationships are an extension to the ECS model where in addition to adding components, a pair of things can be added to an entity. A simple example of a relationship might look like this:

```c
alice.add<Likes>(bob);
```

In this example "Likes, bob" is the pair, "Likes" is a relationship kind and "bob" is the relationship target. Both "alice" and "bob" are regular entities. For more information on entity relationships, see [this article](https://ajmmertens.medium.com/building-games-in-ecs-with-entity-relationships-657275ba2c6c).

## How-to

### How to create a hierarchy in ECS?
There are several ways to implement a hierarchy in ECS, and it depends on an ECS implementation which ones are available to an application. One approach that works in any implementation is to store the hierarchy in components like so:

```c
// Store the parent entity on child entities
struct Parent {
    entity parent;
};

// Store all children of a parent in a component with a vector
struct Children {
    vector<entity> children;
};

// Store children in linked list
struct ChildList {
    entity first_child; // First child of entity
    entity prev_sibling; // Previous sibling
    entity next_sibling; // Next sibling
};
```

The disadvantage of this approach is that it relies on component lookups, which can slow down systems that iterate a hierarchy. While flexible, this approach is not ideal for low-level systems, such as applying transforms.

An approach that works especially well if an application just needs to iterate a hierarchy top-down is to sort entities based on their depth in the hierarchy. This has as advantage that it is fast to iterate. A disadvantage is that it requires frequent sorting.

Archetype ECS frameworks may allow splitting up subtrees across different tables. Tables/subtrees can be sorted according to their depth. This has as advantage that iteration is fast, and that sorting is infrequent. The disadvantage of this approach is that it can create a lot of small tables, which can degrade performance.

### How to store spatial data in ECS?
Spatial data structures like quadtrees and octrees are usually not directly stored in an ECS, as their layout does not match well with the typical ECS layout.

One approach that works well for narrow-phase spatial queries in combination with an ECS is to create a query that iterates relevant entities and stores them in a spatial structure at the beginning (or end) of each frame.

For broad-phase spatial queries an application could leverage runtime tags (if the ECS supports it) where a tag corresponds with a cell in a spatial grid. Combined with queries that match the tag, an application can quickly discard large groups of entities that are not in a certain area.

## Data Oriented Design

### What is Data Oriented Design
Wikipedia defines Data Oriented Design as:

> ... a program optimization approach motivated by efficient usage of the CPU cache, used in video game development. The approach is to focus on the data layout, separating and sorting fields according to when they are needed, and to think about transformations of data.

Data oriented design is an umbrella term for a large collections of techniques and conditions under which those techniques should be used. In general the goal is to analyse the access patterns of the different kinds of data in an application, and select data structures that _for those access patterns_ optimally leverage the underlying hardware. Hardware optimizations are often related (but not limited) to optimizing usage of the CPU cache, limit loading/storing to RAM (cache misses) and usage of SIMD instructions.

A comprehensive overview of Data oriented design is the "Data oriented design" book by Richard Fabian:
[https://www.dataorienteddesign.com/dodbook/](https://www.dataorienteddesign.com/dodbook/)

### Is ECS the same as DoD?
No. It is possible to write code that uses DoD principles without it being ECS, and it is possible to create an ECS that does not leverage DoD.

The ECS pattern does lend itself well towards DoD, which is why many ECS frameworks (though not all) have a storage design that allows applications to leverage the optimizations enabled by DoD.

If an ECS iterates contiguous component arrays, it allows for leveraging DoD principles and optimizations.

### What is Random Access Memory?
RAM is the kind of memory that computers typically have lots of, and is where the entire state of applications and their code is stored. A CPU interfaces with RAM when it executes application code. 

While RAM is incredibly fast in absolute terms, the bus between a CPU and RAM can become a bottleneck in data-heavy applications. This is why in data oriented design, techniques are employed to minimize the number of loads from RAM.

### What is a CPU cache?
A CPU cache is a kind of memory that is much faster, but also _much_ smaller than RAM. When a CPU loads data from RAM it is stored in a cache tier, where lower tiers are faster and larger tiers are slower.

Data oriented design employs techniques to utilize a CPU cache as efficiently as possible, so that the number of loads from RAM are minimized.

### What is a cache line?
A cache line represents the amount of data that is retrieved from RAM in a single load. When an application requests, say 4 bytes from RAM, a CPU will actually load 64 bytes, starting from the requested address.

An application can reduce the number of loads from RAM by storing data in close proximity, which increases the chance that data required for future operations is already loaded in the cache.

### What is locality of reference?
Locality refers to either temporal or spatial locality. Temporal locality refers to the reuse of data within a short amount of time. Spatial locality refers to the proximity of storage locations. High locality in either category increases the efficiency of caching, as a CPU is better able to predict access patterns.

### What is SIMD?
SIMD, or Single Instruction Multiple Data, refers to a set of instructions or instruction families that can process multiple values in the time it takes to do a single instruction.

### What is vectorization?
Vectorization (or automatic vectorization) is the process whereby code that meets certain criteria uses SIMD instructions to improve performance. As a result of using these optimized instructions, vectorized code can run multiple times faster than regular code.

The conditions for vectorized code are:
- Data must be stored contiguously (in arrays)
- The code should contain no branches or function calls

Compilers are generally able to vectorize loops that meet the above conditions. It depends on the compiler however which scenarios will be automatically vectorized. [This page](https://llvm.org/docs/Vectorizers.html) provides an overview of scenarios that the clang compiler is able to automatically vectorize.

### What is false sharing?
False sharing occurs when different threads attempt to load and alter two values that are different, but in the same cache line. This causes a cache sync, which can degrade performance.

False sharing is avoided by ensuring that data accessed by different threads is not in close enough proximity for it to be loaded in a single cache line.

### What is AoS?
AoS, or "array of structs" refers to a memory layout where a struct containing multiple fields is stored in an array. An example of AoS is:

```c
struct AoS {
  int m_1;
  int m_2;
};

AoS values[1000];
```

An advantage of AoS is that data is stored in arrays which benefits cache locality. A potential disadvantage of AoS is that when code only requires a subset of members in a struct, more data is loaded into the cache than is strictly necessary.

In the context of ECS, AoS usually refers to a memory layout where all components are stored in the same array.

### What is SoA?
SoA, or "struct of arrays" refers to a memory layout where a struct contains multiple arrays, one for each field. An example of SoA is:

```c
struct SoA {
  int m_1[1000];
  int m_2[1000];
};

SoA values;
```

Like AoS, data is stored in arrays which benefits cache locality. An additional advantage of SoA is that when code only needs a subset of members in a struct, the other members are not loaded in cache. A potential disadvantage of SoA is that if code randomly needs to access other members, it incurs more cache misses than AoS.

In the context of ECS, SoA usually refers to a memory layout where components are stored in separate arrays.

### What is branch prediction?
When a CPU executes a set of instructions, it tries to predict which path the code will take, by taking an educated guess at how conditional statements (like if-else, switch) will be evaluated. These instructions are then preloaded into the instruction cache, and can even be executed in advance.

When code contains many unpredictable branches, the branch predictor may often have to discard the precomputed results, which results in measurably slower code.

## Glossary

### Entity
An entity in ECS represents a single "thing" in a game and is generally represented as a unique integer value.

### Component
A component is a datatype that can be added to or removed from entities. Components in ECS are generally plain data types and not encapsulated.

### Tag
A tag is a component that has no data.

### System
A system is an executable object that is matched with all entities that have a certain set of components. 

### Query
A query is similar to a system, but cannot be executed by itself.

### World
A world is the container for all ECS data. ECS frameworks often allow a single application to have multiple ECS worlds.

### Registry
Same as world.

### Archetype
A data structure that stores entities for a specific set of components. Components are stored as columns in contiguous arrays. 

### Table
Often used interchangeably with archetype. In some ECS implementations a table refers to an archetype that stores "dense" components (contiguous arrays with aligned indices), where an archetype stores "sparse" components (components not contiguously stored, or not stored with aligned indices) and indexes into a table.

### Sparse set
A data structure that provides fast iteration, lookup, insertion and removal times. Similar to a hashmap, but better suited for sequential identifiers.

