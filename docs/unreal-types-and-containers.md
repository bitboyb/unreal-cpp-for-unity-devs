# Unreal Types and Containers

This page covers the Unreal types you will see most often in gameplay code.

## Type Comparison Table

| C# / Unity Type | Unreal Type | Use Case |
|---|---|---|
| `int` | `int32` | Standard 32-bit integer in Unreal code. |
| `float` | `float` | General gameplay numbers. |
| `bool` | `bool` | True or false values. |
| `string` | `FString` | General string building and manipulation. |
| `string` identifier | `FName` | Fast identifiers, tags, lookup keys, socket names. |
| UI text string | `FText` | User-facing and localised text. |
| `Vector3` | `FVector` | Positions, directions, velocities. |
| `Quaternion` | `FQuat` | Rotation math and interpolation. |
| Euler rotation | `FRotator` | Editor-friendly pitch, yaw, roll values. |
| `List<T>` | `TArray<T>` | Ordered dynamic collection. |
| `Dictionary<TKey,TValue>` | `TMap<Key, Value>` | Key-value storage. |
| `HashSet<T>` | `TSet<T>` | Unique items. |

## Numbers and Booleans

Unreal commonly uses fixed-width integer types such as `int32` and `uint8`.

```cpp
int32 Score = 0;
float MoveSpeed = 600.0f;
bool bCanShoot = true;
```

## Strings, Names, and Text

### `FString`

Use `FString` for:

- building strings
- parsing text
- general string manipulation

```cpp
FString Message = TEXT("Hello");
Message += TEXT(" Unreal");
```

### `FName`

Use `FName` for identifiers:

- row names
- socket names
- tags
- lookup keys used often

```cpp
FName SocketName = TEXT("WeaponSocket");
```

### `FText`

Use `FText` for text shown to players.

```cpp
FText ButtonLabel = FText::FromString(TEXT("Play"));
```

The important difference is:

- `FString` is for string work
- `FName` is for identifiers
- `FText` is for user-facing, localised text

## Math Types

### `FVector`

```cpp
FVector SpawnLocation(0.0f, 0.0f, 200.0f);
```

### `FRotator`

```cpp
FRotator SpawnRotation(0.0f, 90.0f, 0.0f);
```

### `FQuat`

```cpp
FQuat RotationQuat = FQuat::Identity;
```

`FRotator` is easier to read in gameplay code. `FQuat` is better for some rotation math and interpolation cases.

## Containers

### `TArray`

`TArray` is the Unreal equivalent you will use most often when coming from `List<T>`.

```cpp
TArray<FString> InventoryItems;
InventoryItems.Add(TEXT("Potion"));
InventoryItems.Add(TEXT("Key"));
```

### `TMap`

```cpp
TMap<FName, int32> AmmoByType;
AmmoByType.Add(TEXT("Rifle"), 30);
```

### `TSet`

```cpp
TSet<FName> UnlockedAreas;
UnlockedAreas.Add(TEXT("Tutorial"));
```

## Unreal Object Reference Helpers

### `TSubclassOf`

Use `TSubclassOf` when you want to store a class reference rather than an instance reference.

```cpp
UPROPERTY(EditAnywhere, Category = "Spawning")
TSubclassOf<AActor> EnemyClass;
```

This is common when spawning Actors from a Blueprint-derived class.

### `TObjectPtr`

Use `TObjectPtr` for reflected `UObject` references in Unreal Engine 5 codebases that prefer it.

```cpp
UPROPERTY(VisibleAnywhere, Category = "Components")
TObjectPtr<class UStaticMeshComponent> MeshComponent;
```

### `TSoftObjectPtr`

Use `TSoftObjectPtr` for assets that should be referenced without forcing an immediate hard load.

```cpp
UPROPERTY(EditAnywhere, Category = "Assets")
TSoftObjectPtr<UTexture2D> PortraitTexture;
```

See [Assets and References](assets-and-references.md).

## Common Mistake

A common trap is using `FString` for everything. In Unreal, choosing between `FString`, `FName`, and `FText` matters because each one serves a different purpose.

## Related Pages

- [Syntax and C++ Basics](syntax-and-cpp-basics.md)
- [Memory and Object Lifetime](memory-and-object-lifetime.md)
- [Assets and References](assets-and-references.md)
- [Glossary](glossary.md)
