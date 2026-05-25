# Unreal Macros and Reflection

These macros are not normal C++ features. They connect your code to Unreal's reflection, editor, serialization, networking, and Blueprint systems.

## Why They Exist

### Unity Version

In Unity, you may be used to attributes such as `[SerializeField]` or public fields appearing in the Inspector.

### Unreal Version

In Unreal, macros and specifiers tell the engine how to treat your type and its members.

### Key Difference

The compiler sees C++, but Unreal also runs its own header tool to generate metadata and glue code.

## `UCLASS`

Marks a class as a reflected Unreal class.

```cpp
UCLASS()
class MYGAME_API APickupActor : public AActor
{
    GENERATED_BODY()
};
```

Use it for most gameplay classes derived from `UObject` or `AActor`.

## `USTRUCT`

Marks a struct for reflection.

```cpp
USTRUCT(BlueprintType)
struct FItemData
{
    GENERATED_BODY()

    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    int32 Count = 0;
};
```

## `UENUM`

Marks an enum for reflection and optional Blueprint use.

```cpp
UENUM(BlueprintType)
enum class EWeaponType : uint8
{
    Rifle,
    Shotgun
};
```

## `UPROPERTY`

Marks a member variable for Unreal systems.

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Weapon")
int32 Damage = 25;
```

`UPROPERTY` can affect:

- editor visibility
- Blueprint access
- serialization
- replication
- garbage collection visibility for `UObject` references

## `UFUNCTION`

Marks a function for Unreal systems.

```cpp
UFUNCTION(BlueprintCallable, Category = "Weapon")
void Fire();
```

It can expose functions to Blueprints, RPCs, editor calls, and reflection.

## `GENERATED_BODY`

Adds generated boilerplate required by Unreal.

```cpp
UCLASS()
class MYGAME_API AMyActor : public AActor
{
    GENERATED_BODY()
};
```

Without it, reflected classes and structs will not work properly.

## Common Property and Function Specifiers

| Specifier | Use |
|---|---|
| `BlueprintReadOnly` | Blueprint can read the value, but not write it directly. |
| `BlueprintReadWrite` | Blueprint can read and write the value. |
| `EditAnywhere` | Editable in defaults and placed instances, depending on context. |
| `VisibleAnywhere` | Visible in the editor, but not editable there. |
| `BlueprintCallable` | Function can be called from Blueprints. |
| `BlueprintImplementableEvent` | Blueprint provides the implementation. |
| `BlueprintNativeEvent` | C++ can provide a default implementation, and Blueprint can override it. |

## Example

#### Unity C#

```csharp
[SerializeField] private int health = 100;

public void Heal(int amount)
{
    health += amount;
}
```

#### Unreal C++

```cpp
UCLASS()
class MYGAME_API AHealthActor : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Health")
    int32 Health = 100;

    UFUNCTION(BlueprintCallable, Category = "Health")
    void Heal(int32 Amount);
};
```

## Common Mistake

A common trap is assuming `UPROPERTY` is only for editor exposure. It also matters for serialization, replication metadata, and safe tracking of `UObject` references by the engine.

## Related Pages

- [Getting Started](getting-started.md)
- [Blueprints and C++](blueprints-and-cpp.md)
- [Memory and Object Lifetime](memory-and-object-lifetime.md)
