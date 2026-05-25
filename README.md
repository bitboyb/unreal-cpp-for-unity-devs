# Unreal C++ for Unity Developers

A practical guide for Unity developers who are learning Unreal Engine 5 C++ and the gameplay framework around it.

## Who This Is For

This guide is for developers who:

- know Unity and basic C#
- are new to Unreal terminology and workflows
- want practical examples instead of deep engine theory
- need help translating familiar Unity patterns into Unreal-friendly ones

## What This Guide Covers

- how Unreal differs from Unity at a project and engine level
- the C++ basics you need to read and write Unreal gameplay code
- Unreal types, reflection macros, gameplay classes, components, and lifecycle
- Blueprints, networking, AI, UI, profiling, editor tooling, and source control

## Suggested Reading Order

1. [Getting Started](docs/getting-started.md)
2. [Unity to Unreal Overview](docs/unity-to-unreal-overview.md)
3. [Syntax and C++ Basics](docs/syntax-and-cpp-basics.md)
4. [Unreal Types and Containers](docs/unreal-types-and-containers.md)
5. [Macros and Reflection](docs/unreal-macros-and-reflection.md)
6. [Actors, Pawns and Characters](docs/actors-pawns-and-characters.md)
7. [Components](docs/components.md)
8. [Lifecycle and Events](docs/lifecycle-and-events.md)
9. Continue with the topic pages that match your project

## Documentation Index

| Topic | Description |
|---|---|
| [Getting Started](docs/getting-started.md) | First steps for Unity developers moving to Unreal. |
| [Unity to Unreal Overview](docs/unity-to-unreal-overview.md) | High-level comparison of project structure, editor workflow, assets, scripting, and builds. |
| [Syntax and C++ Basics](docs/syntax-and-cpp-basics.md) | The C++ syntax and Unreal coding conventions Unity developers hit first. |
| [Unreal Types and Containers](docs/unreal-types-and-containers.md) | Common Unreal data types, math types, and container types. |
| [Unreal Macros and Reflection](docs/unreal-macros-and-reflection.md) | How `UCLASS`, `UPROPERTY`, and related macros connect C++ to the engine. |
| [Actors, Pawns and Characters](docs/actors-pawns-and-characters.md) | The main gameplay classes and their rough Unity equivalents. |
| [Components](docs/components.md) | Building behaviour with components and scene hierarchies. |
| [Lifecycle and Events](docs/lifecycle-and-events.md) | Constructors, `BeginPlay`, `Tick`, input setup, and delegates. |
| [Input](docs/input.md) | Unreal Enhanced Input, mapping contexts, and character binding. |
| [Physics and Collision](docs/physics-and-collision.md) | Physics components, collision channels, overlaps, hits, and traces. |
| [Memory and Object Lifetime](docs/memory-and-object-lifetime.md) | Garbage collection, spawning, destroying, and safe pointer choices. |
| [Assets and References](docs/assets-and-references.md) | Hard references, soft references, Blueprints, Data Assets, and loading. |
| [Gameplay Framework](docs/gameplay-framework.md) | `GameMode`, `GameState`, controllers, pawns, world, and level roles. |
| [Blueprints and C++](docs/blueprints-and-cpp.md) | A practical hybrid workflow for code and visual scripting. |
| [UI with UMG](docs/ui-with-umg.md) | Building widgets and wiring UI to gameplay code. |
| [Networking and Replication](docs/networking-and-replication.md) | Unreal's authority model, replicated properties, and RPCs. |
| [AI and Behaviour Trees](docs/ai-and-behaviour-trees.md) | AI controllers, blackboards, perception, and navigation. |
| [Profiling and Optimisation](docs/profiling-and-optimisation.md) | Unreal Insights, `stat` commands, and practical optimisation checks. |
| [Editor Tools](docs/editor-tools.md) | Editor Utility Widgets, commandlets, plugins, and custom editor extensions. |
| [Version Control](docs/version-control.md) | Git, Git LFS, Perforce, locking, and Unreal-specific source-control practice. |
| [Glossary](docs/glossary.md) | Short definitions for Unity and Unreal terms used across the guide. |

## Contributing

Contributions are welcome, especially:

- corrections for Unreal Engine 5 best practices
- additional Unity-to-Unreal comparisons
- better C# and C++ examples
- workflow notes for teams
- version-control improvements

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidance.

## Licence

No licence file was present when this documentation refactor was prepared. Add a project licence before accepting outside contributions or redistributing the content.
