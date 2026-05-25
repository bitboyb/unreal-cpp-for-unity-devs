# Unity to Unreal Overview

This page gives you the broad comparison before you get into API details.

## Core Concept Comparison

| Unity | Unreal | Notes |
|---|---|---|
| `GameObject` | `Actor` | Actors are level-placeable objects, but not every Unreal object is an Actor. |
| `MonoBehaviour` | `UActorComponent` or `Actor` subclass | Unreal separates Actor ownership and Component behaviour more explicitly. |
| Scene | Level / Map | Unreal levels are usually `.umap` assets. |
| Prefab | Blueprint Class | Similar role, different workflow and inheritance model. |
| ScriptableObject | Data Asset / Primary Data Asset | Unreal usually uses asset classes rather than plain code-only data containers. |
| Transform | `USceneComponent` transform | Transforms usually live on scene components, especially the root component. |
| Inspector | Details panel | Similar purpose, but powered through reflection metadata. |
| Package Manager | Plugins / modules / marketplace assets | Unreal code is commonly organized into modules. |

## Project Structure

### Unity Version

Unity projects usually centre around the `Assets` folder, with scripts, scenes, prefabs, and resources stored beneath it.

### Unreal Version

Unreal projects usually separate concerns more clearly:

- `Content/` for assets such as Blueprints, materials, maps, and widgets
- `Source/` for C++ modules, headers, and source files
- `Config/` for `.ini` settings
- generated folders such as `Binaries/`, `Intermediate/`, and `Saved/`

### Key Difference

In Unity, scripts and assets often feel like one large content tree. In Unreal, code modules and content assets are more distinct.

## Editor Workflow

### Unity Version

Unity developers often work by selecting a `GameObject`, adding components, then editing fields in the Inspector.

### Unreal Version

In Unreal, you often:

1. create a C++ class or Blueprint class
2. add components in C++ or in the Blueprint editor
3. place the resulting Actor or Blueprint instance in a level
4. tune defaults in the details panel

### Key Difference

A Blueprint is often both the editable asset and the reusable class template. It is closer to a prefab plus scriptable subclass than a direct one-to-one Unity object.

## Asset Workflow

### Unity Version

Unity commonly uses prefabs, materials, scenes, and ScriptableObjects with drag-and-drop references.

### Unreal Version

Unreal uses:

- Blueprint classes
- maps
- materials and material instances
- static and skeletal meshes
- Data Assets
- hard and soft asset references

### Key Difference

Asset references matter more for loading and memory planning in Unreal. A hard reference can cause the engine to load more content than you expect.

See [Assets and References](assets-and-references.md).

## Scripting Workflow

### Unity Version

Unity scripting is usually pure C# with engine APIs. You compile managed assemblies and the editor reloads them.

### Unreal Version

Unreal scripting is usually a mix of:

- C++ gameplay code
- Blueprint graphs
- reflected properties and events

### Key Difference

Unreal C++ depends on engine macros and generated code. Blueprints are a first-class part of the gameplay workflow, not just an optional visual layer.

## Build Workflow

### Unity Version

Unity hides much of the low-level build system until you need platform-specific work.

### Unreal Version

Unreal exposes more of the build pipeline:

- Unreal Build Tool compiles C++ modules
- Unreal Header Tool generates reflection glue
- IDE project files are generated from the `.uproject`

### Key Difference

A compile error can come from C++, generated headers, missing includes, or reflection metadata. That is normal when learning Unreal.

## Common Mistake

A common trap is assuming a Blueprint is only comparable to a Unity script. In Unreal, a Blueprint can define components, defaults, references, inherited behavior, editor events, and even be the main asset designers work with.

## Related Pages

- [Getting Started](getting-started.md)
- [Gameplay Framework](gameplay-framework.md)
- [Assets and References](assets-and-references.md)
- [Glossary](glossary.md)
