# Assets and References

Unreal projects depend heavily on asset references, class assets, and the difference between hard and soft loading.

## Prefabs, ScriptableObjects, and Unreal Assets

| Unity Concept | Unreal Rough Equivalent | Notes |
|---|---|---|
| Prefab | Blueprint Class | Similar reuse goal, different inheritance and authoring workflow. |
| ScriptableObject | Data Asset / Primary Data Asset | Common for shared data-driven content. |
| Dragged scene reference | Hard object reference | Loads directly through a strong reference. |
| Addressables-style delayed load | Soft object reference | Load on demand when needed. |

## Hard References

A hard reference directly points to another asset or object.

```cpp
UPROPERTY(EditAnywhere, Category = "Assets")
TObjectPtr<UStaticMesh> PickupMesh;
```

This is simple, but too many hard references can pull large asset chains into memory.

## Soft References

A soft reference stores an asset path and can be loaded later.

```cpp
UPROPERTY(EditAnywhere, Category = "Assets")
TSoftObjectPtr<UTexture2D> Portrait;
```

Soft references are useful for:

- optional content
- large UI media
- delayed loading
- reducing hard dependency chains

## `TSubclassOf`

Use `TSubclassOf` when you want to choose a class in the editor, often a Blueprint subclass of your C++ base class.

```cpp
UPROPERTY(EditDefaultsOnly, Category = "Spawning")
TSubclassOf<AActor> ProjectileClass;
```

## `ConstructorHelpers`

`ConstructorHelpers` can load assets during class construction.

```cpp
static ConstructorHelpers::FObjectFinder<UStaticMesh> MeshFinder(TEXT("/Game/Meshes/SM_Crate.SM_Crate"));
```

Use this sparingly. It creates a hard reference and is often better for sample code or fixed defaults than for flexible production loading.

## Async Loading Conceptually

Unreal can load soft references later rather than all at once during startup.

The practical takeaway is simple:

- hard references are easier
- soft references are better when load timing matters

## Content Browser Paths

Unreal asset references often use paths like:

```text
/Game/UI/WBP_MainMenu.WBP_MainMenu
```

`/Game/` maps to your project's `Content/` folder.

## Common Mistake

A common trap is assuming a Blueprint class reference is the same as an instance reference. `TSubclassOf<AActor>` points to a class you can spawn, not a placed Actor already in the level.

## Related Pages

- [Unreal Types and Containers](unreal-types-and-containers.md)
- [Memory and Object Lifetime](memory-and-object-lifetime.md)
- [Blueprints and C++](blueprints-and-cpp.md)
