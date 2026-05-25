# Getting Started

This page explains the mindset shift from Unity to Unreal before you dive into specific APIs.

## Why Unreal Feels Different

In Unity, you may be used to starting with a `GameObject` and adding several `MonoBehaviour` scripts. In Unreal, you usually start with an `Actor`, `Pawn`, `Character`, or a Blueprint class based on one of those types.

The important difference is that Unreal is not just "Unity with C++". Unreal gameplay code sits inside a large engine framework with:

- reflection macros
- a code generation step
- engine-managed object lifetimes
- asset classes that can contain logic, defaults, and editor data

See [Unity to Unreal Overview](unity-to-unreal-overview.md) for the bigger picture.

## Why Unreal C++ Is Not Plain C++

Unreal uses standard C++ syntax, but you also work with engine-specific systems:

- `UCLASS`, `USTRUCT`, `UPROPERTY`, and `UFUNCTION`
- `GENERATED_BODY()`
- Unreal Header Tool, often shortened to UHT
- Unreal Build Tool, often shortened to UBT
- engine types such as `FString`, `TArray`, and `TObjectPtr`

These are not ordinary language features. They help Unreal expose your code to the editor, Blueprints, serialization, garbage collection, and networking.

## Unreal Header Tool

UHT is a code-generation step that runs before your C++ is compiled.

It scans macros like `UCLASS()` and `UPROPERTY()` and generates glue code so Unreal can:

- show variables in the editor
- save and load object data
- replicate properties over the network
- call C++ functions from Blueprints

A common trap is treating Unreal macros like comments or annotations. They affect how the engine sees your class.

## Reflection System

Reflection is Unreal's way of understanding your gameplay types at runtime and in the editor.

Without reflection:

- your class may compile as C++, but not appear properly in the editor
- properties may not be editable in details panels
- references may not be visible to garbage collection
- Blueprint access and replication metadata may not work

Read [Unreal Macros and Reflection](unreal-macros-and-reflection.md) next if this is still new.

## C++ and Blueprints Work Together

Blueprints are not only visual scripts. They are also asset classes that can store defaults, references, components, and event graphs.

In practice, many Unreal projects use a hybrid workflow:

- C++ for core systems, data structures, performance-sensitive code, and reusable gameplay foundations
- Blueprints for designer-friendly assembly, tuning, and event wiring

See [Blueprints and C++](blueprints-and-cpp.md) for when to choose each.

## Unity Habit Comparison

| Unity Habit | Unreal Equivalent | Important Difference |
|---|---|---|
| Attach many scripts to a `GameObject` | Build an `Actor` or Blueprint and attach Components | Unreal separates Actor roles and Component roles more explicitly. |
| Expose a field with `[SerializeField]` | Use `UPROPERTY(...)` | `UPROPERTY` also affects reflection, serialization, and sometimes GC visibility. |
| Instantiate a prefab at runtime | Spawn an `Actor` or widget, or load a class asset | Spawning often uses a class type, not a direct scene object reference. |
| Use C# reflection rarely | Use Unreal reflection constantly | Editor, Blueprints, save/load, and replication depend on it. |
| Rely on managed references | Use reflected `UObject` references carefully | Unreal object lifetime rules differ from plain C# GC. |

## Recommended Learning Path

1. Learn the high-level framework terms: Actor, Pawn, Character, Controller, GameMode, GameState.
2. Learn the C++ basics you need every day: headers, pointers, references, `const`, and Unreal naming.
3. Learn reflection macros and property specifiers.
4. Learn Components and lifecycle methods.
5. Learn asset references and memory rules before building larger systems.
6. Learn Blueprints, networking, and editor tooling after the basics feel comfortable.

## Common Mistake

A common trap is trying to map every Unity concept to one exact Unreal equivalent. Some roles overlap, but the engine architecture is different. Treat the comparisons in this guide as rough translations, not exact matches.

## Related Pages

- [Unity to Unreal Overview](unity-to-unreal-overview.md)
- [Syntax and C++ Basics](syntax-and-cpp-basics.md)
- [Unreal Macros and Reflection](unreal-macros-and-reflection.md)
- [Glossary](glossary.md)
