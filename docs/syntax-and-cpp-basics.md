# Syntax and C++ Basics

This page covers the C++ features Unity developers usually run into first when reading Unreal code.

## Header and Source Files

### Unity Version

In Unity, a class often lives in one `.cs` file.

### Unreal Version

In Unreal C++, a class usually has:

- a header file such as `MyActor.h`
- a source file such as `MyActor.cpp`

The header declares the class. The source file defines the function bodies.

### Key Difference

You usually split declarations and implementations. That is standard C++, and it affects includes, compile times, and generated code.

### Example

#### Unity C#

```csharp
public class Health : MonoBehaviour
{
    public int currentHealth = 100;

    public void TakeDamage(int amount)
    {
        currentHealth -= amount;
    }
}
```

#### Unreal C++

```cpp
// HealthActor.h
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "HealthActor.generated.h"

UCLASS()
class MYGAME_API AHealthActor : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Health")
    int32 CurrentHealth = 100;

    UFUNCTION(BlueprintCallable, Category = "Health")
    void TakeDamageAmount(int32 Amount);
};
```

```cpp
// HealthActor.cpp
#include "HealthActor.h"

void AHealthActor::TakeDamageAmount(int32 Amount)
{
    CurrentHealth -= Amount;
}
```

## Important Syntax

| Syntax | Meaning | Why You See It in Unreal |
|---|---|---|
| `#include` | Includes declarations from another header | Unreal code still follows C++ include rules. |
| `::` | Scope resolution | Used for class functions, namespaces, and static members. |
| `->` | Access a member through a pointer | Common because many engine APIs return pointers. |
| `*` | Pointer declaration or dereference | Unreal uses pointers heavily for `UObject` references. |
| `&` | Reference or address-of operator | Used for output parameters and pass-by-reference. |
| `const` | Says a value or method should not modify data | Common in Unreal APIs and function parameters. |
| `auto` | Let the compiler infer the type | Useful when the type is obvious from the right side. |
| `nullptr` | Null pointer literal | Use this instead of `NULL` or `0`. |
| `TEXT("...")` | Wraps string literals for Unreal character encoding expectations | Common with logging and `FString` construction. |

## Variables

| Unity C# | Unreal C++ |
|---|---|
| `float speed = 5f;` | `float Speed = 5.0f;` |

#### Unity C#

```csharp
float speed = 5f;
bool isAlive = true;
```

#### Unreal C++

```cpp
float Speed = 5.0f;
bool bIsAlive = true;
```

Unreal commonly prefixes booleans with `b`, such as `bIsAlive`.

## Functions

| Unity C# | Unreal C++ |
|---|---|
| `void JumpNow()` | `void JumpNow();` in the header, then define it in `.cpp` |

#### Unity C#

```csharp
void JumpNow()
{
    Debug.Log("Jump");
}
```

#### Unreal C++

```cpp
void AMyCharacter::JumpNow()
{
    UE_LOG(LogTemp, Log, TEXT("Jump"));
}
```

## Classes

| Unity C# | Unreal C++ |
|---|---|
| `public class Mover : MonoBehaviour` | `class AMyMover : public AActor` |

#### Unity C#

```csharp
public class Mover : MonoBehaviour
{
}
```

#### Unreal C++

```cpp
UCLASS()
class MYGAME_API AMyMover : public AActor
{
    GENERATED_BODY()
};
```

## Null Checks

| Unity C# | Unreal C++ |
|---|---|
| `if (target != null)` | `if (Target != nullptr)` |

#### Unity C#

```csharp
if (target != null)
{
    target.SetActive(true);
}
```

#### Unreal C++

```cpp
if (Target != nullptr)
{
    Target->SetActorHiddenInGame(false);
}
```

## Logging

| Unity C# | Unreal C++ |
|---|---|
| `Debug.Log("Hello");` | `UE_LOG(LogTemp, Log, TEXT("Hello"));` |

#### Unity C#

```csharp
Debug.Log("Hello, Unity!");
```

#### Unreal C++

```cpp
UE_LOG(LogTemp, Log, TEXT("Hello, Unreal!"));
```

## `const` and References

Pass larger structs by const reference when you do not need to copy them.

```cpp
void SetSpawnPoint(const FVector& NewLocation);
```

This means:

- do not copy the `FVector`
- do not modify `NewLocation` inside the function

## `auto`

`auto` is useful when the type is obvious or long.

```cpp
auto* World = GetWorld();
auto Location = GetActorLocation();
```

Do not overuse it when the type would become unclear to a beginner.

## Unreal Naming Conventions

| Pattern | Example | Meaning |
|---|---|---|
| `A` prefix | `AActor` | Actor-derived class |
| `U` prefix | `UObject`, `UActorComponent` | UObject-derived class |
| `F` prefix | `FVector`, `FText` | Struct or value type |
| `E` prefix | `EInputEvent` | Enum |
| `T` prefix | `TArray`, `TMap` | Template type |
| `b` prefix | `bIsVisible` | Boolean |

## Common Mistake

A common trap is writing a wrapper method with the same name as an engine method, such as `SetActorLocation`, then accidentally calling itself and causing recursion. Use a clearer name like `MoveToLocation` if you are adding your own helper.

## Related Pages

- [Unreal Types and Containers](unreal-types-and-containers.md)
- [Unreal Macros and Reflection](unreal-macros-and-reflection.md)
- [Memory and Object Lifetime](memory-and-object-lifetime.md)
