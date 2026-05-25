# Lifecycle and Events

This page compares Unity lifecycle methods with the Unreal equivalents you will use most.

## Lifecycle Comparison

| Unity | Unreal | Notes |
|---|---|---|
| `Awake` | Constructor | Constructor sets defaults and creates default subobjects. World state may not be ready yet. |
| `Start` | `BeginPlay` | Safe place for gameplay startup logic. |
| `Update` | `Tick` | Runs every frame if ticking is enabled. |
| `OnDestroy` | `EndPlay` / destruction flow | `EndPlay` tells you why the actor is ending play. |
| Input method setup | `SetupPlayerInputComponent` | Common on `APawn` and `ACharacter`. |

## Constructor

### Unity Version

Unity developers often put setup in `Awake`.

### Unreal Version

The constructor is for:

- default values
- component creation
- configuration that should exist before play

Do not rely on other world objects being ready here.

## `BeginPlay`

`BeginPlay` is the common place for runtime startup logic.

```cpp
void AMyActor::BeginPlay()
{
    Super::BeginPlay();
}
```

## `Tick`

Use `Tick` only when the object truly needs per-frame work.

```cpp
AMyActor::AMyActor()
{
    PrimaryActorTick.bCanEverTick = true;
}

void AMyActor::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
}
```

Frequent ticking is easy to overuse. See [Profiling and Optimisation](profiling-and-optimisation.md).

## `EndPlay`

`EndPlay` is often clearer than thinking only in terms of destruction.

```cpp
void AMyActor::EndPlay(const EEndPlayReason::Type EndPlayReason)
{
    Super::EndPlay(EndPlayReason);
}
```

## `SetupPlayerInputComponent`

Characters and pawns commonly bind input here.

```cpp
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);
}
```

With Enhanced Input, you usually add mapping contexts elsewhere as well. See [Input](input.md).

## Delegates

Delegates are Unreal's event callback system.

### Single-cast Delegate

```cpp
DECLARE_DELEGATE(FOnReloaded);
```

### Multicast Delegate

```cpp
DECLARE_MULTICAST_DELEGATE(FOnReloadedMulti);
```

### Dynamic Multicast Delegate

Use this when Blueprints need to bind to the event.

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE(FOnHealthChanged);
```

```cpp
UPROPERTY(BlueprintAssignable, Category = "Events")
FOnHealthChanged OnHealthChanged;
```

## Common Mistake

A common trap is treating the constructor like `Start`. In Unreal, constructor code is often about defaults and component setup, not world-dependent gameplay logic.

## Related Pages

- [Components](components.md)
- [Input](input.md)
- [Blueprints and C++](blueprints-and-cpp.md)
