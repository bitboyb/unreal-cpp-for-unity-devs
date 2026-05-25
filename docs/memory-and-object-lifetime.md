# Memory and Object Lifetime

This is one of the biggest mindset shifts for Unity developers.

## Unreal Garbage Collection

### Unity Version

In Unity, C# objects are managed by .NET garbage collection, while `UnityEngine.Object` has its own engine lifetime behaviour.

### Unreal Version

In Unreal, many gameplay objects derive from `UObject` and are tracked by Unreal's garbage collector.

### Key Difference

Unreal object lifetime depends heavily on reflected references and engine ownership rules, not only plain C++ scope rules.

## `UObject`

`UObject` instances are usually created with `NewObject`.

```cpp
UMyInventoryObject* Inventory = NewObject<UMyInventoryObject>(this);
```

## `SpawnActor`

Actors live in a `UWorld`, so they are spawned with `SpawnActor`.

```cpp
AEnemy* Enemy = GetWorld()->SpawnActor<AEnemy>(EnemyClass, SpawnTransform);
```

## `Destroy`

Actors are usually removed with `Destroy()`.

```cpp
Destroy();
```

Do not use `delete` on Actors or normal `UObject` gameplay instances.

## `UPROPERTY` References

For `UObject` references stored on reflected classes, use `UPROPERTY` so Unreal can see the reference.

```cpp
UPROPERTY()
TObjectPtr<UUserWidget> ActiveWidget;
```

## Raw Pointers

Raw pointers still appear everywhere in Unreal APIs.

That does not automatically mean manual ownership.

```cpp
AActor* TargetActor = nullptr;
```

When stored as members on reflected classes, pair object references with `UPROPERTY` or the project-standard reflected pointer style.

## `TObjectPtr`

`TObjectPtr` is a UE5-friendly wrapper for reflected `UObject` member references.

```cpp
UPROPERTY(EditAnywhere)
TObjectPtr<UStaticMesh> PreviewMesh;
```

## `TWeakObjectPtr`

Use `TWeakObjectPtr` when you need a non-owning reference to a `UObject`.

```cpp
TWeakObjectPtr<AActor> CachedTarget;
```

This is useful when the referenced object may go away and you do not want to keep it alive.

## `TSharedPtr` and `TUniquePtr`

These are for regular C++ objects that are not managed by Unreal garbage collection.

```cpp
TSharedPtr<FMyPlainData> SharedData = MakeShared<FMyPlainData>();
TUniquePtr<FMyPlainWorker> Worker = MakeUnique<FMyPlainWorker>();
```

Warning: `TSharedPtr` is generally not for owning `UObject` or `AActor` instances.

## Common Mistake

A common trap is treating `UObject` references like normal heap objects and trying to manage them with `new`, `delete`, or `TSharedPtr`. For normal Unreal object ownership, use Unreal creation APIs and reflected references.

## Related Pages

- [Unreal Macros and Reflection](unreal-macros-and-reflection.md)
- [Assets and References](assets-and-references.md)
- [Networking and Replication](networking-and-replication.md)
